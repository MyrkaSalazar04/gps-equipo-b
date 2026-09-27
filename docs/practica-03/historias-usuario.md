# Historias de Usuario — Práctica 3

Formato: Como [actor], quiero [acción], para [beneficio].
Prioridad según MoSCoW (Must / Should / Could / Won't).

---

## Actor: Alumno

### HU-01
Como Alumno, quiero crear mi cuenta con mi matrícula, para poder acceder al sistema y comenzar mi proceso de residencia.

**Criterios de aceptación:**
- Dado que soy un alumno sin cuenta, cuando lleno el formulario de `crearCuenta` con mi matrícula, nombre, carrera y demás datos, entonces el sistema crea mi usuario con rol "Alumno".
- Dado que dejo algún campo obligatorio vacío, cuando intento enviar el formulario, entonces el sistema no crea la cuenta y me redirige de vuelta al login.

**Prioridad (MoSCoW):** Must

---

### HU-02
Como Alumno, quiero iniciar sesión con mi matrícula y contraseña, para acceder a mi información personal dentro del sistema.

**Criterios de aceptación:**
- Dado que ingreso mi matrícula y contraseña correctas, cuando presiono "Iniciar sesión", entonces el sistema me redirige a `inicio` y guarda mi rol, carrera y datos en sesión.
- Dado que ingreso una contraseña incorrecta, cuando intento iniciar sesión, entonces el sistema muestra un mensaje de error y me ofrece la opción de recuperar contraseña.

**Prioridad (MoSCoW):** Must

---

### HU-03
Como Alumno, quiero consultar el catálogo de empresas vinculadas, para elegir dónde realizar mi residencia profesional.

**Criterios de aceptación:**
- Dado que tengo sesión iniciada como Alumno, cuando entro a "Catálogo", entonces veo la lista de empresas disponibles con su sector y actividad.
- Dado que el catálogo está vacío o no carga, cuando entro a esa sección, entonces el sistema me muestra un mensaje indicándolo, no una pantalla en blanco.

**Prioridad (MoSCoW):** Must

---

### HU-04
Como Alumno, quiero subir mis documentos (CV, actas, cartas, constancias) a mi carpeta personal, para cumplir con los requisitos administrativos de mi residencia.

**Criterios de aceptación:**
- Dado que tengo sesión iniciada, cuando entro a "Carpetas" y subo un archivo PDF, entonces el documento queda asociado a mi matrícula y visible para mis asesores.
- Dado que intento subir un archivo que no es PDF, cuando lo selecciono, entonces el sistema rechaza el archivo y me indica el formato permitido.

**Prioridad (MoSCoW):** Must

---

### HU-05
Como Alumno, quiero ver mi horario de materias inscritas ("Mi horario"), para saber qué materias curso en el periodo actual.

**Criterios de aceptación:**
- Dado que tengo sesión iniciada, cuando entro a "Mi horario", entonces veo únicamente las materias en las que estoy inscrito, no las de otros alumnos.

**Prioridad (MoSCoW):** Should

---

### HU-06
Como Alumno, quiero solicitar mi constancia/certificado usando mi propia matrícula, para comprobar mi situación en el proceso de residencia.

**Criterios de aceptación:**
- Dado que tengo sesión iniciada, cuando entro a "Certificados", entonces el sistema genera la constancia usando mi matrícula y carrera automáticamente (sin que pueda solicitar la de otro alumno).

**Prioridad (MoSCoW):** Should

---

## Actor: Asesor Académico

### HU-07
Como Asesor Académico, quiero iniciar sesión y ver únicamente el menú correspondiente a mi rol, para acceder solo a las funciones que me corresponden dentro del sistema.

**Criterios de aceptación:**
- Dado que inicio sesión con un usuario de rol "a_Academico", cuando el sistema carga la plantilla, entonces se muestra `menuAcademico.php` (Inicio, Usuarios, Catálogo, Carpetas, Subir Calificaciones, Certificados, Visitas a empresa).
- Dado que intento acceder por URL directa a una sección exclusiva de Admin (por ejemplo "Solicitudes" o "CRUD Carreras"), cuando el sistema procesa la petición, entonces debería impedir el acceso, ya que esas rutas no están en mi menú.

**Prioridad (MoSCoW):** Must

---

### HU-08
Como Asesor Académico, quiero ver la lista de alumnos que tengo asignados en la pestaña "Alumnos" de Usuarios, para dar seguimiento únicamente a quienes me corresponden.

**Criterios de aceptación:**
- Dado que tengo alumnos asignados (campo `a_academico` igual a mi nombre), cuando entro a la pestaña "Alumnos", entonces veo solo a esos alumnos y a los que aún no tienen asesor asignado.
- Dado que un alumno de mi misma carrera está asignado a otro Asesor Académico, cuando reviso la lista, entonces ese alumno NO debe aparecerme.

**Prioridad (MoSCoW):** Must

---

### HU-09
Como Asesor Académico, quiero crear cuentas de usuario para Alumno, Asesor Académico o Asesor Industrial, para dar de alta al personal operativo sin depender del Administrador.

**Criterios de aceptación:**
- Dado que soy Asesor Académico, cuando abro el formulario "Crear Nuevo Usuario", entonces solo veo las opciones Alumno, Asesor Académico y Asesor Industrial (no veo Admin ni Jefe).
- Dado que lleno el formulario correctamente, cuando presiono "Crear", entonces el nuevo usuario queda visible en la pestaña correspondiente a su rol.

**Prioridad (MoSCoW):** Must

---

### HU-10
Como Asesor Académico, quiero editar o eliminar los usuarios que veo en mi lista, para mantener actualizada su información o dar de baja cuentas que ya no correspondan.

**Criterios de aceptación:**
- Dado que estoy en la lista de usuarios, cuando presiono el botón de editar, entonces se abre el formulario `Editar-usuario` con los datos precargados.
- Dado que presiono el botón de eliminar y confirmo, entonces el usuario se elimina de la base de datos.

**Prioridad (MoSCoW):** Should

---

### HU-11
Como Asesor Académico, quiero subir las calificaciones de mis alumnos asignados, para reportar su desempeño en el periodo de residencia a control escolar.

**Criterios de aceptación:**
- Dado que tengo sesión iniciada, cuando entro a "Subir Calificaciones" y selecciono a un alumno mío, entonces puedo capturar y guardar su calificación.
- Dado que intento subir la calificación de un alumno que no me corresponde, cuando busco su matrícula, entonces el sistema no debería permitírmelo.

**Prioridad (MoSCoW):** Must

---

### HU-12
Como Asesor Académico, quiero consultar las carpetas de documentos y dar seguimiento a las visitas a empresa de mis alumnos, para verificar que estén cumpliendo correctamente su proceso de residencia.

**Criterios de aceptación:**
- Dado que tengo sesión iniciada, cuando entro a "Carpetas" de un alumno asignado, entonces puedo ver los documentos que ha subido.
- Dado que entro a "Visitas a empresa", cuando reviso el listado, entonces veo las visitas registradas relacionadas con mis alumnos.

**Prioridad (MoSCoW):** Should
