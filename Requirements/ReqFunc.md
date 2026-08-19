# Requerimientos Funcionales

## Gestión de horarios

- **RF01 — Programación de turnos:** El sistema permitirá al coordinador crear, editar y publicar turnos de médicos y enfermeras por hospital, UCI y especialidad.
- **RF02 — Detección automática de cruces:** El sistema rechazará automáticamente cualquier asignación que genere cruce de horario para un mismo profesional (incluso entre hospitales distintos de la red) y alertará antes de publicar.
- **RF03 — Detección de huecos de cobertura:** El sistema alertará al coordinador y a la enfermera jefe cuando un turno de UCI quede sin la dotación mínima requerida (médico internista y ratio de enfermeras por paciente).
- **RF04 — Horario consolidado personal:** Cada profesional verá su horario consolidado de todos los hospitales donde rota, en web y móvil.
- **RF05 — Gestión de suplentes:** Ante una ausencia, el sistema propondrá suplentes disponibles (sin cruce, con la especialidad requerida, ordenados por cercanía) y permitirá asignarlos con un clic, notificándolos de inmediato.

## Diagnósticos y traspaso de turno

- **RF06 — Registro de diagnóstico:** El médico registrará diagnóstico, indicaciones y plan de cada paciente desde web o móvil. Cada registro queda versionado con autor, fecha y hora.
- **RF07 — Traspaso de turno obligatorio:** Antes de cerrar su turno, el sistema exigirá al médico confirmar el diagnóstico actualizado de cada paciente a su cargo. El médico entrante verá un resumen de traspaso por paciente al iniciar sesión.
- **RF08 — Disponibilidad del diagnóstico offline:** La aplicación mantendrá una copia local (caché cifrada) de los diagnósticos de los pacientes del turno activo, consultable aunque no haya conexión; los registros hechos offline se sincronizarán automáticamente al recuperar red.
- **RF09 — Registro de eventos de enfermería:** Las enfermeras registrarán signos vitales y eventos del paciente; el médico responsable los verá reflejados en tiempo real.
- **RF10 — Traspaso de turno de enfermería:** El sistema generará automáticamente el resumen de traspaso de enfermería por paciente (eventos, pendientes, indicaciones vigentes) para el equipo entrante.

## Emergencias y notificaciones (problema de medianoche)

- **RF11 — Médico responsable visible:** Para cada paciente, el sistema mostrará en todo momento quién es el médico responsable del turno actual y su canal de contacto directo.
- **RF12 — Alerta de paciente grave:** Cuando se marque a un paciente como agravado, el sistema notificará por push, SMS y llamada automática al médico responsable del turno.
- **RF13 — Escalamiento automático:** Si el médico responsable no confirma recepción de la alerta en 3 minutos, el sistema escalará automáticamente al suplente de guardia y luego al jefe de la UCI, dejando registro de cada intento.
- **RF14 — Notificaciones de cambios:** Todo cambio de indicaciones médicas o de horario notificará por push a los involucrados (médico, enfermeras del paciente, coordinador según corresponda), con confirmación de lectura.

## Administración y auditoría

- **RF15 — Tablero regional:** El coordinador verá un tablero en tiempo real con el estado de cobertura de todas las UCI de la región (turnos cubiertos, huecos, ausencias, alertas activas).
- **RF16 — Reportes:** El sistema generará reportes exportables de horas trabajadas, cobertura por hospital y tiempos de respuesta a emergencias.
- **RF17 — Auditoría:** Toda acción clínica (diagnósticos, indicaciones, alertas, confirmaciones) quedará en una bitácora inmutable con autor y timestamp.
- **RF18 — Autenticación por sesión personal:** Cada registro se asociará al usuario autenticado; las sesiones en estaciones compartidas expirarán automáticamente por inactividad y permitirán cambio rápido de usuario (badge/PIN).
