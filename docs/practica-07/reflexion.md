# Reflexión — Práctica 7: Riesgos y deuda técnica

**Sistema analizado:** Sistema de Control Escolar de Servicio Social y Residencia Profesional
**Evidencia de apoyo:** `matriz-riesgos.xlsx`, `mapa-calor.png`, `deuda-tecnica.md`, `top10-riesgos.md`

---

## 1. ¿Cuál Es El Riesgo Más Grave Que Encontraron y Por Qué?

El riesgo más grave es **R06: documentos personales de alumnos y bases de datos con registros publicados en un repositorio público**. Es el único que alcanzó la exposición máxima de la matriz (probabilidad 5 × impacto 5 = 25), y las razones son estas:

- **Ya ocurrió.** No es una posibilidad futura. Las carpetas `Kardex/`, `IMSS/` y `Servicio/` contienen PDF de alumnos, y los tres archivos `.sql` de la raíz traen sentencias `INSERT INTO` con registros. Cualquier persona con el enlace del repositorio puede acceder a ellos.
- **Es difícil de deshacer.** Aunque los archivos se borren hoy, siguen en el historial de Git. Corregirlo exige purgar el historial, y aun así pudo haber copias ya descargadas.
- **Afecta a terceros.** Las personas expuestas son los alumnos, que no tomaron ninguna decisión sobre el repositorio. Sus datos incluyen matrícula, documentos académicos, de seguridad social y del servicio social, además de teléfono, dirección y fecha de nacimiento en las bases de datos.
- **Se combina con otros riesgos críticos.** Los `.sql` públicos también revelan la estructura de la base y la columna `clave`, que guarda las contraseñas en texto plano (R02, `Controladores/usuariosC.php`, método `IniciarSesionC()`, líneas 91 y 99). Junto con las credenciales de la base remota en `Modelos/ConexionBD.php` (R01), un solo descuido permite tanto ver los datos como suplantar a usuarios.
- **Tiene consecuencias legales** (R07), que se detallan en la pregunta 2.

Además, es de los riesgos más baratos de atender: retirar los archivos y reemplazarlos por datos ficticios se estimó entre 6 y 8 horas (punto D04 de la deuda técnica). Por eso debería ser lo primero que se haga.

---

## 2. ¿Qué Obligaciones Establece La Ley Federal de Protección de Datos Personales Para Un Sistema Como Este?

En México, la ley aplicable a datos en manos de particulares es la **Ley Federal de Protección de Datos Personales en Posesión de los Particulares (LFPDPPP)**. La versión vigente es la nueva ley publicada en el Diario Oficial de la Federación el 20 de marzo de 2025, que entró en vigor el 21 de marzo de 2025 y sustituyó a la de 2010. Desde entonces, la supervisión corresponde a la Secretaría Anticorrupción y Buen Gobierno, y ya no al INAI.

Quien trata los datos, llamado "responsable", tiene entre otras las siguientes obligaciones. A la derecha se indica qué encontró este análisis:

| Obligación | Qué exige | Situación del sistema |
|---|---|---|
| **Aviso de privacidad** | Informar a la persona titular qué datos se tratan, cuáles son sensibles y para qué finalidades, desde que se recaban. | No se encontró aviso de privacidad ni en el código ni en `Documentacion/` (R07). |
| **Consentimiento** | Debe ser libre, específico e informado, y se requiere uno nuevo si se usan los datos para una finalidad distinta a la del aviso. | No hay evidencia de un mecanismo de consentimiento (R07). |
| **Principios del tratamiento** | Licitud, finalidad, calidad, responsabilidad, y que se traten solo los datos necesarios y relevantes para la finalidad. | El sistema recaba `numIMSS`, `fechanac`, `direccion`, `telefono` y `correo`; habría que justificar si todos son necesarios. |
| **Medidas de seguridad** | Adoptar medidas administrativas, técnicas y físicas para proteger los datos contra pérdida, acceso o uso no autorizado. | Contraseñas en texto plano (R02), credenciales en el código (R01, R03, R04, R05), PHP sin soporte (R09), sin pruebas (R13). |
| **Confidencialidad** | Guardar secreto de los datos, incluso frente a terceros con quienes se relacione el responsable. | Los PDF y los `.sql` con registros están publicados (R06). |
| **Derechos de las personas titulares** | Atender las solicitudes de acceso, rectificación, cancelación y oposición (derechos ARCO), y permitir revocar el consentimiento. | No hay un procedimiento visible para ejercerlos (R07). |
| **Conservación y supresión** | Conservar los datos solo por el tiempo necesario y luego suprimirlos. | No se encontró ninguna política de conservación; los respaldos `.sql` se acumulan en tres versiones (R16). |
| **Sanciones** | El incumplimiento se sanciona con multas calculadas en UMA. | La exposición de datos ya publicados aumenta el riesgo de sanción. |

**Para el sistema analizado** esto significa que, antes de operarlo con datos reales, la institución tendría que redactar el aviso de privacidad, definir los mecanismos de consentimiento y de atención de los derechos ARCO, aplicar medidas técnicas de seguridad (al menos cifrar las contraseñas, sacar las credenciales del código y controlar el acceso a los documentos), y dejar de publicar los datos personales existentes.

**Puntos Por Confirmar Con El Área Jurídica de La Institución:**

- Si el sistema pertenece a una institución pública educativa, la ley que le corresponde puede ser la **Ley General de Protección de Datos Personales en Posesión de Sujetos Obligados** y no la LFPDPPP, que regula a los particulares. Los principios y obligaciones son parecidos, pero conviene verificar cuál aplica.
- Si los documentos del IMSS revelan información de salud, se tratarían como **datos sensibles**, con requisitos más estrictos. Este análisis no abrió los documentos, así que no puede confirmarlo.
- El Reglamento de la nueva ley estaba pendiente de emitirse, por lo que algunos detalles pueden haber cambiado; conviene consultar el texto vigente en el sitio de la Cámara de Diputados.

---

## 3. Con Lo Que Saben Ahora, ¿Recomendarían Adoptar, Modernizar o Descartar el Sistema? Justifiquen.

**Por Qué No Adoptarlo Tal Cual:**
- Tiene fallas de seguridad graves: contraseñas en texto plano, credenciales en el código y datos personales publicados (R01, R02, R06).
- Su base tecnológica no tiene soporte: PHP 7.2.34 terminó su ciclo en noviembre de 2020, y también están fuera de soporte PHPExcel, jQuery 1.9.1, Bootstrap 3.3.7 y AdminLTE 2.4.0 (R09, R10, R11).
- No tiene pruebas, README, manual de instalación ni licencia (R08, R13, R14), y su conocimiento está en una sola persona, sin actividad desde junio de 2021 (R15).

**Por Qué Modernizar y No Descartar:**
- El sistema resuelve un proceso real: el control escolar del servicio social y la residencia profesional, con módulos de solicitudes, documentos, observaciones y correo. Ese conocimiento del negocio ya está implementado y sería costoso volver a levantarlo.
- El costo de corregir la deuda es acotado: se estimó entre 196 y 290 horas (de 24.5 a 36 días-persona) en `deuda-tecnica.md`. Como referencia, la estimación de la Práctica 5 para construir el sistema desde cero fue de entre 11 y 29 personas-mes, según el método usado.
- Lo más grave (seguridad y datos personales, D01 a D04) es lo más barato de corregir: entre 30 y 42 horas.

**Condiciones Para Que La Recomendación Sea Válida:**
1. **Licencia.** Sin autorización escrita del autor no queda claro que se pueda usar ni modificar el código (R08). Si no la otorga, la opción pasa a ser **reescribir**, aprovechando el análisis funcional ya hecho.
2. **Orden de trabajo.** Primero contener el daño (retirar datos personales, rotar credenciales, cifrar contraseñas), después crear pruebas de los flujos críticos y solo entonces migrar PHP y las librerías.
3. **Responsable de mantenimiento.** Debe asignarse a una persona o equipo interno para no repetir la dependencia de un solo desarrollador.

**Limitaciones de Esta Recomendación:** las horas de la deuda técnica son estimaciones del analista y no incluyen funcionalidades nuevas. Además, el análisis no verificó el código a fondo (por ejemplo, el control de acceso a los archivos por URL directa, que identificó el otro equipo), por lo que la lista de riesgos podría crecer.

Firma del Integrante: Myrka<3
