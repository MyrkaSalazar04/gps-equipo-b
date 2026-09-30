# Riesgos y Calidad del Proyecto de Reingeniería
## Sistema de Control Escolar de Servicio Social y Residencia Profesional

| Dato | Descripción |
|---|---|
| Proyecto | Modernización del Sistema de Control Escolar GPS |
| Consultora | Consultora TecNM Solutions |
| Director | Myrka Salazar |
| Fecha | Septiembre 30, 2026 |
| Versión | 1.0 |

---

## 1. Top 10 de Riesgos Actualizados

Los riesgos se clasifican en cuatro categorías: **técnico**, **seguridad**, **legal** y **proyecto**.

| ID | Descripción | Categoría | Prob. (1-5) | Impacto (1-5) | Exposición | Estrategia | Acción concreta |
|---|---|---|---|---|---|---|---|
| R01 | Credenciales de BD en la nube visibles en `Modelos/ConexionBD.php` (líneas 7-12) | Seguridad | 5 | 5 | 25 | Mitigar | Rotar credenciales y moverlas a variables de entorno (`.env`) |
| R02 | Contraseñas de usuarios en texto plano en `usuariosC.php` (líneas 91, 99) | Seguridad | 5 | 5 | 25 | Mitigar | Migrar a `password_hash()` y forzar cambio de contraseña |
| R03 | Contraseña del correo en `EnviarCorreo.php` (línea 24) | Seguridad | 4 | 4 | 16 | Mitigar | Mover a `.env` y rotar credenciales |
| R04 | Llave de cifrado expuesta en `config/server.php` | Seguridad | 4 | 4 | 16 | Mitigar | Regenerar llave y guardarla fuera del repositorio |
| R05 | Conexión con `root` sin contraseña en 4 archivos | Seguridad | 5 | 4 | 20 | Mitigar | Crear usuario de BD con privilegios mínimos |
| R06 | Datos personales (kardex, IMSS, cartas) en repositorio público | Legal | 5 | 5 | 25 | Evitar | Retirar del repo y purgar historial con `git filter-repo` |
| R07 | Librerías obsoletas (PHPExcel, jQuery 1.9, Bootstrap 3) | Técnico | 4 | 3 | 12 | Mitigar | Sustituir por versiones vigentes vía Composer |
| R08 | Sin licencia declarada en el repositorio original | Legal | 3 | 5 | 15 | Transferir | Solicitar autorización por escrito al autor o al plantel de origen |
| R09 | Dependencia de un solo desarrollador (historial de 10 commits) | Proyecto | 4 | 4 | 16 | Mitigar | Documentar arquitectura y establecer equipo de mantenimiento |
| R10 | Sin pruebas automatizadas | Técnico | 4 | 4 | 16 | Mitigar | Implementar PHPUnit con cobertura ≥ 60% |

**Mapa de Calor Resumido:**

| Exposición | Nivel | Riesgos |
|---|---|---|
| 20-25 | 🔴 Crítico | R01, R02, R05, R06 |
| 15-19 | 🟠 Alto | R03, R04, R08, R09, R10 |
| 10-14 | 🟡 Medio | R07 |
| 5-9 | 🟢 Bajo | — |

---

## 2. Criterios de Calidad del Proyecto

### 2.1 Calidad de Código

| Criterio | Estándar | Verificación |
|---|---|---|
| Estilo de código | PSR-12 | PHP_CodeSniffer |
| Complejidad ciclomática | ≤ 10 por función | PHP Mess Detector |
| Duplicación de código | ≤ 5% | PHPCPD |
| Deuda técnica | ≤ 5 días | SonarQube |

### 2.2 Calidad de Seguridad

| Criterio | Estándar |
|---|---|
| Credenciales en código | 0 (cero) |
| Contraseñas | `password_hash()` con bcrypt |
| Conexiones BD | Usuario con privilegios mínimos |
| Cifrado en tránsito | HTTPS obligatorio |
| Validación de entrada | Filtros y sanitización en todos los formularios |

### 2.3 Calidad de Datos Personales

| Criterio | Estándar |
|---|---|
| Archivos con datos reales | 0 en repositorio e historial |
| Aviso de privacidad | Publicado en el sistema |
| Consentimiento | Formulario de aceptación por usuario |
| Minimización de datos | Solo datos estrictamente necesarios |

### 2.4 Calidad de Pruebas

| Criterio | Estándar |
|---|---|
| Cobertura unitaria | ≥ 60% en flujos críticos |
| Pruebas de integración | Cubrir los 12 módulos |
| Pruebas de aceptación | Aprobadas por el cliente |
| Defectos críticos abiertos | 0 al cierre |

### 2.5 Calidad de Documentación

| Criterio | Estándar |
|---|---|
| README técnico | Completo (arquitectura, stack, instalación) |
| Manual de instalación | Paso a paso, verificado |
| Manual de usuario | Por cada uno de los 5 roles |
| Comentarios en código | En funciones complejas |

---

## 3. Plan de Aseguramiento de Calidad

| Actividad | Frecuencia | Responsable |
|---|---|---|
| Revisión de código (Pull Requests) | Cada cambio | Director |
| Ejecución de pruebas unitarias | Cada push (CI) | Automatizado |
| Pruebas de integración | Semanal | Director |
| Revisión de seguridad | Quincenal | Director |
| Auditoría de datos personales | Mensual | Director |
| Revisión de documentación | Al cierre de cada fase | Director |

---

## Aprobación

| Nombre | Rol | Fecha |
|---|---|---|
| Myrka Salazar | Director de Proyecto | Septiembre 30, 2026 |
