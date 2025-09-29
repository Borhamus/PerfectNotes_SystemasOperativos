24/09/2025 - Teoría Sys Op - Horacio Pendenti.

Clase Anterior: [[Clase 11]]

---

## Administración bajo demanda

![[Pasted image 20250924163013.png]]


## Reemplazo de páginas

![[Pasted image 20250924163308.png]]

Tenemos que ver como hacer esto de manera inteligente, y debemos tener en cuenta las estrategias.

1° si me quede sin memoria, porque ocurre eso?

no le asigne la suficiente cantidad de frames en la memoria principal.

si yo a un proceso le asigno mucha memoria, se supone que no tendría muchos fallos de paginas. una vez que cargo las primeras, luego cargas las demás, pero ..... 

mientras mas frames le asigne a un proceso, menor es la cantidad de fallos de pagina.

CUANTOS MARCOS DE PAGINA LE ASIGNO A CADA PROCESO?

Paginación bajo demanda pura. es: Cargo 1 pagina y de ahí cargo de a una pagina cada vez que se dispara una referencia.

Minimizar la tasa de fallos de página.




![[Pasted image 20250924164128.png]]


![[Pasted image 20250924164623.png]]
Los inclusivos son de pila.

FIFO NO ES INCLUSIVO equisde


Este no se puede implementar, pero esta fachero. básicamente y se usa para medir y calcular weas.
![[Pasted image 20250924165912.png]]


![[Pasted image 20250924170309.png]]
esta es cara.

usar un timestamp(? =marca de tiempo)

implementarlo con pilas. 

el timestamp y las pilas son lentas.


---
Bit de referencias. 

bit de modificado y bit de referencia.


bit de referencia = Es si le hiciste una referencia o no. cada referencia pone este bit en 1.
#### NRU - "No Recientemente Usada"

---

![[Pasted image 20250924172127.png]]

## Algoritmo de reemplazo: Segunda Oportunidad Mejorado

Considera el bit de referencia y el bit de modificación
	**(0 = R de remplazo, 0 M de modificada)**

	Clase A (0, 0) : mejor página para sustitución
	
	Clase B (0, 1): no se ha usado pero ha sido modificada
	
	Clase C (1, 0): se ha utilizado recientemente y está limpia
	
	Clase D (1, 1): se ha utilizado recientemente y se la ha modificado

Páginas clasificadas en clases

Se aplica el algoritmo de segunda oportunidad revisando las clases no vacías en orden ascendente

---
## Algoritmos de conteo

● Guarde un contador con las referencias hechas a cada página

● LFU (Least Frequently Used):
Reemplace la página con el contador más pequeño.

● MFU (Most Frequently Used):
Reemplace la página con el contador más grande.

(Como en WorstFit<- hago el pero laburo y hace que funcione mejor xD)

---

## Asignación de marcos de página

#### Algoritmos para buffering de páginas

Mantenga un pool de marcos libres
	● No debe buscarse un marco disponible al momento de la falla
	● Lea la página en el marco y seleccione la víctima para agregar al pool
	● Cuando sea conveniente concrete el desplazamiento

Guarde una lista de las páginas modificadas (posible)
	● Cuando no se esté utilizando el almacenamiento secundario guarde las páginas y actualice el bit de modificada

Conserve el contenido de los marcos en el pool de marcos libres y a qué proceso y página corresponde
	● Si se requiere una de esas páginas antes de que el marco sea utilizado no se necesita recargar desde el almacenamiento secundario
	● Permite reducir la penalidad ante elecciones incorrectas de la víctima

El número máximo de marcos que pueden asignarse a un proceso es el de marcos disponibles en el sistema

Cada proceso necesita un número mínimo de marcos (depende de la arquitectura del sistema) - Ejemplos:
	● MVC en IBM 370.
	● Referencias indirectas en PDP-11.
	● Múltiples niveles de indirección.

Estrategias de asignación:
	● Equitativa.
	● Proporcional por tamaño.
	● Proporcional por prioridad.
	● Proporcional combinando tamaño y prioridad.


### Reemplazo de páginas con Asignación global y local

Reemplazo global
● La “víctima” se selecciona entre todos los marcos
	● Los procesos ganan y pierden marcos
	● Puede afectar el tiempo de ejecución en función de condiciones ajenas al proceso
	● Mejora el uso de la memoria

Remplazo local
● La “víctima” se selecciona entre los marcos asignados al proceso
	● El proceso mantiene constante el número de marcos.
	● Consistencia en los tiempos de ejecución.
	● Posible subutilización de la memoria.


---
## Sobrepaginación (Thrashing)

Una alta tasa de fallos de página y, en consecuencia, bajo uso de CPU

El SO puede suponer que es conveniente aumentar el grado de multiprogramación y agrega otro proceso al sistema.

![[Pasted image 20250924175544.png]]
Hago mucho intercambio de paginas y esto provoca el caos.


Siguiente Clase: [[Clase 13]]