# Práctica 7 – Top 10 de Riesgos

**Grupo:** Equipos A y B
**Elaboró La Propuesta:** Equipo A y B

## 1. Propuesta del Equipo A

Seleccionamos los diez riesgos con mayor exposición. En caso de empate, se priorizó el que afecta a personas (datos y credenciales) sobre el que afecta al software.

| # | ID | Riesgo | Categoría | P | I | Exp. | Estrategia | Acción principal |
|---|---|---|---|---|---|---|---|---|
| 1 | R01 | Credenciales de MySQL en la nube expuestas en el código y en el historial | Seguridad | 5 | 5 | 25 | Evitar | Rotar credenciales y limpiar el historial |
| 2 | R03 | PDF con datos personales de alumnos en repositorio público | Legal | 5 | 5 | 25 | Evitar | Retirarlos del repositorio y del historial |
| 3 | R04 | Respaldos SQL con datos personales | Legal | 5 | 5 | 25 | Evitar | Reemplazar por datos ficticios |
| 4 | R02 | Contraseñas en texto plano iguales a la matrícula | Seguridad | 5 | 5 | 25 | Mitigar | `password_hash()` y cambio obligatorio |
| 5 | R05 | Archivos accesibles por URL directa con nombre predecible | Seguridad | 4 | 5 | 20 | Mitigar | Servirlos con validación de sesión y rol |
| 6 | R18 | Sin aviso de privacidad ni derechos ARCO | Legal | 5 | 4 | 20 | Evitar | Aviso de privacidad con el área jurídica |
| 7 | R20 | Un solo desarrollador, sin mantenimiento desde 2021 | Proyecto | 5 | 4 | 20 | Mitigar | Documentar y asignar responsable interno |
| 8 | R13 | Script de BD incompleto respecto al código | Técnico | 5 | 4 | 20 | Mitigar | Script único y versionado |
| 9 | R17 | Repositorio sin licencia | Legal | 4 | 4 | 16 | Transferir | Autorización escrita del autor |
| 10 | R12 | PHP 7.x fuera de soporte | Técnico | 4 | 4 | 16 | Mitigar | Migrar a PHP 8.2 |

Quedaron fuera, con exposición 16, R06, R07, R08 y R22. Proponemos agrupar R06, R07 y R08 con R01 en una sola acción ("sacar todos los secretos del código"), ya que se resuelven juntos.

## 2. Propuesta del Equipo B

Seleccionamos los diez riesgos con mayor exposición (probabilidad × impacto) de nuestra matriz. En caso de empate se aplicó el mismo criterio del Equipo A: primero el que afecta a personas (datos y credenciales) y después el que afecta al software o al proyecto.

| # | ID (Equipo B) | Riesgo | Exp. |
|---|---|---|---|
| 1 | R06 | Documentos personales de alumnos (Kardex, IMSS, Servicio) y respaldos `.sql` con registros publicados en el repositorio público | 25 (5×5) |
| 2 | R01 | Credenciales de la BD remota (Clever Cloud) en texto plano en el código | 20 (4×5) |
| 3 | R02 | Contraseñas de usuarios guardadas y comparadas en texto plano (`usuariosC.php`, `IniciarSesionC()`, líneas 91 y 99) | 20 (4×5) |
| 4 | R07 | Incumplimiento de la ley de protección de datos personales: sin aviso de privacidad ni medidas de protección | 20 (4×5) |
| 5 | R15 | Un solo desarrollador y sin mantenimiento desde jun-2021 | 20 (5×4) |
| 6 | R09 | PHP 7.2.34 sin soporte desde noviembre de 2020 | 20 (5×4) |
| 7 | R05 | Conexión a la BD con usuario `root` y sin contraseña en 4 archivos | 16 (4×4) |
| 8 | R08 | Repositorio sin licencia declarada | 15 (5×3) |
| 9 | R13 | Sin pruebas automáticas | 15 (5×3) |
| 10 | R03 | Contraseña de la cuenta de correo en texto plano (`EnviarCorreo.php`, línea 24) | 12 (4×3) |

Quedaron fuera, con exposición 12, R04, R10, R11 y R16. R03 y R04 empataban en el décimo lugar y se eligió R03 por ser una credencial de una cuenta institucional; R04 (clave y vector de cifrado fijos en `config/server.php`) se propone agrupar con la acción de "sacar todos los secretos del código".

## 3. Diferencias Discutidas

**Correspondencia Entre Las Matrices**

| Equipo A | Equipo B | Exp. A | Exp. B | Comentario |
|---|---|---|---|---|
| R01 Credenciales MySQL en la nube | R01 Credenciales BD remota | 25 | 20 | Mismo riesgo; A asigna probabilidad 5 y B probabilidad 4. |
| R03 PDF con datos personales | R06 Documentos y respaldos en repo público | 25 | 25 | B junta en un solo riesgo los PDF y los `.sql`. |
| R04 Respaldos SQL con datos personales | R06 (incluido) | 25 | 25 | A lo separa en dos riesgos. |
| R02 Contraseñas en texto plano | R02 Contraseñas en texto plano | 25 | 20 | Mismo riesgo; A asigna probabilidad 5. |
| R18 Sin aviso de privacidad | R07 Incumplimiento de la ley de datos personales | 20 | 20 | Misma exposición con distinta combinación (A: 5×4, B: 4×5). |
| R20 Un solo desarrollador | R15 Un solo desarrollador | 20 | 20 | Coinciden (5×4). |
| R12 PHP fuera de soporte | R09 PHP 7.2.34 sin soporte | 16 | 20 | B asigna probabilidad 5 por estar sin parches desde 2020. |
| R17 Sin licencia | R08 Sin licencia | 16 | 15 | Distinta combinación (A: 4×4, B: 5×3) y distinta estrategia (A: Transferir, B: Evitar). |

**Riesgos Que Solo Identificó Un Equipo**

- Solo el Equipo A: R05 (archivos accesibles por URL directa con nombre predecible) y R13 (script de BD incompleto respecto al código). El Equipo B no revisó el acceso directo a los archivos ni si el script cubre todo el código.
- Solo el Equipo B: R10 (PHPExcel abandonada y duplicada), R11 (frontend fuera de soporte: jQuery 1.9.1, Bootstrap 3.3.7, AdminLTE 2.4.0), R12 (librerías desactualizadas), R13 (sin pruebas automáticas), R14 (sin README ni manual de instalación) y R16 (gestión de la configuración deficiente).
- Por confirmar: el Equipo A agrupa R06, R07 y R08 (exposición 16) con R01 como "secretos en el código". El Equipo B los reconocería como sus R03 (contraseña de correo), R04 (clave y vector fijos) y R05 (`root` sin contraseña), pero hay que confirmar con el Equipo A qué contiene cada uno.
- El Equipo A indica que las contraseñas son "iguales a la matrícula". El Equipo B no verificó ese punto y solo confirmó que se guardan y se comparan en texto plano.

**Diferencias en Probabilidad o Impacto Asignados**

El Equipo A asignó probabilidad 5 a R01 y R02 (B: 4). El Equipo B considera que el daño depende de que el servidor remoto siga activo y de que alguien use las credenciales, aunque el repositorio sea público. En PHP fuera de soporte (R12 de A y R09 de B) la diferencia es a la inversa: A asignó 4 y B asignó 5.

**Criterio Para Desempatar**

1. Cuando ambos equipos asignaron valores distintos al mismo riesgo, se propone tomar la **mayor exposición** de las dos, por criterio de prudencia.
2. En empate de exposición, primero los riesgos que afectan a personas (datos y credenciales) y después los del software o del proyecto.
3. Los riesgos con la misma solución se agrupan en una sola acción.

## 4. Top 10 Acordado

> **Propuesta del Equipo B Para El Acuerdo.** Aplica los criterios de la sección 3 (mayor exposición entre ambos equipos, personas antes que software, y agrupar riesgos con la misma solución) y solo incluye riesgos que el Equipo B verificó en el código. Queda pendiente de confirmar con el Equipo A en el cierre grupal.

| # | Riesgo | Categoría | Exposición acordada | Responsable de la acción |
|---|---|---|---|---|
| 1 | Documentos personales y respaldos `.sql` con datos publicados en el repositorio (A: R03 y R04; B: R06) | Legal | 25 | Administrador del repositorio, con apoyo del área jurídica |
| 2 | Credenciales y claves en el código: BD remota, correo y clave de cifrado (A: R01, R06, R07, R08; B: R01, R03, R04) | Seguridad | 25 | Administrador de la base de datos |
| 3 | Contraseñas de usuarios en texto plano (A: R02; B: R02) | Seguridad | 25 | Desarrollador de mantenimiento |
| 4 | Sin aviso de privacidad ni medidas de protección de datos personales (A: R18; B: R07) | Legal | 20 | Área jurídica / responsable de datos personales |
| 5 | Un solo desarrollador y sin mantenimiento desde 2021 (A: R20; B: R15) | Proyecto | 20 | Jefatura o responsable del proyecto |
| 6 | PHP 7.2.34 fuera de soporte (A: R12; B: R09) | Técnico | 20 | Desarrollador de mantenimiento |
| 7 | Script de BD incompleto y tres versiones de respaldo sin control (A: R13; B: R16) | Técnico | 20 | Administrador de la base de datos |
| 8 | Conexión a la BD con `root` y sin contraseña, repetida en 4 archivos (B: R05) | Seguridad | 16 | Desarrollador de mantenimiento |
| 9 | Repositorio sin licencia (A: R17; B: R08) | Legal | 16 | Jefatura o responsable del proyecto, con el autor del sistema |
| 10 | Sin pruebas automáticas (B: R13) | Técnico | 15 | Desarrollador de mantenimiento |

**Fecha del Acuerdo:** 28 de septiembre 2026
