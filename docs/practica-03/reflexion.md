# Reflexión - Práctica 3

**Integrante:** Myrka Salazar

## ¿Qué Tan Fácil o Difícil Fue Identificar Los Actores y Sus Permisos Reales a Partir del Código, Comparado con Solo Leer Una Descripción del Sistema?

Fue más difícil de lo que esperaba. Al principio, con solo ver los cinco archivos de menú (menu.php, menuAlumno.php, menuAcademico.php, 
menuIndustrial.php, menuJefe.php) pensé que ya tenía identificados todos los permisos de cada actor, porque cada menú mostraba claramente qué 
opciones veía cada rol. Sin embargo, al construir el diagrama de casos de uso me di cuenta de que había hecho suposiciones (como que "gestionar" y 
"consultar" eran cosas distintas) que no estaban realmente sustentadas en el código, sino en cómo yo interpretaba los nombres de las cosas. Leer una 
descripción del sistema (o incluso los menús) da una idea general, pero solo revisando el código de las vistas y controladores se puede confirmar 
qué hace el sistema de verdad.

## ¿Qué Diferencia Encontraste Entre Lo Que "Parecía" Un Permiso y Lo Que El Código Realmente Hacía (El Caso de "Usuarios" y Quién Puede Crear Qué Rol)?

Al principio supuse que Admin, Asesor Académico y Jefe tenían permisos distintos sobre Usuarios: pensé que unos "gestionaban" (crear, editar, 
eliminar) y otros solo "consultaban". Pero al revisar el archivo usuarios.php encontré evidencia real de que los tres pueden editar y 
eliminar cualquier usuario por igual; la única diferencia real está en qué roles puede crear cada uno (Admin puede crear cualquier rol incluyendo 
Admin y Jefe; Asesor Académico y Jefe solo pueden crear Alumno, Asesor Académico o Asesor Industrial, pero no Admin ni Jefe). También encontré 
algo que no esperaba: el código expulsa directamente a Alumno y Asesor Industrial de esa vista si intentan entrar por URL, algo que no se ve 
en ningún menú, solo revisando el archivo completo.

## ¿Por Qué Es Importante Escribir Criterios de Aceptación Verificables En Una Historia de Usuario, En Lugar de Solo La Frase "Como... quiero... para..."?

Porque la frase "Como... quiero... para..." explica la intención general, pero no dice cómo saber si esa funcionalidad ya está bien hecha o no. Los 
criterios de aceptación (en formato Dado/Cuando/Entonces) obligan a pensar en casos concretos, incluyendo qué pasa cuando algo sale mal (por ejemplo, 
subir un archivo que no es PDF, o intentar calificar a un alumno que no me corresponde). Esto también ayuda a detectar, como nos pasó en esta 
práctica, posibles huecos de seguridad o validaciones que el código debería tener pero que no confirmamos si realmente existen 
(como si el formulario de crear usuario solo oculta opciones en el HTML o si el servidor también las bloquea).

Firma: Myrka<3
