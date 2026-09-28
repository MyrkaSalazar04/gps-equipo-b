# Reflexión — Práctica 5: Estimación Inversa de Tamaño, Esfuerzo y Costo

**Integrantes:** Myrka Salazar, Jehyson Martínez, José Martínez

## ¿Por Qué Los Dos Métodos Dieron Resultados Distintos? ¿Cuál Te Parece Más Confiable?

COCOMO y Puntos de Función parten de bases completamente diferentes para medir lo mismo. COCOMO mide el tamaño del sistema en líneas de código y aplica constantes
empíricas (2.4 y 1.05) que fueron calibradas sobre una base histórica de proyectos que no necesariamente se parece a este sistema en particular; además, su fórmula captura implícitamente todo el ciclo de vida del desarrollo, incluida la curva de aprendizaje de un equipo que apenas se está formando. Puntos de Función, en cambio, mide la funcionalidad de negocio entregada (entradas, salidas, consultas y archivos de datos) sin importar el lenguaje de programación, pero su conversión a esfuerzo depende totalmente de la tasa de productividad que se elija (en nuestro caso, 7 horas por punto de función, tomada de un promedio de la industria y no de datos reales de este proyecto).

Obtuve **29.87 personas-mes** con COCOMO y **10.89 personas-mes** con Puntos de Función: casi 3 veces de diferencia. Me parece que Puntos de Función es un poco
más confiable para *este* sistema, porque está anclado a funcionalidades concretas que sí verifiqué en las historias de usuario y en el modelo de datos,
mientras que COCOMO depende de un conteo de líneas que puede inflarse o desinflarse según qué tan "verboso" sea el estilo de programación del
desarrollador original (por ejemplo, su código de plantilla.php mezcla HTML y PHP de forma poco modular, lo que puede aumentar las líneas sin aumentar la
funcionalidad real). Aun así, ninguno de los dos métodos por sí solo me daría la confianza suficiente para presentarle una sola cifra al cliente sin más contexto.

---

## ¿Por Qué Los Dos Equipos Obtuvieron Cifras Distintas Analizando El Mismo Sistema?

Al comparar mis cifras con las del Equipo A en el cierre grupal (ver `delphi.md`),
la diferencia fue clara:

| Equipo | KLOC | PF | Esfuerzo COCOMO (PM) | Esfuerzo PF (PM) | Costo total (MXN) |
|---|---|---|---|---|---|
| A | 8.66 | 459 | 23.15 | 23.81 | $388,209 – $399,334 |
| B (yo) | 11.039 | 249 | 29.87 | 10.89 | $204,257.81 – $560,129.87 |

Lo primero que salta a la vista es que, aunque el tamaño en KLOC es parecido entre los dos equipos, el total de Puntos de Función es muy distinto (459 contra 249).
Esto me hace pensar que la principal fuente de diferencia no fue el tamaño del código en sí, sino los **criterios de clasificación** que cada equipo usó al
contar Entradas, Salidas, Consultas y Archivos Lógicos — por ejemplo, cuántas historias de usuario consideró cada quien, o si incluyeron pantallas como el login o el menú de navegación como funciones de negocio.

También es notable que el rango entre mis dos métodos (COCOMO vs. PF) es mucho más amplio (~174% de diferencia) que el del Equipo A (~3%). 
Eso sugiere que la tasa de productividad (horas/PF) o el salario base que usó cada equipo en su investigación fueron bastante distintos entre sí, 
lo cual demuestra que ese tipo de dato "de mercado" no es tan estándar como parece, y que la fuente que se elige para investigarlo cambia el resultado final de forma importante. 
Esto refuerza la idea de que la estimación no depende solo de contar bien el sistema, sino también de los supuestos externos (salarios, productividad) que cada persona decide usar.

---

## ¿Qué Aprendí Sobre La Incertidumbre de Estimar Un Proyecto Antes de Construirlo?

Aprendí que estimar no es una operación matemática exacta, sino un ejercicio de juicio apoyado en métricas. Dos métodos "formales" y reconocidos en la industria
(COCOMO y Puntos de Función) pueden dar cifras que difieren en cientos de miles de pesos para el mismo sistema, simplemente por las suposiciones que cada uno hace.
Esto me hizo entender por qué en proyectos reales rara vez se confía en un solo número: se usan varios métodos, se contrastan, y se ajustan con el criterio de
personas con experiencia. También aprendí que la calidad de una estimación depende directamente de qué tan bien se conoce el sistema antes de medirlo encontrar código de negocio escondido dentro de una carpeta de librería, o tablas que no existen en el volcado real de la base de datos, me hubiera hecho estimar
mal si no lo hubiera revisado con cuidado en las prácticas anteriores. 
Estimar bien, entonces, depende tanto del método que se elige como de qué tan a fondo se investigó el producto antes de aplicarlo.

**Firma del Integrante:** Myrka<3
**Firma del Integrante:**
**Firma del Integrante:**
