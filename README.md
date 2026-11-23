# B Focus X — App de reservas, WOD y portal de alumnos

Aplicación web (un solo archivo `index.html`) para un box de CrossFit. Diseño oscuro con naranja `#f47b0b`, pensada para usarse en celular y en navegador de escritorio.

> **Estado:** prototipo funcional. Todos los datos se guardan en el navegador (localStorage), no en un servidor. Ver [Limitaciones](#limitaciones) antes de usarla en producción.

## Cómo usarla

1. Descargá `index.html` (y la carpeta `assets/` si querés tus fotos).
2. Abrí `index.html` con doble clic en cualquier navegador moderno (Chrome, Safari, Edge, Firefox).
3. Necesitás internet para cargar las tipografías de Google Fonts (Exo 2 y Roboto).

No requiere instalación, build ni servidor.

## Cuentas de prueba

| Rol | Email | Contraseña |
|---|---|---|
| Administrador fijo (Prof. Mati) | `mati@bfocusx.com` | `coach123` |
| Administrador fijo (Prof. Leo) | `leo@bfocusx.com` | `coach123` |
| Alumno / cliente | `Fernanda Colcombet` (nombre) | `alumno123` |

**Cómo funcionan los roles**

- Hay **dos administradores fijos**: Prof. Mati y Prof. Leo. Son los profes: arman las clases y los WOD diarios y gestionan todo el box. No se pueden crear, borrar ni suspender desde la app.
- **Registro de alumnos:** solo con **nombre o alias** y el botón **Entrar** (también funciona con la tecla Enter). No pide email, teléfono ni contraseña. El alias debe ser único.
- **Ingreso de alumnos:** escriben su nombre o alias en *Iniciar sesión* y entran sin contraseña. Si un alumno se puso una contraseña desde su perfil, se le pide.
- **Ingreso de los profes:** siempre con contraseña.
- Todo el que se registra queda como **alumno / cliente**. Nadie puede ascender a administrador desde la app.
- Los administradores pueden crear, suspender, activar y eliminar clientes desde *Admin → Gestionar Usuarios*.
- Cada usuario puede cambiar su contraseña desde *Perfil → Editar perfil*. Cambiá las de los administradores antes de usar la app de verdad.

## Imágenes

Creá una carpeta `assets/` junto al `index.html` y guardá tus imágenes originales con estos nombres:

| Archivo | Dónde se usa |
|---|---|
| `assets/logo.png` | Logo B Focus X (splash, login, inicio). Extraído de tu imagen del logo, con fondo transparente |
| `assets/hero.jpg` | Foto de la atleta en el inicio del alumno. Recortada del mockup (baja resolución) |
| `assets/perfil.jpg` | Foto de perfil de la cuenta de ejemplo. Recortada del mockup |
| `assets/gym.jpg` | *(opcional)* Fondo del splash y del login |
| `assets/wod.jpg` | *(opcional)* Cabecera de la pantalla WOD |

`hero.jpg` y `perfil.jpg` salen del mockup, por eso tienen poca resolución. Para mejor calidad, reemplazalos con las fotos originales usando el mismo nombre. Si `gym.jpg` o `wod.jpg` no existen, se muestra un fondo oscuro.

**Tipografía:** Roboto (Google Fonts). Los íconos son de línea en naranja, como en el diseño.

## Funcionalidades

### Alumno
- Registro solo con nombre o alias, ingreso, cierre de sesión y foto de perfil opcional desde *Editar perfil*.
- Calendario semanal de lunes a viernes, de 08:00 a 21:00, con profesor, lugares libres y estado de cada clase.
- Reserva y cancelación de clases.
- Lista de espera cuando la clase está completa, con oferta de lugar y 10 minutos para confirmar.
- Vista del WOD de las clases reservadas.
- Historial de reservas, estadísticas semanales y marcas personales (PR).
- Perfil editable, estado de membresía y recordatorios configurables (2 h y 30 min antes).
- Notificaciones dentro de la app.

### Administradores (los dos profes)
Tienen el panel Coach y el panel Admin en la misma cuenta. Barra inferior: Inicio, Clases, Coach, Admin y Perfil.

**Panel Coach**
- Panel con las clases del día y la semana.
- Lista de inscriptos por horario, marcado de asistencia y observaciones.
- Planificador de WOD por bloques: entrada en calor, mobility, fuerza, skill, conditioning, WOD y vuelta a la calma.
- 12 modalidades (AMRAP, EMOM, For Time, Tabata, etc.), versiones RX y Scaled, notas del coach y video de referencia.
- Plantillas de WOD, duplicación a otra fecha y aplicación a todos los horarios de un día.
- **Ejercicio sorpresa** con notas privadas y recomendaciones de seguridad.

**Panel Admin**
- Panel con alumnos activos, reservas de la semana, ocupación y clases completas.
- Gestión de usuarios: ver los dos administradores fijos y administrar clientes (alta, suspensión, activación y baja).
- Biblioteca de ejercicios por categoría, con búsqueda y ejercicios personalizados.
- Configuración de horarios: activar o desactivar clases, asignar profesor y duplicar la semana.
- Estadísticas: lugares libres, horarios más pedidos, asistencias y ausencias.

## Reglas de reserva

- Cupo máximo de **10 alumnos** por horario.
- Se puede reservar y cancelar hasta **15 minutos antes** del inicio.
- No se puede reservar una clase que ya empezó ni reservar dos veces el mismo horario.
- Al cancelar, el lugar se libera y se ofrece al siguiente de la lista de espera.
- Estados visibles: cupos disponibles, últimos lugares (2 o menos), completo y tu reserva confirmada.

## Ejercicio sorpresa

El profesor o administrador puede cargar un ejercicio secreto en cualquier clase. Los alumnos ven únicamente la tarjeta *"🎁 Hay una sorpresa preparada para esta clase"*, sin nombre, descripción ni pistas. Los datos secretos se guardan separados del WOD público y solo se muestran a profesores y administradores.

## Estructura

```
index.html      # toda la app (HTML, CSS y JavaScript)
assets/         # imágenes opcionales (hero, gym, wod, perfil)
README.md
```

## Limitaciones

- **Los datos viven en el navegador.** Cada dispositivo tiene su propia copia: las reservas de un alumno no se ven en el teléfono de otro. Borrar los datos del sitio borra todo.
- **Cualquiera puede entrar como otro alumno** si conoce su alias, porque los alumnos no usan contraseña. Para un box chico es práctico, pero no protege los datos de cada alumno.
- **La seguridad no es real.** Los permisos, incluido el del ejercicio sorpresa, se aplican en el navegador y se pueden saltear con las herramientas del desarrollador. Las contraseñas se guardan en texto plano. Es válido para una demo, no para producción.
- **Los cupos de ejemplo son simulados.** Las clases muestran ocupación de relleno para poder probar los estados "últimos lugares" y "completo".
- **Sin notificaciones push.** Solo hay avisos dentro de la app.
- **Sin app nativa.** Funciona en el navegador; no hay builds para Google Play ni App Store.
- **Funciones pendientes:** filtros de la biblioteca por dificultad, grupo muscular, equipamiento y duración; duración configurable de cada clase; clases especiales; avisos de cambio de horario o clase cancelada por el box.

## Próximos pasos recomendados

1. **Backend real:** migrar a Supabase (Postgres, autenticación, Row Level Security y Realtime) o Firebase. Las reservas y los permisos del ejercicio sorpresa deben validarse en el servidor.
2. **Reservas seguras:** hacer la reserva con una función transaccional en base de datos para que dos personas no ocupen el último lugar a la vez.
3. **App nativa:** reconstruir con Expo (React Native) o Flutter para publicar en Google Play y App Store, con notificaciones push.
4. **Autenticación segura:** contraseñas con hash, verificación de email y recuperación por enlace real.
5. **Completar funciones pendientes** de la sección anterior.
