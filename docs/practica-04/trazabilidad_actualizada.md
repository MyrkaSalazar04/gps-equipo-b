# Matriz de Trazabilidad — Práctica 3 (Actualizada en Práctica 4)

| Historia | Vista (Vistas/modulos) | Controlador | Tabla de BD |
|---|---|---|---|
| HU-01 | crearCuenta.php | UsuariosC::CrearCuenta() | usuarios |
| HU-02 | Ingresar.php | UsuariosC::IniciarSesionC() | usuarios |
| HU-03 | catalogo.php | MateriasC::VerMateriasC() *(no subirCatalogo.php)* | materias |
| HU-04 | Carpetas.php / verCarpeta.php | subirDoc.php | documentacion |
| HU-05 | inscrito.php | MateriasC::VerInscripcionesMaterias2C() | inscripciones |
| HU-06 | constancia-alumno.php / solicitud-Constancia.php | ConstanciaC.php | **constancias** *(no existe en el volcado oficial)* |
| HU-07 | plantilla.php (menuAcademico.php) | UsuariosC::VerUsuariosC() | usuarios |
| HU-08 | usuarios.php | UsuariosC::VerUsuariosC() | usuarios |
| HU-09 | usuarios.php (modal Crear Usuario) | UsuariosC::CrearUsuarioC() | usuarios |
| HU-10 | Editar-usuario.php | UsuariosC::ActualizarUsuariosC() / EliminarUsuariosC() | usuarios |
| HU-11 | calificaciones.php / nota-materia.php | MateriasC::VerNotasC() | notas |
| HU-12 | Carpetas.php / visitas.php | VisitasC.php | **visitas** *(no existe en el volcado oficial)* |

**Correcciones Respecto a La Versión de La Práctica 3:**
- **HU-03**: el controlador real de `catalogo.php` es `MateriasC::VerMateriasC()`, no `subirCatalogo.php` (ese archivo en realidad sube un PDF de catálogo de empresas a la tabla `inforesidencia`; es una función distinta que comparte nombre de vista).
- **HU-06** y **HU-12**: al revisar el código de `ConstanciaC.php` y `visitasC.php`, ambos apuntan a tablas literales `constancias` y `visitas` que **no existen en ninguna de las 17 tablas del volcado oficial `sistemacontrolescolar 11-06-2021.sql`**. Esto se reporta también como hallazgo en `evaluacion-modelo.md`.
