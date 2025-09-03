25-08-2025 Horacio Pendenti - Teoría
Clase Anterior: [[Clase 5]]

que es un proceso, como se crea, par que sirve, que tiene dentro, los estados que tiene, por los que pasa, las transiciones.

ahora: sobre todo con las transiciones. 

como el so admin los proc, en función de lanzarlos a ejecutar... administración de procesos. no solo gestión de procesos como entidad. sino la admisión, ejecución y terminación.

Planificación. se llama. scheduling

Concept:
Nos concentraremos en el problema de administrar (planificar) el uso de un
procesador único entre todos los procesos existentes en el sistema.

Para hacer una correcta planificación de administración, se deberá tener esto en consideración:
* Maximizar el tiempo de uso del procesador (eficiencia)
* Maximizar el throughput (número de procesos completados por unidad de tiempo)
* Minimizar el tiempo de respuesta (tiempo transcurrido entre el envío de un
requerimiento al sistema y el momento en el que comienza a recibirse la respuesta)

---
### **Planificación de Procesos (Scheduling)**

La **planificación de procesos**, conocida en inglés como **scheduling**, es una función fundamental del sistema operativo que se ocupa de **administrar el uso de la CPU** entre todos los procesos que existen en el sistema. Su objetivo es **optimizar el rendimiento del sistema** y garantizar que los procesos reciban los recursos que necesitan de manera justa y eficiente.

En un **procesador único**, solo un proceso puede ejecutarse a la vez, por lo que el sistema operativo debe decidir **cuál proceso ejecutar, en qué momento y por cuánto tiempo**. Este es el núcleo de la planificación de CPU.

---

### **Concepto Clave**

El **scheduling** se centra en:

> “Administrar de manera eficiente y equitativa el uso de la CPU para maximizar el rendimiento del sistema y minimizar los tiempos de espera de los procesos.”

---

### **Objetivos Principales de la Planificación**

Para realizar una **planificación efectiva**, el sistema operativo debe considerar varios objetivos:

1. **Maximizar el uso de la CPU (eficiencia)**
    
    - La CPU debería estar ocupada la mayor parte del tiempo.
        
    - Evitar que la CPU quede ociosa mientras hay procesos listos para ejecutarse.
        
    - Esto se logra utilizando algoritmos de planificación que minimicen el tiempo muerto.
        
2. **Maximizar el throughput (rendimiento del sistema)**
    
    - **Throughput**: número de procesos completados por unidad de tiempo.
        
    - A mayor throughput, mayor productividad del sistema.
        
    - La planificación debe organizar la ejecución para completar procesos de manera eficiente, priorizando los más cortos o críticos según el algoritmo.
        
3. **Minimizar el tiempo de respuesta**
    
    - **Tiempo de respuesta**: tiempo transcurrido entre que un proceso solicita un recurso o servicio y el momento en que empieza a recibir la atención.
        
    - Es especialmente crítico en sistemas interactivos (como servidores, interfaces de usuario, videojuegos, etc.), donde los usuarios esperan respuestas rápidas.
        
    - Algoritmos como **Round-Robin** ayudan a mantener tiempos de respuesta bajos para todos los procesos.
        

---

### **Factores que Influyen en la Planificación**

1. **Naturaleza de los procesos**
    
    - Procesos **CPU-bound**: necesitan mucho tiempo de CPU.
        
    - Procesos **I/O-bound**: pasan más tiempo esperando E/S que usando la CPU.
        
2. **Estado del sistema**
    
    - Número de procesos listos, bloqueados o en espera de recursos.
        
3. **Políticas de planificación**
    
    - Algoritmos que deciden **quién se ejecuta primero**, basados en criterios como prioridad, tiempo de ejecución estimado o rotación equitativa.
        

---

### **Resumen**

El scheduling es esencial para garantizar que el **procesador sea utilizado eficientemente**, que el **throughput del sistema sea alto**, y que **los procesos interactivos obtengan respuestas rápidas**. En sistemas modernos, la planificación no solo afecta la CPU, sino también la **coordinación con E/S, memoria y otros recursos**, haciendo del **scheduling** un componente central para el **rendimiento global del sistema**.

---

### Tiempo de respuesta:
![[tr.png]]

### Objetivos que persigue una planificación de procesos:
Tratar de que todos los procesos que están vivos, tengan un tiempo de respuesta apropiado, a todos lo que son trabajos interactivos, debe tener una respuesta apropiada.


---

### Se recurre a tres tipos de planificador:

**Planificador de largo plazo:** determina que procesos se admiten en el sistema.
- Es el que admite o no los nuevos procesos en el sistema.
- Controla el grado de Multiprogramación, (**La Multiprogramación es:** la cantidad de programas en el sistema con posibilidad de ser ejecutados).

**Planificador de mediano plazo:** determina que procesos descargar y cargar en la memoria.
* Encargado de hacer los Swap-Out/ Swap-In.
* En otras palabras, el encargado de tomar uno o varios procesos de la memoria principal a la secundaria o viceversa.

**Planificador de corto plazo:** elige, entre los procesos listos, a cual le asignará la CPU.
* Busco en la lista de procesos cuales estan listo y los asigno al procesador.
* de listo a corriendo, de corriendo a bloqueado, y de bloqueado a listo.
* La terminación del proceso también es responsabilidad del planificador de corto plazo.


![[Clasif de la act de Planificacion.png]]

>	lean sobre las transiciones, cada uno de los estados.
	  como un proceso llega a un estado, que hace, que necesita para avanzar.

**Batch:** Poca o nula interacción humana. 

El SO, mide la eficiencia de las ejecuciones de los procesos, y debería tratar de admitir mas procesos si no esta siendo usado el cpu. en cierto modo, el planificador de largo plazo, controla el grado de multiprogramación.

Este sistema garantiza que no haya huecos, siempre esta siendo usado el cpu. 
El sistema operativo se encarga de esto con estos 3 planificadores.
Mejorando la eficiencia.

Una de las cosas que puede pasar, es que cada proceso, puede llegar a tener una tiempo mas pequeña del cpu.
**Ráfagas de tiempo.**
Equilibrio entre pocos y muchos procesos. 
Eficiencia vs grado de multiprogramación.
Mientras mayor grado de multiprogramación, tendré mas eficiencia, hasta que supere cierto punto y genera perdida de eficiencia. 

Si tengo muchos cambios de procesos, pierdo el trabajo útil.
**Trabajo Útil:** Importante para medir la eficiencia del procesador.
![[Acotado por I-O.png]]

---

### Planificación de Largo Plazo (LTS)

**¿Cuándo debe ser invocado el LTS?**
* Cada vez que un proceso termina.
* Cada vez que la eficiencia de la CPU cae debajo de un límite.
* Cada vez que un trabajo es remitido para su procesamiento.

Si hay más de uno: **¿Qué proceso debe elegir el LTS?**
* Contexto (trabajos batch o interactivos).
* Prioridad externa.
* Tiempo esperado de ejecución.
* Disponibilidad de recursos de I/O

---
### Planificación de Mediano Plazo (MTS)

* Toma las decisiones de swapping basadas en la necesidad de manejar multiprogramación.
* Está muy relacionado con el problema de administración de memoria.

---

### Planificación de Corto Plazo (STS)

ver como funciona el despachador, basado en políticas.

* Determina que proceso se ejecutará a continuación (también se denomina planificación de la CPU).
* El planificador de corto plazo es también llamado despachador (dispatcher).
* Es invocado cada vez que un evento puede provocar la elección de otro proceso para su ejecución:
	* Interrupciones de reloj (timer).
	* Interrupciones de I/O.
	* Interrupciones de software (llamadas al SO y traps).
	* un semáforo, un mensaje, una señal que hizo un proceso que por ejemplo hace que se puede ejecutar otro.

### Criterios para el STS
#### Orientados al usuario
* **Tiempo de retorno (turnaround time):** Se utiliza en sistemas batch. Mide el tiempo transcurrido entre el envío de un proceso y su terminación.
* **Tiempo de retorno normalizado:** tiempo de retorno / tiempo de servicio.
* **Tiempo de respuesta (response time):** Se utiliza en sistemas interactivos. Mide el tiempo transcurrido entre el envío de un requerimiento por el usuario y el comienzo de la recepción de la respuesta.
![[TR N.png]]

81/84= TRN


#### Orientados al sistema
* Utilización de la CPU (eficiencia).
* Justicia. Fairness, que tan justo es el tipo de procesos que se ejecutan. Importancia en que no haya prioridad de recursos, tiene que **"ser justo para todos"**.
* Throughput (número de procesos completados por unidad de tiempo).


![[Criterios para el STS.png]]

---

## CPU scheduling

* **Cuando voy a tomar la decisión de tomar el cpu** y el **cómo**.

### Cuando: se toma la decisión de asignar la CPU (decision mode) 

* **Non-preemptive (no apropiativa):** una vez que un proceso se está ejecutando continúa haciéndolo hasta que termina o se bloquea (por ejemplo por I/O).

* **Preemptive (apropiativa):** El proceso que se está ejecutando puede ser interrumpido y movido al estado Listo por el Sistema Operativo. La decisión puede tomarse cuando arriba un nuevo proceso, cuando se produce una interrupción que modifica el estado de algún proceso (bloqueado a listo), o por tiempo.

>*(cuando el so te saca el proceso en ejecución, es apropiativo. cuando no puede, es non-preemptive)*

>Las políticas apropiativas permiten brindar un mejor servicio (ya que un proceso no puede monopolizar el uso de la CPU), pero aumentan el overhead (uso de la CPU "y otros recursos" para tareas del Sistema Operativo)

Puede generar starvation si un proceso ocupa el cpu por mucho tiempo, siendo non-preemptive.

---

#### Cómo se elige un proceso para asignarle la CPU (selection function)

## Prioridades


---
	![[Niveles de Planificacion.jpeg]]


#### Tiempo de Eficiencia (μ)

$$
\mu = \frac{T}{t + s}
$$

- **t** = Tiempo de Servicio  
- **s** = Tiempo de Sobrecarga



Siguiente Clase: [[Clase 7]]
