# Colas (Queues)

## ¿Qué es una cola?

Una **cola** (en inglés, _queue_) es una estructura de datos en la que los elementos se agregan por un extremo (llamado "final" o "cola") y se retiran por el otro extremo (llamado "frente" o "cabeza"). Es similar a una fila de personas esperando su turno: el primero en entrar es el primero en salir.

## Explicación general

Las colas funcionan bajo el principio **FIFO** (_First In, First Out_), es decir, el primer elemento que entra es el primero que sale. Se usan en muchos lugares de la vida real y en informática, como por ejemplo:

- Gestión de tareas de impresión
- Atención de clientes
- Transmisión de datos

---

## ¿Cómo funcionan las colas en FreeRTOS? (El sistema operativo que se usa en el ESP32)

En **FreeRTOS**, una cola es una estructura especial que permite que diferentes tareas (o partes del programa) se comuniquen entre sí de manera segura y ordenada. Imagina una fila de personas esperando para comprar entradas: la primera persona en llegar es la primera en ser atendida. Así funcionan las colas en FreeRTOS, siguiendo el principio FIFO.

### ¿Para qué sirven?

Las colas se usan para enviar datos de una tarea a otra. Por ejemplo, si una tarea recoge datos de un sensor y otra tarea los procesa, pueden usar una cola para pasar esa información de forma segura, sin que los datos se pierdan o se mezclen.

### ¿Cómo se usan?

1. **Creación:** Primero, se crea la cola indicando cuántos elementos puede guardar y de qué tamaño es cada elemento.
2. **Envío:** Una tarea puede enviar (poner) datos en la cola.
3. **Recepción:** Otra tarea puede recibir (sacar) datos de la cola.

FreeRTOS se encarga de que este proceso sea seguro, incluso si varias tareas intentan usar la cola al mismo tiempo. Si la cola está llena, la tarea que quiere enviar puede esperar hasta que haya espacio. Si la cola está vacía, la tarea que quiere recibir puede esperar hasta que llegue un dato.

### Ejemplo de la vida real

Es como una caja de sugerencias: las personas (tareas) pueden dejar mensajes (datos) en la caja (cola), y otra persona puede sacar los mensajes uno por uno para leerlos.

---

Para más información técnica y ejemplos, se puede consultar la [documentación oficial de FreeRTOS sobre colas](https://freertos.org/Documentation/02-Kernel/04-API-references/06-Queues/00-QueueManagement).

## Funciones básicas de gestión de colas en FreeRTOS

### 1. xQueueCreate

**¿Para qué sirve?**  
Crea una nueva cola. Se debe indicar cuántos elementos puede almacenar y de qué tamaño es cada elemento.

**¿Cómo se usa?**

```c
QueueHandle_t myQueue;
myQueue = xQueueCreate(5, sizeof(int));
```

- El primer parámetro (`5`) es la cantidad máxima de elementos que puede guardar la cola.
- El segundo parámetro (`sizeof(int)`) es el tamaño de cada elemento (en este caso, un entero).

---

### 2. xQueueSend

**¿Para qué sirve?**  
Envía (agrega) un dato a la cola. Si la cola está llena, puede esperar hasta que haya espacio.

**¿Cómo se usa?**

```c
int value = 10;
xQueueSend(myQueue, &value, portMAX_DELAY);
```

- El primer parámetro es la cola a la que se quiere enviar el dato.
- El segundo parámetro es la dirección del dato que se quiere enviar.
- El tercer parámetro es el tiempo máximo que la función esperará si la cola está llena (`portMAX_DELAY` significa esperar indefinidamente).

---

### 3. xQueueReceive

**¿Para qué sirve?**  
Recibe (saca) un dato de la cola. Si la cola está vacía, puede esperar hasta que llegue un dato.

**¿Cómo se usa?**

```c
int receivedValue;
xQueueReceive(myQueue, &receivedValue, portMAX_DELAY);
```

- El primer parámetro es la cola de la que se quiere recibir el dato.
- El segundo parámetro es la dirección donde se guardará el dato recibido.
- El tercer parámetro es el tiempo máximo que la función esperará si la cola está vacía.

---

### 4. xQueueSendToFront y xQueueSendToBack

**¿Para qué sirven?**  
Permiten enviar un dato al principio o al final de la cola, respectivamente.

**¿Cómo se usan?**

```c
xQueueSendToFront(myQueue, &value, 0); // Envía al principio de la cola
xQueueSendToBack(myQueue, &value, 0);  // Envía al final de la cola (igual que xQueueSend)
```

- El tercer parámetro es el tiempo de espera (0 significa no esperar).
