# Análisis del Sistema de Control Escolar de Servicio Social y Residencia Profesional

## Índice final del análisis

**Consultora:** TecNM Solutions · **Cliente:** Instituto Tecnológico de Matehuala · **Versión:** v1.0

| Práctica | Tema | Entregables |
|---|---|---|
| 1 | Arranque y control de versiones | [reflexion](practica-01/reflexion.md) · hipótesis inicial (más abajo) |
| 2 | Mapa del sistema y arquitectura | [inventario](practica-02/inventario.md) · [arquitectura](practica-02/arquitectura.md) · [diagrama](practica-02/arquitectura.png) · [reflexion](practica-02/reflexion.md) |
| 3 | Recuperación de requerimientos | [actores](practica-03/actores.md) · [casos de uso](practica-03/casos-uso.png) · [historias de usuario](practica-03/historias-usuario.md) · [trazabilidad](practica-03/trazabilidad.md) · [reflexion](practica-03/reflexion.md) |
| 4 | Modelo de datos | [modelo ER](practica-04/modelo-er.png) · [diccionario](practica-04/diccionario-datos.md) · [evaluación](practica-04/evaluacion-modelo.md) · [trazabilidad actualizada](practica-04/trazabilidad_actualizada.md) · [reflexion](practica-04/reflexion.md) |
| 5 | Estimación de tamaño, esfuerzo y costo | [estimacion.md](practica-05/estimacion.md) · [estimacion.xlsx](practica-05/estimacion.xlsx) · [delphi](practica-05/delphi.md) · [reflexion](practica-05/reflexion.md) |
| 6 | Historia real del proyecto | [historial](practica-06/historial.txt) · [actividad.xlsx](practica-06/actividad.xlsx) · [gantt real](practica-06/gantt-real.png) · [comparación](practica-06/comparacion.md) · [reflexion](practica-06/reflexion.md) |
| 7 | Riesgos y deuda técnica | [matriz de riesgos](practica-07/matriz-riesgos.xlsx) · [mapa de calor](practica-07/mapa-calor.png) · [deuda técnica](practica-07/deuda-tecnica.md) · [top 10](practica-07/top10-riesgos.md) · [reflexion](practica-07/reflexion.md) |
| 8 | Plan de reingeniería | [acta](practica-08/acta-constitucion.md) · [alcance](practica-08/alcance.md) · [EDT](practica-08/edt.png) · [cronograma](practica-08/cronograma.png) · [presupuesto](practica-08/presupuesto.xlsx) · [riesgos y calidad](practica-08/riesgos-calidad.md) · [RACI](practica-08/raci.md) · [propuesta](practica-08/propuesta.pdf) · [reflexion](practica-08/reflexion.md) |
| 9 | Presentación y cierre | [hipótesis vs. realidad](practica-09/hipotesis-vs-realidad.md) · [lecciones aprendidas](practica-09/lecciones-aprendidas.md) · [guion de presentación](practica-09/guion-presentacion.md) · presentación · [reflexion](practica-09/reflexion.md) |

### Resultado en una línea

El sistema resuelve un proceso real pero no puede adoptarse tal cual (datos personales y credenciales expuestos, PHP sin soporte, sin licencia, un solo desarrollador). Se recomienda **modernizarlo**: 18.8 personas-mes, del 01/10/2026 al 28/05/2027, $496,693 MXN antes de IVA ($576,164 con IVA).

---

**Integrantes:** Myrka Salazar, Jehyson Martínez, José Martínez

## Hipótesis Inicial (Práctica 1)

Observando Únicamente La Estructura de Carpetas y Archivos (Sin Abrir Código):

- **¿Qué Creo Que Hace El Sistema?**
  Es una plataforma web integral diseñada para la gestión, seguimiento y automatización de los
  procesos administrativos y académicos del Servicio Social y la Residencia Profesional.

- **¿Para Quién Está Hecho?**
  Estudiantes / Residentes: Para subir documentación, reportes de actividades y consultar el estado de sus trámites.
  Coordinadores / Departamento de Vinculación: Para revisar solicitudes, validar expedientes, asignar proyectos/asesores y gestionar la base de datos institucional.
  Asesores (Internos / Externos): Para evaluar y calificar los reportes de los alumnos asignados.

- **¿Con Qué Tecnología Está Construido?**
  Se ve que es una aplicación web tradicional. En la interfaz usa HTML, CSS y JavaScript para la estructura, diseño y lógica del navegador.
  Para la parte del servidor y la base de datos, tiene la estructura clásica de un sistema en PHP y MySQL para guardar y
  consultar la información de alumnos y trámites.

- **¿Qué Tan Grande Parece Ser?**
  Es un proyecto de tamaño mediano, con alrededor de 10 a 20 carpetas y archivos principales en la raíz.
  Es una estructura web monolítica bien organizada por módulos (estilos, imágenes, scripts y vistas) para cubrir
  el flujo institucional sin llegar a ser extremadamente compleja.
