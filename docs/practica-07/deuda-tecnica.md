# Deuda técnica — Práctica 7

**Sistema analizado:** Sistema de Control Escolar de Servicio Social y Residencia Profesional (PHP 7.2.34, MariaDB 10.4.14)

Este documento lista la deuda técnica detectada en las prácticas 2 a 7 y el esfuerzo aproximado para corregirla. Cada punto se relaciona con el riesgo de `matriz-riesgos.xlsx` al que corresponde.

> **Nota Ética:** se indica archivo y línea de cada hallazgo, pero no se copia ningún valor de contraseñas ni credenciales.

## Supuestos de La Estimación

- Estimación aproximada de un desarrollador con conocimiento de PHP, sin conocer previamente el sistema.
- 1 día-persona = 8 horas.
- Los rangos incluyen la corrección y una verificación manual básica, pero no la creación de pruebas automáticas (eso es el punto D10).
- Son estimaciones del analista, no mediciones.

## Lista de Deuda Técnica

| ID | Deuda técnica | Evidencia (archivo / ubicación) | Corrección propuesta | Esfuerzo (h) | Riesgo | Prioridad |
|---|---|---|---|---|---|---|
| D01 | Credenciales y claves escritas directamente en el código | `Modelos/ConexionBD.php` (líneas 7-12); `config/server.php` (líneas 8-10, 21 y 24); `Controladores/EnviarCorreo.php` (línea 24) | Moverlas a variables de entorno o un archivo de configuración fuera del repositorio y rotar las que ya se expusieron | 8 – 12 | R01, R03, R04, R05 | Alta |
| D02 | Conexión a la BD duplicada en varios archivos, con usuario `root` y sin contraseña | `config/server.php`; `Modelos/importExcel.php` (33-34); `ImportarExcel/insertarCatalogo.php` (10-11); `ImportarExcel/insertarUsuarios.php` (10-11) | Una sola clase de conexión y un usuario de BD con privilegios mínimos | 6 – 8 | R05, R16 | Alta |
| D03 | Contraseñas de usuarios guardadas y comparadas en texto plano | Columna `clave` en los `.sql`; `Controladores/usuariosC.php`, método `IniciarSesionC()` (línea 91: comparación directa; línea 99: la clave se guarda en `$_SESSION`) | Usar `password_hash()` y `password_verify()`, migrar las contraseñas existentes, no guardar la clave en la sesión y forzar restablecimiento | 10 – 14 | R02 | Alta |
| D04 | Documentos personales y bases de datos con registros dentro del repositorio público | Carpetas `Kardex/`, `IMSS/`, `Servicio/`, `Documentos/`; los 3 `.sql` con `INSERT INTO` | Retirar los archivos, purgar el historial de Git (`git filter-repo`) y trabajar con datos ficticios | 6 – 8 | R06 | Alta |
| D05 | Tres versiones del respaldo de la BD en la raíz, sin control de cambios | `sistemacontrolescolar.sql`; `sistemacontrolescolar 2.sql`; `sistemacontrolescolar 11-06-2021.sql` | Dejar un solo esquema versionado con datos de ejemplo ficticios y scripts de migración | 4 – 6 | R16 | Media |
| D06 | PHP 7.2.34 sin soporte desde noviembre de 2020 | Encabezado de los 3 archivos `.sql` | Migrar a PHP 8.2 o superior y corregir funciones y sintaxis incompatibles | 24 – 40 | R09 | Alta |
| D07 | PHPExcel 1.8.0 (2014) abandonada y duplicada en dos carpetas | `impExcel/Classes/PHPExcel.php`; `Modelos/PHPExcel/Classes/PHPExcel.php` | Sustituirla por PhpSpreadsheet y eliminar la copia duplicada | 16 – 24 | R10 | Media |
| D08 | Frontend fuera de soporte: jQuery 1.9.1, Bootstrap 3.3.7 y AdminLTE 2.4.0 | `ImportarExcel/jquery.js`; `Vistas/bower_components/` (~6,800 archivos); `Vistas/dist/` | Migrar a jQuery 3.x y Bootstrap 5 con una plantilla vigente, y quitar `bower_components` del repositorio | 40 – 60 | R11 | Media |
| D09 | Librerías de terceros desactualizadas y copiadas a mano | `tcpdf/` (6.2.6); `PHPMailer/` (6.3.0); `ImportarExcel/xlsx.js` (SheetJS 0.15.4); `Modelos/class.upload.php` (0.33dev) | Actualizarlas y administrarlas con Composer, o reemplazarlas por alternativas mantenidas | 12 – 20 | R12 | Media |
| D10 | Sin pruebas automáticas | No existe `tests/`, `phpunit.xml` ni archivos `*Test.php` propios | Crear pruebas con PHPUnit para los flujos críticos (login, alta de solicitud, generación de documentos, importación de Excel) | 30 – 40 | R13 | Media |
| D11 | Sin README técnico ni manual de instalación | No existe `README.md` ni documentos de despliegue; `Documentacion/` solo tiene formatos operativos | Escribir README (qué hace, requisitos) y manual de instalación (importar BD, configurar credenciales) | 6 – 8 | R14 | Media |
| D12 | Sin `.gitignore`, sin integración continua y sin convención de commits | No existe `.gitignore` ni `.github/`; commits como "2" y "restructura por segunda vez" | Agregar `.gitignore`, una convención de mensajes de commit y un flujo básico de CI | 4 – 6 | R16 | Baja |
| D13 | Sin aviso de privacidad ni medidas de protección de datos personales | Tablas `usuarios` y `datosestudiante` (columnas `numIMSS`, `fechanac`, `direccion`, `telefono`, `correo`) | Redactar el aviso de privacidad (verificando con el área jurídica la ley aplicable), reducir los datos recabados y definir controles de acceso | 16 – 24 | R07 | Alta |
| D14 | Repositorio sin licencia | No existe `LICENSE` en la raíz ni en la página de GitHub | Solicitar autorización o licencia por escrito al autor | 2 – 4 | R08 | Alta |
| D15 | Código sin documentación y conocimiento concentrado en un solo desarrollador | Historial de Git: 10 commits, dos nombres de Git (`cbarreral` y Carlos Alberto Barrera Lugo), último commit el 21-jun-2021 | Documentar arquitectura y módulos (a partir de las prácticas 2 a 4) y transferir el conocimiento al equipo de mantenimiento | 12 – 16 | R15 | Media |

## Resumen del Esfuerzo

| Concepto | Horas | Días-persona |
|---|---|---|
| Mínimo estimado | 196 | ≈ 24.5 |
| Máximo estimado | 290 | ≈ 36.3 |

| Prioridad | Puntos | Horas (mín – máx) |
|---|---|---|
| Alta | D01, D02, D03, D04, D06, D13, D14 | 72 – 110 |
| Media | D05, D07, D08, D09, D10, D11, D15 | 120 – 174 |
| Baja | D12 | 4 – 6 |

## Observaciones

- Lo que más esfuerzo concentra es la modernización tecnológica (PHP, frontend y librerías: D06 a D09, entre 92 y 144 horas) y las pruebas (D10).
- Los puntos de prioridad alta relacionados con seguridad y datos personales (D01 a D04) suman entre 30 y 42 horas. Son los más baratos de corregir y de mayor impacto, por lo que conviene atenderlos primero, antes de cualquier otro trabajo de reingeniería.
- D01 y D03 dependen de rotar credenciales y contraseñas ya expuestas; corregir el código sin rotarlas no elimina el riesgo, porque siguen visibles en el historial de Git.
