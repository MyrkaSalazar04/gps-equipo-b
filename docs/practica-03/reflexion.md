# Reflexión - Práctica 3

**Integrante:** Myrka Salazar

## ¿Qué Requerimientos del Proceso Real de Residencia En Su Instituto No Cubre Este Sistema?

Comparando con la documentación oficial del departamento (el calendario de Residencias Profesionales y los formatos como el código de ética y la solicitud de residencia), el sistema no automatiza los pasos que requieren firma física: la expedición de cartas de presentación, la recepción de cartas de aceptación de la empresa, la firma del código de ética y la carta de confidencialidad, ni la conformidad final de la empresa sobre el proyecto entregado. 
El sistema solo permite subir estos documentos ya firmados en PDF como evidencia (a través de Carpetas), pero no genera, envía ni gestiona la firma de ninguno de ellos. Tampoco encontré un módulo donde la empresa capture directamente su conformidad dentro del sistema.

## ¿Qué Tan Confiable es Recuperar Requerimientos a Partir del Código? ¿Qué Se Pierde?

Es razonablemente confiable para saber qué hace el sistema actualmente, pero no es suficiente por sí solo. Durante esta práctica varias veces tuve 
que corregir suposiciones que parecían lógicas pero que el código no respaldaba: por ejemplo, pensé que había una diferencia entre "gestionar" 
y "consultar" usuarios según el rol, y al revisar usuarios.php descubrí que la diferencia real estaba en qué roles se pueden crear, no en editar/eliminar. 
Lo que se pierde al recuperar requerimientos solo del código es el "por qué": el código muestra qué hace el sistema, pero no explica la intención original del cliente, decisiones que se descartaron, o reglas de negocio que quedaron a medias (como si de verdad se valida en el servidor que un Asesor Académico no pueda crear un usuario Admin, o solo se oculta esa opción en el formulario). Esa intención solo se puede confirmar preguntando directamente al personal del departamento.

## Si Los Dos Equipos Obtienen Listas Distintas, ¿Cómo Decidirían Cuál Es La Correcta?

Ninguna lista sería automáticamente "la correcta" solo por ser diferente; lo primero sería comparar ambas contra la evidencia directa del código 
(como hicimos con usuarios.php), ya que ahí está el comportamiento real del sistema y no una interpretación. Si after revisar el código ambos 
equipos siguen en desacuerdo en algo que el código no aclara del todo (como una regla de negocio implícita), lo correcto sería consultarlo con 
el personal del departamento de Servicio Social y Residencia Profesional, que son quienes conocen el proceso real, en lugar de asumir que un equipo tiene automáticamente la razón sobre el otro.

Firma: Myrka<3
