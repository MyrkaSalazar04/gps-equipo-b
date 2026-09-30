# Riesgos y Calidad del Proyecto de Reingeniería
## Sistema de Control Escolar de Servicio Social y Residencia Profesional

| Dato | Descripción |
|---|---|
| Proyecto | Modernización del Sistema de Control Escolar GPS |
| Consultora | Consultora TecNM Solutions |
| Director | Myrka Salazar |
| Cliente | Instituto Tecnológico de Matehuala |
| Fecha | Septiembre 30, 2026 |
| Versión | 1.1 |

---

## 1. Top 10 de Riesgos Actualizado Para El Proyecto de Reingeniería

Este es el top 10 acordado el 28 de septiembre de 2026 a partir de las propuestas de los Equipos A y B de la Práctica 7. Se aplicaron los criterios de desempate acordados: mayor exposición entre ambos equipos, personas antes que software y agrupación de riesgos con la misma solución. La exposición es probabilidad (P) por impacto (I), en escala de 1 a 5. Las categorías son técnico, seguridad, legal y proyecto.

| # | Riesgo | Categoría | P | I | Exp. | Estrategia | Acción en el proyecto | Paquetes EDT | Responsable de la acción |
|---|---|---|---|---|---|---|---|---|---|
| 1 | Documentos personales y respaldos `.sql` con datos publicados en el repositorio | Legal | 5 | 5 | 25 | Evitar | Retirarlos del repositorio y purgar el historial; trabajar solo con datos ficticios | 1.5.1, 1.3.3 | Administrador del repositorio, con apoyo del área jurídica |
| 2 | Credenciales y claves en el código: BD remota, correo y clave de cifrado | Seguridad | 5 | 5 | 25 | Evitar | Rotar o dar de baja lo expuesto y sacar todos los secretos a variables de entorno | 1.5.4, 1.3.5 | Administrador de la base de datos |
| 3 | Contraseñas de usuarios en texto plano | Seguridad | 5 | 5 | 25 | Mitigar | `password_hash()`, dejar de guardar la clave en sesión y cambio obligatorio de contraseña | 1.3.3, 1.3.5 | Desarrollador de mantenimiento |
| 4 | Sin aviso de privacidad ni medidas de protección de datos personales | Legal | 5 | 4 | 20 | Evitar | Aviso de privacidad validado por el área jurídica; minimización y cifrado de datos | 1.2.4, 1.2.5 | Área jurídica / responsable de datos personales |
| 5 | Un solo desarrollador y sin mantenimiento desde 2021 | Proyecto | 5 | 4 | 20 | Mitigar | Documentar la arquitectura y asignar un responsable interno de mantenimiento | 1.6.3, 1.2.3 | Jefatura o responsable del proyecto |
| 6 | PHP 7.2.34 fuera de soporte | Técnico | 5 | 4 | 20 | Mitigar | Migrar a PHP 8.2 o superior con un framework vigente | 1.3.1, 1.2.3, 1.6.1 | Desarrollador de mantenimiento |
| 7 | Script de BD incompleto y tres versiones de respaldo sin control | Técnico | 5 | 4 | 20 | Mitigar | Esquema único versionado con migraciones y llaves foráneas | 1.2.2, 1.3.3 | Administrador de la base de datos |
| 8 | Conexión a la BD con `root` y sin contraseña, repetida en 4 archivos | Seguridad | 4 | 4 | 16 | Mitigar | Una sola clase de conexión y un usuario con privilegios mínimos | 1.3.5 | Desarrollador de mantenimiento |
| 9 | Repositorio sin licencia | Legal | 4 | 4 | 16 | Transferir | Autorización escrita del autor o del plantel de origen | 1.1.5 | Jefatura o responsable del proyecto, con el autor del sistema |
| 10 | Sin pruebas automatizadas | Técnico | 5 | 3 | 15 | Mitigar | Suite PHPUnit con cobertura mínima del 60 % en flujos críticos | 1.4.1, 1.4.2 | Desarrollador de mantenimiento |

**Exposición Promedio: 20.2 de 25.** Este promedio sustenta la reserva de contingencia del 20 % de `presupuesto.xlsx`.

**Mapa de Calor Resumido**

| Exposición | Nivel | Riesgos (número del top 10) |
|---|---|---|
| 20 a 25 | Crítico | 1, 2, 3, 4, 5, 6, 7 |
| 15 a 19 | Alto | 8, 9, 10 |
| 10 a 14 | Medio | Ninguno; es la meta al cierre del proyecto |
| 5 a 9 | Bajo | Ninguno |

**Notas**
- La estrategia del riesgo 9 es Transferir, según el Equipo A. El Equipo B proponía Evitar. Se conserva Transferir porque la autorización depende del autor del sistema.
- Se ejecutan primero los paquetes 1.5.4, 1.5.1 y 1.1.5, porque son los de menor costo y mayor impacto.
- **Meta al cierre:** los 6 riesgos críticos de la matriz de la Práctica 7 con exposición de 14 o menos y los 10 riesgos de esta tabla con su acción cerrada.
- Los riesgos con exposición de 12 o menos de la matriz de la Práctica 7 (por ejemplo, librerías del frontend desactualizadas) se atienden dentro del paquete 1.3.4 y se vigilan en el tablero, sin entrar al top 10.

---

## 2. Criterios de Calidad del Proyecto

### 2.1 Calidad de Código

| Criterio | Estándar | Verificación |
|---|---|---|
| Estilo de código | PSR-12 | PHP_CodeSniffer en el CI |
| Complejidad ciclomática | 10 o menos por función | PHP Mess Detector |
| Duplicación de código | 5 % o menos | PHPCPD |
| Deuda técnica heredada | Puntos D01 a D15 cerrados o con decisión documentada | Revisión en la Milestone de calidad |

### 2.2 Calidad de Seguridad

| Criterio | Estándar | Verificación |
|---|---|---|
| Credenciales en el código | Cero | Búsqueda global de cadenas de conexión, claves y contraseñas incrustadas |
| Contraseñas | `password_hash()` y ninguna clave en sesión | Revisión de seguridad (1.4.3) |
| Conexión a la BD | Una sola clase y usuario con privilegios mínimos | Revisión de seguridad (1.4.3) |
| Control de acceso | Matriz de permisos por rol; solo un Admin puede editar o eliminar a otro Admin | Pruebas de integración (1.4.2) |
| Cifrado en tránsito | HTTPS obligatorio | Revisión de seguridad (1.4.3) |
| Validación de entrada | Filtros y sanitización en todos los formularios | Revisión de seguridad (1.4.3) |

### 2.3 Calidad de Datos Personales

| Criterio | Estándar | Verificación |
|---|---|---|
| Archivos con datos reales | Cero en el repositorio y en su historial | Auditoría mensual y revisión tras la purga (1.5.1) |
| Aviso de privacidad | Publicado en el sistema y validado por el área jurídica | Paquete 1.2.5 |
| Minimización | Solo los datos estrictamente necesarios (`numIMSS`, `fechanac`, `direccion`, `telefono`, `correo` justificados y cifrados los sensibles) | Diccionario de datos |
| Datos de prueba | Solo datos ficticios | Revisión de las semillas de datos |

### 2.4 Calidad de La Base de Datos

| Criterio | Estándar | Verificación |
|---|---|---|
| Esquema | Un solo script versionado con migraciones | Paquete 1.3.3 |
| Integridad referencial | 100 % de las relaciones con llave foránea declarada | Revisión del esquema |
| Referencia a usuario | Un solo criterio (`id`) en todas las tablas | Revisión del modelo entidad-relación |
| Normalización | Empresa y alumno separados de `solicitudes` | Revisión del modelo entidad-relación |
| Tipos de dato | `date`, `datetime` o `varchar` con longitud en lugar de `text` genérico | Revisión del esquema |
| Diccionario de datos | Identifica los datos personales y coincide con los 17 archivos lógicos de la Práctica 5 | Paquete 1.2.2 |

### 2.5 Calidad de Pruebas

| Criterio | Estándar |
|---|---|
| Cobertura unitaria | 60 % o más en flujos críticos: inicio de sesión, alta de solicitud, generación de documentos e importación de Excel |
| Pruebas de integración | Flujos entre controlador, modelo y base de datos de los 12 módulos |
| Pruebas de aceptación | Acta de aceptación firmada por el Instituto |
| Defectos críticos abiertos | Cero al cierre |

### 2.6 Calidad de Documentación

| Criterio | Estándar |
|---|---|
| README técnico | Arquitectura, stack e instalación |
| Manual de instalación | Paso a paso y verificado en el ambiente de pruebas |
| Manual de usuario | Cubre los 5 perfiles: Administrador, Alumno, Asesor Académico, Asesor Industrial y Jefe |
| Documentación de arquitectura | Entregada y revisada |

---

## 3. Criterios de Aceptación

### 3.1 Por Grupo de Módulos (Paquete 1.3.2)

| Grupo | Módulos | Se Acepta Cuando |
|---|---|---|
| A. Núcleo | Iniciar sesión, Inicio, Usuarios | Autenticación con hash funcionando para los 5 perfiles; ningún rol distinto de Admin puede editar o eliminar a un Admin |
| B. Trámites | Solicitudes (solo Admin) y notificaciones por correo | El Admin registra una solicitud y se envía el correo con credenciales fuera del código |
| C. Expediente | Carpetas y observaciones | Cada alumno sube y consulta sus documentos; los asesores solo ven los de sus alumnos |
| D. Catálogos | Catálogo de empresas, CRUD Carreras e Información | Consulta para todos los perfiles autorizados y alta, edición y baja solo para Admin |
| E. Documentos | Certificados y constancias | Los PDF se generan con los datos correctos y sin datos reales de prueba |
| F. Seguimiento | Visitas a empresa, Subir calificaciones y Mi horario | Las visitas se registran, la importación de Excel funciona con PhpSpreadsheet y el alumno ve su horario |

### 3.2 Por Fase (Milestone)

| Fase | Entregable Que Se Acepta |
|---|---|
| 1. Gestión del proyecto | Acta, alcance, cronograma, presupuesto, top 10 y RACI aprobados |
| 2. Análisis y diseño | Requerimientos validados, modelo de datos, arquitectura, plan de seguridad y aviso de privacidad revisado por el área jurídica |
| 3. Desarrollo | Los 12 módulos migrados, esquema único, seguridad aplicada y control de acceso por rol |
| 4. Calidad y pruebas | Cobertura de 60 % o más, informe de seguridad sin hallazgos críticos y acta de aceptación firmada |
| 5. Depuración del repositorio | Repositorio e historial sin datos personales, `.gitignore`, convención de commits y CI en marcha |
| 6. Despliegue y cierre | Sistema en el ambiente de pruebas, capacitación impartida, documentación entregada y acta de cierre |

---

## 4. Plan de Aseguramiento de Calidad

| Actividad | Frecuencia | Responsable |
|---|---|---|
| Revisión de código (Pull Requests) | En cada cambio | Director |
| Pruebas unitarias | En cada push (CI) | Automatizado |
| Pruebas de integración | Semanal | Equipo técnico |
| Revisión de seguridad | Quincenal | Pareja 2 (costos, riesgos y calidad) |
| Auditoría de datos personales | Mensual | Pareja 2, con el área jurídica |
| Revisión del top 10 de riesgos | Al cierre de cada fase | Pareja 2 |
| Revisión de documentación | Al cierre de cada fase | Director |

---

## Aprobación

| Nombre | Rol | Fecha |
|---|---|---|
| Myrka Salazar | Director de proyecto, Consultora TecNM Solutions | Septiembre 30, 2026 |
| Instituto Tecnológico de Matehuala | Cliente | |
