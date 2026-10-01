# Lecciones Aprendidas — Práctica 9

**Consultora:** TecNM Solutions
**Proyecto:** Diagnóstico y propuesta de reingeniería del Sistema de Control Escolar de Servicio Social y Residencia Profesional
**Cliente:** Instituto Tecnológico de Matehuala
**Fecha:** 30 de septiembre de 2026

> Las secciones marcadas con **[COMPLETAR]** piden una experiencia personal que solo ustedes conocen. Sustitúyanlas antes de entregar.

---

## 1. Qué funcionó

**Separar código propio de código de terceros (Práctica 2).** Fue la decisión que hizo posible todo lo demás. Sin ella, el conteo de líneas habría dado cientos de miles en lugar de 11,039, y las estimaciones de la Práctica 5 habrían sido inservibles.

**Encadenar las prácticas.** Cada entregable alimentó al siguiente: el inventario sirvió para medir el tamaño; las historias de usuario y el modelo de datos, para los puntos de función; el top 10 de riesgos, para fijar la reserva de contingencia del presupuesto (20 %, calculada con la exposición promedio de 20.2 sobre 25). Ninguna cifra del plan final salió "de la nada".

**Mostrar archivo y línea sin copiar credenciales.** La regla ética obligó a documentar hallazgos graves (por ejemplo, en `Modelos/ConexionBD.php` y `Controladores/EnviarCorreo.php`) sin exponerlos de nuevo. Es una práctica profesional que conviene conservar.

**Priorizar por costo e impacto.** La deuda técnica total se estimó en 196 a 290 horas, pero lo más grave (D01 a D04: credenciales, contraseñas y datos personales) cuesta solo 30 a 42 horas. Eso justificó un orden de trabajo claro: primero contener el daño, luego modernizar.

**Comparar dos análisis del mismo sistema.** En el top 10 de riesgos, la comparación entre equipos encontró riesgos que uno había pasado por alto (el equipo A vio el acceso por URL directa a los archivos y el script de BD incompleto; el equipo B vio el frontend obsoleto y la falta de pruebas). Dos revisiones independientes cubrieron más que una.

## 2. Qué no funcionó

**La composición desigual de los equipos.** El Equipo A trabajó con 3 integrantes y el Equipo B fue trabajado de forma individual por una sola persona. Eso quedó registrado en `delphi.md`, pero tuvo efectos concretos: la ronda Delphi aportó 3 estimaciones de un lado y 1 del otro, y algunas reflexiones quedaron sin las firmas de todos los integrantes.

**La ronda Delphi quedó sin cerrar.** Las tablas de estimaciones y la cifra de consenso de `delphi.md` siguen vacías. Como consecuencia, el presupuesto de la Práctica 8 tuvo que usar un **supuesto**: el promedio de ambos métodos (20.4 personas-mes) en lugar de una cifra acordada. El propio `presupuesto.xlsx` lo advierte.

**Cifras que cambiaron entre prácticas.** La Práctica 5 usa 11.039 KLOC y 249 puntos de función; `comparacion.md` de la Práctica 6 cita 10.783 KLOC y 223 puntos de función. Son versiones distintas del mismo conteo. Por eso conviene fijar una fuente única de cifras desde el principio.

**Un techo de presupuesto demasiado pronto.** El acta de constitución fijó $204,258 MXN como máximo, tomado solo de los puntos de función. Al agregar seguridad, protección de datos, pruebas y contingencia, la propuesta final subió a $496,693 antes de IVA ($576,164 con IVA). Se explicó en la propuesta, pero mostró el riesgo de comprometer una cifra antes de definir el alcance.

**Los mensajes de commit.** Las mismas críticas que hicimos al sistema original (commits como "2" o "restructura por segunda vez") aplican a cualquier equipo sin una convención. **[COMPLETAR: ¿cómo fueron sus propios commits? ¿Sirvieron para reconstruir quién hizo qué?]**

## 3. Qué haríamos diferente

1. **Acordar desde la Práctica 1 una única fuente de cifras** (un archivo con KLOC, PF y costo por persona-mes) y citarla en todos los documentos.
2. **Cerrar la ronda Delphi en la sesión grupal**, aunque haya menos participantes, y registrar explícitamente quién aportó cada estimación.
3. **No fijar techos de costo en el acta** antes de tener alcance y riesgos. Usar un rango y dejar la cifra definitiva para la propuesta.
4. **Revisar lo que el otro equipo encontró antes de cerrar el top 10.** Varios riesgos (R05 y R13 del Equipo A) habrían entrado antes a la matriz del Equipo B.
5. **Revisar el código de acceso por rol, no solo los menús.** La hipótesis supuso que el asesor industrial califica; el código dice que no. Validar permisos contra el código desde la Práctica 3 habría evitado ese error.
6. **[COMPLETAR: algo propio sobre organización del tiempo, división del trabajo o uso de GitHub Projects.]**

## 4. Qué recomendaríamos a otra consultora

- **Empiecen por lo que puede hacer daño.** Antes de estimar costos o diseñar mejoras, revisen si el repositorio expone datos personales o credenciales. Es lo más barato de corregir y lo más caro de ignorar.
- **No confíen en el historial de Git como medida de esfuerzo.** En este proyecto, un solo commit agregó 7,598 archivos y más de un millón de líneas (librerías incluidas). El historial mostró 86 días de duración, pero no las horas de trabajo reales.
- **Desconfíen de la estimación única.** COCOMO dio 29.9 personas-mes y los puntos de función, 10.9: casi tres veces de diferencia para el mismo sistema. Presenten siempre un rango y expliquen los supuestos.
- **Verifiquen la licencia antes de proponer nada.** Sin autorización escrita del autor, la opción de modernizar puede convertirse en reescribir, con otro presupuesto.
- **Documenten quién aprueba qué.** La matriz RACI de la Práctica 8 evitó ambigüedades sobre quién rota credenciales, quién valida el aviso de privacidad y quién cierra el proyecto.
- **Escriban la propuesta para quien va a pagarla.** El cliente no necesita saber qué es COCOMO; necesita saber cuánto cuesta, cuánto tarda, qué riesgo corre y qué decisión se le pide.

## 5. Resultado del proyecto

| Pregunta del cliente | Respuesta de la consultora |
|---|---|
| ¿Adoptar, modernizar o descartar? | **Modernizar**, con condiciones: licencia del autor, orden de trabajo (contener, probar, migrar) y un responsable interno de mantenimiento |
| ¿Cuánto cuesta? | $496,693 MXN antes de IVA ($576,164 MXN con IVA), con 20 % de contingencia |
| ¿Cuánto tarda? | Del 01/10/2026 al 28/05/2027 (≈ 8 meses, 6 fases) |
| ¿Cuál es el mayor riesgo hoy? | Datos personales de alumnos publicados en el repositorio (exposición 25 de 25) |
