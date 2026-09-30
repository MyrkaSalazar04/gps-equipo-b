# Reflexión Individual — Práctica 8. Plan de Proyecto de Reingeniería

| Dato | Descripción |
|---|---|
| Integrante | Myrka Salazar |
| Consultora | Consultora TecNM Solutions |
| Rol | Directora de proyecto |
| Proyecto | Modernización del Sistema de Control Escolar GPS |
| Fecha | Septiembre 30, 2026 |

---

## 1. ¿Qué Fue Lo Más Difícil de Integrar El Trabajo de Dos Equipos Que Analizaron Lo Mismo Por Separado?

Lo más difícil fue que los dos equipos describimos los mismos problemas con cifras y nombres distintos. En la Práctica 7, el Equipo A y el Equipo B encontramos 
casi los mismos riesgos, pero cada uno con su propio identificador y su propia agrupación. 
El Equipo A separó los PDF con datos personales de los respaldos `.sql` (R03 y R04), mientras que el Equipo B los reunió en un solo riesgo (R06). 
El A dio exposición 25 a las credenciales en el código y el B les dio 20. Hubo además riesgos que solo vio un equipo: el A detectó los archivos accesibles por URL directa, y el B las librerías del frontend, la falta de pruebas y la falta de README.
Para integrarlos hubo que ponerse de acuerdo en reglas y no solo en resultados: tomar la mayor exposición cuando los valores diferían, poner primero los riesgos que afectan a personas y agrupar los que se resuelven con la misma acción. Con esas reglas salió un top 10 único. 
En el cierre grupal falta confirmarlo con el Equipo A.
Lo segundo más difícil fue mantener todo coherente: la EDT, el alcance, el cronograma, el presupuesto, los riesgos y el RACI tenían que contar la misma historia. 
Cada documento que ajustaba obligaba a revisar los demás.


## 2. ¿Qué Conflictos Surgieron (Técnicos o Humanos) y Cómo Los Resolvieron?

**Técnicos.** Hubo tres desacuerdos entre las matrices de los equipos. El A daba probabilidad 5 a las credenciales expuestas y a las contraseñas en texto plano, y 
el B daba 4. En el PHP fuera de soporte pasó al revés: el A asignó 4 y el B asignó 5. 
Y en el repositorio sin licencia, el A proponía Transferir y el B Evitar. Se resolvió con el criterio de la mayor exposición, y en la licencia se conservó 
Transferir porque la autorización depende del autor del sistema. También surgieron inconsistencias entre mis propios documentos al integrarlos. 
El acta fijaba un techo provisional de $204,258 y 9 meses, pero el presupuesto refinado dio $496,693 antes de IVA y el cronograma cerró en unos 8 meses. Además, 
las fases del presupuesto no coincidían con las de la EDT, y una versión de la matriz de riesgos no correspondía con el top 10 acordado. 
Lo resolví alineando el presupuesto a las fases del cronograma, usando el top 10 acordado en todos los documentos y explicando en la propuesta por qué el techo del acta cambia.


## 3. ¿Qué Parte del Plan Les Genera Más Incertidumbre y Cómo La Controlarían?

**La licencia del sistema (riesgo 9).** El repositorio original no declara licencia y el plan depende de que el autor o el plantel de origen la autoricen por escrito. 
Si no la otorgan, el proyecto pasa a ser una reescritura y el costo se acerca al rango de reconstrucción ($204,258 a $560,130 según la Práctica 5). 
Lo controlaría iniciando el paquete 1.1.5 desde el primer día, dejando por escrito la decisión y tratando la reescritura como un cambio de alcance con el control de cambios de la sección 7 del alcance.
**La estimación de esfuerzo.** La Ronda Delphi quedó pendiente, así que usé el promedio de COCOMO y puntos de función (20.4 personas-mes). 
También son supuestos míos el factor de reutilización de 0.70 y las 4.5 personas-mes de trabajo adicional en seguridad, base de datos y pruebas. 
Lo controlaría con la reserva de contingencia del 20 %, que se calculó con la exposición promedio del top 10, y revisando la estimación al cerrar la fase de análisis y diseño, cuando ya haya datos reales de avance.
**El cumplimiento de datos personales.** Falta confirmar si al Instituto, por ser una institución pública, le corresponde la ley para particulares o la de sujetos obligados. 
Lo controlaría validando el aviso de privacidad con el área jurídica del Instituto desde la fase 2, antes de desarrollar los controles de datos.

**Firma del Integrante:** Myrka<3
