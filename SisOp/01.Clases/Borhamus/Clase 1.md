# Sistemas Operativos
## Lunes 11/08/2025 - Con Horacio: Teoría


* El SO es un administrador de recursos

* El SO es un programa de control


---
Cuando un programa de 3 bloques termina, el registro de próxima instrucción queda cargado en la dirección 3.

Registro de próxima instrucción.

Sincronización por condición.

**[[Buffer]]**  
En sistemas operativos, un **buffer** es una región de memoria temporal utilizada para almacenar datos mientras se trasladan entre dos dispositivos o entre un proceso y un dispositivo. Su función principal es **amortiguar** las diferencias de velocidad o tamaño de transferencia entre el productor de datos (por ejemplo, la CPU o un programa) y el consumidor de datos (por ejemplo, un dispositivo de E/S).

Los controladores de dispositivos suelen implementar sus propios buffers internos para optimizar el flujo de datos y minimizar el tiempo de espera de la CPU. Cuando un programa solicita una operación de entrada/salida, es posible que el dispositivo no pueda recibir o entregar toda la cantidad de datos de una sola vez. El sistema operativo utiliza buffers para:

1. **Compensar diferencias de velocidad** entre dispositivos rápidos (como la memoria principal o la CPU) y dispositivos lentos (como discos duros, impresoras, o redes).
    
2. **Reducir la latencia** percibida por el programa, permitiendo que la CPU continúe ejecutando otras tareas mientras se completa la E/S.
    
3. **Agrupar o fragmentar transferencias** de datos para que se adapten al tamaño de bloque o al protocolo del dispositivo.
    
4. **Sincronizar** procesos productores y consumidores, evitando pérdida de datos en situaciones de desbordamiento o subalimentación.
    

En términos técnicos, el buffer actúa como **memoria intermedia** que permite desacoplar las tasas de producción y consumo, evitando cuellos de botella y mejorando la eficiencia global del sistema.

---

Un SO es un programa [[Interrupt Driven]]:

**Definición más formal**  
Según **Silberschatz, Galvin & Gagne**, un **Sistema Operativo** es un programa que actúa como intermediario entre el usuario y el hardware, y que coordina el uso de los recursos del sistema. Una de sus características clave es que está diseñado como un **sistema impulsado por interrupciones** (_interrupt-driven system_).

Esto significa que el SO normalmente **no ejecuta continuamente un bucle de espera activa** revisando si un evento ocurrió (lo que sería ineficiente). En su lugar:

1. **Estado inactivo o ejecución de usuario**  
    El SO permite que la CPU ejecute programas de usuario o permanezca en espera mientras no haya eventos que requieran atención.
    
2. **Eventos externos o internos generan interrupciones**
    
    - **Hardware interrupts**: señales del hardware (ej. un dispositivo de E/S terminó su tarea, llegada de un paquete de red, fin de temporizador).
        
    - **Software interrupts** (o _traps_): invocaciones de sistema hechas por programas (ej. `read()`, `write()`, manejo de errores).
        
3. **Cambio de contexto y atención al evento**  
    Cuando ocurre una interrupción, el flujo normal de ejecución se detiene, la CPU guarda su estado (_contexto_) y transfiere el control a la rutina de servicio de interrupción (ISR) del SO.
    
4. **Retorno a la tarea anterior**  
    Una vez atendida la interrupción, el SO restaura el contexto y continúa la ejecución del proceso que estaba corriendo o despacha otro según la planificación.
    

---

💡 **Por qué es importante que sea interrupt-driven**

- Permite **multitarea eficiente**: el SO no desperdicia ciclos de CPU revisando constantemente el estado de los dispositivos.
    
- Favorece la **respuesta rápida** a eventos externos.
    
- Es esencial para **sincronizar** hardware y software.
    
- Minimiza la **latencia** en operaciones de entrada/salida.

---

## **[[DMA (Direct Memory Access)]]**

**Definición**  
Según _Silberschatz, Galvin & Gagne_ y _Tanenbaum_, el **DMA** es un mecanismo de hardware (un módulo o controlador) que permite que ciertos dispositivos de E/S transfieran datos directamente hacia o desde la memoria principal **sin la intervención continua de la CPU**.

El **módulo DMA** actúa como un “miniprocesador especializado” que:

1. **Recibe de la CPU** la información necesaria para la transferencia:
    
    - Dirección de origen y destino en memoria.
        
    - Cantidad de datos a transferir.
        
    - Dirección o puerto del dispositivo.
        
    - Dirección de control (lectura o escritura).
        
2. **Se comunica directamente con el controlador del dispositivo**  
    Una vez configurado, el DMA maneja la transferencia bloque a bloque o palabra a palabra, sincronizándose con el dispositivo de E/S.
    
3. **Libera a la CPU**  
    La CPU no necesita copiar cada byte/palabra; puede dedicarse a ejecutar otros procesos mientras el DMA se encarga de mover los datos.
    
4. **Interrumpe a la CPU solo al finalizar**  
    Cuando la transferencia termina (o si hay un error), el DMA envía una **interrupción** para informar al sistema operativo que la operación ha concluido.
    

---

### 🔍 **¿Qué problemas resuelve?**

- **Reduce carga de CPU**: sin DMA, la CPU tendría que mover datos uno por uno mediante instrucciones de E/S.
    
- **Mejora el rendimiento** en transferencias masivas (discos, redes, audio, video).
    
- **Permite paralelismo**: CPU ejecuta tareas mientras DMA mueve datos.
    

---

### 📊 **Flujo típico de operación DMA**

1. CPU configura el módulo DMA con parámetros de transferencia.
    
2. DMA solicita el control del bus (arbitraje con la CPU).
    
3. DMA transfiere datos entre memoria y el dispositivo.
    
4. DMA libera el bus.
    
5. DMA genera una interrupción a la CPU para informar finalización.
    

---

💡 **Importante**:  
El **DMA** no es un _trap_ (trampa por software), porque no es una interrupción generada por código, sino un módulo de hardware que eventualmente **genera una interrupción** al terminar, pero su operación es independiente de la CPU.

---
que es un bus para concurrencia?

[[Bus en Concurrencia]]
## 📚 **Definición**

Un **bus** es un conjunto de líneas de comunicación físicas y protocolos asociados que permiten transferir datos, direcciones y señales de control entre los diferentes componentes de un sistema de cómputo.

Cuando se usa para concurrencia, el concepto clave es que:

- El bus **no es paralelo en uso**: aunque varios dispositivos pueden necesitarlo simultáneamente, solo **uno** puede tener control del bus en un instante dado.
    
- Esto introduce **competencia** (contention) y la necesidad de **arbitraje** para decidir quién lo usa y cuándo.
    

---

## 🔍 **Concurrencia en el bus**

En un sistema real, pueden coexistir varios “maestros” del bus:

- CPU (cuando accede a memoria o dispositivos)
    
- Controladores DMA (cuando transfieren datos)
    
- Otros coprocesadores o controladores inteligentes
    

Todos ellos **pueden solicitar acceso al bus de manera concurrente**. El problema de concurrencia es que:

- Si dos o más lo solicitan a la vez, hay que decidir **cuál tiene prioridad**.
    
- Si no se gestiona bien, puede haber **esperas largas** o **injusticia** (starvation).
    

---

## ⚙ **Mecanismos para manejar concurrencia en el bus**

1. **Arbitraje centralizado**  
    Un controlador de bus decide a quién se le concede acceso según prioridades predefinidas.
    
2. **Arbitraje distribuido**  
    Cada dispositivo participa en un protocolo de decisión para resolver conflictos sin un árbitro único.
    
3. **Priorización y fairness**
    
    - _Prioridad fija_: ciertos dispositivos siempre ganan (rápido pero puede causar starvation).
        
    - _Rotación (round-robin)_: turnos equitativos.
        
    - _Prioridad dinámica_: prioridades cambian según uso o antigüedad en la cola.
        

---

## 📌 En relación con Sistemas Operativos

- El SO debe **coordinar el acceso al bus** indirectamente, asegurando que las operaciones de E/S, memoria y DMA no generen cuellos de botella.
    
- El bus es un ejemplo de **recurso crítico**: no puede ser usado por más de un maestro a la vez, lo que lo convierte en un caso claro para aplicar **principios de sincronización y concurrencia** que también se usan en procesos e hilos.


---

[[Jerarquía de Almacenamiento]]:

## 📚 **Jerarquía de almacenamiento**

La **jerarquía de almacenamiento** es la organización de los distintos tipos de memoria y dispositivos de almacenamiento de un sistema computacional, ordenados según:

1. **Velocidad de acceso** (rápida en la cima, lenta en la base).
    
2. **Costo por bit** (caro arriba, barato abajo).
    
3. **Capacidad de almacenamiento** (baja arriba, alta abajo).
    

---

### 📊 **Estructura típica** (de arriba hacia abajo)

| Nivel                                  | Tipo de memoria                   | Velocidad               | Capacidad          | Costo/bit | Volatilidad |
| -------------------------------------- | --------------------------------- | ----------------------- | ------------------ | --------- | ----------- |
| **Registro de CPU**                    | Dentro del procesador             | Nanosegundos            | Bytes              | Muy alto  | Volátil     |
| **Cache L1 / L2 / L3**                 | En o cerca de la CPU              | Nanosegundos            | KB–MB              | Alto      | Volátil     |
| **Memoria principal (RAM)**            | DRAM                              | Decenas de ns           | GB                 | Medio     | Volátil     |
| **Almacenamiento secundario**          | SSD / HDD                         | Micro–milisegundos      | Cientos de GB – TB | Bajo      | No volátil  |
| **Almacenamiento terciario / offline** | Cintas magnéticas, discos ópticos | Milisegundos – segundos | TB–PB              | Muy bajo  | No volátil  |

---

### 🔍 **Características clave**

- **Principio de localidad**: La jerarquía aprovecha que los programas tienden a acceder repetidamente a un conjunto pequeño de direcciones en un corto período de tiempo (_localidad temporal_) y a direcciones cercanas (_localidad espacial_).
    
- **Transferencia por bloques**: Los datos suelen moverse en bloques desde niveles más lentos hacia niveles más rápidos para anticipar accesos futuros.
    
- **Intercambio automático**: Las capas superiores y medias suelen manejarse mediante mecanismos de _cache_ y _swap_ controlados por hardware y/o el SO.
    

---

### 📌 En el contexto de un SO

El Sistema Operativo:

- Gestiona la **memoria principal** y la asignación de espacio en dispositivos de almacenamiento.
    
- Implementa mecanismos como **memoria virtual** para extender la capacidad aparente de la RAM usando almacenamiento secundario.
    
- Optimiza el uso de caches de disco y búferes para reducir accesos a dispositivos lentos.
    




[[Clase 2]]