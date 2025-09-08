08/09/2025 - Teoría Sys Op - Horacio Pendenti

### Particionado de Memorias

**Particiones Fijas**:
● Características positivas.
● Simple de implementar.
● Bajo overhead.

**Características negativas**

● Todo el programa cargado en memoria principal.
● El programa en memoria está alojado en forma contigua.
● Fragmentación interna.
● Fragmentación externa.
● Número fijo de trabajos activos.

> La idea principal es particionar la memoria a demanda de los trabajos y del tamaño exacto.

* **TODO EL PROGRAMA DEBE ESTAR CARGADO EN LA MEMORIA PRINCIPAL**
Esto quiere decir que hay un 90% del programa que en promedio, no lo vamos a usar.
**Agarramos toda la imagen del proceso que se creó.**
**El programa en memoria esta alojado en forma contigua.**
La cantidad que tenemos para ejecutar siempre es fija, porque da, es estática. como máximo será la partición dictada.
#### First Fit (FF):
Se selecciona la primer partición en la que cabe el programa, comenzando el análisis siempre desde la primer partición libre en la tabla de particiones.
Siempre desde el principio.
#### Next Fit (NF):
Igual que First Fit, pero el análisis comienza a partir de la última asignación de partición realizada.
Se guarda la posición y continua desde donde quedó.
#### Best Fit (BF):
Se asigna la partición libre más chica disponible en la que cabe el proceso.

Todas las libres, la primera que quepe.
No es muy buena realmente, aunque suene contradictorio.

#### Worst Fit (WF):
Se asigna la partición de memoria más grande disponible en la que cabe el proceso. Tiene sentido en particiones fijas?
En particiones estáticas, no tiene sentido.
En dinámicas cambia la cosa.

> **Batch: Secuencial básico.**

---

> Para solucionar el problema de FF, tamaño de partición vs trabajo que quiero cargar, tratando de no desperdiciar tanta memoria, de ahí nace el BF.

---

## Administración de memoria con especificación
## dinámica de particiones (Particiones dinámicas)

La idea es que las particiones se creen solas, las carga el sistema operativo, a medida del proceso, el tamaño del proceso, a demanda.

Fragmentación interna NO HAY.
Si hay externa, es mucho menor, pero existe. (Si administras bien.)

existe una partición "**Única Libre**" al pedir una se divide en 2, y una en el tamaño exacto del proceso, para asignarlo, y queda otra partición y de esta manera queda libre/No asignada.

**Las particiones adyacentes libres se combinan**
![[1.png]]

![[2.png]]

Características de los algoritmos

● FF tiende a dejar muchos agujeros pequeños al principio de la memoria.
● NF algo similar pero en las zonas altas de memoria.
● BF suele tener una mala performance (peor que las anteriores), inunda la memoria de pequeños agujeros.
● WF ?

> **En todos casos suele requerirse compactación.**
> Que significa: Que tomo toda la memoria y la reacomodo sacando los espacios sueltos.
> Es caro, reubica programas, para eso se hace cuando el cpu esta ocioso. 

**Swap out** de procesos puede tener lugar cuando la gran mayoría de procesos están bloqueados y hay poca memoria disponible. Esto hace lugar para hacer un swap-in de procesos que eventualmente estén en estado ready-suspended. Esto implica que debemos reemplazar alguno de los procesos aplicando un algoritmo de reemplazo.

Para no caer en tener mucha memoria desperdiciada, aparece un diseño: 
**Buddy System**. (Ojo, es una *Solución de compromiso*).

![[3.jpeg]]


**Tiene un precio, tiene Fragmentación Interna, baja, pero tiene.**
**Pero estas ganando la posibilidad de no tener tantos espacios inútiles en tus algoritmos. Se vuelven a unir las particiones mas fácilmente.**

#### Particiones Dinámicas:
● Características Positivas
● No fragmentación interna.
● Uso más eficiente de la memoria principal.

#### Características Negativas:
● Todo el programa cargado en memoria principal.
● El programa en memoria está alojado en forma contigua.
● Fragmentación interna, no. Excepto Buddy System.
● Fragmentación externa.
● Overhead por compactación. **<- Esto no pasaba en Estática.**

---

### Reubicación
#### Dirección lógica:
Es una referencia a una ubicación de memoria independiente del actual mapeo a una ubicación física. Ocurre exclusivamente en el espacio de direcciones del programa. Se requiere traducción para determinar la dirección física correspondiente.

**Es en nuestro espacio de memoria, no tiene nada que ver con FISICAS.**

De un espacio de programa, no tienen nada que ver con las físicas.

Cuando esta cargado en la memoria principal, aun siguen siendo direcciones lógicas, y que para poder ejecutarse, recién ahí necesito que las direcciones lógicas terminen siendo traducidas, para ir a la dirección física.



#### Dirección relativa:
Es un caso particular de dirección lógica, en la que la dirección referencia una ubicación en memoria relativa a una base conocida, típicamente un valor en un registro del procesador. Se requiere traducción (típicamente +) para determinar la dirección física correspondiente.

Las relativas arrancan en el 0 de mi programa. Se requiere traducción.
Sigue siendo una dirección lógica, nada mas que envés de ser absoluta es relativa al 0 de mi programa.
#### Dirección física o absoluta:
Ubicación real en la memoria principal. No requiere traducción.

![[4.jpeg]]

DATO: Con ambos esquemas de particiones funciona.

---

## Paginación

### Paginación Simple
Partir a la memoria principal, en pequeños bloques, **"FRAMES"**, todos del mismo tamaño y potencia de 2. 

Frame **Físico**.
Paginas **Imagen del Proceso**.

Para cada una de estos Frames, necesito una dirección.

esto rompe la contigüidad de los programas. con particiones **deben** estar completos y contiguos. Con paginación **ROMPO** con al regla de que los programas deben estar en formato contiguo. ahora tengo o puedo tener varios FRAMES de un programa.
Con esto puedo particionar y gestionar mejor la memoria.

Las paginas son el espacio en la memoria, y los frames son el proceso en si...
Aun necesito todo el programa cargado en la memoria.

Ahora necesito un registro por cada pagina de mi programa, para poder hacer el calculo de direcciones.

Tenemos FRAMES, y cargamos en la memoria principal PAGINAS.

### **Bienvenido a la: Tabla de Páginas.**
Una por cada proceso. no es mas una por sistema.

![[5.jpeg]]

Lo que esta afuera es el numero de paginas, lo que esta adentro es el numero de Frames.
Todo el proceso debe estar mapeado en la tabla de paginas.

Rompo la seria restricción de tener que poner el programa de manera contigua. Costo, una tabla de pagina inmensa. y que tenga un registro base por cada programa.
Funciona como una estática. 

En promedio, tenemos media pagina por programa. Es la Fragmentación interna. 

**VER:**
**Que pasa con los últimos n bits, de una dirección de memoria.**