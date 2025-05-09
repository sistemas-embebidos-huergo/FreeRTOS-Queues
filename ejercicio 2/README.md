# Enunciado: Productor-Consumidor con Prioridad en ESP32

## Objetivo

Desarrollar un programa para ESP32 que utilice ambos núcleos (cores) del microcontrolador para implementar el patrón productor-consumidor usando una cola de comandos para controlar LEDs.

## Requisitos

### Productor (Core 0):

- Debe ejecutarse en el `core 0` del ESP32.
- Su tarea es generar comandos aleatorios del tipo `LedCommand` (pueden ser: `LED_RED`, `LED_GREEN`, `LED_BLUE`, `LED_BLINK`).
- Cada comando debe ser insertado en una cola compartida.
- Si el comando generado es `LED_BLINK`, debe insertarse al principio de la cola (es decir, debe tener prioridad sobre los demás comandos). Los otros comandos se insertan al final de la cola.

Explicación de prioridad:

> El concepto de prioridad en una cola implica que ciertos elementos (en este caso, los comandos `LED_BLINK`) deben ser atendidos antes que otros, independientemente del orden en que llegaron. Esto se logra insertando los comandos prioritarios al principio de la cola.

### Consumidor (Core 1):

- Debe ejecutarse en el core 1 del ESP32.
  Su tarea es extraer comandos de la cola y ejecutar la acción correspondiente:
- Si el comando es `LED_RED`, encender el LED rojo durante 1 segundo.
- Si el comando es `LED_GREEN`, encender el LED verde durante 1 segundo.
- Si el comando es `LED_YELLOW`, encender el LED amarillo durante 1 segundo.
- Si el comando es `LED_BLINK`, hacer parpadear los tres LEDs durante 1 segundo.
- Cada comando debe ejecutarse durante exactamente 1 segundo antes de procesar el siguiente.

### Consideraciones

- Utilizar FreeRTOS y sus mecanismos de colas para la comunicación entre tareas.
- Asegurarse de que el productor y el consumidor corran en diferentes núcleos utilizando las funciones de FreeRTOS (xTaskCreatePinnedToCore).
- Documentar el código y explicar cómo se implementa la prioridad en la cola.
- El programa debe funcionar indefinidamente.
