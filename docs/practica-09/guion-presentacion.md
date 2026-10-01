# Guion de la Presentación al Cliente — 20 minutos

**Audiencia:** el cliente (Instituto Tecnológico de Matehuala), no el profesor.
**Estructura pedida:** problema, diagnóstico, recomendación, plan, costo, riesgos y siguiente paso.
**Regla:** cada integrante presenta una parte. Ajusten los nombres según quién haga cada sección.

## Distribución

| # | Bloque | Tiempo | Presenta |
|---|---|---|---|
| 1 | Problema y contexto | 2 min | Integrante 1 |
| 2 | Diagnóstico | 4 min | Integrante 2 |
| 3 | Recomendación | 2 min | Integrante 3 |
| 4 | Plan de trabajo | 3 min | Integrante 4 |
| 5 | Costo | 3 min | Integrante 5 |
| 6 | Riesgos y siguiente paso | 3 min | Integrante 6 |
| — | Preguntas del cliente | 3 min | Todos |

Sugerencia: que la Directora del proyecto (Myrka Salazar) abra con una frase de bienvenida y cierre con la decisión que se le pide al cliente.

---

## 1. Problema y contexto (2 min)

- El Instituto quiere automatizar residencias profesionales y servicio social.
- Encontró un sistema hecho en 2021 por otro plantel. Preguntas del cliente: ¿lo adoptamos, lo modernizamos o lo descartamos?
- Sin manual, sin README, sin contacto con el autor. Se analizó por ingeniería inversa.

**Frase de cierre:** "Les vamos a mostrar qué encontramos, qué recomendamos y cuánto cuesta."

## 2. Diagnóstico (4 min)

Qué tiene de bueno:
- Resuelve un proceso real: 12 módulos, 5 perfiles de usuario, 11,039 líneas de código propio.

Qué tiene de grave (que lo entienda alguien que no programa):
- **Datos de alumnos públicos.** Kardex, IMSS y cartas de liberación están en un repositorio abierto.
- **Contraseñas y claves expuestas.** Credenciales escritas en el código; contraseñas de usuarios sin proteger.
- **Tecnología sin soporte.** PHP 7.2 dejó de recibir actualizaciones en noviembre de 2020.
- **Una sola persona.** 10 cambios registrados en 86 días; nada desde junio de 2021.
- **Sin licencia.** No queda claro que podamos usarlo ni modificarlo.

**Evitar:** siglas sin explicar (COCOMO, ER, MVC) y mostrar credenciales reales en pantalla.

## 3. Recomendación (2 min)

- **Modernizar**, no descartar ni adoptar tal cual.
- Por qué no descartar: ya contiene el conocimiento del proceso y reconstruirlo costaría entre $204,258 y $560,130 MXN.
- Por qué no adoptar tal cual: los riesgos de seguridad y legales.
- **Tres condiciones:** autorización escrita del autor, orden de trabajo (contener, probar, migrar) y un responsable interno de mantenimiento.

## 4. Plan de trabajo (3 min)

- 6 fases, del 01/10/2026 al 28/05/2027 (≈ 8 meses).
- **Lo primero (primeras semanas):** retirar datos personales y rotar credenciales. Es lo más barato y lo más urgente.
- Después: diseño, desarrollo (migración a PHP 8.2 o superior), pruebas y despliegue.
- Mostrar el cronograma (`cronograma.png`) y señalar los hitos.

## 5. Costo (3 min)

| Concepto | Monto (MXN) |
|---|---|
| Personal (18.8 personas-mes) | $351,911 |
| Otros costos directos | $62,000 |
| Contingencia (20 %) | $82,782 |
| **Total antes de IVA** | **$496,693** |
| **Total con IVA** | **$576,164** |

- Explicar la contingencia en una frase: "la calculamos con el nivel de riesgo que encontramos".
- Aclarar de dónde sale la cifra y por qué es mayor que la estimación inicial (incluye seguridad, protección de datos y pruebas).
- Decir qué **no** incluye: hosting del Instituto, datos reales, nuevos módulos, soporte posterior a la garantía.

## 6. Riesgos y siguiente paso (3 min)

- Top 3 de riesgos: datos personales publicados, credenciales en el código, contraseñas sin proteger. Qué se hará con cada uno.
- Riesgo de proyecto: licencia del autor. Si no la otorga, el plan cambia a reescritura, con ajuste de costo y plazo.
- **Decisión que se le pide al cliente:**
  1. Aprobar el alcance y el presupuesto.
  2. Contactar al autor del sistema para obtener la licencia.
  3. Designar un responsable interno y un contacto jurídico para el aviso de privacidad.

---

## Preguntas que probablemente harán (y respuesta corta)

| Pregunta | Respuesta sugerida |
|---|---|
| ¿Por qué cuesta más que la cifra del acta ($204,258)? | Esa cifra salía solo de puntos de función. La propuesta suma seguridad, protección de datos, pruebas, documentación y contingencia. Está explicado en la sección 6 de la propuesta. |
| ¿Por qué dos métodos dieron cifras tan distintas? | Miden cosas distintas (líneas de código vs. funcionalidad). Por eso usamos el promedio y un rango, y dejamos la contingencia. |
| ¿Se puede usar el sistema mientras tanto? | No con datos reales: primero hay que corregir contraseñas, credenciales y acceso a documentos. |
| ¿Qué pasa si el autor no da licencia? | Se reescribe aprovechando el análisis funcional. Es un cambio de alcance con nuevo presupuesto. |
| ¿Cuántos datos personales hay realmente expuestos? | No abrimos los documentos por ética. Indicamos qué carpetas y qué tipo de información; el Instituto debe revisarlo con su área jurídica. |
| ¿Qué ley aplica? | Depende de si el Instituto se considera sujeto obligado o particular. Lo confirma el área jurídica (punto pendiente en la reflexión de la Práctica 7). |
| ¿Qué tan seguros están de sus números? | Son estimaciones; la ronda Delphi no se cerró con una cifra de consenso, por eso el presupuesto usa un promedio declarado como supuesto. |

## Antes de presentar

- [ ] Ensayar una vez completa con cronómetro (20 minutos máximo).
- [ ] No mostrar contraseñas, matrículas reales ni contenido de los PDF.
- [ ] Tener abiertos `cronograma.png`, `presupuesto.xlsx` y `propuesta.pdf` por si preguntan.
- [ ] Decidir quién responde cada tipo de pregunta (técnica, costos, legal).
