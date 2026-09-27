# Actores del Sistema

El sistema identifica el rol de cada usuario mediante el campo `rol` en la tabla `usuarios`, y en función de ese valor le muestra un menú distinto 
(ver Vistas/modulos/plantilla.php). Se identificaron 5 actores:

## 1. Administrador (rol: "Admin")
Actor con acceso completo al sistema. Según su menú (menu.php), es el único con acceso a "Solicitudes", "CRUD Carreras" e "Información".
**Puede:** gestionar solicitudes de residencia, administrar usuarios, gestionar el catálogo de empresas, administrar carpetas de documentos, 
emitir certificados, dar seguimiento a visitas a empresa, subir calificaciones, y realizar el CRUD completo de carreras.
**Sobre usuarios (confirmado en Vistas/modulos/usuarios.php):** es el único que puede crear usuarios con rol Admin o Jefe. También puede crear, editar 
y eliminar usuarios de cualquier otro rol.

## 2. Alumno (rol: "Alumno")
Actor con permisos de autoservicio, limitado a su propia información.
**Puede:** consultar el catálogo de empresas, ver su horario/materias inscritas ("Mi horario"), subir y consultar sus propios documentos 
(carpetas), solicitar su constancia/certificado (usando su propia matrícula), y consultar sus visitas a empresa.
**Restricción confirmada por código:** la vista de Usuarios (usuarios.php) expulsa explícitamente a este rol a la pantalla de inicio si intenta 
acceder por URL directa (`if ($_SESSION["rol"] == "Alumno" || ...) { redirige a inicio }`). 
No tiene acceso a "Usuarios" ni a "Subir Calificaciones" en ningún caso.

## 3. Asesor Académico (rol: "a_Academico")
Actor asignado a uno o varios alumnos (campo `a_academico` en la tabla de usuarios) para darles seguimiento académico.
**Puede:** acceder a Usuarios (ver, editar y eliminar cualquier usuario, igual que Admin y Jefe), ver el catálogo, gestionar carpetas de sus 
alumnos asignados, subir calificaciones, emitir certificados y dar seguimiento a visitas a empresa.
**Sobre usuarios (confirmado en Vistas/modulos/usuarios.php):** puede crear usuarios con rol Alumno, Asesor Académico o Asesor Industrial, 
pero NO puede crear usuarios con rol Admin ni Jefe.

## 4. Asesor Industrial (rol: "a_Industrial")
Actor asignado a uno o varios alumnos (campo `a_industrial`) para dar seguimiento desde el lado de la empresa donde el alumno realiza su 
residencia. Es el actor con menos permisos después del Alumno.
**Puede:** consultar carpetas de documentos, emitir certificados y dar seguimiento a visitas a empresa.
**Restricción confirmada por código:** al igual que Alumno, la vista de Usuarios lo redirige automáticamente a inicio si intenta acceder no tiene acceso a "Usuarios", "Catálogo" ni "Subir Calificaciones" (no aparecen en su menú, menuIndustrial.php).

## 5. Jefe (rol: "Jefe")
Actor con permisos casi idénticos al Asesor Académico en cuanto a acceso a vistas, probablemente Jefe de Carrera o de Departamento con función de supervisión.
**Puede:** acceder a Usuarios (ver, editar y eliminar cualquier usuario), ver el catálogo, gestionar carpetas, subir calificaciones, y emitir certificados.
**Sobre usuarios (confirmado en Vistas/modulos/usuarios.php):** igual que Asesor Académico, puede crear usuarios con rol Alumno, Asesor Académico o Asesor Industrial, 
pero NO Admin ni Jefe.

## Relación Entre Actores
Un Alumno tiene asignado un Asesor Académico y un Asesor Industrial específicos (visto en ActualizarUsuariosC, campos a_academico y a_industrial), quienes le dan seguimiento durante su proceso de residencia. 
El Jefe y el Administrador tienen visión más amplia sobre el catálogo de usuarios, no limitada a alumnos asignados específicamente.

## Matriz de Acceso a "Usuarios" (Evidencia Directa del Código)
| Acción | Admin | Asesor Académico | Jefe | Alumno | Asesor Industrial |
|---|---|---|---|---|---|
| Ver la lista completa | ✅ | ✅ | ✅ | ❌ | ❌ |
| Editar / eliminar cualquier usuario | ✅ | ✅ | ✅ | ❌ | ❌ |
| Crear usuario con rol Admin o Jefe | ✅ | ❌ | ❌ | ❌ | ❌ |
| Crear Alumno / Asesor Académico / Asesor Industrial | ✅ | ✅ | ✅ | ❌ | ❌ |

## Nota Sobre El Proceso Real vs. Lo Automatizado
Comparando con la documentación oficial del departamento (calendario de residencias y formatos), el sistema automatiza la parte administrativa 
y de seguimiento (solicitud, asignación de asesores, registro documental, calificaciones, constancias), pero deja fuera de digitalización los pasos 
que requieren firma física y validación directa de la empresa (cartas de presentación, aceptación, confidencialidad, código de ética, conformidad 
de la empresa), que siguen dependiendo de documentos en papel subidos como evidencia (PDF) al sistema.
