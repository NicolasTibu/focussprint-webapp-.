# Backend y API (Fase 11)

## Implementacion

Se implementa backend propio en `server/` con Node.js + Express dentro del mismo repositorio.

Arquitectura por capas aplicada:

- `server/src/routes/task.routes.js`: define endpoints y verbos HTTP.
- `server/src/controllers/task.controller.js`: frontera HTTP (request/response y códigos).
- `server/src/services/task.service.js`: lógica de negocio y acceso a datos en memoria.
- `server/src/validators/task.validator.js`: validación de params y body en la frontera de red.

## Base URL

- `http://localhost:3000/api/v1/tasks`

## Endpoints REST

### 1) GET `/api/v1/tasks`

Obtiene todas las tareas.

- **200 OK**:

```json
[
  {
    "id": "1",
    "title": "Planear sprint",
    "completed": false,
    "emoji": "🎯",
    "priority": "medium",
    "dueDate": null
  }
]
```

### 2) GET `/api/v1/tasks/:id`

Obtiene una tarea por id.

- **200 OK**:

```json
{
  "id": "1",
  "title": "Planear sprint",
  "completed": false,
  "emoji": "🎯",
  "priority": "medium",
  "dueDate": null
}
```

- **404 Not Found**: si el id no existe.
- **400 Bad Request**: si el id es inválido.

### 3) POST `/api/v1/tasks`

Crea una tarea.

Request:

```json
{
  "title": "Preparar demo",
  "completed": false,
  "emoji": "🚀",
  "priority": "high",
  "dueDate": "2026-04-30"
}
```

- **201 Created**:

```json
{
  "id": "2",
  "title": "Preparar demo",
  "completed": false,
  "emoji": "🚀",
  "priority": "high",
  "dueDate": "2026-04-30"
}
```

- **400 Bad Request**: body inválido (`INVALID_TITLE`, `INVALID_PRIORITY`, etc).

### 4) PUT `/api/v1/tasks/:id`

Reemplaza completamente una tarea.

Request:

```json
{
  "title": "Demo final",
  "completed": true,
  "emoji": "✅",
  "priority": "medium",
  "dueDate": null
}
```

- **200 OK**: devuelve la tarea reemplazada.
- **400 Bad Request**: faltan campos obligatorios o formato inválido.
- **404 Not Found**: id no encontrado.

### 5) PATCH `/api/v1/tasks/:id`

Actualiza parcialmente una tarea.

Request:

```json
{
  "completed": true
}
```

- **200 OK**: devuelve tarea actualizada.
- **400 Bad Request**: body vacío o campos inválidos.
- **404 Not Found**: id no encontrado.

### 6) DELETE `/api/v1/tasks/:id`

Elimina una tarea por id.

- **204 No Content**: eliminación correcta.
- **400 Bad Request**: id inválido.
- **404 Not Found**: id no encontrado.

## Códigos HTTP y manejo de errores

Se cumplen códigos requeridos:

- `200` operaciones GET/PUT/PATCH exitosas
- `201` creación con POST
- `400` validación en frontera de red (params/body)
- `404` recurso no encontrado
- `500` error interno no controlado (middleware global en `server/src/index.js`)
