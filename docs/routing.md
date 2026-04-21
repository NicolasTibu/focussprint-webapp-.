# Rutas y navegacion (FocusSprint)

## Objetivo
Configurar navegacion cliente con React Router para separar funcionalidades por pagina y mejorar la experiencia de uso.

## Libreria y montaje

- Libreria: `react-router-dom`
- El enrutador se monta en `frontend/src/main.tsx` con `BrowserRouter`.
- La definicion de rutas vive en `frontend/src/App.tsx`.

## Estructura de rutas

Rutas implementadas:

- `/`
  - Redirige a `/home` usando `Navigate`.
- `/home`
  - Pagina principal de tareas diarias.
  - Componente: `HomePage`.
- `/stats`
  - Pagina de metricas y progreso diario.
  - Componente: `StatsPage`.
- `/settings`
  - Pagina de configuracion base y ajustes futuros.
  - Componente: `SettingsPage`.
- `*`
  - Ruta comodin para paths no existentes.
  - Componente: `NotFoundPage` (pagina 404).

## Navegacion entre paginas

La navegacion principal se implementa en `frontend/src/components/layout/AppShell.tsx`:

- Se usa `NavLink` para enlaces a:
  - Inicio (`/home`)
  - Estadisticas (`/stats`)
  - Configuracion (`/settings`)
- `NavLink` permite aplicar estilos activos y mostrar visualmente la pagina actual.

## Pagina 404

`frontend/src/pages/NotFoundPage.tsx` cubre rutas inexistentes:

- Muestra mensaje de "Pagina no encontrada".
- Incluye un enlace para volver a `/home`.

## Beneficios de esta estructura

- Escalabilidad: agregar nuevas secciones no afecta la pagina principal.
- Mantenibilidad: cada pantalla tiene responsabilidad clara.
- UX: usuario siempre puede navegar desde el menu y recuperarse de rutas invalidas con la 404.
