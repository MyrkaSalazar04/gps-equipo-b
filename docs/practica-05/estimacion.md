# Estimación inversa de tamaño, esfuerzo y costo — Práctica 5

**Sistema:** Control Escolar de Servicio Social y Residencia Profesional
**Integrante:** *Myrka Salazar*

---

## 1. Resumen ejecutivo

| Método | Resultado principal |
|---|---|
| Líneas de código (LOC) | 11,039 líneas de código propio → **11.039 KLOC** |
| COCOMO básico (orgánico) | Esfuerzo = **29.87 personas-mes**, Tiempo = **9.09 meses**, Personal = **3.29 personas** |
| Puntos de función (sin ajustar) | **249 PF** → Esfuerzo = **10.89 personas-mes** (1,743 horas-persona) |
| Costo estimado | COCOMO: **$560,129.87 MXN** · Puntos de Función: **$204,257.81 MXN** |

> Este documento se actualiza conforme avanza la práctica. Las secciones marcadas como **(pendiente)** se completan en los siguientes pasos.

---

## 2. Supuestos

- **Código de terceros excluido del conteo:** se excluyeron `Vistas/bower_components` (AdminLTE, ≈6,800 archivos), `tcpdf`, `PHPMailer`, `Modelos/PHPExcel`, `impExcel`, `class.upload.php` y `simplexlsx.class.php`, identificados como librerías en la Práctica 2.
- **Archivos individuales sin desglose de comentarios/blancos:** `Vistas/plantilla.php` (211 líneas) e `index.php` (45 líneas) se contaron como total de líneas, sin separar código/comentarios/blancos, porque la extensión VS Code Counter no permite el conteo por archivo individual. Su peso en el total es marginal (256 de 11,039 líneas, ~2.3%).
- **Login excluido de las Entradas Externas (Puntos de Función):** la pantalla de inicio de sesión (HU-02) se excluye del conteo de Entradas Externas porque, según la metodología IFPUG, el login es una función técnica de seguridad que valida credenciales contra un archivo existente, pero no crea ni actualiza un archivo lógico de negocio. No se considera una función de negocio identificable por el usuario.
- **COCOMO en modo orgánico:** se usó el modo orgánico (no semi-acoplado ni empotrado) porque el sistema es de tamaño pequeño-mediano, desarrollado presumiblemente por un equipo reducido y sin restricciones extremas de tiempo o innovación tecnológica no probada.
- **Complejidad media en Puntos de Función:** siguiendo la instrucción del manual, se usa complejidad media para los cinco elementos (Entradas Externas = 4 PF, Salidas Externas = 5 PF, Consultas Externas = 4 PF, Archivos Lógicos Internos = 10 PF, Archivos de Interfaz Externos = 7 PF).

---

## 3. Método 1: Líneas de Código y COCOMO Básico

### 3.1 Conteo de LOC (código propio)

| Carpeta / archivo | Código | Comentarios | Blancos | Total líneas |
|---|---|---|---|---|
| Controladores | 1,092 | 198 | 443 | 1,733 |
| Modelos (propios, excluye PHPExcel) | 4,220 | 1,954 | 813 | 6,987 |
| Vistas/modulos | 5,471 | 46 | 1,643 | 7,160 |
| Vistas/plantilla.php | 211 | — | — | 211 |
| index.php | 45 | — | — | 45 |
| **TOTAL** | **11,039** | **2,198** | **2,899** | **16,136** |

**KLOC = 11,039 / 1,000 = 11.039**

### 3.2 COCOMO Básico, Modo Orgánico

| Variable | Fórmula | Valor |
|---|---|---|
| Esfuerzo (E) | 2.4 × KLOC^1.05 | 29.87 personas-mes |
| Tiempo (T) | 2.5 × E^0.38 | 9.09 meses |
| Personal promedio (P) | E / T | 3.29 personas |

*(Ver hoja de cálculo `estimacion.xlsx` con fórmulas visibles.)*

---

## 4. Método 2: Puntos de Función

### 4.1 Entradas Externas (EI) — Complejidad Media: 4 PF c/u

| # | Entrada | Historia de Usuario | Justificación |
|---|---|---|---|
| 1 | Crear cuenta | HU-01 | Formulario que guarda un nuevo registro en `usuarios` |
| 2 | Subir documento | HU-04 | Guarda un nuevo registro en `documentacion` |
| 3 | Crear usuario | HU-09 | Formulario que guarda un nuevo registro en `usuarios` |
| 4 | Editar usuario | HU-10 | Actualiza un registro existente en `usuarios` |
| 5 | Eliminar usuario | HU-10 | Elimina un registro de `usuarios` |
| 6 | Subir calificación | HU-11 | Guarda un nuevo registro en `notas` |

**Subtotal EI = 6 × 4 = 24 PF**

*(Login excluido — ver Supuestos, sección 2.)*

### 4.2 Salidas Externas (EO) — Complejidad Media: 5 PF c/u

| # | Salida | Tipo | Justificación |
|---|---|---|---|
| 1 | Constancia.php | PDF | Genera constancia del alumno (HU-06) |
| 2 | CartaPrecentacion.php | PDF | Genera carta de presentación |
| 3 | expCatalogo.php | PDF | Exporta catálogo de empresas |
| 4 | expUsuarios.php | PDF | Exporta listado de usuarios |
| 5 | Inscriptos-Examen.php | PDF | Reporte de inscritos a examen |
| 6 | Inscriptos-Materias.php | PDF | Reporte de inscritos a materias |
| 7 | EnviarCorreo.php | Correo | Envío de notificaciones por correo (PHPMailer) |

**Subtotal EO = 7 × 5 = 35 PF**

*Nota: estos archivos de código propio se encontraron incorrectamente ubicados dentro de la carpeta de la librería de terceros `tcpdf`, mezclados con archivos de ejemplo de la propia librería (como `pdf.php`, descartado por ser un archivo demo de TCPDF sin relación con el negocio). Este hallazgo se documentará como deuda técnica en la Práctica 7.*

### 4.3 Consultas Externas (EQ) — Complejidad Media: 4 PF c/u

| # | Consulta | Historia |
|---|---|---|
| 1 | Consultar catálogo de empresas | HU-03 |
| 2 | Ver horario | HU-05 |
| 3 | Ver lista de alumnos asignados | HU-08 |
| 4 | Consultar carpetas de documentos | HU-12 |
| 5 | Consultar visitas a empresa | HU-12 |

**Subtotal EQ = 5 × 4 = 20 PF**

*(HU-07, "ver menú según rol", se excluye: no es una consulta de datos de negocio, es la carga de interfaz según el rol.)*

### 4.4 Archivos Lógicos Internos (ILF) — Complejidad Media: 10 PF c/u

Las 17 tablas del diccionario de datos (Práctica 4) son mantenidas por el propio sistema:

usuarios, carrera, materias, comisiones, inscripciones, notas, documentos, reportes, solicitudes, notificaciones, evaluaciones, examenes, inscribir_examenes, ajustes, procesos, inforesidencia, documentacion.

**Subtotal ILF = 17 × 10 = 170 PF**

### 4.5 Archivos de Interfaz Externos (EIF)

No se identificó ninguna tabla o archivo externo mantenido por otro sistema; las 17 tablas pertenecen y son gestionadas por este mismo sistema.

**Subtotal EIF = 0 × 7 = 0 PF**

### 4.6 Total de Puntos de Función Sin Ajustar

| Elemento | Cantidad | Peso | Subtotal |
|---|---|---|---|
| Entradas externas (EI) | 6 | 4 | 24 |
| Salidas externas (EO) | 7 | 5 | 35 |
| Consultas externas (EQ) | 5 | 4 | 20 |
| Archivos lógicos internos (ILF) | 17 | 10 | 170 |
| Archivos de interfaz externos (EIF) | 0 | 7 | 0 |
| **Total PF sin ajustar** | | | **249** |

### 4.7 Conversión a Esfuerzo y Productividad

- Productividad estimada para equipo PHP estándar: **7 horas/PF**
  *(Fuente: rangos históricos de productividad de Capers Jones / SPR / ISBSG para PHP, ~6.5-8 hrs/PF en proyectos web tradicionales de complejidad media.)*
- Esfuerzo = 249 PF × 7 hrs/PF = **1,743 horas-persona**
- Esfuerzo en personas-mes (160 hrs/mes) = 1,743 / 160 = **10.89 personas-mes**

---

## 5. Costo

- Salario mensual desarrollador junior en San Luis Potosí: **$15,000 MXN**
  *(Fuente: promedio de plataformas de empleo Indeed y OCC Mundial.)*
- Costo mensual con 25% de costos indirectos: $15,000 × 1.25 = **$18,750 MXN/mes**
- Costo por hora: $18,750 / 160 = **$117.19 MXN/hora**

| Método | Esfuerzo | Costo estimado |
|---|---|---|
| LOC + COCOMO | 29.87 personas-mes | **$560,129.87 MXN** |
| Puntos de Función | 10.89 personas-mes (1,743 hrs) | **$204,257.81 MXN** |

---

## 6. Comparación de Los Métodos

Los dos métodos arrojan resultados muy distintos: COCOMO estima casi **3 veces más esfuerzo y costo** que Puntos de Función para el mismo sistema. Esto ocurre porque cada método parte de supuestos diferentes:

- **COCOMO** se basa en el tamaño en líneas de código y en constantes empíricas (2.4, 1.05) calibradas sobre proyectos históricos que no necesariamente se parecen a este sistema; además, incluye implícitamente curva de aprendizaje, coordinación de equipo y todo el ciclo de vida.
- **Puntos de Función** mide la funcionalidad de negocio entregada (independiente del lenguaje) y depende fuertemente de la tasa de productividad elegida (horas/PF), que aquí se tomó como un valor "estándar" de la industria, no medido directamente en este equipo o este tipo de sistema.

Ninguno de los dos es "el correcto": son dos maneras distintas de aproximarse a la misma incertidumbre. La sección 7 documenta cómo se adaptó el cierre de esta práctica al trabajarla de forma individual.

---

## 7. Ronda Delphi — *(pendiente, ver nota sobre trabajo individual en `delphi.md`)*

*(Se documentará en `delphi.md` según indica el manual: estimaciones de cada ronda y cifra de consenso.)*
