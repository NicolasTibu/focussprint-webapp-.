# Capa de red frontend y tipos (Fase 12)

## Objetivo

Consumir el backend desde el frontend con un cliente tipado y usar la API como fuente unica de verdad para tareas.

## Cliente API tipado

Archivo:

- `frontend/src/api/client.ts`

Responsabilidades:

- Centraliza llamadas HTTP con `fetch`.
- Tipa respuestas y payloads de request.
- Maneja errores HTTP con `ApiClientError` (incluye status).

Funciones expuestas:

- `getTasks()`
- `createTask(payload)`
- `replaceTask(taskId, payload)`
- `updateTask(taskId, payload)`
- `deleteTask(taskId)`

Base URL configurada:

- `VITE_API_BASE_URL` (variable de entorno)
- Fallback local: `http://localhost:3000/api/v1`

## Contrato de tipos alineado con backend

Tipos de red:

- `frontend/src/types/api.ts`
  - `CreateTaskRequest`
  - `UpdateTaskRequest`
  - `TaskResponse`
  - `TasksResponse`
  - `ApiErrorResponse`

Tipo de dominio de tarea:

- `frontend/src/types/task.ts`

Contrato actual (alineado al backend):

- `id: string`
- `title: string`
- `completed: boolean`
- `emoji: string`
- `priority: 'low' | 'medium' | 'high'`
- `dueDate: string | null`

## Estados de red en UI: loading, success, error

Se implementan en `frontend/src/context/AppContext.tsx`:

- `state.isLoading`: activa vista de carga al pedir tareas.
- `state.error`: muestra mensaje de error si falla una llamada.
- `state.tasks`: datos exitosos desde API.

En la UI:

- `HomePage` muestra:
  - loading (`Cargando tareas desde la API...`)
  - error con boton `Reintentar carga`
  - datos en `TaskList` cuando carga correctamente
- `StatsPage` reutiliza los estados de red y permite reintento.

## Fuente unica de verdad

Las tareas ya no se persisten en `LocalStorage`.

Cambios clave:

- `AppContext` elimina `useLocalStorageState` para tareas.
- Al montar la app, `fetchTasks()` carga desde backend.
- Crear/actualizar/eliminar tareas invoca API y sincroniza estado en memoria con la respuesta del servidor.

De esta forma, para el recurso `tasks`, la API backend es la unica fuente de verdad.
