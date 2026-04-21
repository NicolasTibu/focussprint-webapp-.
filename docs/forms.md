# Formularios e interaccion (FocusSprint)

## Objetivo
Implementar formularios controlados en React, con validaciones basicas y feedback claro para el usuario.

## Formulario principal implementado

Archivo:

- `frontend/src/components/tasks/TaskForm.tsx`

Campos:

- `title` (input de texto)
- `priority` (select: `low`, `medium`, `high`)

Ambos campos se gestionan como formulario controlado con estado local (`useState`).

## Estado de inputs (controlado)

En `TaskForm`:

- `title` almacena el valor actual del input.
- `priority` almacena la prioridad seleccionada.
- `titleError` guarda el mensaje de validacion cuando el titulo es invalido.
- `isSubmitted` permite activar validacion reactiva despues del primer intento de envio.

Cada cambio en los inputs actualiza estado y vuelve a renderizar el valor en pantalla.

## Validaciones basicas aplicadas

Validacion del campo `title`:

- Requerido (no vacio).
- Minimo 3 caracteres.
- Maximo 80 caracteres.

Si falla alguna regla:

- Se bloquea el submit.
- Se muestra mensaje de error debajo del input.
- El input marca estado invalido (`aria-invalid` + estilo de borde rojo).

## Mensajes de error y confirmacion

### Error en el formulario

- Se muestra mensaje rojo contextual debajo del campo titulo cuando no cumple reglas.

### Confirmacion en el formulario

- Si el titulo ya es valido, se muestra mensaje de estado:
  - "Formulario valido. Puedes guardar la tarea."

### Confirmacion al guardar

Archivo:

- `frontend/src/pages/HomePage.tsx`

Al crear tarea correctamente:

- Se muestra mensaje de confirmacion sobre la lista:
  - `Tarea "<titulo>" creada correctamente.`
- El mensaje se limpia automaticamente despues de 3 segundos.

## Flujo de ejemplo

1. Usuario abre modal y escribe un titulo.
2. Si el titulo es corto/vacio, el formulario muestra error y no envia.
3. Si el titulo es valido, puede enviar.
4. Se crea la tarea en estado global y aparece confirmacion temporal en la pagina principal.

Este flujo mejora la UX al evitar envios invalidos y dar feedback inmediato del resultado.
