# Idea del proyecto: FocusSprint (microapp de sesiones de enfoque)

## 1) Problema que intenta resolver
Muchas personas (estudiantes, freelancers y trabajadores remotos) tienen tareas grandes, pero les cuesta mantener el enfoque por periodos cortos y constantes.  
Suelen pasar demasiado tiempo decidiendo "por dónde empezar" y no tienen una forma simple de registrar avances diarios sin usar apps complejas.

FocusSprint busca resolver esto con una microapp web ligera que ayude a:
- dividir el trabajo en sesiones cortas de enfoque;
- registrar progreso rápido;
- mantener una racha diaria con datos guardados localmente.

## 2) Usuario objetivo
- Estudiantes de secundaria, universidad o bootcamps.
- Freelancers y personas que trabajan desde casa.
- Usuarios que quieren productividad simple sin configuración avanzada.
- Personas que prefieren apps web rápidas sin necesidad de crear cuenta.

## 3) Funcionalidades principales (MVP)
- Crear una lista corta de tareas del día (3-7 tareas).
- Iniciar una sesión de enfoque con temporizador (por ejemplo 25 minutos).
- Marcar tarea como completada al terminar la sesión.
- Registrar número de sesiones completadas por día.
- Mostrar progreso diario básico (ej. "4/6 tareas completas").
- Guardar y recuperar datos con `LocalStorage`.
- Cargar datos de ejemplo (seed inicial) para probar la app rápido.

## 4) Funcionalidades opcionales
- Duración personalizable del temporizador (15/25/45 min).
- Modo descanso corto entre sesiones (5 min).
- Etiquetas por tipo de tarea (estudio, trabajo, personal).
- Historial semanal con resumen simple.
- Sonido o notificación al finalizar la sesión.
- Modo oscuro.
- Exportar resumen en formato JSON o texto.

## 5) Posibles mejoras futuras
- Sincronización en la nube con autenticación.
- Colaboración (grupos de estudio / equipo).
- Gamificación (insignias por rachas y objetivos).
- Estadísticas avanzadas (horas productivas por franja horaria).
- Integración con calendario (Google Calendar / Outlook).
- Versión móvil con PWA y soporte offline mejorado.

## 6) Nota técnica de datos
Para esta versión inicial no se requiere base de datos:
- Persistencia local con `LocalStorage`.
- API pública opcional para frases motivacionales o datos de ejemplo.
- Estructura de datos simple en JSON para facilitar evolución futura.
