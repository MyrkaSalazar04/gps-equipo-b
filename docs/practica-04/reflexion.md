# Reflexión — Práctica 4

# Integrantes: Myrka Salazar, Jehyson Martínez, José Martínez

## ¿Qué Consecuencias Tiene Que La Base de Datos No Declare Llaves Foráneas?

Al no existir ninguna cláusula `REFERENCES` en las 17 tablas del volcado oficial,el motor de base de datos no impide insertar un registro que apunte a algo
que no existe (por ejemplo, una inscripción con un `id_materia` inválido),ni evita que se borre un registro del que dependen otros (borrar un usuario
sin que el sistema avise que tiene notas, solicitudes o inscripcionesasociadas). 
Toda esa responsabilidad recae únicamente en el código PHP, así que un error de programación o una actualización manual directa a la base de
datos puede dejarla en un estado inconsistente sin que nadie lo note hastaque un reporte o una consulta falle.

## ¿Qué Datos Personales Guarda El Sistema y Qué Obligaciones Legales Implica Eso Para El Instituto?

El sistema guarda datos personales de estudiantes en varias tablas: en`usuarios` se almacenan nombre, apellido, fecha de nacimiento, teléfono,
dirección y correo; en `solicitudes` se agregan además el nombre y correo delalumno, su matrícula, el número de seguro social (IMSS) y la póliza de
seguro. A esto se suman los documentos personales que vimos en elrepositorio (kardex, cartas de liberación). Esto convierte al Instituto en
responsable del tratamiento de datos personales bajo la Ley Federal deProtección de Datos Personales en Posesión de los Particulares, lo que
obliga a tener un aviso de privacidad, medidas de seguridad para protegeresa información (algo que hoy no se cumple, ya que ni siquiera lascontraseñas 
están cifradas) y mecanismos para que el titular de los datospueda ejercer sus derechos de acceso, rectificación, cancelación yoposición (ARCO).

## ¿Qué Cambiarían del Modelo Si Lo Rediseñaran?

Declararíamos explícitamente las llaves foráneas para que la propia base de datos garantice la integridad referencial. Unificaríamos el criterio para
referenciar a un usuario (usar siempre `id` en vez de mezclar `id` y `matricula` entre tablas). Normalizaríamos `solicitudes`, separando los
datos de la empresa en una tabla `empresas` propia en vez de repetirlos encada solicitud. 
Cifraríamos las contraseñas con un algoritmo de hash en vez de guardarlas como enteros en texto plano. Y crearíamos (o corregiríamos la
referencia a) las tablas `constancias` y `visitas`, que el código actual necesita pero que no existen en el volcado oficial de la base de datos.

Firma del Integrante: Myrka<3
Firma del Integrante:
Firma del Integrante:
