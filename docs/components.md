# Componentes reutilizables (FocusSprint)

## Objetivo
Definir una base de componentes React reutilizables, tipados con TypeScript y estilizados con Tailwind CSS para acelerar el desarrollo del MVP.

## Estructura implementada

- `frontend/src/components/common/`
  - `Button.tsx`
  - `Card.tsx`
  - `Modal.tsx`
- `frontend/src/components/layout/`
  - `AppShell.tsx`
- `frontend/src/components/tasks/`
  - `TaskForm.tsx`
  - `TaskList.tsx`
  - `TaskItem.tsx`
- `frontend/src/components/progress/`
  - `DailyProgressCard.tsx`

## Tipos usados por los componentes

- `frontend/src/types/task.ts`
  - `TaskPriority`, `TaskStatus`, `Task`.
- `frontend/src/types/stats.ts`
  - `DailyStats`.

Los componentes de dominio (`TaskList`, `TaskItem`, `TaskForm`, `DailyProgressCard`) consumen datos tipados desde el estado global (`AppContext`).

## Estado global y consumo de datos

- `frontend/src/context/AppContext.tsx`:
  - Gestiona tareas y estado de UI (modal de nueva tarea).
  - Expone acciones tipadas: `addTask`, `toggleTask`, `removeTask`, `openTaskModal`, `closeTaskModal`.
  - Calcula `stats` derivados (`total`, `completadas`, `pendientes`, `completionRate`).
- `frontend/src/hooks/useAppContext.ts`:
  - Hook para consumir el contexto de forma segura y tipada.

## Componentes y responsabilidades

- `Button`
  - Boton reutilizable con variantes (`primary`, `secondary`, `danger`).
  - Extiende `ButtonHTMLAttributes` para ser flexible.
- `Card`
  - Contenedor de secciones con `title`, `subtitle` y `actions`.
  - Permite composicion via `children`.
- `Modal`
  - Overlay reutilizable controlado por `isOpen`.
  - Encapsula titulo, cierre y contenido.
- `AppShell`
  - Layout principal de la pagina.
  - Reutilizable para futuras paginas (`StatsPage`, `SettingsPage`).
- `TaskForm`
  - Formulario tipado para crear tareas.
  - Entrega payload validado hacia `onSubmit`.
- `TaskList`
  - Renderiza lista de tareas tipadas.
  - Maneja estado vacio.
- `TaskItem`
  - Item reutilizable de tarea con acciones de completar/eliminar.
- `DailyProgressCard`
  - Tarjeta de progreso con barra y metrica de cumplimiento.

## Composicion aplicada en HomePage

`HomePage` compone el flujo principal combinando:

1. `AppShell` para layout.
2. `Card` + `DailyProgressCard` para resumen.
3. `Card` + `TaskList` + `Button` para gestion de tareas.
4. `Modal` + `TaskForm` para alta de nueva tarea.

Esto mantiene separacion entre UI base, componentes de dominio y estado global.

## Estilos y layout con Tailwind

- Se usan utilidades de Tailwind para espaciado, tipografia, bordes y grid responsive.
- El layout principal usa `grid` con 1 columna en mobile y 3 columnas en desktop.
- Los componentes mantienen clases autocontenidas para facilitar reuso.
