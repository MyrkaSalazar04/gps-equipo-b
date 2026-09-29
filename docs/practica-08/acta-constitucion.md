# Acta de Constitución del Proyecto
## Reingeniería del Sistema de Control Escolar de Servicio Social y Residencia Profesional

| Dato | Descripción |
|---|---|
| Nombre del proyecto | Modernización del Sistema de Control Escolar GPS |
| Consultora | Consultora TecNM Solutions |
| Director de Proyecto | Myrka Salazar |
| Cliente | Instituto Tecnológico de Matehuala |
| Fecha | 30 de Septiembre 2026 |
| Versión | 1.0 |

---

## 1. Objetivo del Proyecto

Modernizar el Sistema de Control Escolar de Servicio Social y Residencia Profesional, una aplicación web en PHP 7.2 desarrollada en 2021 por otro plantel, para entregar al Instituto Tecnológico de Matehuala una versión mantenible, segura y conforme a la normativa de protección de datos personales. El proyecto se ejecutará en un plazo no mayor a **9 meses** y con un presupuesto no mayor a **$204,258 MXN** (incluida la reserva de contingencia). Ambos valores son techos provisionales tomados de la estimación inversa de la Práctica 5 (tiempo de COCOMO y costo por puntos de función) y se afinarán en el cronograma y en `presupuesto.xlsx`.

**Objetivos Específicos (Medibles):**

1. Migrar la aplicación a un framework PHP actual con soporte vigente (PHP 8.2 o superior), conservando el 100 % de los 12 módulos identificados en los casos de uso de la Práctica 3.
2. Rediseñar la base de datos: una sola versión versionada del esquema (hoy hay tres respaldos `.sql` en la raíz), con llaves foráneas declaradas y un diccionario de datos que identifique los datos personales.
3. Eliminar el 100 % de las credenciales y claves incrustadas en el código (riesgos R01, R03, R04 y R05), rotar las que ya fueron expuestas y sustituir las contraseñas en texto plano por `password_hash()` (R02).
4. Retirar del repositorio y de su historial los documentos y registros con datos personales (R06) y trabajar únicamente con datos ficticios.
5. Reducir a nivel **Medio o inferior** (exposición ≤ 14) los 6 riesgos críticos de la matriz de la Práctica 7 (R01, R02, R06, R07, R09 y R15).
6. Crear pruebas automatizadas con una cobertura mínima de **60 %** (propuesta, a validar con el Instituto) en los flujos críticos, y entregar README técnico, manual de instalación y manual de usuario.
7. Establecer un aviso de privacidad y controles de acceso por rol conforme a las obligaciones de protección de datos personales aplicables al Instituto.

## 2. Justificación

El Instituto necesita automatizar el control de Residencias Profesionales y Servicio Social. El sistema heredado (**11,039 líneas de código propio**, 12 módulos funcionales) resuelve esa necesidad, pero el diagnóstico de las Prácticas 1 a 7 muestra que **no puede adoptarse tal como está**:

- **Seguridad.** La matriz de riesgos identifica 16 riesgos, de los cuales 6 son críticos y 3 altos. Hay credenciales de la base de datos remota escritas en `Modelos/ConexionBD.php` (líneas 7-12), contraseña de la cuenta de correo en `Controladores/EnviarCorreo.php` (línea 24), y conexiones con usuario `root` sin contraseña repetidas en 4 archivos. Las contraseñas de los usuarios se guardan y comparan en texto plano (`Controladores/usuariosC.php`, líneas 91 y 99).
- **Legal.** El repositorio público contiene PDF de kardex, IMSS y cartas (carpetas `Kardex/`, `IMSS/`, `Servicio/` y `Documentos/`) y tres archivos `.sql` con registros. No existe aviso de privacidad ni medidas de protección de datos, y el repositorio no declara licencia. El riesgo más grave (R06, exposición 25) ya está ocurriendo.
- **Tecnología obsoleta.** Usa PHP 7.2.34 (sin soporte desde noviembre de 2020), PHPExcel 1.8.0 abandonada y duplicada, y jQuery 1.9.1, Bootstrap 3.3.7 y AdminLTE 2.4.0 fuera de soporte.
- **Deuda técnica.** Se identificaron 15 puntos de deuda técnica que requieren entre **196 y 290 horas** (≈ 24.5 a 36.3 días-persona) solo para corregirse, sin contar pruebas automatizadas de todo el sistema.
- **Dependencia de una persona.** El historial de Git muestra 10 commits en 86 días, de un solo desarrollador (con dos nombres de Git), y ninguna actividad desde el 21 de junio de 2021.
- **Costo de la alternativa.** Construir un sistema equivalente desde cero costaría entre **$204,258 MXN** (249 puntos de función, ≈ 10.9 personas-mes) y **$560,130 MXN** (COCOMO orgánico, ≈ 29.9 personas-mes y 9.1 meses con 3.3 personas), con un costo cargado de $18,750 MXN por desarrollador al mes.

La reingeniería conserva lo que funciona (los flujos de trámites ya validados) y corrige lo que representa riesgo, con un costo menor que reconstruir y un riesgo mucho menor que operar el sistema sin cambios.

## 3. Alcance General

**Incluye:**

- Migración a un framework PHP vigente con arquitectura MVC ordenada, conservando los 12 módulos: Iniciar sesión, Inicio, Solicitudes, Usuarios, Catálogo, Carpetas, Certificados, Visitas a empresa, Subir calificaciones, CRUD Carreras, Información y Mi horario.
- Rediseño y migración de la base de datos (esquema único, llaves foráneas, índices y diccionario de datos).
- Corrección de las vulnerabilidades del top 10 de riesgos: gestión segura de credenciales y configuración, rotación de secretos, cifrado de contraseñas y una conexión única a la BD con usuario de privilegios mínimos.
- Sustitución de librerías abandonadas (PHPExcel por PhpSpreadsheet) y actualización del frontend y de TCPDF y PHPMailer, administradas con Composer.
- Control de acceso por rol para los 5 perfiles de usuario identificados en los casos de uso.
- Cumplimiento de protección de datos personales: aviso de privacidad, minimización de datos, cifrado y control de acceso.
- Depuración del repositorio: retiro de documentos personales, purga del historial (`git filter-repo`), `.gitignore`, convención de commits e integración continua básica.
- Pruebas automatizadas con PHPUnit, documentación técnica y manual de usuario.
- Despliegue en un ambiente de pruebas del Instituto y capacitación básica al personal usuario.

**No Incluye (Queda Fuera):**

- Nuevos módulos o funciones que no existan en el sistema heredado (por ejemplo, aplicación móvil o integraciones con otros sistemas del TecNM).
- Carga o migración de datos reales de alumnos durante el desarrollo; las pruebas usarán datos ficticios.
- Adquisición de infraestructura, hosting o licencias de terceros.
- Soporte y mantenimiento posteriores al periodo de garantía acordado.
- Cualquier conexión a los servidores externos ni uso de las credenciales encontradas en el código heredado (se rotan o se dan de baja, nunca se usan).

## 4. Interesados

| Interesado | Rol en el proyecto | Interés / expectativa | Influencia |
|---|---|---|---|
| Instituto Tecnológico de Matehuala (dirección y áreas de vinculación / gestión tecnológica) | Cliente y patrocinador | Sistema confiable, legal y de bajo costo de mantenimiento | Alta |
| Área jurídica / responsable de datos personales del Instituto | Responsable de acciones legales | Aviso de privacidad, cumplimiento normativo y licencia del código | Alta |
| Administrador del repositorio y de la base de datos | Responsable de acciones técnicas | Depurar el repositorio, rotar credenciales y administrar el esquema único | Alta |
| Jefaturas y personal que gestiona Residencia Profesional y Servicio Social | Usuarios principales | Simplificar trámites y reducir trabajo manual | Media |
| Asesores internos y externos | Usuarios | Seguimiento claro de los proyectos de sus asesorados | Media |
| Estudiantes | Usuarios finales | Realizar sus trámites en línea con protección de sus datos | Media |
| Empresas y dependencias receptoras | Usuarios externos | Registro ágil de convenios y visitas | Baja |
| Consultora (Director y equipo) | Ejecutor del proyecto | Entregar en tiempo, costo y calidad acordados | Alta |
| Mtro. Jesús Alberto Garza Ortega | Docente y evaluador académico | Que el plan cumpla los criterios de la práctica | Alta (académica) |
| Autor del sistema original (`cbarreral` en GitHub) | Titular de derechos | Reconocimiento de autoría y autorización o licencia de uso | Media |

## 5. Supuestos

1. El Instituto designará un responsable de negocio que valide requisitos y apruebe entregables en un máximo de 5 días hábiles.
2. Los casos de uso, el modelo de datos y la arquitectura recuperados en las Prácticas 2 a 4 representan el comportamiento real del sistema.
3. El autor del sistema o el plantel de origen otorgará autorización o licencia por escrito (riesgo R08). Si no la otorga, la alternativa es reescribir el sistema y el presupuesto se ajustará hacia el rango de reconstrucción.
4. El Instituto proporcionará un ambiente de pruebas (servidor y base de datos) al inicio de la fase de desarrollo.
5. Las estimaciones de la Práctica 5 son una base razonable para el presupuesto: 11.039 KLOC, 249 puntos de función a 7 h/PF (1,743 horas) y un costo cargado de $117.19 MXN por hora.
6. Las horas de la deuda técnica (196 a 290 h) son estimaciones del analista para un desarrollador que no conoce el sistema, no mediciones, y no incluyen pruebas automatizadas completas.
7. Se trabajará únicamente con datos ficticios durante el desarrollo y las pruebas.
8. Las credenciales expuestas se rotan o se dan de baja antes de cualquier otra actividad, porque corregir el código no elimina el riesgo mientras sigan visibles en el historial de Git.

## 6. Restricciones

- **Tiempo:** el plan debe presentarse al cliente en la Práctica 9 (cierre del periodo agosto–diciembre 2026). La duración de la ejecución no debe superar los 9 meses de referencia de COCOMO.
- **Costo:** el presupuesto no excederá $204,258 MXN, incluida la reserva de contingencia, salvo aprobación expresa del cliente.
- **Recursos:** equipo reducido; sin presupuesto para licencias comerciales (se prefieren herramientas de código abierto).
- **Legales y éticas:** el repositorio no tiene licencia declarada; no se distribuye, no se vende ni se instala con datos reales. Está prohibido usar las credenciales encontradas o conectarse a servidores externos.
- **Técnicas:** debe mantenerse la compatibilidad funcional con los procesos actuales del Instituto y usar PHP con MySQL/MariaDB o equivalentes.
- **Gestión:** todo el trabajo se gestiona en GitHub (Issues, Milestones y Projects) y se entrega mediante Pull Request.

## 7. Criterios de Éxito

| # | Criterio | Indicador de aceptación |
|---|---|---|
| 1 | Paridad funcional | Los 12 módulos de los casos de uso operando en el sistema nuevo, con los 5 perfiles de usuario |
| 2 | Seguridad | 0 credenciales o secretos en el código; contraseñas con hash; 0 conexiones con `root` sin contraseña |
| 3 | Datos personales | 0 archivos con datos personales en el repositorio y en su historial; aviso de privacidad publicado |
| 4 | Riesgos | Los 6 riesgos críticos reducidos a exposición ≤ 14; los 10 riesgos del top 10 con acción cerrada |
| 5 | Base de datos | Esquema único versionado, con todas las relaciones declaradas con llaves foráneas |
| 6 | Tecnología | PHP 8.2 o superior y librerías con soporte vigente, administradas con Composer |
| 7 | Calidad | Cobertura de pruebas ≥ 60 % en flujos críticos; pruebas de aceptación aprobadas |
| 8 | Documentación | README técnico, manual de instalación y manual de usuario entregados y revisados |
| 9 | Tiempo | Entregables dentro de las fechas del cronograma, con desviación ≤ 10 % |
| 10 | Costo | Gasto real dentro del presupuesto aprobado, sin exceder la reserva de contingencia |
| 11 | Aceptación | Firma de conformidad del Instituto sobre los entregables finales |

---

## Aprobación

| Nombre | Rol | Firma | Fecha |
|---|---|---|---|
| Myrka Salazar | Director de Proyecto | | |
| Instituto Tecnológico de Matehuala | Cliente / Patrocinador | | |
