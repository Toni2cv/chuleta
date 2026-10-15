# Mapa de URLs de Chuleta

| Pantalla | URL propuesta | ¿Sesión? | Notas |
|---|---|---|---|
| Portada / *landing* (la página de presentación pública) | `/` | No | Es la que atrae usuarios. Si ya hay sesión, puede redirigir a `/asignaturas` |
| Precios | `/precios` | No | Pública |
| Acceso | `/login` | No | Redirige a `/asignaturas` si ya hay sesión. Admite `?next=` para volver a donde estabas |
| Registro | `/registro` | No | Mismo comportamiento que login si ya hay sesión |
| Mis asignaturas | `/asignaturas` | Sí | Pantalla "home" del usuario logueado. Lista de sus asignaturas |
| Una asignatura concreta | `/asignaturas/:id` | Sí | Lista los apuntes de esa asignatura. Solo el dueño (o compartida) puede verla |
| Crear asignatura | `/asignaturas/nueva` | Sí | Declarar antes que `/asignaturas/:id` para que "nueva" no se interprete como un id |
| Un apunte concreto | `/apuntes/:id` | Sí | Ver el apunte y botón para hacer el test |
| Subir apunte | `/asignaturas/:id/subir` | Sí | Anidada: ya sabes a qué asignatura pertenece. Alternativa: `/apuntes/nuevo?asignatura=:id` |
| Hacer el test de un apunte | `/apuntes/:id/test` | Sí | Genera o carga las preguntas del apunte |
| Resultado del test | `/apuntes/:id/test/resultado` | Sí | Alternativa más robusta: `/tests/:intentoId` (permite histórico de intentos) |
| Mi cuenta | `/cuenta` | Sí | Perfil, plan contratado, cambio de contraseña, borrar cuenta |
| Página de error 404 | *(cualquier URL no reconocida)* | No | Sin URL propia: es la respuesta por defecto. Debe devolver código HTTP 404 real |

## Decisiones pendientes

1. **¿Id o slug?** `/asignaturas/42` (simple, estable) frente a `/asignaturas/calculo-1` (legible, pero hay que resolver duplicados). Opción intermedia: `/asignaturas/42-calculo-1`.
2. **Anidar o no anidar.** Anidada (`/asignaturas/:id/apuntes/:apunteId`) refleja la jerarquía; plana (`/apuntes/:id`) es más corta y estable si un apunte puede cambiar de asignatura. La tabla usa un híbrido.
3. **Resultado del test.** `/apuntes/:id/test/resultado` solo admite un resultado por apunte; `/tests/:intentoId` permite guardar el histórico. Condiciona el modelo de datos.
4. **Compartir.** Si un apunte puede compartirse por enlace público, hará falta que `/apuntes/:id` sea accesible sin sesión o una ruta aparte tipo `/p/:token`.

## Rutas que podrían faltar

| Pantalla | URL | ¿Sesión? |
|---|---|---|
| Editar asignatura | `/asignaturas/:id/editar` | Sí |
| Editar apunte | `/apuntes/:id/editar` | Sí |
| Recuperar contraseña | `/recuperar` | No |
| Términos / privacidad | `/terminos`, `/privacidad` | No |
| Salir | `/logout` (mejor como acción POST) | Sí |
