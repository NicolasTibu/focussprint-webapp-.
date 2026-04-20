# Project Management

## Objetivo de esta fase
Preparar una base tecnica solida para construir FocusSprint con entregas incrementales y validaciones frecuentes.

## Estructura de trabajo
- **Frontend**: `frontend/` con Vite + React + TypeScript.
- **Backend**: `server/` conservando estructura `server/src/` con `routes/`, `controllers/`, `services/`, `config/`.
- **Documentacion**: `docs/` para idea, decisiones tecnicas y gestion del proyecto.

## Organizacion por fases
- **Fase 1 - Setup**: scaffolding del frontend, dependencias base y estructura de carpetas.
- **Fase 2 - UI base**: layout principal, rutas y componentes iniciales.
- **Fase 3 - Logica de negocio**: manejo de tareas, sesiones de enfoque y persistencia con LocalStorage.
- **Fase 4 - Integraciones**: API publica opcional para datos de ejemplo.
- **Fase 5 - Calidad**: pruebas, refinamiento UX y ajustes de rendimiento.

## Metodologia
- Trabajo en iteraciones cortas (1-3 dias por bloque funcional).
- Cada iteracion cierra con:
  - entregable funcional;
  - checklist de validacion manual;
  - actualizacion breve en documentacion.

## Gestion de tareas
- El tablero concentra:
  - backlog priorizado;
  - tareas en progreso;
  - tareas finalizadas;
  - bloqueos y riesgos.
- Formato sugerido para cada tarjeta:
  - **Titulo**: accion + modulo;
  - **Criterio de aceptacion**;
  - **Estimacion**;
  - **Dependencias**.

## Convenciones operativas
- Commits pequenos y descriptivos.
- Rama principal estable (`main`).
- Cambios de arquitectura documentados en `docs/`.
- Evitar alcance extra en una misma tarea para mantener foco.
