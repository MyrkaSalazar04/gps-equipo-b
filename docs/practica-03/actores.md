# Actores del sistema

El sistema identifica el rol de cada usuario mediante el campo `rol` en la tabla `usuarios`, y en función de ese valor le muestra un menú distinto 
(ver Vistas/modulos/plantilla.php). Se identificaron 5 actores:

## 1. Administrador (rol: "Admin")
Actor con acceso completo al sistema.
**Puede:** gestionar solicitudes de residencia, administrar usuarios (crear, editar, eliminar), gestionar el catálogo de empresas, administrar carpetas 
de documentos, emitir certificados, dar seguimiento a visitas a empresa, subir calificaciones, y realizar el CRUD completo de carreras.

## 2. Alumno (rol: "Alumno")
Actor con permisos de autoservicio, limitado a su propia información.
**Puede:** consultar el catálogo de empresas, ver su horario/materias inscritas, subir y consultar sus propios documentos (carpetas), solicitar 
su constancia/certificado (usando su propia matrícula), y consultar sus visitas a empresa.

## 3. Asesor Académico (rol: "a_Academico")
Actor asignado a uno o varios alumnos (campo `a_academico` en la tabla de usuarios) para darles seguimiento académico.
**Puede:** consultar usuarios, ver el catálogo, gestionar carpetas de sus alumnos asignados, subir calificaciones, emitir certificados y dar seguimiento a visitas a empresa.

## 4. Asesor Industrial (rol: "a_Industrial")
Actor asignado a uno o varios alumnos (campo `a_industrial`) para dar seguimiento desde el lado de la empresa donde el alumno realiza su residencia.
**Puede:** consultar carpetas de documentos, emitir certificados y dar seguimiento a visitas a empresa. Es el actor con menos permisos después del Alumno.

## 5. Jefe (rol: "Jefe")
Actor con permisos casi idénticos al Asesor Académico, probablemente Jefe de Carrera o de Departamento con función de supervisión.
**Puede:** consultar usuarios, ver el catálogo, gestionar carpetas, subir calificaciones, y emitir certificados.

## Relación Entre Actores
Un Alumno tiene asignado un Asesor Académico y un Asesor Industrial específicos (visto en ActualizarUsuariosC, campos a_academico y 
a_industrial), quienes le dan seguimiento durante su proceso de residencia. El Jefe y el Administrador tienen visión más amplia, 
no limitada a alumnos asignados específicamente.

## Nota Sobre El Proceso Real vs. Lo Automatizado
Comparando con la documentación oficial del departamento (calendario de residencias y formatos), el sistema automatiza la parte administrativa 
y de seguimiento (solicitud, asignación de asesores, registro documental, calificaciones, constancias), pero deja fuera de digitalización los pasos 
que requieren firma física y validación directa de la empresa (cartas de presentación, aceptación, confidencialidad, código de ética, conformidad 
de la empresa), que siguen dependiendo de documentos en papel subidos como evidencia (PDF) al sistema.
