# Evaluación del Modelo de Datos

## Hallazgos Principales

### 1. Cero Llaves Foráneas Declaradas
En las 17 tablas del volcado `sistemacontrolescolar 11-06-2021.sql` no existeni una sola cláusula `REFERENCES`. 
Todas las relaciones (`usuarios.id_carrera → carrera.id`,`comisiones.id_materia → materias.id`, `notas.id_alumno → usuarios.id`, etc.) deben
inferirse por el nombre de la columna. 
Esto significa que la base de datos nogarantiza integridad referencial: se puede insertar un `id_materia` que no exista,
o borrar un usuario sin que el motor avise que hay notas, inscripciones osolicitudes huérfanas.

### 2. Falta de Un Estándar Para Referenciar Al Usuario
El sistema mezcla dos formas distintas de apuntar a un alumno:
- Por **`id`** (llave interna): `notas.id_alumno`, `inscripciones.id_alumno`,  `inscribir_examenes.id_alumno`, `notificaciones.id_alumno`.
- Por **`matricula`** (dato de negocio): `solicitudes.matricula`, `documentos.matricula`, `reportes.matricula`.

Al no haber un criterio único, cualquier consulta que cruce estas tablas necesitaun `JOIN` adicional contra `usuarios` para traducir entre ambos valores, lo que
aumenta la probabilidad de errores y hace más difícil el mantenimiento.

### 3. Contraseñas en Texto Plano
La columna `usuarios.clave` es de tipo `int(10)`, sin ningún mecanismo de hash(bcrypt, SHA-256, etc.). Además, en los datos de ejemplo la contraseña de cada
usuario es idéntica a su matrícula, lo que la vuelve trivialmente adivinable.
Esto es una vulnerabilidad de seguridad grave, no solo un detalle de diseño.

### 4. Diseño Desnormalizado En `Solicitudes`
La tabla `solicitudes` guarda directamente todos los datos del alumno(`nombreAlumno`, `carreraAlumno`, `especialidadAlumno`, `emailAlumno`,
`telefonoAlumno`) y de la empresa (`nombreEmpresa`, `domicilioEmpresa`,`telefonoEmpresa`, `emailEmpresa`) como columnas de texto, en vez de referenciar
tablas separadas de `alumnos` y `empresas`. 
Esto duplica la misma informacióndel alumno o de la empresa en cada solicitud que se registre, en vez demantenerla una sola vez.

### 5. Tipos de Dato Poco Estrictos
La mayoría de las columnas —incluyendo fechas (`fechanac`, `fechaSolicitud`) y correos (`correo`, `emailAlumno`, `emailEmpresa`)— están declaradas como `text`
en vez de `date`, `datetime` o `varchar` con longitud definida. Esto impide quela propia base de datos valide formatos y obliga a que toda la validación viva
en el código PHP.

## Conclusión
El modelo funciona para la operación diaria del sistema, pero no está diseñadopara escalar ni para garantizar consistencia de datos. Un rediseño debería:
declarar las llaves foráneas, unificar la referencia a usuario (`id` en todoslos casos), normalizar `solicitudes` separando empresa/alumno en tablas propias,
cifrar contraseñas, y usar tipos de dato específicos en vez de `text` genérico.
