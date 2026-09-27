# Diccionario de Datos — Sistema de Control Escolar

## Tabla: usuarios
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único del usuario |
| matricula | int | Número de matrícula, usado también como usuario de login |
| clave | int | Contraseña del usuario |
| nombre | varchar(200) | Nombre del usuario |
| apellido | varchar(200) | Apellido del usuario |
| id_carrera | int (FK → carrera.id) | Carrera a la que pertenece |
| fechanac | text | Fecha de nacimiento |
| telefono | text | Teléfono de contacto |
| direccion | text | Dirección del usuario |
| correo | text | Correo electrónico |
| rol | text | Rol del usuario: Admin, Alumno, a_Academico, a_Industrial, Jefe |
| tipo | text | Clasificación adicional del usuario (uso poco claro en el código) |
| periodo | text | Periodo escolar en el que se registró |
| a_academico | text (FK\* por nombre) | Nombre del Asesor Académico asignado (solo alumnos) |
| a_industrial | text (FK\* por nombre) | Nombre del Asesor Industrial asignado (solo alumnos) |
| institucion | text | Institución de procedencia (uso poco claro) |
| especialidad | text | Especialidad o tema de residencia del alumno |

## Tabla: carrera
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único de la carrera |
| nombre | text | Nombre de la carrera |

## Tabla: materias
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único de la materia |
| id_carrera | int (FK → carrera.id) | Carrera a la que pertenece la materia |
| codigo | text | Código o clave de la materia |
| nombre | text | Nombre de la materia |
| grado | text | Grado o semestre en que se cursa |
| tipo | text | Tipo de materia (ej. "Servicio Social") |
| PDF | blob | Archivo PDF relacionado con la materia |

## Tabla: comisiones
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único de la comisión (grupo/horario) |
| id_materia | int (FK → materias.id) | Materia a la que pertenece la comisión |
| c_maxima | int | Cupo máximo de alumnos |
| horario | text | Horario de la comisión |
| numero | int | Número de grupo |
| horas | text | Horas asignadas |

## Tabla: inscripciones
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único de la inscripción |
| id_materia | int (FK → materias.id) | Materia en la que se inscribe |
| id_alumno | int (FK → usuarios.id) | Alumno inscrito |
| id_comision | int (FK → comisiones.id) | Comisión/grupo en el que se inscribe |

## Tabla: notas
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único de la calificación |
| id_alumno | int (FK → usuarios.id) | Alumno calificado |
| matricula | int | Matrícula del alumno (dato repetido) |
| id_materia | int (FK → materias.id) | Materia calificada |
| fecha | text | Fecha del registro |
| a_academico | text | Nombre del asesor académico que calificó |
| a_industrial | text | Nombre del asesor industrial que calificó |
| tipo | text | Tipo de evaluación |
| estado | text | Estado del proceso |
| nota_final | text | Calificación final |
| nota_academico | text | Calificación asignada por el asesor académico |
| nota_industrial | text | Calificación asignada por el asesor industrial |
| PDF | text | Documento de soporte de la calificación |

## Tabla: documentos
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único del documento |
| nombre | text | Nombre original del archivo |
| PDF | text | Nombre del archivo guardado en el servidor |
| fecha | text | Fecha de subida |
| matricula | int (FK → usuarios.matricula) | Alumno propietario del documento |
| id_materia | int (FK → materias.id) | Materia relacionada |

## Tabla: reportes
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único del reporte |
| nombre | text | Nombre del archivo |
| PDF | text | Nombre del archivo guardado |
| fecha | text | Fecha de entrega |
| matricula | int (FK → usuarios.matricula) | Alumno que entrega el reporte |
| id_materia | int (FK → materias.id) | Materia relacionada |
| nota_industrial | int | Calificación del asesor industrial sobre el reporte |
| nota_academico | int | Calificación del asesor académico sobre el reporte |
| promedioFinal | int | Promedio final del reporte |
| revisadoJefe | int | Indicador si el Jefe revisó el reporte (booleano) |
| revisadoAdmin | int | Indicador si el Admin revisó el reporte (booleano) |

## Tabla: solicitudes
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único de la solicitud |
| fechaSolicitud | text | Fecha en que se envió la solicitud |
| periodo | text | Periodo escolar |
| nombreCarta | text | Nombre de la carta de presentación |
| nombreEmpresa | text | Empresa donde se realizará la residencia |
| domicilioEmpresa | text | Dirección de la empresa |
| telefonoEmpresa | text | Teléfono de la empresa |
| emailEmpresa | text | Correo de la empresa |
| nombreAlumno | text | Nombre del alumno solicitante (dato denormalizado) |
| carreraAlumno | text | Carrera del alumno (dato denormalizado, guardado como texto) |
| especialidadAlumno | text | Especialidad del proyecto |
| matricula | int (FK → usuarios.matricula) | Alumno que solicita |
| emailAlumno | text | Correo del alumno |
| telefonoAlumno | int | Teléfono del alumno |
| tipoProyecto | text | Tipo de proyecto de residencia |
| IMSS | text | Número de afiliación al IMSS |
| polizaSeguroAlumno | text | Número de póliza de seguro |
| estado | int | Estado de la solicitud (numérico, sin catálogo visible) |

## Tabla: notificaciones
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único de la notificación |
| numero | int | Número de notificación |
| estado | text | Estado de la notificación |
| id_alumno | int (FK → usuarios.id) | Alumno relacionado |
| id_aAcademico | int (FK → usuarios.id) | Asesor académico relacionado |
| id_aIndustrial | int (FK → usuarios.id) | Asesor industrial relacionado |

## Tabla: evaluaciones
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único de la evaluación |
| estado | int | Estado de la evaluación |
| id_carrera | int (FK → carrera.id) | Carrera relacionada |
| id_materia | int (FK → materias.id) | Materia evaluada |
| carrera | text | Nombre de la carrera (dato denormalizado) |
| a_academico | text | Nombre del asesor académico |
| fecha | text | Fecha de la evaluación |
| a_industrial | text | Nombre del asesor industrial |
| hora | text | Hora de la evaluación |
| tipo | text | Tipo de evaluación |

## Tabla: examenes
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único del examen |
| estado | int | Estado del examen |
| id_carrera | int (FK → carrera.id) | Carrera relacionada |
| id_materia | int (FK → materias.id) | Materia relacionada |
| aula | text | Aula donde se aplica |
| profesor | text | Profesor a cargo |
| hora | text | Hora del examen |
| fecha | text | Fecha del examen |

## Tabla: inscribir_examenes
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único |
| id_alumno | int (FK → usuarios.id) | Alumno inscrito al examen |
| id_examen | int (FK → examenes.id) | Examen al que se inscribe |
| matricula | text | Matrícula del alumno (dato repetido) |

## Tabla: ajustes
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador (tabla tipo configuración, un solo registro) |
| periodo | text | Nombre del periodo escolar activo |
| 1_fecha_inicio / 1_fecha_fin | text | Fechas de la primera etapa del periodo |
| 2_fecha_inicio / 2_fecha_fin | text | Fechas de la segunda etapa del periodo |
| evaluacion_i / evaluacion_f | text | Fechas de inicio/fin de evaluaciones |
| inscripciones_i / inscripciones_f | text | Fechas de inicio/fin de inscripciones |
| h_reportes | int | Bandera/hora relacionada a reportes |
| h_evaluacion | int | Bandera/hora relacionada a evaluación |
| h_inscripciones | int | Bandera/hora relacionada a inscripciones |

## Tabla: procesos
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único |
| info | text | Texto de un requisito del proceso de residencia |
| num | int | Número de orden del requisito |

## Tabla: inforesidencia
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador (tabla singleton, un solo registro) |
| objetivos | text | Texto con los objetivos del programa de residencias |
| empresasPDF | text | Nombre del PDF con el catálogo de empresas |
| calendarioPDF | text | Nombre del PDF con el calendario oficial |

## Tabla: documentacion
| Columna | Tipo | Descripción |
|---|---|---|
| id | int (PK) | Identificador único |
| PDF | text | Nombre del archivo (ej. código de ética) |
| nombre | text | Nombre descriptivo del documento |
---

**Nota general:** ningún `FOREIGN KEY` está declarado formalmente en la base de datos (confirmado al revisar el `.sql` completo); todas las relaciones marcadas como FK son por convención de nombres de columna, no por integridad referencial real de MySQL.
