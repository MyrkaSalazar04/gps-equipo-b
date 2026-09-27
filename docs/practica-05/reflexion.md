# Reflexión — Práctica 5: Estimación Inversa de Tamaño, Esfuerzo y Costo

## ¿Por Qué Los Dos Métodos Dieron Resultados Distintos? ¿Cuál Te Parece Más Confiable?

COCOMO y Puntos de Función parten de bases completamente diferentes para medir lomismo. 
COCOMO mide el tamaño del sistema en líneas de código y aplica constantes empíricas (2.4 y 1.05) que fueron calibradas sobre una base histórica de proyectos
que no necesariamente se parece a este sistema en particular; además, su fórmula captura implícitamente todo el ciclo de vida del desarrollo, incluida la curva de
aprendizaje de un equipo que apenas se está formando. 
Puntos de Función, en cambio, mide la funcionalidad de negocio entregada (entradas, salidas, consultas y archivos de datos) sin importar el lenguaje de 
programación, pero su conversión a esfuerzodepende totalmente de la tasa de productividad que se elija (en nuestro caso, 7 horas por punto de función, 
tomada de un promedio de la industria y no de datos reales de este proyecto).

Obtuve **29.87 personas-mes** con COCOMO y **10.89 personas-mes** con Puntos de Función: casi 3 veces de diferencia. Me parece que Puntos de Función es un poco
más confiable para *este* sistema, porque está anclado a funcionalidades concretas que sí verifiqué en las historias de usuario y en el modelo de datos,
mientras que COCOMO depende de un conteo de líneas que puede inflarse o desinflarse según qué tan "verboso" sea el estilo de programación del
desarrollador original (por ejemplo, su código de plantilla.php mezcla HTML y PHP de forma poco modular, lo que puede aumentar las líneas 
sin aumentar la funcionalidad real). Aun así, ninguno de los dos métodos por sí solo me daría la confianza suficiente para presentarle una sola cifra al 
cliente sin máscontexto.

---

## ¿Por Qué Los Dos Equipos Obtuvieron Cifras Distintas Analizando El Mismo Sistema?

- **Qué se cuenta como código propio.** Encontré, por ejemplo, archivos de
  negocio (`Constancia.php`, `expUsuarios.php`, etc.) mezclados dentro de la
  carpeta de la librería de terceros `tcpdf`. Alguien que no revisara con el
  mismo cuidado esa carpeta obtendría un conteo de LOC y de Puntos de Función
  distinto al mío.
- **Criterios de clasificación en Puntos de Función.** Decisiones como incluir o
  no el login como Entrada Externa, o cómo agrupar consultas similares, son
  subjetivas y pueden variar de una persona a otra aunque ambas revisen el mismo
  código.
- **La tasa de productividad elegida.** Yo usé 7 horas/PF de una fuente
  específica; otra persona con otra fuente obtendría un esfuerzo final distinto
  aunque su conteo de PF fuera idéntico al mío.

---

## ¿Qué Aprendí Sobre La Incertidumbre de Estimar Un Proyecto Antes de Construirlo?

Aprendí que estimar no es una operación matemática exacta, sino un ejercicio de juicio apoyado en métricas. Dos métodos "formales" y reconocidos en la industria
(COCOMO y Puntos de Función) pueden dar cifras que difieren en cientos de miles de pesos para el mismo sistema, simplemente por las suposiciones que cada uno hace.
Esto me hizo entender por qué en proyectos reales rara vez se confía en un solo número: se usan varios métodos, se contrastan, y se ajustan con el criterio de
personas con experiencia. También aprendí que la calidad de una estimación depende directamente de qué tan bien se conoce el sistema antes de medirlo 
encontrar código de negocio escondido dentro de una carpeta de librería, o tablas que no existen en el volcado real de la base de datos, me hubiera hecho estimar
mal si no lo hubiera revisado con cuidado en las prácticas anteriores. 
Estimar bien, entonces, depende tanto del método que se elige como de qué tan a fondo se investigó el producto antes de aplicarlo.

Firma: Myrka<3
