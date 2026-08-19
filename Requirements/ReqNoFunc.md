# Requerimientos No Funcionales

## Escalabilidad

- **RNF01:** El sistema soportará 1K hospitales al lanzamiento, 100K a los 6 meses y 10M a los 2 años, sin rediseño de la arquitectura (escalamiento horizontal).
- **RNF02:** La arquitectura permitirá el despliegue por regiones (multi-región), iniciando en Lima y agregando regiones sin downtime del resto de la red.

## Rendimiento

- **RNF03:** Tiempo de inicio de la aplicación: **< 1 segundo**.
- **RNF04:** Tiempo de configuración inicial de la aplicación: **< 5 segundos**.
- **RNF05:** Las notificaciones de emergencia (paciente grave) se entregarán en **< 5 segundos** desde que se genera el evento.
- **RNF06:** Las consultas de diagnóstico y horario responderán en **< 2 segundos** en percentil 95.

## Disponibilidad y recuperación

- **RNF07:** Disponibilidad del sistema: **99.9%** (máximo ~8.7 horas de indisponibilidad al año).
- **RNF08:** Tiempo de recuperación ante caída (RTO): **< 5 minutos**.
- **RNF09:** Los diagnósticos del turno activo estarán disponibles en modo offline (caché local cifrada) ante pérdida de conectividad del hospital o caída del backend, con sincronización automática al restablecerse.
- **RNF10:** Sin pérdida de registros clínicos confirmados ante una caída (RPO = 0 para diagnósticos e indicaciones): replicación síncrona en al menos 2 zonas.

## Seguridad y cumplimiento

- **RNF11:** Datos clínicos cifrados en tránsito (TLS 1.3) y en reposo (AES-256), incluyendo la caché local de los dispositivos.
- **RNF12:** Control de acceso por roles (médico, enfermera, coordinador, dirección): cada usuario ve solo los pacientes y horarios que le corresponden.
- **RNF13:** Cumplimiento de la Ley de Protección de Datos Personales del Perú (Ley 29733) para historias clínicas.
- **RNF14:** Sesiones en estaciones compartidas con expiración automática por inactividad (≤ 2 minutos) y cambio de usuario rápido sin cerrar la aplicación.

## Usabilidad

- **RNF15:** Las acciones críticas del flujo diario (ver traspaso, registrar diagnóstico, confirmar alerta) tomarán como máximo 3 interacciones desde la pantalla principal.
- **RNF16:** La aplicación móvil funcionará en Android e iOS de gama media, e interfaz en español.

## Auditoría

- **RNF17:** La bitácora de auditoría será inmutable (append-only) y se retendrá por el período legal exigido para registros clínicos.
