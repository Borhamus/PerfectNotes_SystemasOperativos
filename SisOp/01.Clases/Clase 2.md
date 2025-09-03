"Clase previa": [[Clase 1]]

Martes 12 de agosto de 2025 - Con Luis, es practica

* Verificación de disco


varias políticas:
preventivo, prentivo. variantes

quantum, eficiencia(midiendo el tiempo de servicio).

diagramas de gantt, tiempo de procesos, de fin.

hacer el integrador o morir.
entregable en modo ejecutable, o en docker.
planificación, administración de memoria, planificación de disco.

métodos de acceso, organización de archivos.

---

[[Proceso]]
## **Definición de proceso**

Según **Silberschatz, Galvin & Gagne** y **Tanenbaum**, un **proceso** es:

> “Un programa en ejecución, junto con su estado actual y todos los recursos asociados que necesita para llevar a cabo su tarea.”

Un **programa** es un conjunto estático de instrucciones almacenadas en algún medio.  
Un **proceso** es **dinámico**: incluye la ejecución actual del programa, los valores de variables, el contador de programa, los registros de CPU, las pilas y el espacio de memoria asignado.

---

### 🔍 **Componentes de un proceso**

En un modelo típico, un proceso contiene:

1. **Código** (_text segment_): instrucciones del programa.
    
2. **Datos estáticos** (_data segment_): variables globales y estáticas.
    
3. **Pila** (_stack_): variables locales, direcciones de retorno y control de llamadas a funciones.
    
4. **Montículo** (_heap_): memoria dinámica solicitada en tiempo de ejecución.
    
5. **Contexto de CPU**: valores de registros, contador de programa, banderas, etc.
    
6. **Recursos asociados**: archivos abiertos, dispositivos asignados, permisos, etc.
    

---

### 📌 Relación con paginación

- En sistemas con **gestión de memoria por paginación**, el espacio de direcciones de un proceso se divide en **páginas** (unidades lógicas) que se asignan a **marcos** (_frames_) de la memoria física.
    
- Esto es **una técnica de implementación** de la memoria virtual, no parte esencial de la definición de proceso.
    
- El proceso “se ve” como un bloque de memoria continua para el programador, pero internamente el SO lo maneja por páginas o segmentos según el esquema elegido.
    

---

💡 Resumen rápido para examen:

> Un **proceso** es un programa en ejecución más su estado y recursos asociados. Es la unidad básica de trabajo del SO, que gestiona su ejecución y memoria. En sistemas con memoria virtual, el espacio de direcciones del proceso puede dividirse en páginas que el SO mapea a la memoria física.

---
paginación con segmentación, combinaciones, tablas de paginas invertidas.
Memoria virtual, que es el concepto de swaping.

## **[[Paginación y Segmentación]]**
## 📚 **1. Paginación con segmentación**

La paginación y la segmentación son dos técnicas distintas de gestión de memoria.  
En **paginación con segmentación** se combinan para aprovechar ventajas de ambas:

- **Paginación**: divide la memoria física en marcos de tamaño fijo, y la memoria lógica en páginas del mismo tamaño.
    
- **Segmentación**: divide el espacio lógico en segmentos que representan unidades lógicas de un programa (código, datos, pila).
    

💡 **Cómo se combinan**

- Cada **segmento** se divide internamente en **páginas**.
    
- Cada segmento tiene su **tabla de páginas** correspondiente.
    
- La dirección lógica se especifica como:
    
    ```
    (número de segmento, número de página, desplazamiento)
    ```
    
- El sistema usa la **tabla de segmentos** para localizar la **tabla de páginas** correcta, y luego la tabla de páginas para encontrar el marco físico.
    

**Ventajas**:

- Flexibilidad lógica de segmentación + control simple de fragmentación de la paginación.
    
- Permite protección y compartición a nivel de segmento.
    

---

## 📚 **2. Tablas de páginas invertidas**

- En paginación tradicional, cada proceso tiene su propia tabla de páginas, lo que consume mucha memoria si el espacio de direcciones es grande.
    
- En una **tabla de páginas invertida**, hay **una sola tabla global para todo el sistema**, con **una entrada por cada marco de memoria física**, no por cada página lógica.
    
- Cada entrada indica **qué página de qué proceso** está ocupando ese marco.
    
- Para traducir una dirección lógica → física:
    
    1. Se busca en la tabla invertida (normalmente usando un _hash_) el marco que corresponde a `(id_proceso, num_página)`.
        
    2. Se obtiene el marco físico y se suma el desplazamiento.
        

**Ventajas**: ahorro de memoria en la tabla.  
**Desventaja**: traducción más lenta, requiere búsquedas y TLB eficientes.

---

## 📚 **3. Memoria virtual**

- **Concepto**: La memoria virtual es una abstracción que permite a un proceso tener un espacio de direcciones lógico mucho mayor que la memoria física real.
    
- Permite que los programas se carguen parcialmente en memoria y el resto permanezca en almacenamiento secundario, trayendo las partes necesarias bajo demanda.
    
- Se implementa mediante **paginación bajo demanda** o **segmentación bajo demanda**.
    

**Objetivos**:

1. Ejecutar programas más grandes que la memoria física.
    
2. Aislar procesos entre sí (protección).
    
3. Optimizar uso de memoria física.
    

---

## 📚 **4. Swapping**

- **Definición**: Técnica donde **un proceso completo** se copia temporalmente desde la memoria principal a almacenamiento secundario (por ejemplo, disco), para liberar memoria para otros procesos.
    
- Cuando el proceso necesita ejecutarse nuevamente, se trae de vuelta a memoria.
    
- Puede ocurrir:
    
    - **Total**: el proceso entero se mueve.
        
    - **Parcial**: solo algunas partes (páginas o segmentos).
        
- El área de disco usada para esto se llama **área de swapping** o _swap space_.
    

**Diferencia clave con paginación bajo demanda**:

- En _swapping_ tradicional se mueven bloques grandes (todo el proceso).
    
- En _paginación bajo demanda_ solo se cargan páginas necesarias.
    

---

💡 Si querés, puedo prepararte un **diagrama unificado** con:

- Segmentación con paginación.
    
- Tabla de páginas invertida.
    
- Ciclo de swapping.
    

---

memoria virtual, como funciona.
memoria de intercambio, porque se reserva? que es? que rol cumple?

Te lo explico con teoría de **Sistemas Operativos** de **Silberschatz** y **Tanenbaum**, organizando por conceptos y con el porqué de cada uno.

---

## 📚 **1. Memoria virtual – cómo funciona**

La **memoria virtual** es una técnica que permite que los programas se ejecuten como si tuvieran disponible un espacio de direcciones grande y contiguo, aunque físicamente la memoria RAM sea limitada y no todo el programa esté cargado al mismo tiempo.

**Funcionamiento básico**:

1. **Abstracción**: cada proceso ve un espacio de direcciones lógico propio (por ejemplo, 4 GB en un sistema de 32 bits).
    
2. **Traducción de direcciones**: el hardware de gestión de memoria (MMU) traduce direcciones lógicas a direcciones físicas usando tablas de páginas (o segmentos).
    
3. **Carga bajo demanda**: las partes del programa (páginas o segmentos) se cargan a RAM solo cuando se necesitan (_demand paging_ o _demand segmentation_).
    
4. **Fallos de página**: si una página requerida no está en RAM, se produce un **page fault**. El SO pausa el proceso, trae la página desde almacenamiento secundario y luego continúa la ejecución.
    
5. **Reemplazo de páginas**: si la RAM está llena, el SO elige una página para expulsar (_page replacement_), normalmente usando algoritmos como LRU, FIFO, Clock, etc.
    

**Ventajas**:

- Permite programas más grandes que la memoria física.
    
- Facilita multiprogramación (varios procesos activos a la vez).
    
- Aísla procesos entre sí (protección).
    

---

## 📚 **2. Memoria de intercambio (Swap Space)**

La **memoria de intercambio** o **área de swap** es una zona reservada en un dispositivo de almacenamiento (generalmente un disco duro o SSD) que el sistema operativo utiliza para **almacenar temporalmente datos que no caben en la RAM**.

**¿Por qué se reserva?**

- La RAM es limitada y costosa; el swap actúa como “extensión” de la memoria física.
    
- Al estar predefinida y separada de otras áreas del disco, el SO puede acceder a ella de forma más rápida y predecible que si usara espacio común del sistema de archivos.
    
- Garantiza que siempre habrá un área dedicada para volcar páginas o procesos completos sin competir con otros usos del disco.
    

**¿Qué es exactamente?**

- Puede ser un **archivo especial** en el sistema de archivos o una **partición dedicada**.
    
- Contiene páginas de procesos que han sido expulsadas de la RAM (_paged out_) o procesos enteros en sistemas con _swapping_ total.
    

**Rol en el sistema**:

1. **Almacén temporal** para páginas expulsadas (memoria virtual).
    
2. **Permitir más procesos simultáneos** de lo que cabría solo en RAM.
    
3. **Soporte para hibernación**: en algunos sistemas, el estado completo de la RAM se guarda en el área de swap.
    

---

💡 Resumen de relación:

- **Memoria virtual** → Técnica general para dar a los procesos más espacio del que físicamente existe, usando almacenamiento secundario como respaldo.
    
- **Memoria de intercambio (swap)** → Área física en disco reservada para guardar temporalmente partes de memoria que están fuera de la RAM como parte de la implementación de memoria virtual o _swapping_.
    

---


estados del proceso-
cache L1,L2,L3
 niveles de memoria.
 tamaños de chache, que paginas metemos ahi y como lo manejamos?

Vamos por partes, como si fuera un apunte de examen de Sistemas Operativos + Arquitectura de Computadoras, siguiendo estructura de libro (**Tanenbaum**, **Silberschatz**, **Patterson & Hennessy**).

---

## 📚 **1. Estados del Proceso**

Un proceso, mientras es gestionado por el SO, pasa por distintos **estados** que representan su situación actual de ejecución:

|Estado|Descripción|
|---|---|
|**Nuevo (New)**|El proceso está siendo creado, cargado en memoria y asignando recursos.|
|**Listo (Ready)**|Está en memoria principal, listo para ejecutar, esperando ser despachado por la CPU.|
|**En ejecución (Running)**|Está usando la CPU en ese momento.|
|**Bloqueado/Esperando (Waiting/Blocked)**|Espera un evento externo (por ejemplo, finalización de E/S).|
|**Terminado (Terminated)**|El proceso ha finalizado su ejecución y sus recursos serán liberados.|
|_(Opcional)_ **Suspendido (Suspended)**|El proceso está en memoria secundaria (swap), temporalmente detenido por el SO o el usuario.|

🔍 **Nota**: La transición entre estos estados se maneja mediante **planificación** (scheduling) y **cambio de contexto** (context switch).

---

## 📚 **2. Caché L1, L2, L3 – Niveles de memoria**

En la jerarquía de memoria, las **cachés** son memorias rápidas, pequeñas y costosas ubicadas cerca de la CPU para reducir la latencia de acceso a datos e instrucciones.

- **L1**:
    
    - Integrada en el núcleo del procesador.
        
    - Más rápida y pequeña (generalmente 16 KB – 128 KB por núcleo).
        
    - Puede estar dividida en **L1 de datos (D-cache)** y **L1 de instrucciones (I-cache)**.
        
- **L2**:
    
    - Más grande (256 KB – 2 MB), más lenta que L1 pero más rápida que RAM.
        
    - Puede estar dedicada por núcleo o compartida entre pocos núcleos.
        
- **L3**:
    
    - Más grande (4 MB – 64 MB), más lenta que L2 pero más rápida que RAM.
        
    - Normalmente compartida entre todos los núcleos de un procesador.
        

---

## 📚 **3. Niveles de memoria (Jerarquía)**

De arriba (más rápida y cara) a abajo (más lenta y barata):

1. **Registros** – Nanosegundos – Bytes.
    
2. **Caché L1** – Nanosegundos – KB.
    
3. **Caché L2** – Nanosegundos – MB.
    
4. **Caché L3** – Nanosegundos/microsegundos – MB.
    
5. **RAM** – Decenas de nanosegundos – GB.
    
6. **Swap / SSD / HDD** – Microsegundos a milisegundos – GB/TB.
    
7. **Almacenamiento terciario** (cintas, óptico) – Milisegundos/segundos – TB+.
    

---

## 📚 **4. Tamaños de caché, qué “páginas” metemos y cómo se maneja**

### **Tamaños típicos** (aproximados, dependen de CPU):

- **L1**: 16–128 KB por núcleo.
    
- **L2**: 256 KB – 2 MB por núcleo.
    
- **L3**: 4–64 MB compartidos.
    

### **Qué “metemos” en caché**:

- En realidad no se guardan páginas enteras del sistema operativo, sino **líneas de caché** (cache lines), que suelen medir 32–128 bytes.
    
- Estas líneas contienen datos o instrucciones que la CPU predice que necesitará pronto, según:
    
    - **Localidad temporal**: reutilizar datos usados recientemente.
        
    - **Localidad espacial**: acceder a datos cercanos a los ya usados.
        

### **Cómo se maneja**:

- **Mapeo**: directo, asociativo por conjunto o totalmente asociativo.
    
- **Política de reemplazo**: normalmente _LRU_ (Least Recently Used) o variantes.
    
- **Política de escritura**: _write-through_ (escribir en RAM y caché) o _write-back_ (escribir solo en caché y pasar a RAM cuando se expulsa la línea).
    

---

💡 Resumen clave para examen:

> Estados de proceso → describe su ciclo de vida.  
> Caché L1/L2/L3 → son memorias intermedias cada vez más grandes y lentas.  
> Jerarquía de memoria → organiza velocidad, costo y capacidad.  
> Caché almacena **líneas**, no páginas enteras, y usa políticas de reemplazo/escritura para optimizar rendimiento.

---

Si querés, te puedo armar un **esquema gráfico único** con:

- Estados de proceso.
    
- Jerarquía de memoria.
    
- Flujo de datos de caché y RAM.  


---
discos:
indexada, secuenciada, como va a parar al disco, y políticas de disco.
tiempos de acceso, atención de requerimientos de bloque, 

Te lo organizo con teoría de **Sistemas Operativos** (Silberschatz, Tanenbaum) y un poco de **Organización de Computadoras** para la parte física.

---

## 📚 **1. Métodos de acceso a disco**

Cuando hablamos de _indexada_ y _secuencial_, nos referimos a **cómo están organizados los archivos y cómo se localizan sus bloques**.

### **a) Acceso secuencial**

- Los datos se almacenan en bloques uno tras otro.
    
- Para acceder a un bloque intermedio, se deben leer los anteriores (o conocer la posición exacta).
    
- Ejemplo: cintas magnéticas o ficheros de texto lineales.
    
- Ventaja: simple y eficiente para lecturas completas.
    
- Desventaja: lento para acceso aleatorio.
    

### **b) Acceso indexado**

- Existe una **tabla de índices** (como una tabla de páginas pero para archivos) que almacena las direcciones de cada bloque de datos.
    
- Permite **acceso directo** a cualquier bloque.
    
- Ejemplo: sistema de archivos UNIX con **i-nodos**.
    
- Ventaja: rápido para saltar a datos específicos.
    
- Desventaja: requiere espacio extra para el índice.
    

💡 En discos modernos, incluso un acceso “secuencial” a nivel lógico termina siendo traducido por el **sistema de archivos** y el **controlador de disco** a accesos físicos optimizados.

---

## 📚 **2. Cómo “va a parar” la información al disco**

1. **Aplicación** pide leer/escribir datos.
    
2. **Sistema de archivos** traduce la solicitud a bloques lógicos.
    
3. **Gestor de E/S del SO** convierte esos bloques lógicos en direcciones físicas (cilindro, pista, sector) usando la **estructura del disco**.
    
4. **Controlador de disco** recibe la orden y mueve el brazo (si es HDD) o direcciona la celda (si es SSD).
    
5. Datos pasan por el **buffer del controlador** y luego por el **bus** hasta la RAM.
    

---

## 📚 **3. Políticas de planificación de disco**

Objetivo: minimizar el **tiempo medio de acceso**.

- **FCFS (First Come, First Served)**: atiende en el orden de llegada. Justo, pero no optimiza movimientos.
    
- **SSTF (Shortest Seek Time First)**: elige la petición más cercana a la posición actual del cabezal. Minimiza búsqueda pero puede provocar inanición (_starvation_).
    
- **SCAN (Elevator)**: el cabezal se mueve en una dirección atendiendo todas las solicitudes en el camino, luego invierte dirección.
    
- **C-SCAN (Circular SCAN)**: como SCAN, pero al llegar al extremo, vuelve directamente al inicio sin atender en el regreso.
    
- **LOOK / C-LOOK**: variantes de SCAN/C-SCAN que paran en la última petición en vez de ir hasta el borde del disco.
    

---

## 📚 **4. Tiempos de acceso al disco (HDD)**

Tiempo total de acceso (**TA**) ≈ **Tbúsqueda + Trotación + Ttransferencia**.

1. **Tiempo de búsqueda** (_seek time_):  
    Tiempo para mover el brazo al cilindro deseado. Típico: 2–10 ms.
    
2. **Latencia rotacional**:  
    Tiempo de espera para que el sector deseado pase bajo el cabezal. Promedio ≈ ½ revolución. Típico: 2–6 ms.
    
3. **Tiempo de transferencia**:  
    Tiempo para leer/escribir los bits del sector. Depende de la velocidad de rotación y el tamaño del sector.
    

---

## 📚 **5. Atención de requerimientos de bloque**

- **Cola de solicitudes**: el SO mantiene una lista de peticiones pendientes.
    
- **Planificador de disco**: decide el orden en que se procesarán (según política elegida).
    
- **Despachador**: envía la orden al controlador del disco.
    
- **Gestión de buffer**: puede usar _read-ahead_ (leer bloques contiguos anticipadamente) y _write-back_ (acumular escrituras antes de hacerlas).
    

---

💡 Resumen rápido:

> - **Secuencial**: bloques uno tras otro, acceso lineal.
>     
> - **Indexada**: tabla de direcciones → acceso aleatorio.
>     
> - **Tiempo de acceso**: búsqueda + rotación + transferencia.
>     
> - **Políticas de disco**: FCFS, SSTF, SCAN, C-SCAN, LOOK.
>     
> - El SO traduce de bloques lógicos a físicos y optimiza el orden para minimizar movimientos.
>     

---



el trabajo 
Procesos, memoria y discos.

jueves de 6 a 8

Siguiente Clase: [[Clase 3]]


