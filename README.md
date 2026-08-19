# Lab 01 — Caso de Estudio: Essalud UCI

**Curso:** Arquitectura de Software — UTEC 2026-II

## Definición del Problema

Essalud lanza un piloto para el manejo de sus Unidades de Cuidados Intensivos (UCI) en Lima y sus distritos. Los problemas centrales son:

1. **Desorden en los horarios** de médicos y enfermeras: cruces de turnos, huecos sin cobertura.
2. **Alta rotación de médicos internistas**: el diagnóstico del médico saliente debe estar siempre disponible para el médico entrante en el cambio de turno.
3. **Problema de medianoche**: si un paciente se agrava en el turno noche, el sistema debe contactar rápidamente al médico encargado, y escalar a un suplente si no responde.
4. **Actualizaciones en tiempo real**: notificaciones push a múltiples médicos/enfermeras y persistencia del diagnóstico disponible en todo momento.

### Metas de escalamiento y rendimiento

| Meta | Valor |
|---|---|
| Lanzamiento | 1K hospitales |
| 6 meses | 100K hospitales |
| 2 años | 10M hospitales |
| Inicio de aplicación | < 1 segundo |
| Configuración de aplicación | < 5 segundos |
| Disponibilidad | 99.9% |
| Recuperación ante caída | < 5 minutos |

## Usuarios / Clientes del sistema

| Usuario | Rol | Interés principal |
|---|---|---|
| Médico internista UCI | Usuario primario | Ver diagnóstico del turno anterior, registrar el suyo, recibir alertas de pacientes graves |
| Enfermera jefe UCI | Usuario primario | Ver su horario sin cruces, recibir notificaciones de cambios de estado de pacientes |
| Coordinador de turnos (admin) | Usuario secundario | Programar horarios sin cruces ni huecos de cobertura en toda la red |
| Essalud (institución) | Cliente | Piloto exitoso en Lima, escalable a nivel nacional, disponibilidad 99.9% |
| Paciente / familiares | Beneficiario indirecto | Continuidad de atención, respuesta rápida en emergencias |

## Personas (usuarios modelo)

- [Roberto](Personas/Roberto.md) — Médico internista UCI (alta rotación)
- [Claudia](Personas/Claudia.md) — Enfermera jefe UCI
- [Pablo](Personas/Pablo.md) — Coordinador de turnos de la red Essalud Lima

## Requerimientos

- [Requerimientos Funcionales](Requirements/ReqFunc.md)
- [Requerimientos No Funcionales](Requirements/ReqNoFunc.md)

## Agentes

- [Agente Roberto](Agents/Roberto-Agent.md), [Agente Claudia](Agents/Claudia-Agent.md), [Agente Pablo](Agents/Pablo-Agent.md) — cada agente encarna a una persona y evalúa si los requerimientos satisfacen sus necesidades.
- [Eval-Spec](Agents/Spec/Eval-Spec.md) — agente juez que recibe personas + requerimientos y devuelve un % de calidad según rúbrica.

## Prompt usado para evaluar (requerimientos vs personas)

```
Actúa como el agente definido en el archivo [Persona]-Agent.md adjunto.
Encarna completamente a esa persona: sus necesidades, contexto y pain points.

Te adjunto también ReqFunc.md y ReqNoFunc.md.

Tarea:
1. Recorre cada una de tus necesidades y pain points.
2. Para cada uno, indica qué requerimiento(s) lo cubren y si la cobertura es
   total, parcial o nula.
3. Señala necesidades tuyas que NINGÚN requerimiento cubre.
4. Termina con un veredicto en primera persona: ¿este sistema te sirve en tu
   día a día en la UCI? ¿Qué te falta?

Luego, actúa como el agente Eval-Spec.md y aplica su rúbrica para darme el
score de esta persona (X/10) con justificación por criterio.
```

## Reporte de iteraciones

Ver [REPORTE.md](REPORTE.md) — Iteración 1 (personas sin pain points) vs Iteración 2 (personas con pain points).

## Estructura del repo

```
lab01/
├── README.md
├── REPORTE.md
├── Personas/
│   ├── Roberto.md
│   ├── Claudia.md
│   └── Pablo.md
├── Requirements/
│   ├── ReqFunc.md
│   └── ReqNoFunc.md
└── Agents/
    ├── Roberto-Agent.md
    ├── Claudia-Agent.md
    ├── Pablo-Agent.md
    └── Spec/
        └── Eval-Spec.md
```
