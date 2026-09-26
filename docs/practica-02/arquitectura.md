### Integrante: Myrka Salazar

### Explicación Del Patrón MVC En El Sistema ###

## ¿Qué Es El Patrón MVC?
El patrón Modelo-Vista-Controlador organiza el código en tres capas con responsabilidades separadas: el Modelo maneja los datos y se comunica 
con la base de datos, la Vista es la interfaz que ve el usuario, y el Controlador actúa como intermediario, recibiendo las peticiones y 
coordinando entre el Modelo y la Vista.

## Punto de Entrada Del Sistema (index.php y .htaccess)

**Lo que contiene .htaccess:**
Significa que todas las URLs que el usuario escribe en el navegador (por ejemplo sistema/usuarios/lista) se reescriben automáticamente y se 
convierten en una petición a index.php, pasando lo que el usuario escribió como parámetro url. Es decir: no importa qué dirección visite 
el usuario, el servidor siempre termina llamando a index.php.

**Lo que contiene index.php:**
Carga la configuración (config/app.php). Carga (con require/require_once) todos los Modelos y Controladores del sistema, uno por uno, de forma 
fija no los carga "bajo demanda" según lo que pida el usuario, sino todos de golpe cada vez que se recibe una petición. Carga las librerías 
de terceros PHPMailer. Al final (líneas 44-45), Crea un objeto de la clase Plantilla (definida en Vistas/plantilla.php) y llama a su método verPlantilla(). 
Es ahí, dentro de esa clase, donde seguramente se revisa el parámetro url que llegó desde .htaccess y se decide qué vista mostrar según el rol del usuario.

**¿Qué Archivo Recibe Todas Las Peticiones del Usuario?**
index.php, gracias a la regla de .htaccess que reescribe cualquier URL hacia él. Esto es el patrón de front controller.

**¿Hacia Dónde Las Redirige?**
Internamente, index.php no filtra nada por sí mismo: carga todos los Controladores y Modelos del sistema y delega la decisión de qué mostrar 
a la clase Plantilla, que interpreta el parámetro url y arma la vista correspondiente.

## Controlador (ejemplo: CarrerasC.php)
La clase CarrerasC es el Controlador del módulo de carreras. Recibe las peticiones y coordina todo su ciclo de vida: registrar una carrera nueva, 
consultar el listado o un registro específico, mostrar el formulario de edición, procesar la actualización cuando se envía, y eliminar un registro 
usando el id que llega por la URL. No accede directamente a la base de datos: le pide los datos a CarrerasM y después redirige al usuario a la 
vista correspondiente.

## Modelo (ejemplo: CarrerasM.php)
La clase CarrerasM hereda de ConexionBD y es la que se conecta a la base de datos usando PDO con sentencias preparadas (para evitar inyecciones SQL). 
Sus métodos hacen las operaciones básicas sobre la tabla de carreras: crear, consultar todas, obtener una por su id, buscar por una columna, actualizar y eliminar. 
Regresan los datos o un valor booleano al Controlador, que decide qué hacer con esa respuesta.

## Relación Entre Controlador y Modelo
CarrerasC nunca habla directamente con la base de datos: cuando necesita datos, llama a los métodos de CarrerasM, y este le regresa la información 
o confirma si la operación se hizo. Así, si algún día cambia la forma en que se guardan los datos, solo habría que modificar el Modelo, sin tocar 
el Controlador.

## Vistas
Las vistas del sistema están en la carpeta Vistas/modulos (49 archivos), y todas se cargan a través de Vistas/plantilla.php, que actúa como un 
punto central de renderizado según el menú y el rol del usuario.

## Conclusión: Cómo Aplica Este Sistema El Patrón MVC
El sistema sigue el patrón MVC de forma manual, sin usar ningún framework: cada módulo (por ejemplo "carreras") tiene su propio Controlador y su propio Modelo, 
identificables por el sufijo C o M en el nombre del archivo. Sin embargo, index.php carga TODOS los Controladores y Modelos en cada petición, 
en lugar de cargar solo los necesarios, lo cual no es una práctica eficiente ni escalable a medida que el sistema crece.
