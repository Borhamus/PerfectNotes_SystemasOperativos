20-08-2025 Teoría Horacio.
Clase Anterior: [[Clase 4]]

![[Modelo de 7 estados.png]]
Es importante saber que hace cada estado, como llego hasta ahí, y que esta esperando para salir de ahí. 
Tres preguntas clave:
* Que hace un proceso en esos estados.
* Como llego ahí. 
* Que esta esperando para salir de ahí.
---
En el modelo de 7 estados, cada estado representa una fase del ciclo de vida de un proceso en el sistema operativo. A continuación te ayudo a completar las respuestas clave:

1. **Qué hace un proceso en esos estados**:
    
    - **Nuevo**: El proceso se está creando, reservando recursos y estructuras de datos.
        
    - **Listo**: El proceso está esperando ser ejecutado, pero no está en ejecución todavía.
        
    - **Ejecutando**: El proceso está utilizando la CPU y ejecutando sus instrucciones.
        
    - **Bloqueado**: El proceso está esperando que ocurra un evento, como una entrada/salida.
        
    - **Listo suspendido**: El proceso está en espera, pero no tiene acceso a la CPU debido a la política de planificación.
        
    - **Bloqueado suspendido**: El proceso está esperando algún evento pero se encuentra fuera de la memoria principal, en disco.
        
    - **Terminado**: El proceso ha finalizado su ejecución y los recursos asignados se están liberando.
        
2. **Cómo llegó ahí**:
    
    - Un proceso transita entre estos estados dependiendo de las acciones del sistema operativo y los recursos disponibles. Por ejemplo:
        
        - Un proceso puede pasar de "Listo" a "Ejecutando" cuando el planificador de CPU lo elige para su ejecución.
            
        - De "Ejecutando" a "Bloqueado" si espera una operación de E/S.
            
        - De "Bloqueado" a "Listo" cuando la operación de E/S se completa.
            
        - De "Ejecutando" a "Terminado" cuando ha finalizado su tarea.
            
3. **Qué está esperando para salir de ahí**:
    
    - En el estado de **Listo**, el proceso espera que el planificador de CPU le asigne tiempo de ejecución.
        
    - En el estado **Ejecutando**, el proceso está esperando completar sus instrucciones antes de ser suspendido o finalizado.
        
    - En el estado **Bloqueado**, el proceso espera que se complete la operación de E/S o algún otro evento, como la liberación de un recurso.
        
    - En los estados suspendidos, el proceso espera ser cargado de nuevo en la memoria principal cuando sea necesario.
        

Estas preguntas son clave para entender cómo un sistema operativo gestiona la ejecución de procesos.

---

● Cambio de modo

	● El proceso es detenido (por ejemplo para procesar una interrupción), pero  inmediatamente después retoma la ejecución
	
	● Sólo la información necesaria para retomar la ejecución debe ser salvada (por ejemplo PC y registros de la UCP)

● Cambio de proceso

	● El proceso es detenido y otro proceso toma la CPU
	
	● Además de la información por cambio de modo se necesita salvar otra información (contexto, data)
	
	● Se debe actualizar el estado del proceso


Planificador del sistema operativo

![[Diseño de proceso.png]]
#### Generalmente: 
	Un cambio de proceso lleva mas tiempo.
	Un cambio de modo lleva menos tiempo.

---

En un sistema operativo, **el cambio de modo** y **el cambio de proceso** son dos conceptos clave que están íntimamente relacionados con la gestión de procesos y la seguridad del sistema. A continuación, te explico ambos con más detalle, basándome en los libros de **Stallings** y otros referentes como **Silberschatz et al.**:

### 1. **Cambio de Modo (Mode Switching)**

El **cambio de modo** se refiere al proceso de cambiar entre diferentes niveles de privilegio en un sistema operativo. Estos niveles son típicamente:

- **Modo Usuario**: El proceso está ejecutándose en un contexto de privilegios limitados, donde no puede acceder directamente a recursos críticos del sistema (como la memoria protegida, el hardware, o el espacio de otros procesos).
    
- **Modo Núcleo (Kernel)**: El proceso tiene acceso completo a todo el hardware y recursos del sistema operativo. Este modo es utilizado por el sistema operativo para ejecutar operaciones sensibles como la gestión de memoria, la programación de procesos, el manejo de interrupciones, etc.
    

#### **¿Cómo se realiza un cambio de modo?**

- **De usuario a núcleo**: Se produce generalmente cuando ocurre una **interrupción** o una **excepción** (por ejemplo, un fallo de página o un sistema de llamadas). Cuando un proceso en modo usuario necesita ejecutar una operación privilegiada, como acceder a la memoria o realizar una E/S, se realiza una **llamada al sistema** (system call). Esta llamada provoca una interrupción, que cambia el modo de usuario a modo núcleo.
    
- **De núcleo a usuario**: El cambio de modo de vuelta se realiza cuando el proceso del sistema operativo termina su ejecución en modo núcleo, y el control vuelve al proceso de usuario que estaba esperando.
    

#### **Importancia del cambio de modo:**

El cambio de modo es crucial para:

- **Seguridad**: Protege el sistema y la memoria del usuario al asegurar que los procesos de usuario no puedan ejecutar instrucciones privilegiadas.
    
- **Aislamiento de procesos**: Evita que los procesos de usuario interfieran entre sí o con el núcleo, protegiendo los recursos del sistema.
    

### 2. **Cambio de Proceso (Context Switching)**

El **cambio de proceso** se refiere al mecanismo por el cual el sistema operativo detiene la ejecución de un proceso y guarda su contexto para luego reanudar otro proceso. Este proceso se llama **context switch** y es fundamental para la multitarea en los sistemas operativos.

#### **¿Cómo se realiza un cambio de proceso?**

Cuando un proceso es interrumpido (ya sea por una interrupción de hardware, una interrupción de software, o por una política de planificación de procesos), el sistema operativo realiza un cambio de proceso siguiendo estos pasos:

1. **Guardar el contexto del proceso actual**: El sistema operativo guarda el estado del proceso que se va a suspender (esto incluye el valor de los registros de la CPU, el contador de programa, y cualquier otro dato necesario para que el proceso pueda continuar desde el mismo punto más tarde).
    
2. **Seleccionar el siguiente proceso para ejecutar**: El planificador de procesos (scheduler) elige otro proceso que esté listo para ejecutarse (en función de políticas como Round-Robin, prioridad, etc.).
    
3. **Restaurar el contexto del nuevo proceso**: El sistema operativo restaura el estado del proceso que va a ejecutarse (incluyendo el contador de programa y los registros).
    
4. **Reanudar la ejecución del nuevo proceso**: Finalmente, el nuevo proceso comienza o continúa su ejecución desde el punto en que fue interrumpido.
    

#### **¿Por qué es importante el cambio de proceso?**

El cambio de proceso es esencial para:

- **Multitarea**: Permite que varios procesos se ejecuten de forma concurrente en el sistema, maximizando el uso de la CPU.
    
- **Uso eficiente de la CPU**: Asegura que la CPU siempre esté en uso, cambiando entre procesos cuando uno está esperando o bloqueado.
    
- **Aislamiento de procesos**: Cada proceso mantiene su propio contexto (variables, pila, registros), evitando interferencias entre procesos.
    

#### **Costos del Cambio de Proceso:**

Aunque el cambio de proceso es fundamental para la multitarea, también tiene ciertos costos:

- **Tiempo de CPU**: El cambio de contexto en sí mismo consume tiempo de la CPU, ya que implica guardar y restaurar estados, lo que se denomina **overhead de contexto**.
    
- **Accesos a memoria**: Puede implicar accesos a la memoria más costosos, especialmente si los procesos no están en la caché y requieren acceso a la memoria principal o al disco.
    

#### **Relación entre cambio de modo y cambio de proceso:**

- En un **cambio de modo**, el procesador cambia entre los modos de ejecución (usuario a núcleo o viceversa) para acceder a recursos privilegiados.
    
- En un **cambio de proceso**, el sistema operativo cambia la ejecución de un proceso por otro, lo que implica guardar y restaurar el contexto del proceso.
    

### Conclusión

Ambos, el **cambio de modo** y el **cambio de proceso**, son fundamentales para la gestión eficiente y segura de los recursos del sistema operativo. Mientras que el cambio de modo es esencial para la separación de niveles de privilegio (usuario/núcleo), el cambio de proceso es crucial para la multitarea y el uso eficiente de la CPU. Estos mecanismos son claves en la ejecución y el aislamiento de procesos, y juegan un papel central en el diseño de sistemas operativos modernos.

Este enfoque se puede encontrar en libros como **Stallings (Operating Systems: Internals and Design Principles)** y **Silberschatz et al. (Operating System Concepts)**, que abordan en profundidad estos mecanismos y su implementación en diferentes tipos de sistemas operativos.

---

#### Creación de proceso

Asignar un identificador único

Asignar espacio para la imagen del proceso

Inicializar el PCB

Vincular apropiadamente

Establecer o actualizar estructuras de datos

---
La **creación de un proceso** es un paso fundamental en la gestión de procesos de un sistema operativo. A continuación, te explico cada uno de los pasos mencionados, basándome en los libros de Stallings y Silberschatz:

### 1. **Asignar un Identificador Único (PID - Process Identifier)**

Cada proceso en el sistema operativo necesita un **identificador único** para poder ser referenciado y gestionado. Este identificador se denomina **PID** (Process Identifier). Es importante porque:

- Permite al sistema operativo hacer un seguimiento del proceso y gestionarlo de manera eficiente.
    
- Cada proceso en ejecución debe tener un PID único dentro de un espacio determinado (generalmente por el sistema operativo).
    

El PID se asigna generalmente cuando el proceso es creado, y se utiliza en las estructuras de datos del sistema operativo para manejar la planificación, las señales, y la gestión de recursos.

### 2. **Asignar Espacio para la Imagen del Proceso**

Cada proceso tiene una **imagen en memoria** que incluye todo el contexto necesario para su ejecución, como:

- **Código ejecutable**: Instrucciones que el procesador ejecutará.
    
- **Datos estáticos**: Variables globales y estáticas del proceso.
    
- **Heap y Stack**: Espacios para almacenamiento dinámico (heap) y de ejecución (stack) para el manejo de funciones y llamadas.
    

El **espacio de la imagen del proceso** es reservado por el sistema operativo para alojar estos componentes. En sistemas modernos, este espacio es aislado de otros procesos mediante mecanismos de **protección de memoria**, garantizando que los procesos no se sobrescriban entre sí.

### 3. **Inicializar el PCB (Process Control Block)**

El **PCB** es una estructura de datos crucial en el sistema operativo que almacena toda la información relacionada con un proceso, como:

- **PID**: Identificador único del proceso.
    
- **Estado del proceso**: Puede ser "listo", "ejecutando", "bloqueado", etc.
    
- **Registros de CPU**: El contador de programa, los registros de estado, y los punteros de pila.
    
- **Memoria asignada**: Direcciones de memoria del código, datos, heap y stack.
    
- **Información de planificación**: Prioridad, tiempo de ejecución, etc.
    

El **PCB** es esencial para poder gestionar la ejecución del proceso y realizar un **context switch** (cambio de contexto) eficiente cuando sea necesario.

### 4. **Vincular Apropiadamente**

La **vinculación** es el proceso mediante el cual el sistema operativo establece las conexiones necesarias entre el proceso recién creado y las estructuras internas del sistema operativo. Esto incluye:

- **Asignar el proceso a una cola** de procesos listos o en espera, dependiendo de su estado inicial.
    
- **Establecer relaciones de padre-hijo** en el caso de procesos creados por otros procesos (a través de llamadas como `fork()` en sistemas UNIX).
    
- **Vincular el proceso con recursos** como la memoria, archivos abiertos, dispositivos de E/S, etc.
    

Esto garantiza que el proceso esté correctamente registrado en las estructuras de gestión del sistema operativo y listo para su ejecución.

### 5. **Establecer o Actualizar Estructuras de Datos**

Finalmente, el sistema operativo debe **actualizar o establecer varias estructuras de datos** para gestionar el proceso. Estas estructuras incluyen:

- **Tablas de procesos**: Mantienen un registro de todos los procesos activos en el sistema.
    
- **Tablas de archivos abiertos**: En caso de que el proceso haya abierto archivos, el sistema operativo gestiona sus descriptores de archivo.
    
- **Listas de recursos**: Si el proceso requiere recursos (como memoria, CPU, dispositivos de entrada/salida), estas listas son actualizadas para reflejar el estado del recurso.
    

Una vez estas estructuras estén correctamente establecidas, el proceso podrá ser **planificado** para su ejecución en la CPU o pasar a un estado de espera según corresponda.

### Conclusión

La **creación de un proceso** implica la asignación de un **identificador único**, la **reserva de espacio en memoria** para su ejecución, la **inicialización del PCB**, la **vinculación con otras estructuras del sistema** y la **actualización de las estructuras de datos internas del sistema operativo**. Estos pasos permiten que el sistema operativo pueda gestionar de manera efectiva los procesos en ejecución, garantizando un funcionamiento seguro y eficiente del sistema.

Esta explicación se encuentra en el contexto de los libros **"Operating Systems: Internals and Design Principles"** de **William Stallings** y **"Operating System Concepts"** de **Silberschatz et al.**, que cubren los detalles teóricos y prácticos sobre la creación y gestión de procesos.


---

#### Cuándo conmutar entre procesos

La conmutación entre procesos puede ocurrir cuando el SO obtiene el control de la CPU

●SVC (SWI) (requerimiento explícito del proceso)

●Trap (error en la ejecución de una instrucción del proceso)

● Interrupción (externa al proceso) (El control debe ser transferido a la rutina de manejo de
interrupciones)

	● Tiempo
	
	●Terminación de I/O
	
	●Page fault
---
La **conmutación entre procesos** (también conocida como **cambio de contexto**) es el mecanismo por el cual el sistema operativo cambia la ejecución de la CPU de un proceso a otro. Este proceso es esencial para la **multitarea** en sistemas operativos, permitiendo que varios procesos se ejecuten de forma concurrente en una sola CPU. A continuación, se explican los casos en los que la conmutación entre procesos puede ocurrir.

### **Cuándo se produce la conmutación entre procesos**

La conmutación entre procesos puede ocurrir cuando el sistema operativo obtiene el control de la CPU debido a varias situaciones. Estas situaciones incluyen:

#### 1. **SVC (SWI) - Requerimiento explícito del proceso**

- **Definición**: **SVC (Supervisor Call)** o **SWI (Software Interrupt)** es una interrupción provocada **por el propio proceso** que solicita al sistema operativo ejecutar una acción específica, como una llamada al sistema (System Call).
    
- **¿Qué pasa durante un SVC?**:  
    Cuando un proceso realiza una llamada al sistema (como **lectura/escritura de archivos**, **asignación de memoria**, **creación de procesos**, etc.), el sistema operativo obtiene el control de la CPU y realiza la operación solicitada. En este caso, se realiza un **cambio de modo de usuario a modo núcleo**, ya que el proceso pasa de un modo con privilegios limitados a uno con privilegios completos.
    
- **Ejemplo**: Un proceso realiza una solicitud de E/S (entrada/salida), como leer un archivo. El sistema operativo toma el control de la CPU y procesa la solicitud de E/S en modo núcleo.
    

#### 2. **Trap - Error en la ejecución de una instrucción del proceso**

- **Definición**: Un **trap** es un tipo específico de interrupción provocada por un **error** en la ejecución del proceso, como un error de **memoria** o una **instrucción ilegal**.
    
- **¿Qué pasa durante un trap?**:  
    Cuando un proceso genera un error (como una división por cero o el acceso a una dirección de memoria no válida), el sistema operativo transfiere el control a un **manejador de excepciones** que maneja el error. Este manejo puede llevar a que el proceso sea suspendido o que se tomen acciones correctivas (como liberar recursos o corregir el estado del proceso).
    
- **Ejemplo**: Si un proceso intenta acceder a una dirección de memoria fuera de su espacio asignado, se genera un "segmentation fault" (error de segmentación), y el sistema operativo maneja este error.
    

#### 3. **Interrupción - Externa al proceso (control transferido a la rutina de manejo de interrupciones)**

Las **interrupciones** son eventos **externos al proceso** que requieren que el sistema operativo tome el control de la CPU para manejar una acción inmediata. Hay varias causas para las interrupciones, incluyendo eventos de hardware y de software.

##### 3.1 **Tiempo (Timer Interrupts)**

- **Definición**: El sistema operativo puede configurar un **temporizador** para generar una interrupción después de un intervalo de tiempo predeterminado.
    
- **¿Qué pasa durante una interrupción de tiempo?**:  
    Cada vez que el temporizador genera una interrupción, el sistema operativo interrumpe el proceso en ejecución y realiza una **conmutación de contexto**. Esto permite que el sistema operativo gestione la ejecución de múltiples procesos de manera equitativa. Este tipo de interrupción es común en la **planificación de procesos** (scheduling), donde el sistema operativo decide cuándo cambiar de un proceso a otro.
    
- **Ejemplo**: El planificador de procesos del sistema operativo utiliza una interrupción de tiempo para cambiar el proceso en ejecución y dar tiempo de CPU a otros procesos.
    

##### 3.2 **Terminación de I/O (Interrupción de Entrada/Salida)**

- **Definición**: Las **interrupciones de I/O** ocurren cuando un proceso solicita una operación de entrada o salida, y el dispositivo de I/O (como un disco, una impresora o una red) termina su operación.
    
- **¿Qué pasa durante una interrupción de I/O?**:  
    Cuando una operación de I/O se completa (por ejemplo, lectura de un archivo desde el disco), el dispositivo de I/O genera una interrupción que transfiere el control al sistema operativo. El proceso que estaba esperando la operación de E/S es **desbloqueado** y puede continuar su ejecución. Además, el sistema operativo puede realizar la **conmutación de contexto** si es necesario.
    
- **Ejemplo**: Un proceso realiza una lectura desde un disco. Cuando la lectura finaliza, el disco genera una interrupción, y el sistema operativo reactiva el proceso que estaba esperando.
    

##### 3.3 **Page Fault (Fallo de Página)**

- **Definición**: Un **page fault** ocurre cuando un proceso intenta acceder a una página de memoria que no está cargada en la memoria física.
    
- **¿Qué pasa durante un page fault?**:  
    Cuando un proceso accede a una página que no está en la memoria (porque fue **swappeada** a disco o nunca fue cargada), se genera una interrupción de **page fault**. El sistema operativo maneja la interrupción, cargando la página solicitada desde el disco a la memoria principal. Esto puede implicar la **conmutación de contexto**, especialmente si se necesita intercambiar páginas entre la memoria y el disco.
    
- **Ejemplo**: Un proceso intenta acceder a una página de memoria virtual que no está en la memoria física. El sistema operativo gestiona la carga de la página desde el disco, lo que genera un cambio en el proceso.
    

### **Resumen de Cuándo Ocurre la Conmutación de Contexto**

La conmutación entre procesos (o cambio de contexto) puede ocurrir cuando el sistema operativo obtiene el control de la CPU debido a:

- **SVC (SWI)**: Solicitudes explícitas de los procesos.
    
- **Trap**: Errores durante la ejecución del proceso.
    
- **Interrupciones**: Eventos externos que requieren la atención inmediata del sistema operativo, como:
    
    - **Interrupción de tiempo**: Para la planificación de procesos.
        
    - **Interrupción de I/O**: Cuando las operaciones de entrada/salida terminan.
        
    - **Page Fault**: Cuando el proceso accede a una página de memoria no cargada.
        

La conmutación de contexto es esencial para la multitarea, ya que permite que múltiples procesos compartan la CPU de manera eficiente y sin interferir entre sí.

---

![[CambioDeModoYCambioDeProceso.png]]

![[DondeSeGuardaEnLaPCB.png]]


---



> **Ejecución del SO**
> Kernel


### **Ejecución del Sistema Operativo (SO) - El Kernel**

El **kernel** es la parte central del sistema operativo, y su principal responsabilidad es gestionar los recursos del sistema (como la CPU, la memoria, y los dispositivos de entrada/salida) y proporcionar servicios a los procesos en ejecución. A continuación, te doy una descripción detallada de lo que hace el kernel durante la **ejecución del sistema operativo**.

### 1. **Definición del Kernel**

El **kernel** es el **núcleo del sistema operativo** y tiene el control total del hardware del sistema. A diferencia de las aplicaciones o procesos de usuario, el kernel se ejecuta en **modo núcleo** (privilegiado), lo que le da acceso completo y directo a todos los recursos del sistema.

### 2. **Responsabilidades del Kernel**

El kernel se encarga de varias tareas críticas para el funcionamiento del sistema operativo. Estas son algunas de las responsabilidades clave:

#### 2.1 **Gestión de Procesos**

- **Planificación y ejecución de procesos**: El kernel gestiona el ciclo de vida de los procesos, desde su creación hasta su terminación. Esto incluye la asignación de la CPU a los procesos listos para ejecutar, la conmutación entre procesos y el manejo de interrupciones y traps.
    
- **Cambio de contexto**: El kernel es responsable de realizar la **conmutación de contexto** entre procesos, lo que permite que múltiples procesos se ejecuten de manera **concurrente** o **simultánea** en un sistema de CPU única (a través de la multitarea).
    
- **Sincronización y comunicación entre procesos**: El kernel maneja los mecanismos de sincronización entre procesos, como los semáforos y los mutex, para evitar que los procesos interfieran entre sí y provoquen condiciones de carrera. Además, gestiona la **comunicación entre procesos** (IPC), permitiendo que los procesos se envíen mensajes y compartan datos.
    

#### 2.2 **Gestión de Memoria**

- **Asignación de memoria**: El kernel es responsable de asignar y gestionar la memoria RAM del sistema para los procesos en ejecución. Esto incluye la **gestión de la memoria virtual**, la asignación de páginas de memoria y la gestión de **segmentos de memoria**.
    
- **Paginación y segmentación**: Cuando los procesos requieren más memoria de la que está disponible físicamente, el kernel gestiona la **paginación** (movimiento de páginas entre la memoria física y el disco) y la **segmentación** (división de la memoria en bloques lógicos).
    
- **Manejo de errores de memoria**: El kernel maneja errores como los **page faults** (cuando un proceso intenta acceder a una página de memoria que no está en la RAM) y gestiona la **liberación de memoria** cuando los procesos terminan o liberan recursos.
    

#### 2.3 **Gestión de Entrada/Salida (E/S)**

- **Control de dispositivos**: El kernel gestiona las operaciones de **entrada y salida (E/S)**, como leer o escribir en discos duros, pantallas, teclados, redes, etc. Para cada dispositivo, el kernel tiene un **controlador de dispositivo** que actúa como intermediario entre el hardware y el sistema operativo.
    
- **Manejo de interrupciones de E/S**: Cuando un dispositivo termina una operación de E/S (como una lectura o escritura), el kernel gestiona la **interrupción** generada por el dispositivo para que el proceso que estaba esperando la E/S pueda continuar su ejecución.
    

#### 2.4 **Gestión de Archivos**

- **Sistema de archivos**: El kernel también se encarga de la **gestión de archivos** en el sistema. Administra los sistemas de archivos (como ext4, NTFS, FAT32) y facilita la creación, lectura, escritura y eliminación de archivos. Los archivos son administrados en **directorios**, y el kernel se asegura de que los procesos tengan acceso controlado a ellos.
    
- **Seguridad y permisos**: El kernel aplica políticas de **seguridad y control de acceso** para determinar qué procesos pueden acceder a qué archivos. Este control se realiza mediante los **permisos de archivos** (lectura, escritura, ejecución).
    

#### 2.5 **Gestión de Recursos**

- **Asignación de recursos**: El kernel se encarga de la asignación de **recursos del sistema**, como la **CPU**, **memoria** y **dispositivos de E/S**. Esto implica la gestión eficiente de los recursos y la **protección** para evitar que un proceso monopolice todos los recursos.
    
- **Manejo de recursos compartidos**: En un sistema multitarea, el kernel gestiona cómo los procesos comparten recursos. Por ejemplo, si varios procesos intentan acceder a un archivo al mismo tiempo, el kernel garantiza que el acceso sea seguro y consistente.
    

#### 2.6 **Seguridad y Control de Acceso**

- **Modo núcleo vs. modo usuario**: El kernel ejecuta operaciones críticas en **modo núcleo** (privilegiado), mientras que las aplicaciones de usuario se ejecutan en **modo usuario**, con privilegios limitados. Esto garantiza la **seguridad del sistema**, evitando que los procesos de usuario puedan modificar o interferir con el kernel.
    
- **Autenticación y autorización**: El kernel gestiona las **políticas de seguridad** y la **autenticación** de los usuarios, asegurando que solo los usuarios autorizados puedan acceder a ciertos recursos del sistema.
    

### 3. **El Proceso de Ejecución del Kernel**

Cuando un proceso solicita un servicio o recurso del sistema, el kernel toma el control de la CPU para manejar la solicitud. El proceso de ejecución de un sistema operativo incluye varias fases clave:

#### 3.1 **Interrupciones y Traps**

Las interrupciones son mecanismos que permiten al kernel obtener el control en respuesta a eventos externos (como hardware o temporizadores). Los **traps** son interrupciones provocadas por errores o solicitudes explícitas de los procesos (como llamadas al sistema). El kernel gestiona estas interrupciones y traps para decidir si debe conmutar entre procesos o realizar otra acción.

#### 3.2 **Planificación de Procesos**

Cuando el kernel decide qué proceso ejecutar, elige un proceso de la **cola de procesos listos** utilizando un algoritmo de **planificación** (por ejemplo, Round-Robin, prioridad, etc.). El kernel asigna la CPU al proceso seleccionado y cambia el contexto para ejecutar el proceso.

#### 3.3 **Cambio de Contexto**

El **cambio de contexto** es el proceso mediante el cual el kernel guarda el estado de un proceso (como el contador de programa, registros, etc.) y carga el estado de otro proceso para su ejecución. Esto se realiza cada vez que el kernel necesita pasar de un proceso a otro.

#### 3.4 **Manejo de Fallos de Páginas y Memoria**

Cuando un proceso accede a una página de memoria que no está en la RAM, se genera un **page fault**. El kernel maneja este evento al cargar la página faltante desde el disco (si es necesario) y retomar la ejecución del proceso.

### 4. **Conclusión**

El kernel es la **pieza fundamental del sistema operativo**. Se encarga de la **gestión de procesos**, **memoria**, **E/S**, **archivos**, **seguridad**, y **planificación de recursos**, entre otras tareas. Es responsable de **proteger** el sistema y los procesos de usuario, asegurando que el hardware y los recursos del sistema se utilicen de manera eficiente y segura. Sin el kernel, el sistema operativo no podría proporcionar los servicios y funcionalidades que permiten a las aplicaciones de usuario interactuar con el hardware de manera segura y controlada.


---
#### Ejecución dentro de los procesos usuarios

### **Ejecución dentro de los Procesos de Usuario**

Los **procesos de usuario** son aquellos que se ejecutan en el **modo usuario** del sistema operativo, a diferencia del **modo núcleo** o **modo privilegiado**, donde opera el **kernel** del sistema operativo. Los procesos de usuario son aplicaciones o programas que interactúan con el sistema a través de las **llamadas al sistema** (system calls) proporcionadas por el kernel para acceder a recursos como memoria, E/S, y servicios del sistema operativo.

A continuación, se describen los aspectos clave de la **ejecución de procesos dentro del modo usuario**, desde su creación hasta su ejecución, pasando por las interacciones con el sistema operativo.

### 1. **Creación del Proceso de Usuario**

El **proceso de usuario** es creado generalmente mediante una llamada al sistema, como la función `fork()` en sistemas basados en UNIX/Linux o `CreateProcess()` en sistemas Windows. Cuando se crea un proceso, el sistema operativo asigna un **identificador único** (PID) y prepara recursos como memoria, registros y espacio de pila para el proceso.

### 2. **Ejecución de un Proceso de Usuario**

Cuando el proceso de usuario está listo para ejecutarse, el **kernel** lo coloca en la cola de procesos listos. La ejecución de procesos de usuario se realiza en el **modo usuario**, lo que significa que tienen acceso restringido al hardware y recursos del sistema. Los procesos de usuario solo pueden interactuar con el sistema operativo mediante **llamadas al sistema**.

#### 2.1 **Modo Usuario vs. Modo Núcleo**

- **Modo Usuario**: Los procesos en modo usuario no pueden ejecutar instrucciones privilegiadas. Esto significa que no pueden acceder directamente a la memoria del sistema, interactuar con dispositivos de hardware o ejecutar operaciones sensibles.
    
- **Modo Núcleo**: El kernel del sistema operativo se ejecuta en modo núcleo, con privilegios completos para interactuar con el hardware y gestionar los recursos del sistema.
    

Para realizar operaciones sensibles, como la E/S o la asignación de memoria, un proceso de usuario debe hacer una **llamada al sistema** (System Call), que genera una interrupción y cambia el proceso de modo usuario a modo núcleo.

### 3. **Interacciones con el Sistema Operativo**

Los procesos de usuario interactúan con el sistema operativo mediante **llamadas al sistema**. Estas son solicitudes de servicio que permiten a los procesos de usuario realizar operaciones que no pueden realizar en modo usuario, como:

#### 3.1 **Llamadas al Sistema**

- **Llamadas para gestionar archivos**: Como `open()`, `read()`, `write()`, y `close()` que permiten al proceso acceder y manipular archivos.
    
- **Llamadas para gestionar memoria**: Como `malloc()`, `free()`, o `mmap()` que permiten al proceso gestionar su espacio de memoria.
    
- **Llamadas para crear y gestionar procesos**: Como `fork()`, `exec()`, `wait()` que permiten crear nuevos procesos, reemplazar el espacio de memoria de un proceso, o esperar la finalización de un proceso hijo.
    
- **Llamadas para gestión de señales y control de procesos**: Como `kill()`, `signal()` o `exit()` que permiten la gestión de señales (como la terminación de procesos).
    

Cuando un proceso de usuario realiza una **llamada al sistema**, el sistema operativo lo **interrumpe** y cambia al **modo núcleo** para ejecutar la operación solicitada. Una vez que la operación se ha completado, el sistema operativo **restaura** el proceso de usuario y vuelve al **modo usuario**.

#### 3.2 **Interrupciones y Traps**

Las **interrupciones** son eventos externos que interrumpen la ejecución del proceso, como una solicitud de E/S completada, un fallo de página o un temporizador de interrupción. El proceso de usuario no tiene control directo sobre las interrupciones, pero debe ser consciente de ellas.

- **Trap**: Cuando un proceso de usuario realiza una llamada al sistema, se genera una **interrupción por software** (trap), lo que provoca que el sistema operativo transfiera el control al **modo núcleo** para ejecutar la operación solicitada.
    
- **Interrupciones de hardware**: Ocurren debido a eventos externos, como operaciones de E/S que terminan o errores en la ejecución, lo que también transfiere el control al kernel para manejar el evento.
    

### 4. **Manejo de Excepciones y Errores en Procesos de Usuario**

Cuando un proceso de usuario comete un error o realiza una operación no válida (como acceso a memoria no autorizada, división por cero, etc.), se genera una **excepción** o **error de ejecución**. Esto provoca que el sistema operativo interrumpa el proceso y lo maneje adecuadamente.

- **Excepciones**: Pueden ser **traps** generados por el propio proceso (como un intento de acceso a una dirección de memoria no válida).
    
- **Errores de hardware**: Como un **fallo de página** o una **interrupción de hardware**.
    

El sistema operativo debe gestionar estos errores y excepciones. A veces, se interrumpe el proceso de usuario para corregir el problema, o se envía una señal para que el proceso termine o recupere su estado.

### 5. **Terminación de un Proceso de Usuario**

Cuando un proceso de usuario termina su ejecución, ya sea de manera exitosa o por un error, debe **liberar los recursos** que estaba utilizando. El sistema operativo gestiona este proceso, asegurando que la memoria se libere, los archivos sean cerrados y que otros recursos sean devueltos al sistema.

#### 5.1 **Terminación Normal**

Cuando un proceso termina **normalmente** (es decir, al llamar a `exit()` o al completar su ejecución), el sistema operativo realiza las siguientes acciones:

- **Libera la memoria** que había asignado al proceso.
    
- **Cierra los archivos** abiertos por el proceso.
    
- **Elimina el PCB (Process Control Block)** y otras estructuras relacionadas con el proceso.
    

#### 5.2 **Terminación Abnormal**

Si el proceso termina de manera **anormal** debido a un error (como un **segmentation fault**), el sistema operativo puede **terminar el proceso** y, dependiendo del tipo de error, puede enviar una señal al proceso padre o registrar el evento.

### 6. **Conclusión**

La **ejecución dentro de los procesos de usuario** se lleva a cabo en el **modo usuario** del sistema operativo, donde los procesos tienen acceso restringido a los recursos del sistema. Las interacciones con el sistema operativo se realizan mediante **llamadas al sistema** que permiten a los procesos de usuario realizar operaciones privilegiadas (como gestión de memoria y E/S). Además, el sistema operativo gestiona las interrupciones, excepciones y errores generados por los procesos de usuario y se encarga de la **terminación** de los procesos una vez que han completado su ejecución.

Este modelo de ejecución garantiza que los procesos de usuario se mantengan aislados y protegidos, y que el sistema operativo pueda gestionar eficientemente los recursos y asegurar la estabilidad y seguridad del sistema.

---
#### Sistema Operativo basado en procesos

### **Sistema Operativo Basado en Procesos**

Un **sistema operativo basado en procesos** es un sistema que organiza y gestiona la ejecución de **procesos** (programas en ejecución) como sus unidades fundamentales de trabajo. En este modelo, el sistema operativo **abstrae las tareas del hardware** y las organiza a través de la ejecución y gestión de procesos, permitiendo que el sistema maneje múltiples tareas de manera concurrente o simultánea. El concepto de procesos es central para el funcionamiento del sistema operativo, y todos los recursos del sistema se asignan y administran en función de estos procesos.

A continuación, se detalla cómo un sistema operativo basado en procesos maneja estos aspectos clave:

### 1. **¿Qué es un Proceso?**

Un **proceso** es un **programa en ejecución**. Es más que solo el código del programa: incluye el **estado de ejecución** (como los registros de la CPU, el contador de programa, etc.), **memoria asignada**, y los **recursos** utilizados, como archivos abiertos, dispositivos de E/S, y más.

Cada proceso tiene su propio espacio de memoria, y el sistema operativo gestiona su ciclo de vida desde que es creado hasta que termina su ejecución.

### 2. **Características de un Sistema Operativo Basado en Procesos**

#### 2.1 **Abstracción de Hardware**

En un sistema operativo basado en procesos, el sistema operativo abstrae los detalles del hardware y presenta a los procesos una **vista virtualizada** de los recursos del sistema. Esto permite que los procesos interactúen con el sistema sin tener que preocuparse por los detalles del hardware, como la gestión de memoria, la asignación de CPU, etc.

#### 2.2 **Multitarea**

Un sistema operativo basado en procesos puede ejecutar varios procesos simultáneamente, aunque en un **sistema de CPU única**, solo puede ejecutar un proceso a la vez. Sin embargo, mediante la **conmutación de contexto** (context switching), el sistema operativo da la impresión de que los procesos se ejecutan de manera concurrente.

- **Multitarea cooperativa**: Los procesos deben ceder el control voluntariamente.
    
- **Multitarea preventiva**: El sistema operativo interrumpe a los procesos de manera periódica para darles tiempo a otros procesos.
    

#### 2.3 **Aislamiento de Procesos**

Cada proceso tiene su propio **espacio de memoria** y no puede acceder directamente a la memoria de otros procesos, lo que garantiza la **seguridad** y el **aislamiento**. El sistema operativo se encarga de gestionar y proteger la memoria para evitar que los procesos interfieran entre sí.

#### 2.4 **Control de Ejecución**

El sistema operativo controla el **ciclo de vida** de los procesos. Esto incluye su **creación**, **ejecución**, **suspensión**, y **terminación**. El sistema operativo también gestiona las **interrupciones** y **llamadas al sistema** que los procesos pueden hacer para interactuar con el hardware o el sistema operativo.

#### 2.5 **Sincronización y Comunicación entre Procesos**

En un sistema basado en procesos, los procesos pueden necesitar **sincronizarse** o **comunicarse** entre sí para realizar tareas cooperativas. El sistema operativo proporciona **mecanismos de comunicación** e **intercambio de información**, como **pipes**, **colas de mensajes**, **semaforos**, y **mutexes**, que permiten a los procesos coordinarse sin interferir en el trabajo de los demás.

### 3. **Estructura de un Proceso**

Un proceso no es solo un conjunto de instrucciones en ejecución, sino que tiene varios componentes clave, incluidos los siguientes:

#### 3.1 **Proceso Control Block (PCB)**

Cada proceso en ejecución tiene un bloque de control llamado **PCB**. Este bloque almacena toda la información necesaria para gestionar y controlar el proceso. Un PCB típicamente contiene:

- **PID** (Process ID): Identificador único del proceso.
    
- **Estado**: El estado actual del proceso (listo, en ejecución, bloqueado, etc.).
    
- **Contador de Programa**: La dirección de la próxima instrucción a ejecutar.
    
- **Registros de la CPU**: Los valores de los registros cuando el proceso es interrumpido.
    
- **Memoria Asignada**: El espacio de memoria (dirección base y límite) asignado al proceso.
    
- **Información de E/S**: Información sobre los dispositivos de entrada/salida que el proceso está utilizando.
    

#### 3.2 **Espacio de Dirección**

Cada proceso tiene su propio **espacio de direcciones**, que generalmente se divide en varias áreas:

- **Código**: El código del programa.
    
- **Datos**: Variables globales y estáticas.
    
- **Pila (Stack)**: Almacena las funciones llamadas y las variables locales.
    
- **Heap**: Espacio para la asignación dinámica de memoria durante la ejecución del programa.
    

#### 3.3 **Colas de Procesos**

El sistema operativo mantiene diferentes colas para gestionar el estado de los procesos. Estas colas incluyen:

- **Cola de procesos listos**: Contiene procesos que están listos para ser ejecutados.
    
- **Cola de procesos bloqueados**: Contiene procesos que están esperando algún recurso o evento (por ejemplo, I/O o semáforo).
    
- **Cola de procesos en espera de interrupciones**: Contiene procesos que están esperando una señal de interrupción.
    

### 4. **Ciclo de Vida de un Proceso**

El ciclo de vida de un proceso en un sistema operativo basado en procesos generalmente sigue estos pasos:

1. **Creación**: El proceso es creado por un proceso padre a través de una llamada al sistema (como `fork()` en sistemas UNIX). En esta fase, se le asignan recursos y se inicializan sus estructuras de datos.
    
2. **Ejecución**: El proceso entra en el estado **listo** y espera ser programado por el **planificador de procesos**. Cuando es seleccionado, pasa al estado **ejecutando**.
    
3. **Bloqueo**: El proceso puede entrar en el estado **bloqueado** cuando espera un recurso (como E/S o una condición de sincronización).
    
4. **Finalización**: El proceso termina cuando completa su ejecución o es terminado por el sistema operativo (por ejemplo, por un error o por una llamada a `exit()`).
    

### 5. **Manejo de Recursos en un Sistema Operativo Basado en Procesos**

#### 5.1 **Asignación de Recursos**

El sistema operativo debe gestionar y **asignar recursos** como la CPU, memoria y dispositivos de E/S a los procesos. Para hacer esto de manera eficiente y justa, el sistema operativo utiliza **algoritmos de planificación de procesos**, como **Round-Robin**, **First-Come-First-Served (FCFS)**, o **Prioridad**.

#### 5.2 **Protección y Seguridad**

El sistema operativo debe garantizar que los procesos no interfieran entre sí de forma inapropiada. Para lograr esto, implementa **mecanismos de protección**, como la **protección de memoria**, para evitar que un proceso acceda a la memoria de otro. Además, los procesos se ejecutan en **modo usuario**, lo que limita el acceso a recursos críticos del sistema (como la memoria del kernel).

### 6. **Conclusión**

Un **sistema operativo basado en procesos** organiza y gestiona la ejecución de múltiples procesos, proporcionando una abstracción del hardware y recursos del sistema. A través de la creación, planificación, sincronización y terminación de procesos, el sistema operativo asegura que los recursos se utilicen de manera eficiente y segura. La correcta gestión de procesos es esencial para la **multitarea** y el **rendimiento** del sistema, lo que permite la ejecución concurrente de varias aplicaciones y servicios en el mismo sistema.

---
tipo de interrupción, buscas el tipo, cada tipo tiene un puntero y este trabaja cada interrupción de manera diferente.

### **Tipos de Interrupciones y su Manejo en el Sistema Operativo**

Las **interrupciones** son eventos que desvían el flujo de ejecución normal de un proceso para que el sistema operativo (SO) pueda atender situaciones importantes, como errores de hardware o la solicitud de recursos. Las interrupciones pueden provenir de diversos orígenes y el sistema operativo las gestiona mediante un mecanismo de **rutinas de manejo de interrupciones** (ISR, Interrupt Service Routines).

Cada tipo de interrupción tiene un **puntero** o **vector** que señala a la rutina específica de manejo de la interrupción. Este puntero se almacena en una **tabla de vectores de interrupción**, lo que permite que el sistema operativo responda correctamente a cada tipo de interrupción.

A continuación, describo los **tipos de interrupciones** y cómo cada tipo tiene un manejo específico, dependiendo de su origen:

### 1. **Interrupciones de Hardware (Externas)**

Las interrupciones de hardware son generadas por dispositivos de hardware externos (como teclados, discos duros, o temporizadores) y requieren la atención del procesador para gestionar algún evento. Este tipo de interrupción es crucial para la interacción entre los dispositivos de hardware y el sistema operativo.

#### **Subtipos de Interrupciones de Hardware**:

- **Interrupción de Entrada/Salida (E/S)**: Ocurre cuando un dispositivo de E/S (por ejemplo, un disco o una tarjeta de red) ha completado una operación y necesita que el sistema operativo procese la información.
    
    - **Ejemplo**: Un dispositivo de almacenamiento ha terminado de leer o escribir datos, y necesita que el sistema operativo gestione los resultados.
        
    - **Manejo**: El puntero de la interrupción apunta a una rutina de manejo de E/S que gestiona la lectura o escritura de datos desde o hacia el dispositivo.
        
- **Interrupción de Tiempo (Timer Interrupt)**: Generada por un temporizador o reloj del sistema, esta interrupción se usa para implementar **multitarea** y **planificación de procesos**. Suele generar una interrupción periódica para permitir que el sistema operativo cambie de un proceso a otro (cambio de contexto).
    
    - **Ejemplo**: Un temporizador genera una interrupción cada 10 ms para permitir que el planificador de procesos ejecute una tarea de planificación.
        
    - **Manejo**: El puntero lleva a la rutina de manejo del temporizador, que puede ser responsable de cambiar de contexto entre procesos.
        
- **Interrupción de Error de Hardware**: Estas interrupciones se generan por fallos de hardware, como una **fallo de disco** o un **error de memoria**.
    
    - **Ejemplo**: Si el procesador detecta un fallo en el acceso a la memoria, como un **page fault**, se genera una interrupción para notificar al sistema operativo que debe intervenir.
        
    - **Manejo**: El puntero apunta a una rutina que gestiona el fallo de hardware. Por ejemplo, en el caso de un fallo de página, se podría cargar la página desde el disco al espacio de memoria.
        

### 2. **Interrupciones por Software (Internas)**

Las interrupciones por software son generadas por el propio sistema operativo o los programas de usuario, como resultado de una **llamada al sistema** (System Call) o un **error de ejecución** (como una excepción).

#### **Subtipos de Interrupciones por Software**:

- **Software Interrupt (SVC o SWI)**: Generada por un **proceso de usuario** para solicitar un servicio del sistema operativo. Las llamadas al sistema permiten que un proceso de usuario acceda a recursos que están bajo el control del sistema operativo, como E/S o asignación de memoria.
    
    - **Ejemplo**: Un proceso de usuario hace una llamada al sistema para leer un archivo, lo que genera una interrupción de software para que el sistema operativo maneje la operación de E/S.
        
    - **Manejo**: El puntero de la interrupción apunta a la rutina de manejo de **llamadas al sistema** que gestiona la solicitud de E/S.
        
- **Excepciones o Errores de Ejecución**: Ocurren cuando un proceso ejecuta una instrucción ilegal o produce un error de ejecución. Un ejemplo común es el **segmentation fault** o la **división por cero**.
    
    - **Ejemplo**: Un proceso intenta acceder a una dirección de memoria inválida, lo que genera una interrupción de error.
        
    - **Manejo**: El puntero apunta a una rutina que maneja el error, como abortar el proceso o recuperar el estado del proceso.
        
- **Page Fault**: Es un tipo específico de interrupción interna que ocurre cuando un proceso intenta acceder a una página de memoria que no está actualmente cargada en la RAM. Esta interrupción es esencial en la **gestión de la memoria virtual**.
    
    - **Ejemplo**: Un proceso intenta acceder a una página de memoria virtual que no está en la memoria principal, lo que genera un **page fault**.
        
    - **Manejo**: El puntero apunta a una rutina que carga la página solicitada desde el disco a la memoria física.
        

### 3. **Interrupciones por Condición Externa (Interrupciones Asíncronas)**

Este tipo de interrupciones no están directamente relacionadas con el proceso que se ejecuta, sino con **eventos externos** que necesitan atención inmediata del sistema.

#### **Subtipos de Interrupciones por Condición Externa**:

- **Interrupciones por Fallo de Hardware (Failure Interrupts)**: Como un fallo de un componente crítico del sistema, como la **perdida de energía** o un **fallo de disco**.
    
    - **Ejemplo**: Si el disco duro detecta un error crítico y no puede continuar, genera una interrupción para que el sistema operativo intervenga.
        
    - **Manejo**: El puntero de la interrupción se dirige a la rutina que gestiona la recuperación del fallo de hardware o la notificación del error al usuario.
        
- **Interrupciones por Exceso de Temperatura o Daños Físicos**: Algunos sistemas pueden generar interrupciones si se detecta que el **sistema está sobrecalentado** o tiene un **fallo de hardware**.
    
    - **Ejemplo**: El procesador genera una interrupción de error si la temperatura excede el límite seguro.
        
    - **Manejo**: El puntero de la interrupción dirige a una rutina que gestiona la alerta, posiblemente apagando el sistema o deteniendo el proceso peligroso.
        

### 4. **Tabla de Vectores de Interrupción**

Cada tipo de interrupción tiene su propio **puntero** que apunta a una **rutina de servicio de interrupción** (ISR). Estas rutinas son funciones específicas diseñadas para manejar el tipo de interrupción que ocurrió. La **tabla de vectores de interrupción** (IVT, Interrupt Vector Table) es una estructura de datos que contiene estos punteros.

- **Estructura**: La tabla contiene direcciones de memoria (direcciones de punteros) a las rutinas de manejo de interrupciones correspondientes.
    
- **Función**: Cuando ocurre una interrupción, el sistema operativo consulta la tabla de vectores y transfiere el control a la rutina de servicio correspondiente.
    

### **Resumen de Tipos de Interrupciones y Manejo**

1. **Interrupciones de Hardware (Externas)**:
    
    - E/S: Operaciones de dispositivos.
        
    - Temporizador: Planificación de procesos.
        
    - Fallo de Hardware: Errores de hardware (ej., fallo de memoria).
        
2. **Interrupciones por Software (Internas)**:
    
    - Llamadas al Sistema: Solicitudes de procesos de usuario.
        
    - Excepciones: Errores en la ejecución de procesos (ej., divisiones por cero).
        
    - Page Fault: Errores de acceso a memoria virtual.
        
3. **Interrupciones por Condición Externa**:
    
    - Fallos de hardware o eventos críticos del sistema.
        

Cada tipo de interrupción tiene un puntero en la tabla de vectores de interrupción, lo que permite que el sistema operativo maneje cada tipo de interrupción de manera adecuada, garantizando la eficiencia, la estabilidad y la seguridad del sistema.

---

![[Modelo de estados en Unix SVR4.png]]

Clase Siguiente: 
Próxima Clase: [[Clase 6]]