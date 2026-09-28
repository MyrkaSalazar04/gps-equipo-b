# Reflexión — Práctica 6

**Integrantes** Myrka Salazar, Jehyson Martínez, José Martínez

## ¿Cuántas Personas Desarrollaron El Sistema? ¿Qué Riesgo Representa Eso Para Quien lo Adopte?

El historial de Git muestra dos nombres de autor (`cbarreral` y `Carlos Alberto Barrera Lugo`), pero por la continuidad de los commits y por ser el mismo dueño del repositorio, 
lo más probable es que sea **una sola persona** con dos configuraciones de Git. 
El riesgo para quien adopte el sistema es que todo el conocimiento está concentrado en esa persona: si no está disponible, nadie más conoce las decisiones de diseño. 
Además, no hay evidencia de revisión de código ni de documentación, así que mantener o corregir el sistema depende de reconstruirlo desde cero, justo lo que hicimos en estas prácticas.

## ¿La Duración Real Se Parece a La Estimada? ¿Qué Factores Explican La Diferencia?

No se parece. COCOMO estimó cerca de 9 meses y unas 3 personas; el historial muestra 86 días (≈ 2.8 meses) y un solo desarrollador. 
Los factores que lo explican son: el segundo commit importó más de 7,000 archivos de golpe, así que parte del trabajo anterior no aparece en el historial; 
se reutilizaron muchas librerías de terceros; COCOMO incluye actividades de análisis, pruebas y documentación que Git no registra; y un commit no equivale a horas trabajadas. 
Por eso, el historial da un mínimo visible de duración, no el esfuerzo real total.

## ¿Qué Convenciones de Commits Propondrían Para Su Propio Equipo?

Propondría usar prefijos de tipo (`feat:`, `fix:`, `docs:`, `refactor:`), escribir el mensaje en imperativo y describiendo qué cambió y dónde 
(por ejemplo, `fix: corrige validación de matrícula en login`), un commit por cambio lógico en vez de mezclar varios, nunca usar mensajes vacíos como "2", 
y tener el mismo nombre y correo configurados en Git (`git config user.name` y `user.email`) para que cada persona aparezca con una sola identidad.

**Firma del Integrante:** Myrka<3
**Firma del Integrante:**
**Firma del Integrante:**
