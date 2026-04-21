# Context API y estado global (FocusSprint)

## Objetivo
Implementar estado global con Context API para compartir datos y acciones entre componentes sin prop drilling.

## 1) Creacion del contexto con `createContext`

Archivo principal:

- `frontend/src/context/AppContext.tsx`

Implementacion:

- Se define `AppContextValue` con estado global (`state`, `stats`) y acciones (`addTask`, `toggleTask`, `removeTask`, `openTaskModal`, `closeTaskModal`).
- Se crea el contexto tipado con:
  - `createContext<AppContextValue | undefined>(undefined)`

Esto permite:

- Tipado fuerte en TypeScript.
- Detectar uso incorrecto del contexto fuera del Provider.

## 2) Provider para compartir estado global

El `AppProvider` en `AppContext.tsx`:

- Mantiene estado global de tareas y UI (`isTaskModalOpen`) usando `useReducer`.
- Calcula estadisticas derivadas (`stats`) con `useMemo`.
- Expone acciones memorizadas con `useCallback`.
- Envuelve la app con:
  - `<AppContext.Provider value={value}>{children}</AppContext.Provider>`

Integracion en la app:

- `frontend/src/main.tsx` envuelve `App` con `<AppProvider>`, dejando el contexto disponible en todo el arbol de componentes.

## 3) Consumo del contexto en componentes

Hook de acceso:

- `frontend/src/hooks/useAppContext.ts`
- Encapsula `useContext(AppContext)` y lanza error si no hay Provider.

Consumo real:

- `frontend/src/pages/HomePage.tsx` usa `useAppContext()` para leer:
  - `state` (tareas, modal)
  - `stats` (progreso diario)
  - acciones (`addTask`, `toggleTask`, `removeTask`, `openTaskModal`, `closeTaskModal`)

Desde `HomePage`, esos datos/acciones se distribuyen a componentes como:

- `TaskList`
- `TaskForm`
- `DailyProgressCard`
- `Modal`

## 4) Cuando conviene usar Context API

Context API es util cuando:

- Varias partes de la app necesitan los mismos datos o acciones.
- Se quiere evitar pasar props por muchos niveles (prop drilling).
- El estado es transversal (usuario autenticado, tema, idioma, UI global, datos base de dominio).
- No se necesita aun una libreria externa de estado global.

En este proyecto, Context API se usa para:

- Centralizar tareas y estado de interfaz.
- Compartir una unica fuente de verdad entre formulario, lista, modal y tarjetas de progreso.

## 5) Beneficios obtenidos en FocusSprint

- Menos complejidad en el paso de props.
- Estado mas consistente entre componentes.
- Logica de negocio y actualizacion de estado concentrada en un solo lugar (`AppContext`).
- Escalabilidad para agregar nuevas pantallas y modulos sin duplicar estado.
