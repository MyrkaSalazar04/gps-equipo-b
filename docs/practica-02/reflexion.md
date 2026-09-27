# Reflexión - Práctica 2

**Integrante:** Myrka Salazar

## ¿Qué porcentaje aproximado de los archivos del repositorio es código propio? ¿Qué implica eso para estimar el tamaño del proyecto?

Al hacer el inventario me di cuenta de que la mayoría de los archivos del repositorio no son código propio, sino librerías de terceros: solo 
bower_components tiene aproximadamente 6,800 archivos, a los que hay que sumar tcpdf, PHPMailer y PHPExcel. En comparación, las carpetas de código 
propio (Controladores, Modelos, Vistas/modulos, Ajax, expExcel, etc.) son muchísimo más pequeñas. 
Esto implica que si alguien intentara estimar el tamaño del proyecto contando todos los archivos del repositorio sin distinguir esta diferencia, 
obtendría una cifra completamente inflada y poco realista. 
Para estimar el tamaño real hay que excluir las librerías de terceros y enfocarse solo en el código que el equipo original desarrolló.

## ¿Qué riesgos trae depender de librerías que el equipo no escribió ni mantiene?

El riesgo principal es que si esas librerías dejan de recibir actualizaciones (como parece ser el caso de PHPExcel, que ya está descontinuada a favor de 
PhpSpreadsheet) o tienen vulnerabilidades de seguridad conocidas, el sistema queda expuesto sin que el equipo pueda corregirlo fácilmente, 
porque no conocen a fondo ese código. 
También existe el riesgo de incompatibilidad: si en algún momento se necesita actualizar la versión de PHP, estas librerías antiguas podrían dejar de 
funcionar correctamente, como ya advierte el propio manual sobre PHPExcel y PHP 8.

## ¿La arquitectura encontrada facilita o dificulta que otro equipo le dé mantenimiento? ¿Por qué?

Facilita algunas cosas: al seguir el patrón MVC de forma consistente (cada módulo con su Controlador y su Modelo, identificables por el sufijo C o M), 
es relativamente fácil ubicar dónde está la lógica de cada funcionalidad. 
Sin embargo, también dificulta el mantenimiento en otros aspectos: index.php carga TODOS los Controladores y Modelos en cada petición sin importar cuáles 
se van a usar, lo cual no es eficiente y hace que cualquier error en un solo archivo pueda afectar a todo el sistema. 
Además, el hecho de que no se use ningún framework moderno significa que un desarrollador nuevo tiene que entender las convenciones propias del proyecto 
en vez de apoyarse en documentación estándar de un framework conocido.

Firma del Integrante: Myrka<3
