# Hooks de React en FocusSprint

## Objetivo
Aplicar hooks de React para gestionar estado, efectos secundarios, optimizacion de render y reutilizacion de logica.

## 1) `useState`

Uso principal:

- `frontend/src/components/tasks/TaskForm.tsx`
  - `title` guarda el valor del input de tarea.
  - `priority` guarda la prioridad seleccionada.

Como funciona aqui:

- Cada cambio del usuario en el formulario actualiza estado local.
- Al enviar, se valida y reinicia el formulario sin afectar otras partes de la app.

## 2) `useEffect`

Usos principales:

- `frontend/src/context/AppContext.tsx`
  - Persiste `state.tasks` en `LocalStorage` cuando cambian las tareas.
- `frontend/src/components/common/Modal.tsx`
  - Agrega un listener de teclado para cerrar con `Escape` y lo limpia al cerrar/desmontar.

Como funciona aqui:

- Ejecuta efectos secundarios despues del render (persistencia y listeners).
- Incluye cleanup para evitar fugas de memoria o listeners duplicados.

## 3) `useMemo`

Usos principales:

- `frontend/src/context/AppContext.tsx`
  - Calcula `stats` derivadas (`total`, `completadas`, `pendientes`, `%`).
  - Memoiza el `value` del contexto para no recrearlo en cada render.
- `frontend/src/pages/HomePage.tsx`
  - Memoiza `sortedTasks` para ordenar tareas (pendientes primero) solo cuando cambia `state.tasks`.

Como funciona aqui:

- Evita recalculos innecesarios en cada render.
- Mejora rendimiento cuando crece el numero de tareas.

## 4) `useCallback`

Uso principal:

- `frontend/src/context/AppContext.tsx`
  - `addTask`, `toggleTask`, `removeTask`, `openTaskModal`, `closeTaskModal`.

Como funciona aqui:

- Mantiene referencia estable de funciones entre renders.
- Reduce rerenders de componentes hijos que reciben handlers por props.

## 5) Custom hook reutilizable: `useLocalStorageState`

Archivo:

- `frontend/src/hooks/useLocalStorageState.ts`

Que hace:

- Lee un valor inicial de `LocalStorage` (si existe).
- Mantiene el estado en memoria con `useState`.
- Sincroniza automaticamente en `LocalStorage` con `useEffect`.

Firma:

- `useLocalStorageState<T>(key: string, initialValue: T)`
- Retorna `[value, setValue]` tipado.

Ventaja:

- Centraliza logica de persistencia y evita duplicar codigo en varios componentes/contextos.

## 6) Hook de acceso al contexto: `useAppContext`

Archivo:

- `frontend/src/hooks/useAppContext.ts`

Que hace:

- Encapsula `useContext(AppContext)`.
- Lanza error claro si se usa fuera de `AppProvider`.

Ventaja:

- Simplifica imports y mejora seguridad al consumir el estado global.
