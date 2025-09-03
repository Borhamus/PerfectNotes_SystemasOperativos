27-08-2025 - Horacio Pendenti: Teoría.
Clase anterior: [[Clase 6]]

---

## Hoy vamos a ver:
*Como se implementan estas políticas.*

Prioridad. 

Implementación de prioridad es atreves de múltiples colas, que debemos armar para el estado de listo, ahora va a ser un estado, donde un proceso va a estar esperando.

![[WhatsApp Image 2025-08-27 at 18.14.21.jpeg]]
### Estáticas o Dinámicas.
La prioridad estática solo puede ser interrumpida de manera manual
Luego se mejoro, para que se pueda interrumpir de manera dinámica(?)

Establecer prioridades dinámicas: a lo largo de la ejecución de un proceso, teniendo en cuenta algunas variables que son, el tiempo que un proceso estuvo en un sistema, todo el tiempo en el que esta vivo. Tiempo de servicio que recibió ese servicio. Tiempo de espera/Tiempo total.

En la dinámica el sistema operativo recalcula la prioridad.

---
Exacto, vamos a desarrollar esto con claridad y detalle para que quede completo y comprensible, usando la terminología de **Sistemas Operativos** y conceptos de **Stallings**:

---

## **Prioridades de procesos: Estáticas vs Dinámicas**

En **sistemas operativos**, la **planificación de procesos** puede basarse en **prioridades**, lo que permite al **planificador (scheduler)** decidir qué proceso debe ejecutarse primero en la CPU. Las prioridades pueden ser **estáticas** o **dinámicas**, y cada enfoque tiene sus ventajas y desventajas.

---

### **1. Prioridad Estática**

- **Definición:**  
    La **prioridad estática** se asigna a un proceso **una sola vez**, generalmente al momento de su **creación**, y **no cambia durante la ejecución** del proceso.
    
- **Comportamiento:**
    
    - Un proceso con mayor prioridad **siempre** tiene preferencia sobre procesos con menor prioridad.
        
    - Solo se puede **interrumpir** o cambiar manualmente su prioridad mediante **intervención del sistema o del administrador**.
        
- **Ventajas:**
    
    - Sencillo de implementar.
        
    - Predecible: se conoce de antemano qué procesos recibirán CPU primero.
        
- **Desventajas:**
    
    - **Riesgo de inanición (starvation):** procesos de baja prioridad podrían **nunca ejecutarse** si siempre hay procesos de alta prioridad en el sistema.
        
    - No se adapta a cambios dinámicos en el comportamiento del proceso o del sistema.
        

---

### **2. Prioridad Dinámica**

- **Definición:**  
    La **prioridad dinámica** **cambia durante la ejecución del proceso**, dependiendo de **factores del sistema y del comportamiento del proceso**.
    
- **Variables que influyen en la prioridad dinámica:**
    
    1. **Tiempo de espera:** cuánto tiempo ha estado un proceso esperando en la cola de listos.
        
    2. **Tiempo total de vida del proceso:** cuánto tiempo lleva en el sistema desde su creación.
        
    3. **Tiempo de servicio recibido:** cuánto tiempo de CPU ha consumido el proceso hasta ahora.
        
    4. **Otros factores:** como la frecuencia de E/S, el tipo de proceso (interactivo vs por lotes), etc.
        
- **Comportamiento:**
    
    - El sistema operativo **recalcula periódicamente la prioridad** de cada proceso.
        
    - Esto permite que un proceso que ha estado esperando mucho tiempo **suba su prioridad**, evitando la **inanición**.
        
    - También puede **bajar la prioridad** de procesos que consumen mucha CPU, para favorecer la equidad.
        
- **Ventajas:**
    
    - Mejora la **justicia y equidad** entre procesos.
        
    - Evita que procesos de baja prioridad queden bloqueados indefinidamente.
        
    - Permite **adaptarse a cambios dinámicos** en la carga de trabajo del sistema.
        
- **Desventajas:**
    
    - Más complejo de implementar: requiere cálculos periódicos de prioridad y seguimiento de métricas de cada proceso.
        
    - Puede generar **variabilidad en la ejecución**, menos predecible que la prioridad estática.
        

---

### **Resumen comparativo**

|Característica|Prioridad Estática|Prioridad Dinámica|
|---|---|---|
|Cambios durante ejecución|No (solo manual)|Sí, recalculada por el sistema operativo|
|Prevención de inanición|No|Sí, aumenta prioridad de procesos que esperan mucho|
|Complejidad de implementación|Baja|Alta|
|Previsibilidad|Alta|Menor|
|Adaptabilidad|Baja|Alta|

---

### **Ejemplo práctico de prioridad dinámica:**

- Un proceso A de baja prioridad lleva **20 segundos** esperando en la cola de listos.
    
- Un proceso B de alta prioridad llega al sistema y consume CPU.
    
- El sistema recalcula prioridades dinámicas: A incrementa su prioridad por el **tiempo de espera**, B baja su prioridad tras consumir CPU demasiado tiempo.
    
- Esto asegura que eventualmente A también reciba CPU, evitando inanición.
    

---

### Ejemplo
El momento al que llega a la lista de listos: Arrival Time

![[Pasted image 20250827182604.png]]

Service time, podría verse como ráfagas. como un trabajo batch lo vamos a ver, tiempo de uso de cpu requerido. tiempo de 1 ciclo de cpu.

necesita 3 unidades de tiempo para terminar.


### Problemas que nacen con las políticas de planificación:

* Cuando un proceso espera mucho tiempo, se le llama "starvation".
* 


---

### First Come First Served (FCFS)
Prioridad pura. 

**Función de selección:** 
	El proceso que ha estado más tiempo esperando en la cola de procesos listos.

**Modo de decisión:** 
	Non-preemptive (un proceso se ejecuta hasta que termina o se bloquea a la espera de un servicio (I/O u otro).

![[Pasted image 20250827183009.png]]

---

### Concept:

 
 ![[Pasted image 20250827183923.png]]

Para que sea non-preemptive

La versión preemptive de FCFS es : (poniendo un timer) 
### Round Robin (RR)
![[Pasted image 20250827184520.png]]

**Es una solución mas justa que la de FCFS**

* **Función de selección:** La misma que FCFS
* **Modo de decisión:** Preemptive.
	* A un proceso se le permite ejecutarse hasta que se bloquea o expira su período de tiempo (quantum).
	* Cuando el quantum se agota se produce una  interrupción de reloj y el proceso es ubicado nuevamente en la cola de listos.

### Concept:
![[Pasted image 20250827184839.png]]
### Tamaño del Quantum (Q) en RR

* Debe ser considerablemente más grande que el tiempo necesario para tratar la interrupción del reloj y elegir un nuevo proceso (switch time).
* Debe ser más grande que la interacción típica, pero no tanto que termine penalizando los procesos acotados por I/O.

> **"Menor que un tiempo medio de ráfaga de cpu, es el de un cambio de proceso."**


lo que queremos saber es cuanto Quantum darle a un proceso.

> NOTA: si mi Quantum es muy grande, te queda un FCFS.

![[Pasted image 20250827185749.png]]
Podes tener un RR con un quantum estático.

que pasa cuando tenés un sistema con RR que usas un Q estático para todos los procesos iguales, o un q estático para cada proceso,  a cada proceso le doy un q distinto pero fijo.

	Quantum fijo, estático, igual para todos.
	Quantum dinámico igual para todos los procesos.
	Quantum dinámico para cada proceso.


### Crítica a RR
Siguen favoreciendo a los procesos acotados por el cpu.

* **Solución: RR virtual.**

![[Pasted image 20250827191505.png]]
Mas formal:
![[Pasted image 20250827191650.png]]

Sugerencia para arreglar este Problema. 
Manteniendo la eficiencia en lo posible.


---

### Shortest Process Next (SPN o SJF)

![[Pasted image 20250827192536.png]]
* **Función de selección:** El proceso con la ráfaga esperada de CPU más corta.
* **Modo de decisión:** Non-preemptive.
* Los procesos acotados por I/O serán ejecutados primero.
* Necesitamos estimar el tiempo de procesamiento requerido (CPU burst time) para cada proceso. Esto puede hacerse en función del comportamiento anterior.

Tengo que ser predictivo, y tiene su costo en tiempo.

![[Pasted image 20250827193227.png]]

![[Pasted image 20250827193917.png]]

Explicación del Algoritmo de:
[[Algoritmo de Envejecimiento]]


$$
2 + 8 + 3 + 5 
$$

$$
\left(2 * \frac{1}{8}\right) + \left(8 * \frac{1}{8}\right) + \left(3 * \frac{1}{4}\right) + \left(5 * \frac{1}{2}\right) = 4.5\\
$$

---

