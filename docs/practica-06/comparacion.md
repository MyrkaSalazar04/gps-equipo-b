# Comparación: Estimado vs. Real — Práctica 6

## Datos del Historial de Git (Repositorio Original, Hasta El Commit `1d726bf`)

| Dato | Valor |
|---|---|
| Primer commit | 2021-03-27 ("Initial commit") |
| Último commit | 2021-06-21 ("2") |
| Total de commits | 10 |
| Duración calendario | 86 días (≈ 2.8 meses) |
| Días con actividad | 8 días distintos |
| Autores | 2 nombres en Git (`cbarreral` con 8 commits y `Carlos Alberto Barrera Lugo` con 2), muy probablemente la misma persona con dos configuraciones de Git |

## Fases Identificadas (Evidencia En Los Mensajes de Commit)

1. **Estructura inicial** (27 mar): "Initial commit".
2. **Módulo correo** (27–29 mar): "Implantación de notificaciones mediante correo" e "integración de la clase phpmailer".
3. **Rediseño + Chat** (8 abr): "rediseño moderno e incorporación del modulo de observaciones (Chat)".
4. **Módulo observaciones** (8 abr): "Modulo de Observaciones en carpetas".
5. **Corrección de bugs** (9 abr): "correccion de bugs en el modulo constancia".
6. **Pausa sin commits** (10 abr – 8 jun): unos 60 días sin actividad registrada.
7. **Módulo residencia** (9 jun): "modulo info residencia".
8. **Módulos de inicio** (11 jun): "modulos de inicio".
9. **Reestructura** (19 jun): "restructura por segunda vez".
10. **Cierre / ajustes finales** (21 jun): "2".

## Estimado (Práctica 5) vs. Real

| Métrica | Estimado | Real (Git) |
|---|---|---|
| Tiempo (COCOMO orgánico, 10.783 KLOC) | ≈ 9.0 meses | ≈ 2.8 meses (86 días) |
| Esfuerzo (COCOMO) | ≈ 29.15 personas-mes | Sin dato directo; con 1 desarrollador, como máximo ≈ 2.8 personas-mes |
| Esfuerzo (223 puntos de función × 8 h/PF = 1,784 h) | ≈ 11.15 personas-mes | Sin dato directo |
| Personal promedio (COCOMO) | ≈ 3.2 personas | 1 persona |

La duración real equivale a cerca de **31 %** del tiempo que predice COCOMO. Con puntos de función, el esfuerzo estimado también es varias veces mayor que lo que un solo desarrollador pudo invertir en 86 días.

## Análisis de La Diferencia

- **Importación masiva en el segundo commit.** El commit del 27-mar ("Implantación de notificaciones mediante correo") agrega 7,598 archivos y más de un millón de líneas. Esto indica que el trabajo previo o las librerías de terceros entraron de golpe, así que el historial **no refleja** todo el esfuerzo real anterior a esa fecha.
- **Reutilización de componentes.** El proyecto incluye muchas librerías de terceros (`Vistas/bower_components`, PHPExcel, PHPMailer, TCPDF). COCOMO se aplicó solo al código propio (10.783 KLOC), pero el desarrollador ahorró tiempo al apoyarse en ellas.
- **Alcance del modelo.** COCOMO orgánico supone un equipo con análisis, diseño, pruebas y documentación. El historial de Git solo muestra código subido; no hay evidencia de esas actividades.
- **Los commits no miden horas.** Cada commit agrupa trabajo de duración desconocida. Solo hay 8 días con actividad registrada, pero el trabajo pudo hacerse en más días y subirse en pocos commits.
- **Un solo desarrollador.** COCOMO calcula ≈ 3.2 personas; el historial apunta a una. No se puede afirmar cuántas horas reales se invirtieron.

**Conclusión:** la estimación y la realidad no coinciden, y no es posible saber cuál es "más correcta" solo con Git. El historial da un límite inferior visible de duración (86 días), no el esfuerzo total.

## Calidad de Los Mensajes de Commit

- Algunos mensajes sí permiten entender el cambio: "integración de la clase phpmailer", "correccion de bugs en el modulo constancia", "modulo info residencia".
- Otros no informan nada: "Initial commit" (estándar de GitHub) y **"2"** (último commit, sin ninguna descripción).
- Falta una convención: no hay prefijos (`feat`, `fix`), mayúsculas inconsistentes y faltas de ortografía ("restructura", "correccion").
- Un mismo commit mezcla muchas cosas (por ejemplo, "rediseño moderno" junto con el módulo de Observaciones), lo que dificulta rastrear cambios.
- **Valoración:** calidad baja a media; sirven para reconstruir fases generales, no para auditar cambios concretos.
