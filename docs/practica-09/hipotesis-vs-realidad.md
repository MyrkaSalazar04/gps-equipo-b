# Hipótesis vs. Realidad — Práctica 9

**Sistema:** Control Escolar de Servicio Social y Residencia Profesional
**Hipótesis original:** `docs/README.md` (Práctica 1), escrita sin abrir el código, solo con nombres de carpetas y archivos.
**Realidad:** hallazgos de las Prácticas 2 a 8.

---

## 1. Resumen

| Aspecto de la hipótesis | Veredicto | Comentario corto |
|---|---|---|
| Qué hace el sistema | Acertó en lo esencial, se quedó corta en alcance | Es más "control escolar" que solo trámites |
| Para quién es | Acertó en parte | Son 5 roles, no 3 grupos; algunos permisos no coinciden |
| Tecnología | Acertó | PHP + MySQL + HTML/CSS/JS, pero con versiones sin soporte |
| Tamaño | Acertó en carpetas, falló en archivos | 15 carpetas en la raíz, pero más de 7,600 archivos |
| Calidad, seguridad y legalidad | No se anticipó | Es lo más importante que se encontró |

Lo que una hipótesis hecha solo con nombres de carpetas **sí** puede predecir es el propósito y la pila tecnológica. Lo que **no** puede predecir es la calidad del producto, y eso terminó siendo el centro del diagnóstico.

---

## 2. Comparación punto por punto

### 2.1 ¿Qué hace el sistema?

**Hipótesis:** "plataforma web integral para la gestión, seguimiento y automatización de los procesos administrativos y académicos del Servicio Social y la Residencia Profesional".

**Realidad:** la idea general fue correcta. El sistema tiene 12 módulos: Iniciar sesión, Inicio, Solicitudes, Usuarios, Catálogo, Carpetas, Certificados, Visitas a empresa, Subir calificaciones, CRUD Carreras, Información y Mi horario. Además incluye un chat de observaciones por documento, constancias y cartas en PDF, y notificaciones por correo.

**Qué no se vio:** el componente propiamente escolar. Hay materias, comisiones, inscripciones, exámenes y notas (tablas `materias`, `comisiones`, `inscripciones`, `examenes`, `notas`). El nombre completo del sistema ("Control Escolar") lo sugería, pero la hipótesis se centró solo en los trámites de residencia y servicio.

**Veredicto:** acierto parcial alto.

### 2.2 ¿Para quién está hecho?

**Hipótesis:** estudiantes, coordinadores / vinculación, y asesores internos y externos.

**Realidad:** `Vistas/plantilla.php` define 5 roles, cada uno con su menú:

| Rol | Lo que la hipótesis decía | Lo que se encontró |
|---|---|---|
| Alumno | Sube documentos y consulta trámites | Correcto: carpetas, constancias, horario, catálogo y visitas |
| Coordinadores / Vinculación | Revisan solicitudes y gestionan la base | Se materializa en **Admin** (acceso total) y **Jefe** (casi igual al asesor académico) |
| Asesor interno | Evalúa y califica | **a_Academico**: puede subir calificaciones, gestionar carpetas y crear usuarios |
| Asesor externo | Evalúa y califica | **a_Industrial**: solo consulta carpetas, emite certificados y ve visitas; **no sube calificaciones** |

**Qué no se vio:** que el asesor industrial tiene un rol de consulta, no de evaluación, y que hay un rol "Jefe" que la hipótesis no separó del coordinador.

**Veredicto:** acierto parcial. Identificó bien a los grupos de usuarios, pero supuso permisos que el código no otorga.

### 2.3 ¿Con qué tecnología está construido?

**Hipótesis:** aplicación web tradicional con HTML, CSS y JavaScript en el navegador, y PHP con MySQL en el servidor.

**Realidad:** correcto. Se confirmó además:

- PHP 7.2.34 y MariaDB 10.4.14 (encabezado de los archivos `.sql`).
- Arquitectura MVC sin framework: `Controladores/`, `Modelos/`, `Vistas/`, con enrutamiento por `.htaccess` hacia `index.php`.
- Librerías de terceros: AdminLTE 2.4.0, Bootstrap 3.3.7 y jQuery 1.9.1 en el frontend; TCPDF (PDF), PHPMailer (correo) y PHPExcel (Excel).

**Qué no se vio:** que casi todo eso está **fuera de soporte**. PHP 7.2 terminó su ciclo en noviembre de 2020 y PHPExcel está abandonada. Saber qué tecnología se usa no dice en qué estado está.

**Veredicto:** acierto total en la pila, sin información sobre su estado.

### 2.4 ¿Qué tan grande es?

**Hipótesis:** proyecto mediano, con unas 10 a 20 carpetas y archivos principales en la raíz, monolítico y "sin llegar a ser extremadamente complejo".

**Realidad:**

| Medida | Valor |
|---|---|
| Carpetas en la raíz | 15 (dentro del rango 10 a 20) |
| Archivos en el repositorio | más de 7,600 |
| Peso aproximado | 150 MB |
| Código propio | 11,039 líneas (≈ 11 KLOC); 16,136 con comentarios y blancos |
| Esfuerzo de reconstrucción estimado | de 10.9 a 29.9 personas-mes, según el método (Práctica 5) |

**Qué no se vio:** la hipótesis contó carpetas, no archivos. Una sola carpeta (`Vistas/bower_components`, con AdminLTE) concentra unos 6,800 archivos. Eso hace que el repositorio *parezca* enorme cuando el código propio es modesto. A la inversa, 11 KLOC no son triviales: reconstruirlos costaría entre $204,258 y $560,130 MXN.

**Veredicto:** acertó en "mediano", pero por una razón distinta a la que tenía en mente.

---

## 3. Lo que la hipótesis no anticipó

Estos hallazgos no se pueden deducir de los nombres de carpetas y fueron los que más pesaron en la recomendación final:

1. **Datos personales en un repositorio público.** Las carpetas `Kardex/`, `IMSS/`, `Servicio/` y `Documentos/`, y tres respaldos `.sql` con registros (riesgo R06, exposición 25).
2. **Credenciales en el código.** Base de datos remota, cuenta de correo y clave de cifrado escritas en archivos (`Modelos/ConexionBD.php`, `Controladores/EnviarCorreo.php`, `config/server.php`).
3. **Contraseñas en texto plano** (`usuariosC.php`, método `IniciarSesionC()`), y la columna `clave` sin ningún hash.
4. **Cero llaves foráneas** en las 17 tablas.
5. **Dependencia de una sola persona.** 10 commits en 86 días (27 de marzo al 21 de junio de 2021), sin actividad desde entonces.
6. **Sin licencia, sin README, sin pruebas.**

---

## 4. ¿Qué tanto se equivocó la hipótesis?

En lo que **hace** y **con qué está hecho**, poco. En lo que **vale** (seguridad, legalidad, mantenibilidad), por completo, y eso no era algo que pudiera saberse desde afuera.

Esto deja tres lecciones sobre los supuestos de un proyecto:

- **Una estructura de carpetas ordenada no garantiza un producto sano.** El sistema "se ve" bien organizado, pero arrastra riesgos graves.
- **Los supuestos sobre usuarios y permisos hay que validarlos con el código o con el cliente.** Aquí se supuso que los asesores externos evalúan y el código dice que no.
- **Contar carpetas no es medir tamaño.** El tamaño real se obtuvo al separar código propio de código de terceros.

> **Nota de método:** la hipótesis se conserva tal como se escribió en la Práctica 1 (sin corregirla después), como pide el cuadernillo.
