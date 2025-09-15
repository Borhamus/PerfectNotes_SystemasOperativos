10/09/2025 - Teoría Sys Op - Horacio Pendenti

 Clase Anterior: [[Clase 9]]

---

## Administración de Memoria con Especificación Estática de Particiones.

Puntero a dos cosas distintas.
///////////////////////////////
// 000000 // 0000000000 //
///////////////////////////////
	Numero de Pagina		
			El desplazamiento
		
>**La primera parte, es la lógica de posición de la tabla de paginas, y la segunda es el offset, diferencia de posicionamiento interno del frame.**


---

## Paginación

6-bit Page    10-bit Offset
///////////////////////////////  <- 16-Bits Lógical Addres
// 000000 // 0000000000 // ---------
///////////////////////////////              |
    |                                                 |
////////////////// **Tabla de Procesos**  |
// 0   000 000 //                                 |
// 1   000 000 //                                 |
// 2   000 000 //------                        |
//////////////////        |                        | 
                 |                        |
               ///////////////////////////////  <- 16-Bits Physical Addres
               // 000000 // 0000000000 // 
              ///////////////////////////////

## Segmentación

4-bit Page    12-bit Offset
///////////////////////////////  <- 16-Bits Lógical Addres
// 0000 // 000000000000 // ---------
///////////////////////////////
   |
   |     Lenght             Base
//////////////////////////////////////////////// <- Tabla de Segmentos de Procesos.
// 0  000000000000  0000000000000000 //
// 1  000000000000  0000000000000000 //
////////////////////////////////////////////////
   |
   |
//////////////////////////// <- 16-Bits Physical Addres
// 0000000000000000 // 
////////////////////////////

---
Hasta acá el primer parcial

---
## Memoria Virtual

Herramienta para crear la ilusión al usuario de que tenés la memoria mas grande de lo que es realmente.

A la memoria principal, le agrego parte de la memoria secundaria.
![[1.jpeg]]
Una tabla por proceso.

la tabla con un bit adicional, si esta o no en la Memoria Virtual.

### Variantes de implementación:
● Paginación.
● Segmentación.
● Algunos sistemas combinan las dos variantes.

>**Espacio virtual de direcciones (R):** 
	*Rango de direcciones virtuales que puede referenciar un proceso.*

>**Espacio real de direcciones (DAT):** 
	*Corresponde al rango de direcciones físicas existentes en un sistema de cómputo particular*

## Mete el programa entero
### Paginado a la memoria secundaria

### Y carga las que va a usar.

### Ojo:
Esta era la **ultima barrera** que teníamos que romper para poder solo cargar un pedazo útil del programa a la memoria principal. De esta manera es ultra eficiente ya que solo tendremos cargado lo mínimo necesario.

---
### Mapeo de Bloques

Tenemos Direcciones de comienzos de Frames. y esa es la magia detrás del mapeo de bloques, es un sistema de direcciones, que con un set de reglas, podrás manipular y encontrar bloques de frames útiles para un programa. Un set de datos que indica todo el programa X que quieras cargar. 
Se hace una suma en este proceso. 

Los primeros 2 son Pagina
Los otros 2 son Offset.

**Mapeo de Bloques:**
"Direccion Base" + (Sumarle)  + "El Desplazamiento"
//////////// <---Numero de Dirección de Comienzo del frame
// 00 + 00 //
// 00 + 01 //
// 00 + 10 //
// 00 + 11 //
// 01 + 00 //
// 01 + 01 //
// 01 + 10 // <- *Esta es la magia de sumar 4-bits*
// 01 + 11 //
// 10 + 00 //
// 10 + 01 //
// 10 + 10 //
// 10 + 11 //
// 11 + 00 //
// 11 + 01 //
// 11 + 10 //
// 11 + 11 //
////////////// 

(A) Registro que me indica donde empieza la tabla de Pagina/Segmento
Puntero a la primera tabla de pagina.

**Se lo sumo al registro A** + 
**El desplazamiento para saber donde esta la dirección física real.**

---
Siguiente Clase: [[Clase 11]]