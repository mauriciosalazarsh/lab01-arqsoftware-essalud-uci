# Reporte de Evaluaciones (Eval-Spec)

Evaluaciones ejecutadas con Claude como cliente de IA, usando los agentes `Roberto-Agent.md`, `Claudia-Agent.md`, `Pablo-Agent.md` y el juez `Eval-Spec.md` contra `ReqFunc.md` + `ReqNoFunc.md`.

---

## Iteración #1 — Personas SIN pain points (solo necesidades)

Las personas solo definían perfil + necesidades (N1–N4). El criterio "pain points" de la rúbrica quedó **NO EVALUABLE**.

### Roberto (Médico internista)

| Ítem | Req que lo cubre | Nivel |
|---|---|---|
| N1 Diagnóstico del turno anterior al iniciar | RF06, RF07 | 5 |
| N2 Registrar diagnóstico con red inestable | RF06, RF08 | 5 |
| N3 Notificación instantánea de paciente grave | RF12 | 5 |
| N4 Horario consolidado multi-hospital | RF04 | 5 |

Necesidades 5/5 · Pain points **NO EVALUABLE** (0/3) · Flujo 2/2 → **Total 7/10**

### Claudia (Enfermera jefe)

| Ítem | Req que lo cubre | Nivel |
|---|---|---|
| N1 Ver horario del equipo y detectar huecos | RF03 (¿con cuánta anticipación? no se especifica) | 1 |
| N2 Registrar estado del paciente en tiempo real | RF09 | 5 |
| N3 Saber quién es el médico responsable + contacto | RF11 | 5 |
| N4 Recibir indicaciones actualizadas al instante | RF14 | 5 |

Necesidades 4/5 · Pain points **NO EVALUABLE** (0/3) · Flujo 2/2 → **Total 6/10**

### Pablo (Coordinador de turnos)

| Ítem | Req que lo cubre | Nivel |
|---|---|---|
| N1 Programar sin cruces ni UCIs descubiertas | RF01, RF02, RF03 | 5 |
| N2 Tablero regional en tiempo real | RF15 | 5 |
| N3 Reasignar suplentes rápido | RF05 | 5 |
| N4 Reportes para la dirección | RF16 (formato/contenido no especificado) | 1 |

Necesidades 4/5 · Pain points **NO EVALUABLE** (0/3) · Flujo 1/2 (el flujo de adopción desde su Excel actual no está descrito) → **Total 5/10**

### Resumen Iteración #1

| Persona | Score |
|---|---|
| Roberto | 7/10 |
| Claudia | 6/10 |
| Pablo | 5/10 |
| **PROMEDIO** | **6/10 (60%) — FAILED** |

**Gaps detectados:** sin pain points, el juez no puede verificar que los requerimientos ataquen los dolores reales del día a día — la evaluación queda genérica y con techo bajo. Anticipación de alertas de cobertura (Claudia N1) y contenido de reportes (Pablo N4) quedan vagos.

---

## Iteración #2 — Personas CON pain points (práctica en clase)

**Cambio aplicado:** se agregaron 5 pain points a cada persona (`Personas/*.md`, sección "Pain Points"). Se volvió a correr el mismo eval, con los mismos requerimientos.

### Roberto

| Ítem | Req que lo cubre | Nivel |
|---|---|---|
| P1 Diagnóstico ilegible/perdido en cambio de turno | RF06, RF07 (traspaso obligatorio y versionado) | 5 |
| P2 Doble turno en hospitales distintos | RF02 (rechazo automático de cruces inter-hospital) | 5 |
| P3 Llamada a las 3am al médico equivocado | RF11, RF12, RF13 (responsable visible + escalamiento) | 5 |
| P4 Sistema lento → termina usando WhatsApp | RNF03, RNF06, RNF15 (inicio <1s, p95 <2s, ≤3 interacciones) | 5 |
| P5 Caída del sistema = sin información en UCI | RF08, RNF08, RNF09, RNF10 (offline + RTO <5min + RPO 0) | 5 |

Necesidades 5/5 · Pain points 3/3 · Flujo 2/2 → **Total 10/10**

### Claudia

| Ítem | Req que lo cubre | Nivel |
|---|---|---|
| P1 Medianoche: no ubica al médico de guardia | RF11, RF12, RF13 | 5 |
| P2 Huecos de cobertura descubiertos tarde | RF03 (alerta, pero sigue sin definirse anticipación mínima) | 1 |
| P3 Ejecuta indicaciones desactualizadas | RF14 (push con confirmación de lectura) | 5 |
| P4 Traspaso verbal de enfermería pierde información | RF10 (resumen automático de traspaso) | 5 |
| P5 Sesiones ajenas en estaciones compartidas | RF18, RNF14 | 5 |

Necesidades 4/5 · Pain points 2.5/3 · Flujo 2/2 → **Total 8.5/10 ≈ 8/10**

### Pablo

| Ítem | Req que lo cubre | Nivel |
|---|---|---|
| P1 Cruces descubiertos por el médico furioso | RF02 | 5 |
| P2 10 llamadas para hallar suplente, UCI descubierta | RF05, RF13 | 5 |
| P3 2 días consolidando Excels para la dirección | RF15, RF16 | 5 |
| P4 Formatos de horario distintos por hospital | RF01 lo implica, pero **no hay requerimiento de estandarización/migración de datos existentes** | 1 |
| P5 El método actual no escala a más regiones | RNF01, RNF02 | 5 |

Necesidades 4/5 · Pain points 2.5/3 · Flujo 1.5/2 → **Total 8/10**

### Resumen Iteración #2

| Persona | Score |
|---|---|
| Roberto | 10/10 |
| Claudia | 8/10 |
| Pablo | 8/10 |
| **PROMEDIO** | **8.7/10 (87%) — PASSED** |

### Gaps detectados (entrada para iteración #3)

- **Claudia P2:** RF03 debe especificar anticipación mínima de la alerta de hueco de cobertura (ej: ≥ 12 horas antes del turno).
- **Pablo P4:** falta un requerimiento de estandarización del formato de horarios y migración de los datos actuales (Excel) de cada hospital.
- **Pablo N4:** RF16 debe definir contenido mínimo de los reportes para la dirección regional.

---

## ¿Cambió algo? (respuesta de la práctica)

**Sí, cambió — el promedio subió de 6/10 (FAILED) a 8.7/10 (PASSED), y el eval se volvió más útil:**

1. **El eval pasó de genérico a verificable.** Sin pain points, el juez solo podía comparar contra necesidades abstractas y el criterio de dolores quedaba NO EVALUABLE. Con pain points concretos, cada requerimiento se pudo trazar contra un dolor real (ej: RF13 escalamiento ↔ "a las 3am llaman al médico equivocado").
2. **Los scores subieron porque la cobertura ahora es demostrable**, no porque los requerimientos cambiaran: son los mismos RF/RNF en ambas iteraciones.
3. **Aparecieron gaps que antes eran invisibles:** la migración de los Excels de Pablo y la anticipación de alertas de cobertura de Claudia solo se detectaron cuando el dolor estuvo escrito de forma concreta.

**Conclusión:** los pain points hacen al eval más discriminativo — mejor rúbrica de entrada ⇒ mejor señal de salida. La siguiente iteración debe atacar los 3 gaps listados.
