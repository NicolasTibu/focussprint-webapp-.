# Despliegue (Fase 14)

## Objetivo

Desplegar frontend y backend por separado, conectar ambos con variables de entorno y validar funcionamiento en produccion.

## Arquitectura de despliegue recomendada

- Frontend (Vite + React): **Vercel** o **Netlify**
- Backend (Node.js + Express): **Render** (o Railway/Fly.io)

## 1) Preparar variables de entorno

### Frontend

Archivo de referencia:

- `frontend/.env.example`

Variable usada por el cliente API:

- `VITE_API_BASE_URL` (ejemplo: `https://tu-api.onrender.com/api/v1`)

El cliente usa esta variable en:

- `frontend/src/api/client.ts`

### Backend

El backend usa:

- `PORT` (inyectado por el proveedor en produccion)

En local puedes usar:

- PowerShell: `$env:PORT=3000; npm start`

## 2) Desplegar backend en Render (Web Service)

1. Crear servicio en Render conectado al repo.
2. Configurar:
   - Root directory: `server`
   - Build command: `npm install`
   - Start command: `npm start`
3. Deploy y copiar URL publica (ejemplo):
   - `https://taskflow-api.onrender.com`
4. Verificar health/API:
   - `GET https://taskflow-api.onrender.com/health`
   - `GET https://taskflow-api.onrender.com/api/v1/tasks`

## 3) Desplegar frontend en Vercel

1. Importar repo en Vercel.
2. Configurar:
   - Root directory: `frontend`
   - Build command: `npm run build`
   - Output directory: `dist`
3. Definir variable de entorno en Vercel:
   - `VITE_API_BASE_URL=https://taskflow-api.onrender.com/api/v1`
4. Deploy y copiar URL publica (ejemplo):
   - `https://taskflow-pro.vercel.app`

## 4) Validacion en produccion

Checklist de smoke test:

1. Abrir frontend publicado.
2. Comprobar carga inicial de tareas (`loading -> datos`).
3. Crear tarea.
4. Marcar tarea completada y luego reabrir.
5. Eliminar tarea.
6. Probar ruta invalida y validar pagina 404.
7. Revisar consola del navegador: sin errores de CORS/Network.

## 5) Si usas Netlify + Railway (alternativa)

- Frontend en Netlify:
  - Root `frontend`, build `npm run build`, publish `dist`
- Backend en Railway:
  - Root `server`, start `npm start`
- Variable en Netlify:
  - `VITE_API_BASE_URL=https://tu-api.railway.app/api/v1`

## 6) URLs del proyecto

Actualizar `README.md` con:

- URL frontend (Vercel/Netlify)
- URL API (Render/Railway/Fly.io)

Plantilla:

- Frontend: `https://TU_FRONTEND_URL`
- API: `https://TU_API_URL/api/v1`
