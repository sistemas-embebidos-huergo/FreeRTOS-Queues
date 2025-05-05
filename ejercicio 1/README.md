# Enunciado: Productor/Consumidor con FreeRTOS Queues

## Objetivo

Utilizando los archivos `data.h` y `data.cpp` (que contienen un arreglo de 200 personas), implementar un programa para el ESP32 que simule el clásico problema productor/consumidor usando colas (queues).

## Requisitos

### Productor:

- Debera correr en el core 0.
- Crear una tarea (task) llamada `productor`.
- Cada vez que se ejecute, debe esperar un tiempo aleatorio entre 500 ms y 2000 ms.
- Luego, debe tomar la siguiente persona del arreglo people y agregarla a una cola de FreeRTOS.
- Si la cola está llena, debe esperar hasta que haya espacio disponible.

### Consumidor:

- Debera correr en el core 1.
- Crear una tarea (task) llamada `consumidor`.
- Cada vez que se ejecute, debe esperar exactamente 1 segundo.
- Luego, debe leer (remover) una persona de la cola.
- Debe imprimir por puerto serie (Serial) los datos de la persona consumida (id, nombre, apellido, email).
- Si la cola está vacía, debe esperar hasta que haya una persona disponible.

### Cola:

- La cola debe ser de tipo `Person` y tener una capacidad de al menos 30 elementos.

## Consideraciones:

- El programa debe incluir los archivos data.h y data.cpp para acceder al arreglo de personas.
- El productor debe recorrer el arreglo people desde el primer elemento hasta el último, y luego detenerse (o reiniciar desde el principio, a elección del alumno).
- El consumidor debe funcionar indefinidamente.
- El código debe estar bien comentado y estructurado.
