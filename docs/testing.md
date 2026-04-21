# Testing y mejoras (Fase 13)

## Alcance de pruebas ejecutadas

Se realizaron pruebas sobre frontend y backend para validar flujo funcional, compilacion y errores.

## 1) Pruebas de funcionalidades principales

### Frontend

- `npm run lint` en `frontend/`: OK.
- `npm run build` en `frontend/`: OK (TypeScript + Vite).
- Verificacion de estados de red en UI (implementados y compilando):
  - loading (`state.isLoading`)
  - success (`state.tasks`)
  - error (`state.error` + boton reintento)

### Backend (smoke test API)

Servidor levantado en `PORT=3000` y prueba CRUD sobre `/api/v1/tasks`:

- `POST /tasks`: crea tarea correctamente.
- `PATCH /tasks/:id`: actualiza `completed` correctamente.
- `DELETE /tasks/:id`: elimina correctamente.
- `GET /tasks/:id` tras eliminar: responde `404` como esperado.

Evidencia de salida:

- `MISSING_STATUS=404`
- `CREATED_ID=2 PATCH_COMPLETED=True`

## 2) Responsive design

Revision de layout responsive en codigo:

- `HomePage`, `StatsPage`, `SettingsPage` usan grid con breakpoints `md:*`.
- `AppShell` y componentes comunes usan clases Tailwind adaptativas (`px-4/md:px-6`, `md:grid-cols-*`).

Nota:

- Se validaron los breakpoints a nivel de implementacion y build.
- Recomendado complementar con verificacion visual manual en navegador (mobile/tablet/desktop) para QA final.

## 3) Revision de errores en consola

Se detectaron y corrigieron errores durante validacion:

1. **Lint React hooks**
   - Error: `react-hooks/set-state-in-effect` en `AppContext`.
   - Fix: se diferio la carga inicial (`fetchTasks`) usando `setTimeout` con cleanup.

2. **Error de tipos TypeScript**
   - Error: retorno `Promise<boolean | undefined>` en `toggleTask`.
   - Fix: retorno explicito `false` cuando no existe tarea.

Resultado posterior:

- `npm run lint` ✅
- `npm run build` ✅

## 4) Bugs encontrados y corregidos

- Bug de lint por setState sincrono en efecto: corregido.
- Bug de tipado en retorno async de toggle: corregido.
- Entorno backend sin dependencias instaladas (`Cannot find module 'express'`): resuelto con `npm install` en `server/`.

## 5) Estado final de la Fase 13

- Funcionalidades principales probadas (build/lint + smoke API).
- Errores detectados durante testing corregidos.
- Proyecto en estado compilable.

## 6) Checklist manual recomendado (QA final)

- Crear tarea desde modal.
- Ver mensaje de confirmacion.
- Completar/reabrir tarea.
- Eliminar tarea.
- Simular backend caido y usar boton reintentar.
- Revisar vistas `Home`, `Stats`, `Settings` en anchos:
  - 360px (mobile)
  - 768px (tablet)
  - 1280px (desktop)
