"Clase previa": [[Clase 2]]

13-08-2025 - Teoría con Horacio.

Caché:
que es, principios, jerarquías.

Perfecto, esos son justamente los pilares para responder con base sólida.  
Te hago un resumen de **Caché: qué es, principios y jerarquías** citando únicamente **Tanenbaum**, **Silberschatz**, y **Patterson & Hennessy**.

---

## 📌 Memoria Caché

### **Definición**

Según Tanenbaum (_Modern Operating Systems_, 4ª ed., cap. 3) y Patterson & Hennessy (_Computer Organization and Design_, 5ª ed., cap. 5),  
la memoria caché es una **memoria intermedia de alta velocidad** situada entre la CPU y la memoria principal, destinada a **reducir el tiempo promedio de acceso a datos e instrucciones**.

El principio es aprovechar la **localidad de referencia**:

- **Localidad temporal**: si un dato se usa, probablemente se vuelva a usar pronto.
    
- **Localidad espacial**: si se accede a una posición de memoria, es probable que las adyacentes también se usen pronto.
    

---

### **Principios de funcionamiento**

> (Basado en Silberschatz _Operating System Concepts_, 10ª ed., cap. 9, y Patterson & Hennessy, cap. 5)

1. **Jerarquía de memoria**: la caché es más pequeña pero más rápida que la RAM, y almacena copias de bloques de memoria.
    
2. **Mapeo de bloques**:
    
    - **Directo**: cada bloque de memoria principal va a una posición específica en caché.
        
    - **Asociativo**: cualquier bloque puede ir a cualquier línea de caché.
        
    - **Asociativo por conjunto**: híbrido entre los dos anteriores.
        
3. **Políticas de reemplazo**: deciden qué bloque expulsar cuando la caché está llena (ej.: LRU — _Least Recently Used_, FIFO, Random).
    
4. **Políticas de escritura**:
    
    - **Write-through**: escribe en memoria principal y caché simultáneamente.
        
    - **Write-back**: escribe solo en caché y actualiza la memoria principal cuando el bloque es reemplazado.
        

---

### **Jerarquías**

> (Patterson & Hennessy, cap. 5)

- **L1**: Caché más pequeña y rápida (normalmente separada en instrucciones y datos). Latencia de 1-3 ciclos.
    
- **L2**: Mayor capacidad, algo más lenta, comparte datos e instrucciones.
    
- **L3**: Aún más grande, compartida entre núcleos, pero más lenta que L1 y L2.
    
- En procesadores modernos, esta jerarquía permite que la CPU mantenga un alto _throughput_ minimizando accesos a la RAM.
    

---

### **Tamaños y gestión de páginas**

Aunque la caché no almacena páginas completas de memoria virtual, sino **bloques (líneas de caché)** típicamente de 32 a 128 bytes, su efectividad se basa en:

- Detectar qué datos se usan con frecuencia y mantenerlos en niveles más rápidos.
    
- Coordinarse con la **MMU (Memory Management Unit)** y la **TLB (Translation Lookaside Buffer)** para acelerar traducciones de direcciones virtuales a físicas.
    

---

Si querés, puedo hacerte el mismo resumen con **memoria virtual** y **swapping** usando únicamente _Tanenbaum_, _Silberschatz_ y _Patterson & Hennessy_, así mantenemos coherencia de fuentes.7---7



---

Multiprocesador:
en un principio, eran monoprocesador.
ventajas, desventajas.
dos tipos: Asimétrico, Simétrico.

Perfecto, te lo explico con base en **Tanenbaum**, **Silberschatz** y **Patterson & Hennessy**.

---

## Multiprocesadores

### 1. Contexto histórico

Según **Tanenbaum, "Sistemas Operativos Modernos" (4ta ed.)**, los primeros computadores eran **monoprocesador**, es decir, con **una sola CPU** que ejecutaba todas las instrucciones secuencialmente.  
Con la evolución de la tecnología y la disminución de costos de fabricación de procesadores, se desarrollaron sistemas **multiprocesador** para mejorar rendimiento, tolerancia a fallos y capacidad de procesamiento paralelo.

---

### 2. Ventajas de los multiprocesadores

**Referencias:**

- Tanenbaum, _Sistemas Operativos Modernos_
    
- Silberschatz, _Operating System Concepts_
    
- Patterson & Hennessy, _Computer Organization and Design_
    
- **Mayor rendimiento**: pueden ejecutar múltiples hilos/procesos en paralelo.
    
- **Mayor disponibilidad**: si un procesador falla, otro puede asumir parte de la carga.
    
- **Mejor utilización de recursos**: pueden compartir memoria y periféricos.
    
- **Escalabilidad**: se pueden agregar más CPUs para soportar más carga.
    

---

### 3. Desventajas

- **Complejidad del hardware**: requiere interconexiones rápidas y mecanismos de coherencia de caché.
    
- **Software más complejo**: el sistema operativo debe coordinar y balancear la carga entre CPUs.
    
- **Problemas de concurrencia**: mayor dificultad para evitar condiciones de carrera y asegurar sincronización.
    
- **Costos**: más procesadores implican más inversión inicial y consumo energético.
    

---

### 4. Tipos de multiprocesadores

#### a) **Asimétrico (AMP – Asymmetric Multiprocessing)**

- **Definición** (Tanenbaum, Silberschatz): un procesador maestro controla el sistema y asigna tareas a procesadores esclavos.
    
- **Uso histórico**: común en sistemas más antiguos, donde solo un CPU ejecutaba el núcleo del SO y el resto hacía tareas específicas.
    
- **Ventajas**: más sencillo de implementar, control centralizado.
    
- **Desventajas**: cuello de botella en el CPU maestro.
    

#### b) **Simétrico (SMP – Symmetric Multiprocessing)**

- **Definición** (Patterson & Hennessy): todos los procesadores comparten la misma memoria y tienen acceso igual al sistema operativo.
    
- **Uso actual**: estándar en servidores y PCs multiprocesador.
    
- **Ventajas**: todos los CPUs pueden ejecutar cualquier tarea, mejor balance de carga, sin único punto de fallo.
    
- **Desventajas**: complejidad para manejar la coherencia de caché y sincronización.
    

---

📖 **Bibliografía exacta**:

- Tanenbaum, Andrew S. _Sistemas Operativos Modernos_, 4ta edición, Pearson, 2015. Cap. 8.
    
- Silberschatz, Abraham; Galvin, Peter; Gagne, Greg. _Operating System Concepts_, 10ma edición, Wiley, 2018. Cap. 17.
    
- Patterson, David; Hennessy, John. _Computer Organization and Design_, 5ta edición, Morgan Kaufmann, 2014. Cap. 5.
    

---

Si querés, puedo pasarte un **cuadro comparativo AMP vs SMP** con ejemplos reales de cada uno, usando las referencias de estos libros para tu trabajo.

---

La idea es que simulen un monoprocesador, simule que es multi, para poder hacer varias cosas a la vez.

otros programas puedan ejecutar programas y estos usen los periféricos de e/s, teniendo un mejor aprovechamiento de todos los recursos del sistema.
Paralelismo real.
economia de escala: fabricas mas grandes, producen mas barato.
des-economia de ecala: se usa mucho en software.

ejecutar rutinas de bajo nivel, de administracion.
con coordinación, un procesador trabaja o no con otro sincronizado de alto nivel.



---

## **Multiprocesadores**

En sus inicios, la mayoría de los sistemas eran **monoprocesador**, donde un único CPU se encargaba de ejecutar todas las tareas. Con el tiempo, se introdujeron **arquitecturas multiprocesador** para aumentar el rendimiento y la eficiencia.

### **Ventajas**

- **Paralelismo real**: posibilidad de ejecutar múltiples procesos de forma simultánea, no solo mediante multitarea simulada.
    
- **Mejor aprovechamiento de recursos**: otros programas pueden ejecutarse mientras algunos procesadores manejan tareas específicas, incluyendo periféricos de E/S.
    
- **Economía de escala**: producir procesadores en sistemas más grandes reduce costos unitarios en comparación con fabricar varias máquinas pequeñas.
    
- **Mayor disponibilidad**: en algunos diseños, la falla de un procesador no detiene todo el sistema.
    

### **Desventajas**

- **Des-economía de escala en software**: no todo software aprovecha múltiples procesadores de manera eficiente, lo que puede implicar más costo de desarrollo.
    
- **Complejidad de coordinación**: la sincronización y comunicación entre procesadores requiere hardware y software más sofisticado.
    
- **Contención de recursos**: múltiples procesadores pueden competir por memoria, buses o dispositivos de E/S.
    

---

### **Tipos de Multiprocesadores**

Según Silberschatz et al. (_Operating System Concepts_, 9th ed.) y Tanenbaum (_Modern Operating Systems_, 4th ed.), los multiprocesadores se dividen principalmente en:

1. **Asimétricos (AMP)**
    
    - Un procesador maestro controla la asignación de tareas y la comunicación con el sistema operativo.
        
    - Los demás procesadores ejecutan únicamente tareas asignadas por el maestro.
        
    - Más simple de implementar, pero con riesgo de cuello de botella en el procesador maestro.
        
2. **Simétricos (SMP)**
    
    - Todos los procesadores son iguales y ejecutan el sistema operativo de forma concurrente.
        
    - Cualquier procesador puede ejecutar cualquier tarea o rutina, incluyendo administración de recursos.
        
    - Mejor distribución de carga, pero mayor complejidad de sincronización.
        

---

### **Objetivo del Diseño**

- **Simular un monoprocesador**, pero con capacidad real de procesamiento paralelo.
    
- Permitir que varios programas compartan recursos de E/S de forma eficiente.
    
- Ejecución de **rutinas de bajo nivel** (administración) por un procesador mientras otros ejecutan aplicaciones de usuario.
    
- Coordinación opcional: algunos procesadores pueden trabajar de forma independiente, o bien sincronizarse en tareas de alto nivel.
    

---

**Referencias bibliográficas:**

- Tanenbaum, A. S., & Bos, H. (2015). _Modern Operating Systems_ (4th ed.). Pearson.
    
- Silberschatz, A., Galvin, P. B., & Gagne, G. (2018). _Operating System Concepts_ (9th ed.). Wiley.
    
- Patterson, D. A., & Hennessy, J. L. (2017). _Computer Organization and Design: The Hardware/Software Interface_ (5th ed.). Morgan Kaufmann.
    

---

Si querés, puedo ahora hacerte el **esquema comparativo** entre monoprocesador y multiprocesador para que lo tengas en formato de tabla resumida.

---

Cpu con sus propios registros
clusters

nodos, con sus memorias y procesadores(en clusters)
en un programa concurrente, puede terminar un thred de un nodo, y otro en otro procesador de otro modo. sincronizando los threds.
funciona porque, un programa distribuido en un sistema de cluster, se puede romper un modulo entero pero anda igual. se puede relentizar un poco pero sigue andando.
SAN= Storage-Area-Network
Cluster, como armar uno, como funciona, para que es, beneficios.

Perfecto, con lo que me pasaste puedo armarte una explicación completa y ordenada sobre **multiprocesadores** y **clusters**, integrando las ideas que escribiste.

---

## **Multiprocesadores**

### 1. Introducción

En sus inicios, los sistemas eran **monoprocesador**, es decir, una única CPU realizaba todas las tareas del sistema, ejecutando instrucciones de manera secuencial.  
Con el tiempo, para mejorar el rendimiento, se desarrollaron los **multiprocesadores**, que permiten ejecutar varios procesos o hilos al mismo tiempo.

---

### 2. Ventajas

- **Paralelismo real**: posibilidad de ejecutar varias tareas a la vez, no solo simular multitarea.
    
- **Mejor aprovechamiento de recursos**: varios programas pueden usar la CPU y los periféricos en paralelo.
    
- **Mayor rendimiento** en tareas intensivas en cómputo.
    
- **Economía de escala**: producir procesadores con más núcleos resulta más barato que producir varias máquinas separadas.
    

---

### 3. Desventajas

- **Des-economía de escala en software**: desarrollar aplicaciones que aprovechen múltiples procesadores es más complejo y costoso.
    
- **Coordinación y sincronización**: se necesita control para que los procesadores trabajen sin conflictos.
    
- **Posibles cuellos de botella** en memoria y buses si no están bien diseñados.
    

---

### 4. Tipos de Multiprocesadores

- **Asimétrico (AMP)**
    
    - Un procesador principal coordina y asigna trabajo a procesadores secundarios.
        
    - Los secundarios pueden estar dedicados a tareas específicas (por ejemplo, manejo de E/S).
        
    - Simplicidad en control, pero menos flexible.
        
- **Simétrico (SMP)**
    
    - Todos los procesadores son iguales y comparten la misma memoria.
        
    - Pueden ejecutar cualquier tarea.
        
    - Mayor flexibilidad, pero requiere más complejidad en sincronización.
        

---

## **Clusters**

### 1. Concepto

Un **cluster** es un conjunto de computadoras (nodos) que trabajan juntas como si fueran un único sistema.  
Cada nodo tiene:

- Su propia CPU y registros.
    
- Su propia memoria.
    
- Sus propios dispositivos de almacenamiento o conexión a una red de almacenamiento (**SAN**, _Storage Area Network_).
    

---

### 2. Funcionamiento

- Los nodos están conectados por una red de alta velocidad.
    
- El sistema distribuye la carga de trabajo entre los nodos.
    
- En programas concurrentes, un hilo (thread) puede ejecutarse en un nodo y otro hilo en otro nodo distinto.
    
- Si un nodo falla, el resto sigue trabajando (**tolerancia a fallos**), aunque puede reducirse la velocidad.
    

---

### 3. Beneficios

- **Escalabilidad**: se pueden agregar más nodos para aumentar la capacidad de cómputo.
    
- **Tolerancia a fallos**: un fallo en un nodo no detiene todo el sistema.
    
- **Costos optimizados**: se pueden usar servidores estándar conectados.
    
- **Alto rendimiento**: ideal para computación científica, bases de datos distribuidas, big data, etc.
    

---

### 4. Cómo armar un cluster

1. **Hardware**: varios servidores o PCs con conexión de red rápida.
    
2. **Almacenamiento**: opcionalmente, una SAN para que todos accedan a los mismos datos.
    
3. **Software de cluster**: gestiona la distribución de tareas y la sincronización (ej.: Kubernetes, Hadoop, OpenMPI, Pacemaker).
    
4. **Configuración**: definir políticas de balanceo de carga y failover.
    

---


como funciona la memoria virtual

memoria principal + memoria virtual

memoria secundaria + memoria virtual mas grande

Como funciona para que sirva?

La **memoria virtual** funciona como una especie de "ilusión controlada" que le da al sistema operativo la capacidad de hacerle creer a los programas que tienen a su disposición una memoria RAM más grande, continua y privada de lo que realmente existe físicamente.

Voy a desglosarlo en cómo funciona y para qué sirve:

---

## **1. Cómo funciona la memoria virtual**

La memoria virtual combina **memoria principal (RAM)** y **memoria secundaria (disco duro o SSD)** para dar una visión unificada al procesador.

### 🔹 Paso a paso:

1. **Espacio de direcciones virtuales**
    
    - Cada proceso cree que tiene su propio espacio de memoria que empieza en la dirección 0 y puede llegar a un límite muy grande (por ejemplo, 4 GB en sistemas de 32 bits o muchísimo más en 64 bits).
        
    - Estas direcciones son **virtuales**, no coinciden con la RAM física real.
        
2. **Paginación (Paging)**
    
    - El sistema divide la memoria en bloques llamados **páginas** (típicamente de 4 KB).
        
    - Cada página virtual puede estar:
        
        - En **RAM física** (rápido acceso)
            
        - O en **almacenamiento secundario** (archivo de intercambio o _swap_).
            
3. **MMU (Unidad de Gestión de Memoria)**
    
    - Hardware que traduce direcciones virtuales a direcciones físicas usando una **tabla de páginas**.
        
    - Si la página que necesita el programa no está en RAM, ocurre un **page fault**.
        
4. **Intercambio (Swapping)**
    
    - Cuando hay un _page fault_, el sistema trae la página requerida desde el disco a la RAM, y si es necesario, guarda una página menos usada de la RAM al disco (_swap out_).
        

---

## **2. Para qué sirve**

- **Aumentar el espacio de memoria disponible**  
    Permite ejecutar programas más grandes que la RAM física.
    
- **Aislar procesos**  
    Un programa no puede acceder directamente a la memoria de otro, lo que aumenta la seguridad y estabilidad.
    
- **Protección de memoria**  
    Evita que un error en un programa corrompa la memoria de todo el sistema.
    
- **Eficiencia**  
    Se cargan en RAM solo las partes del programa que realmente se usan (_carga bajo demanda_).
    
- **Multiprogramación**  
    Permite que múltiples procesos coexistan en la RAM, con parte de sus datos en disco.
    

---

📌 **Ejemplo simple**  
Imagina que tu computadora tiene **8 GB de RAM** pero el sistema operativo permite que los programas crean que hay **32 GB** gracias a que usa **24 GB de espacio en disco** como _swap_.  
Esto funciona bien mientras el sistema no abuse del disco, porque el disco es **miles de veces más lento** que la RAM.

---

Si quieres, te puedo hacer un **diagrama visual** que muestre el flujo: _dirección virtual → tabla de páginas → RAM → swap_.  
Así quedaría muy claro cómo interactúa todo.

La **memoria virtual** es una técnica que usa el sistema operativo para simular que hay más memoria RAM de la que físicamente existe, combinando la **memoria principal (RAM)** con parte de la **memoria secundaria** (normalmente el disco duro o SSD).

---

## 📌 ¿Qué es exactamente?

Es una **abstracción** que permite que cada programa crea que tiene a su disposición un espacio de direcciones de memoria continuo y muy grande, aunque físicamente:

- La RAM sea más pequeña.
    
- Los datos estén repartidos entre RAM y disco.
    

---

## ⚙️ ¿Cómo funciona?

1. **Direcciones lógicas vs físicas**
    
    - El programa no trabaja con direcciones reales de memoria, sino con **direcciones virtuales**.
        
    - El sistema operativo y la **MMU** (Unidad de Gestión de Memoria) las traducen a direcciones físicas reales.
        
2. **Paginación o segmentación**
    
    - La memoria virtual se divide en **páginas** (bloques de tamaño fijo, por ejemplo 4 KB).
        
    - Cuando una página no está en RAM, se guarda en un **archivo de intercambio** (_swap file_ o _pagefile_) en el disco.
        
3. **Carga bajo demanda**
    
    - Si un programa necesita datos que están en disco, el sistema operativo los trae a la RAM (esto se llama **page fault**).
        
4. **Liberación de RAM**
    
    - Si la RAM se llena, páginas menos usadas se envían al disco para liberar espacio para otras.
        

---

## 🎯 ¿Para qué sirve?

- **Ejecutar programas más grandes** que la memoria física disponible.
    
- **Tener más programas abiertos** al mismo tiempo sin que el sistema se quede sin RAM.
    
- **Aislar procesos**: cada uno cree que tiene su propio espacio de memoria.
    
- **Protección de memoria**: evita que un programa interfiera con otro o con el sistema operativo.
    

---

💡 Ejemplo rápido:  
Si tienes **8 GB de RAM** y activas memoria virtual con **16 GB de swap**, el sistema podría manejar **hasta 24 GB de direcciones virtuales** (aunque la parte que está en disco será más lenta que la RAM).

---

interrupciones
Interrupciones (software) = exceptions o traps
instrucciones (privilegiadas) sólo pueden ser ejecutadas en modo privilegiado.
todo procesador, tiene un bit de modo. modo root, supervisor, privilegiado, y si esta en 0 esta en modo usuario.


---

## **Interrupciones**

Son señales que **alteran el flujo normal de ejecución** de un procesador para que atienda un evento específico.  
Al ocurrir, el CPU **detiene** la ejecución actual, guarda el estado y salta a una **rutina de servicio** para manejar ese evento.

---

### **Tipos principales**

1. **Interrupciones de hardware**
    
    - Provienen de dispositivos externos al procesador.
        
    - Ejemplos:
        
        - Teclado presionado.
            
        - Llega un paquete de red.
            
        - Fin de lectura/escritura de disco.
            
    - Asíncronas respecto al CPU.
        
2. **Interrupciones de software**
    
    - Generadas por el propio CPU o por instrucciones especiales.
        
    - Dos subtipos importantes:
        
        - **Exceptions** → Ocurren cuando algo sale mal durante la ejecución (ej. división por cero, acceso inválido a memoria).
            
        - **Traps** → Usadas para llamar explícitamente a rutinas del sistema operativo (ej. llamadas al sistema, `syscall`).
            
    - Son síncronas respecto a la ejecución del programa.
        

---

## **Instrucciones privilegiadas**

- Son instrucciones que **solo el sistema operativo** puede ejecutar.
    
- Ejemplos:
    
    - Configurar la MMU (unidad de gestión de memoria).
        
    - Cambiar registros de control.
        
    - Apagar o reiniciar el sistema.
        
- La razón es **seguridad y estabilidad**: si un programa de usuario pudiera usarlas libremente, podría bloquear el sistema o acceder a recursos no autorizados.
    

---

## **Modos del procesador**

El procesador tiene **al menos dos modos** para distinguir si está ejecutando código del sistema operativo o de usuario:

|**Modo**|**Bit de Modo**|**Nombre común**|**Acceso**|
|---|---|---|---|
|Privilegiado|1 (o ON)|_Kernel mode_, _supervisor mode_, _root mode_|Puede ejecutar **todas** las instrucciones (incluyendo privilegiadas).|
|Usuario|0 (o OFF)|_User mode_|Puede ejecutar **solo** instrucciones seguras. Las privilegiadas generan una excepción.|

---

## **Ciclo típico con interrupción**

1. CPU ejecuta instrucciones en modo usuario.
    
2. Ocurre una **interrupción** (hardware) o **trap** (software).
    
3. El CPU:
    
    - Guarda el estado actual (program counter, registros).
        
    - Cambia a **modo privilegiado**.
        
    - Salta a la rutina de manejo correspondiente.
        
4. El sistema operativo atiende la interrupción.
    
5. Se restaura el estado y se vuelve al modo usuario.
    

---

💡 En resumen:

- Las **interrupciones** permiten al CPU responder a eventos sin estar verificando constantemente si pasaron.
    
- Los **modos de operación** son un mecanismo de seguridad para que solo el SO maneje recursos críticos.
    
- Las **instrucciones privilegiadas** son las herramientas que solo el kernel puede usar.
    

---

repertorio del cpu, tiene asociada a si mismas, cada una de ellas, el modo que las permite.
hay algunas que es para ambas, pero otras solo se ejecutan en un modo especifico.

en una primera instancia, podemos decir que las instrucciones que ejecuta el sistema op corren en sistemas privilegiados, el procesador tiene que tener el bit de modo en privilegiado, sino, esta en modo usuario, y el usuario quiere usar una que es privilegiada, debería darte error. para admitir la ejecución de la instrucción.


Exacto, lo que describes es el mecanismo de **protección de modos del CPU** para garantizar que un usuario o programa no pueda ejecutar instrucciones críticas sin pasar por el sistema operativo.

Te lo explico ordenado:

---

### **1. Modos de ejecución del CPU**

- **Modo privilegiado / supervisor / kernel**:  
    Permite ejecutar **todas** las instrucciones, incluidas las **privilegiadas** (acceso directo a hardware, control de interrupciones, manejo de memoria, etc.).
    
- **Modo usuario**:  
    Sólo permite ejecutar instrucciones seguras. Si intenta ejecutar una instrucción privilegiada → genera **trampa (trap)** o **exception**, y el control pasa al sistema operativo.
    

El **bit de modo** en el registro de estado del procesador indica en qué modo está:

- `1` → Modo kernel (privilegiado)
    
- `0` → Modo usuario (no privilegiado)  
    _(El valor exacto puede variar según la arquitectura, pero la idea es esa.)_
    

---

### **2. Repertorio de instrucciones y privilegios**

Cada instrucción en el set del CPU tiene un nivel:

- **Instrucciones para ambos modos**: operaciones aritméticas, lógicas, carga/almacenamiento de datos en memoria de usuario, saltos, etc.
    
- **Instrucciones privilegiadas**: manipular registros de control, cambiar mapeo de memoria virtual, habilitar/deshabilitar interrupciones, acceso directo a dispositivos de E/S.
    

---

### **3. Ejecución de instrucciones privilegiadas**

1. El CPU está en **modo usuario**.
    
2. El programa intenta ejecutar una instrucción privilegiada.
    
3. El **hardware del CPU** detecta que el bit de modo ≠ privilegiado.
    
4. Genera **exception** → salta al sistema operativo.
    
5. El SO decide si la instrucción se permite (por ejemplo, a través de una llamada al sistema) o se deniega.
    

---

💡 En resumen:  
Esto es una medida de **seguridad y estabilidad**. Sin ella, cualquier programa podría:

- Apagar el sistema.
    
- Reescribir memoria de otro proceso.
    
- Manipular el hardware directamente.
    

---

Algunas funciones del SO:

●Administración de procesos (programas en ejecución)
●Administración de la memoria principal
●Administración del almacenamiento secundario
●Administración del subsistema de E/S
●Protección y seguridad

Perfecto, te hago un resumen ordenado y con un poco más de detalle, basado en **Tanenbaum**, **Silberschatz** y **Patterson & Hennessy**:

---

## **Funciones del Sistema Operativo (SO)**

El **sistema operativo** actúa como intermediario entre el hardware y los programas de usuario, gestionando los recursos del sistema y proporcionando servicios esenciales.

---

### 1. **Administración de procesos**

- Gestiona la **creación, ejecución y finalización** de procesos.
    
- Implementa **planificación (scheduling)** para decidir qué proceso se ejecuta y por cuánto tiempo.
    
- Maneja la **concurrencia** y la sincronización de procesos o hilos.
    

> _Referencia:_ Silberschatz, Galvin & Gagne, _Operating System Concepts_, Cap. 3.

---

### 2. **Administración de memoria principal**

- Controla el **asignamiento de memoria a procesos**.
    
- Implementa **memoria virtual**, **paginación** y **segmentación** para optimizar el uso de la RAM.
    
- Protege a los procesos unos de otros mediante límites de memoria.
    

> _Referencia:_ Tanenbaum, _Modern Operating Systems_, Cap. 3.  
> _Referencia:_ Patterson & Hennessy, _Computer Organization and Design_, Cap. 5.

---

### 3. **Administración del almacenamiento secundario**

- Maneja discos, SSD y otros dispositivos de almacenamiento.
    
- Se encarga de **sistemas de archivos**, directorios, lectura/escritura de bloques y control de acceso.
    
- Implementa **políticas de almacenamiento y cache de disco** para mejorar el rendimiento.
    

> _Referencia:_ Silberschatz, Cap. 11.

---

### 4. **Administración del subsistema de E/S**

- Coordina la comunicación entre **dispositivos de entrada/salida** y la CPU.
    
- Utiliza **buffers**, **colas** y controladores de dispositivos.
    
- Puede emplear **DMA (Direct Memory Access)** para mejorar la eficiencia de transferencias sin intervención constante del CPU.
    

> _Referencia:_ Tanenbaum, Cap. 5.

---

### 5. **Protección y seguridad**

- Garantiza que **un proceso no interfiera con otro** ni acceda a recursos sin autorización.
    
- Controla permisos de archivos, memoria y dispositivos.
    
- Administra **usuarios, autenticación y privilegios**.
    

> _Referencia:_ Silberschatz, Cap. 14.

---

En resumen, el SO **orquesta todos los recursos del sistema** para que múltiples programas puedan ejecutarse de manera segura y eficiente, aprovechando al máximo el hardware disponible.

---

Los procesos requieren recursos para realizar lo que deben realizar
La terminación de un proceso debe permitir recuperar los recursos reusables.
recursos reusables, y recursos que no.

Exacto, esto forma parte de la **gestión de recursos** en un sistema operativo. Te lo explico con detalle y referencias:

---

## **Recursos en un sistema operativo**

Un **proceso** necesita distintos **recursos** para ejecutarse correctamente, como CPU, memoria, dispositivos de E/S o archivos.  
El SO se encarga de **asignar**, **controlar** y **recuperar** esos recursos de manera eficiente.

---

### 1. **Tipos de recursos según reutilización**

#### a) **Recursos reutilizables**

- Son recursos que **no se consumen al usarse**, sino que pueden volver a ser utilizados por otros procesos después de ser liberados.
    
- Ejemplos:
    
    - **CPU**: un proceso la usa durante su ejecución, luego otro proceso puede usarla.
        
    - **Memoria principal**: después de terminar el proceso, la memoria se libera para otros procesos.
        
    - **Dispositivos de E/S**: impresoras, discos, etc., pueden ser usados por varios procesos, pero solo uno a la vez.
        
- Gestión típica: **asignación dinámica**, **colas de espera**, **señales de disponibilidad**.
    

> _Referencia:_ Silberschatz, Galvin & Gagne, _Operating System Concepts_, 10th ed., Cap. 6.

#### b) **Recursos consumibles o no reutilizables**

- Son recursos que se **agotan al usarse** y no pueden recuperarse para otro proceso.
    
- Ejemplos:
    
    - Archivos temporales que se eliminan tras su uso.
        
    - Tokens o créditos contables que representan unidades limitadas de algo.
        
    - Algunos tipos de datos de un flujo de información que se consumen al ser leídos.
        
- Gestión típica: **control de acceso estricto**, **seguimiento de consumo**.
    

> _Referencia:_ Tanenbaum, _Modern Operating Systems_, 4th ed., Cap. 3.

---

### 2. **Recuperación de recursos**

Cuando un proceso termina:

- El SO debe liberar **todos los recursos reutilizables** asignados a ese proceso.
    
- Para los recursos consumibles, simplemente se da por hecho que **ya se consumieron** y no pueden reutilizarse.
    
- Esto evita **fugas de recursos** (_resource leaks_) y mantiene el sistema estable.
    

---

cuando el sistema operativo tiene que administrar:

● Crear y eliminar procesos del usuario y del sistema
● Suspender y rehabilitar procesos
● Suministrar mecanismos para la sincronización de procesos
● Suministrar mecanismos para la comunicación entre procesos
● Suministrar mecanismos para el manejo de interbloqueo (deadlock)

controlador, ya es un software, pero para el pendrive necesita otro controlador, es software.
mas arriba me dan mas
abrir dispositivo A usa el archivo tal y cerrar el dispositivo.
normalmente guardo datos, en forma de archivos.

Administración del Almacenamiento

●El SO debe suministrar una visión lógica uniforme del
almacenamiento

●Ocultar características físicas y mostrar unidades lógicas-de almacenamiento (files)

●Los medios de almacenamiento son muy diversos, con
propiedades distintas

●Administración de archivos (files)

●Usualmente organizados en directorios

●Debe determinarse quien puede acceder y para qué

●Las actividades del SO incluyen

●Crear y borrar archivos y directorios

●Suministrar primitivas para manipular archivos y directorios

●Mapear los archivos en la memoria secundaria

Perfecto, voy a organizar toda esa información en un **resumen claro sobre la administración de procesos y de almacenamiento** según los conceptos de **Tanenbaum** y **Silberschatz**, usando el lenguaje académico típico de sistemas operativos.

---

## **Administración de Procesos**

El **sistema operativo (SO)** es responsable de gestionar los **procesos**, tanto de usuario como del propio sistema, asegurando que los recursos se usen de forma eficiente y segura.

### Funciones principales:

1. **Creación y eliminación de procesos**
    
    - El SO puede iniciar procesos nuevos según solicitudes del usuario o del sistema.
        
    - Al finalizar un proceso, el SO debe liberar los recursos que el proceso utilizó.
        
2. **Suspender y reanudar procesos**
    
    - Permite **detener temporalmente** un proceso para liberar CPU o recursos y **reanudarlo** posteriormente.
        
3. **Sincronización de procesos**
    
    - Proporciona mecanismos para coordinar procesos que **comparten recursos**, evitando conflictos y condiciones de carrera.
        
4. **Comunicación entre procesos**
    
    - Incluye **pipes, colas de mensajes, memoria compartida**, etc., para que los procesos intercambien información de manera segura.
        
5. **Manejo de interbloqueo (deadlock)**
    
    - Detecta y evita situaciones donde dos o más procesos quedan **bloqueados esperando recursos mutuamente**.
        

> _Referencia:_ Silberschatz, Galvin & Gagne, _Operating System Concepts_, 10th ed., Cap. 3–6.  
> _Referencia:_ Tanenbaum, _Modern Operating Systems_, 4th ed., Cap. 3–4.

---

## **Administración del Almacenamiento Secundario**

El SO debe proporcionar una **visión lógica uniforme** del almacenamiento, ocultando la complejidad del hardware y facilitando la gestión de datos.

### Principales funciones:

1. **Organización de almacenamiento**
    
    - Oculta la **estructura física** de los dispositivos (sectores, pistas, cilindros).
        
    - Presenta **unidades lógicas**, los archivos (_files_), que son manipulables por los usuarios y programas.
        
2. **Administración de archivos y directorios**
    
    - Crear, borrar y manipular archivos y directorios.
        
    - Organizar archivos en **jerarquías lógicas** (directorios y subdirectorios).
        
    - Determinar **permisos de acceso**: quién puede leer, escribir o ejecutar.
        
3. **Mapeo en memoria secundaria**
    
    - Asocia los archivos a **espacios físicos en disco o almacenamiento externo**.
        
    - Permite al SO usar técnicas de **caching y buffering** para mejorar el rendimiento.
        
4. **Gestión de dispositivos**
    
    - Cada dispositivo (pendrive, disco, impresora) tiene un **controlador específico** (software).
        
    - Operaciones típicas:
        
        - Abrir el dispositivo → abrir el archivo o recurso correspondiente.
            
        - Leer/escribir datos → manipulación de los bloques físicos mediante el controlador.
            
        - Cerrar el dispositivo → liberar recursos.
            

> _Referencia:_ Silberschatz et al., Cap. 11–12.  
> _Referencia:_ Tanenbaum, Cap. 5.

---

para hacer un uso mas eficiente, del recurso al dispositivo periférico
por eso es importante buscar el eso

buen rendimiento, uso eficiente del uso de almacenamiento masivo.
lo que hago es, llegan los requerimientos y pongo los procesos en una lista.
planificación. de acuerdo a las políticas de orden.

Exacto, lo que estás describiendo corresponde a la **planificación de recursos y de dispositivos de E/S** en un sistema operativo, que busca **maximizar eficiencia y rendimiento**. Te lo explico ordenadamente y con referencias:

---

## **Administración de Dispositivos y Planificación de E/S**

### 1. **Objetivo**

El SO gestiona dispositivos de E/S (discos, impresoras, redes, etc.) para que varios procesos puedan compartirlos de manera eficiente y sin conflictos.

- Garantiza **uso óptimo de recursos**.
    
- Mejora **rendimiento general** del sistema.
    
- Evita que procesos se bloqueen innecesariamente.
    

---

### 2. **Cómo se logra**

1. **Colas de solicitudes**
    
    - Las peticiones de E/S de todos los procesos se colocan en **listas o colas**.
        
    - Cada solicitud espera su turno según la política de planificación.
        
2. **Políticas de planificación**
    
    - **FIFO (First-In-First-Out)**: atiende solicitudes en orden de llegada.
        
    - **SSTF (Shortest Seek Time First)**: da prioridad a la solicitud más cercana en disco (minimiza tiempo de búsqueda).
        
    - **SCAN / C-SCAN**: el cabezal del disco recorre en una dirección atendiendo solicitudes y luego regresa.
        
    - **Prioridades**: algunas solicitudes críticas pueden adelantarse a otras.
        
3. **Buffers y caching**
    
    - Se utilizan **buffers** para almacenar temporalmente los datos que van hacia o desde el dispositivo.
        
    - Permite que el CPU y los procesos no esperen a que termine la operación física.
        
4. **Objetivo final**
    
    - **Eficiencia del dispositivo**: que el hardware trabaje lo menos posible en vacío.
        
    - **Equidad**: que todos los procesos tengan acceso a los dispositivos.
        
    - **Rendimiento del sistema**: menor tiempo de respuesta y mayor throughput.
        

---

### 3. **Referencias**

- Silberschatz, Galvin & Gagne, _Operating System Concepts_, Cap. 11–12.
    
- Tanenbaum, _Modern Operating Systems_, Cap. 5.
    
- Patterson & Hennessy, _Computer Organization and Design_, Cap. 5 (para acceso a discos y E/S).
    

---

Planificación de disco.
con una capa de soft, toma todos los requerimiento, planifica y aplica. para resolver todos los requerimientos.

Exacto, lo que estás describiendo es la **planificación de disco** (_disk scheduling_) en un sistema operativo. Te lo resumo de forma organizada y con referencias:

---

## **Planificación de Disco**

### 1. **Concepto**

- Los discos son **dispositivos de almacenamiento relativamente lentos** comparados con la CPU y la RAM.
    
- Para mejorar eficiencia, el SO utiliza una **capa de software** que:
    
    1. Recibe **todos los requerimientos de lectura/escritura** de los procesos.
        
    2. Los organiza según **políticas de planificación**.
        
    3. Ejecuta los requerimientos de manera **optimizada**, reduciendo tiempo de búsqueda y esperando lo menos posible.
        

> _Referencia:_ Silberschatz, Galvin & Gagne, _Operating System Concepts_, Cap. 11.  
> _Referencia:_ Tanenbaum, _Modern Operating Systems_, Cap. 5.

---

### 2. **Funcionamiento**

1. **Recepción de solicitudes**
    
    - Todos los procesos que necesitan acceder al disco generan **peticiones de E/S**.
        
    - Estas solicitudes se colocan en una **cola de disco**.
        
2. **Planificación**
    
    - El **software del SO** analiza la cola y decide el **orden de ejecución** según la política elegida.
        
    - Ejemplos de políticas:
        
        - **FIFO (First-In-First-Out)**: atender en orden de llegada.
            
        - **SSTF (Shortest Seek Time First)**: atender la solicitud más cercana al cabezal.
            
        - **SCAN / C-SCAN**: el cabezal recorre el disco de un extremo al otro, atendiendo solicitudes en el camino.
            
        - **Prioridad**: solicitudes críticas se atienden antes que otras.
            
3. **Aplicación de las solicitudes**
    
    - El SO envía las órdenes al **controlador del disco**, que realiza la operación física de lectura/escritura.
        
    - El **buffer** permite que la CPU y el proceso no tengan que esperar a que la operación física termine.
        

---

### 3. **Objetivo**

- **Maximizar eficiencia del disco**: minimizar movimientos del cabezal y tiempos de espera.
    
- **Equidad**: que todos los procesos puedan acceder al disco.
    
- **Mejor rendimiento del sistema**: menor tiempo de respuesta y mayor throughput.
    

---

Subsistema de I/O
Administrar la memoria de I/O

	Buffering: almacenamiento temporario de datos mientras están siendo transferidos
	Caching: almacenamiento temporario de datos en un almacenamiento más rápido
	Spooling: simulacion de perifericos en linea.
	Suministrar drivers para dispositivos específicos

Perfecto, podemos organizar toda esta información dentro del concepto de **Subsistema de E/S (I/O)** según la literatura de Tanenbaum y Silberschatz:

---

## **Subsistema de Entrada/Salida (I/O)**

El **subsistema de I/O** del sistema operativo se encarga de **administrar la comunicación entre los procesos y los dispositivos periféricos**, de manera eficiente y segura. Esto incluye la **gestión de memoria de I/O**, controladores y mecanismos de optimización.

---

### 1. **Administración de la memoria de I/O**

Para optimizar la transferencia de datos entre **CPU y dispositivos**, se utilizan varias técnicas:

#### a) **Buffering**

- Almacena temporalmente los datos en memoria mientras se transfieren entre el dispositivo y la CPU.
    
- Permite que los procesos continúen ejecutándose sin esperar a que el dispositivo complete la operación.
    
- Ejemplo: almacenar temporalmente datos que se van a imprimir.
    

> _Referencia:_ Tanenbaum, _Modern Operating Systems_, Cap. 5.

#### b) **Caching**

- Almacena temporalmente los datos en un **almacenamiento más rápido**, típicamente RAM, para acelerar futuras operaciones.
    
- Evita accesos repetidos a dispositivos lentos como discos.
    
- Ejemplo: almacenar bloques de disco leídos recientemente en memoria.
    

> _Referencia:_ Silberschatz et al., _Operating System Concepts_, Cap. 11.

#### c) **Spooling**

- Simula dispositivos en línea mediante **colocación de trabajos en una cola** para su ejecución posterior.
    
- Muy usado en impresoras: los trabajos se almacenan en disco y se procesan en orden sin bloquear a los programas que los enviaron.
    

> _Referencia:_ Tanenbaum, Cap. 5.

---

### 2. **Drivers de dispositivos**

- Cada dispositivo (pendrive, disco, impresora, tarjeta de red) tiene un **driver específico**: un módulo de software que traduce las solicitudes genéricas del SO en comandos que el dispositivo puede entender.
    
- El SO suministra una **interfaz uniforme**, de modo que los programas **no necesiten conocer la implementación física** del dispositivo.
    

---

### 3. **Objetivos del Subsistema de I/O**

- Optimizar el **rendimiento de los dispositivos**.
    
- Permitir **concurrencia**: varios procesos pueden solicitar E/S sin bloquearse mutuamente.
    
- Abstraer la **heterogeneidad de hardware**, ofreciendo una visión uniforme al resto del sistema.
    

---

Protección: cualquier mecanismo que controle el acceso de procesos o usuarios a los recursos
● Seguridad: defensa del sistema contra ataques internos y externos
● Los SO deben distinguir entre usuarios para determinar quién puede hacer qué
● Identificación de usuarios (user IDs)
● Asociación del user ID con archivos y procesos para determinar el control de acceso
● Identificación de grupos

protección que nadie acceda a donde no se debe acceder.
seguridad, que un ataque no rompa algo indebido.



---

## **Protección y Seguridad en Sistemas Operativos**

El SO debe garantizar que los recursos del sistema se utilicen de manera **segura y controlada**, distinguiendo entre **protección** y **seguridad**.

---

### 1. **Protección**

- Es cualquier **mecanismo que controla el acceso de procesos o usuarios a los recursos** del sistema.
    
- Su objetivo es **evitar accesos indebidos** a memoria, archivos, dispositivos y procesos.
    
- Ejemplos:
    
    - Un proceso no puede modificar la memoria de otro proceso.
        
    - Archivos solo accesibles por ciertos usuarios o grupos.
        
- Implementación típica:
    
    - **User IDs**: identificadores de usuario.
        
    - **Asociación de permisos** con archivos y procesos.
        
    - **Grupos de usuarios**: permiten aplicar políticas de acceso colectivas.
        

> _Referencia:_ Silberschatz, Galvin & Gagne, _Operating System Concepts_, Cap. 14.  
> _Referencia:_ Tanenbaum, _Modern Operating Systems_, Cap. 5.

---

### 2. **Seguridad**

- Es la **defensa del sistema contra ataques internos o externos**.
    
- Busca proteger al sistema de **usuarios maliciosos, virus, malware o intrusiones**.
    
- Incluye:
    
    - Autenticación de usuarios.
        
    - Control de acceso a recursos.
        
    - Prevención de intrusiones y auditoría de actividades.
        
    - Encriptación de información sensible.
        

> _Referencia:_ Silberschatz et al., Cap. 14.

---

### 3. **Distinción clave**

|Concepto|Objetivo|Ejemplos|
|---|---|---|
|Protección|Evitar accesos indebidos de **usuarios y procesos legítimos**|Permisos de lectura/escritura/ejecución, bit de modo CPU, listas de control de acceso (ACL)|
|Seguridad|Evitar **ataques maliciosos** que comprometan el sistema|Firewalls, autenticación, cifrado, detección de intrusos|

---

💡 **Resumiendo en palabras simples**:

- **Protección** → “Que nadie acceda donde no debe” (interno).
    
- **Seguridad** → “Que un ataque no rompa algo indebido” (externo o malicioso).
    

---

Sistemas operativos para clusters.
presento al usuario una unica computadora.
pero son varias pcs, en realidad.
DOS Distributes OS.


Sistemas de tiempo real: recibe input de un ambiente, y debe responder en parametros muy precisos de tiempo.

Perfecto, vamos a organizar estos conceptos usando referencias de **Tanenbaum** y **Silberschatz**:

---

## **1. Sistemas Operativos para Clusters**

Un **cluster** es un conjunto de computadoras independientes que trabajan juntas para **presentar al usuario la apariencia de una sola máquina**.

### Características:

- Los usuarios ven **una única interfaz**, aunque los procesos puedan ejecutarse en distintos nodos.
    
- Cada nodo tiene su **CPU, memoria y dispositivos**, pero el SO de cluster se encarga de **coordinar recursos y procesos**.
    
- Ventajas:
    
    - **Tolerancia a fallos**: si un nodo falla, otros nodos pueden continuar ejecutando los procesos.
        
    - **Paralelismo real**: múltiples procesos o threads pueden ejecutarse simultáneamente en distintos nodos.
        
    - **Escalabilidad**: se pueden añadir más nodos para aumentar capacidad.
        

### Tipos de sistemas de clusters:

1. **Sistemas distribuidos (Distributed OS)**
    
    - Coordinan procesos y recursos a través de la red.
        
    - Gestionan comunicación, sincronización y acceso a memoria distribuida.
        
    - Ejemplos: **Amoeba, LOCUS, MOSIX**.
        

> _Referencia:_ Tanenbaum, _Modern Operating Systems_, Cap. 3.

---

## **2. Sistemas de Tiempo Real (Real-Time OS, RTOS)**

Un **sistema de tiempo real** es aquel que debe responder a eventos del entorno **dentro de límites de tiempo estrictos**.

### Características:

- Entrada de datos del **ambiente físico** (sensores, señales).
    
- Salida debe ser generada en **tiempo predecible y garantizado**.
    
- Clasificación:
    
    - **Hard real-time**: el incumplimiento del plazo puede causar fallo crítico.
        
    - **Soft real-time**: los plazos son deseables, pero no críticos.
        
- Usos típicos:
    
    - Control de maquinaria industrial.
        
    - Sistemas de aviación o automoción.
        
    - Dispositivos médicos críticos.
        

> _Referencia:_ Silberschatz et al., _Operating System Concepts_, Cap. 1–2.  
> _Referencia:_ Tanenbaum, Cap. 5.

---

💡 **Resumiendo**:

- **Cluster OS** → varias PCs funcionando como una sola, optimizando recursos y tolerancia a fallos.
    
- **RTOS** → el SO debe garantizar **respuestas precisas en tiempo**, fundamental para entornos críticos.
    

---

**Finalizado el documento de "clase 1".**