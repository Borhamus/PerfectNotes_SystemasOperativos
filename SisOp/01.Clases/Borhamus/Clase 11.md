15/09/2025 - Teoría Sys Op - Horacio Pendenti.

Clase Anterior: [[Clase 10]]

---

*Tema de segundo parcial:*
## Paginación

Direcciones virtuales, son un grupo de bits que indican un grupo de paginas, par ordenado.

Los marcos de pagina, comienzan en una dirección de memoria principal que es múltiplo del tamaño de la página.

El recordatorio de donde tengo que ir a buscar en la memoria principal.
donde buscar el frame, y como me voy a desplazar.

* Página virtual **p**
* Marco de página **p’**

**Bit de presencia:**
Contienen un bit para indicar si la página reside en la memoria principal.
* Si el bit está en 1, la entrada almacena el número del marco de página.
* Si el Bit está en 0, la entrada contiene la dirección de la página en el almacenamiento secundario.

A la memoria secundaria, no se le dice frame, es memoria secundaria.
Frame de memoria secundaria, virtual.

Lo que vimos hasta ahora:
#### Traducción de direcciones por mapeo directo.

Una dirección a una tabla+ concatenación de la dirección interna del frame.

![[Pasted image 20250915162252.png]]

==Otro método:==
#### Traducción de direcciones por mapeo asociativo

Si yo tengo esta tabla de paginas, cargada en a memoria principal, completa. lo que pasa que el 90% de las paginas no se cargan en la memoria principal, y lo mismo pasa en las tablas, no se utilizan y por eso es ineficiente.

Este esquema lo que hace es también incluir las tablas de paginas, a un área que maneja el Sistema Operativo.

Tabla de pagina en memoria secundaria, necesaria, pero lenta. 
Que hacemos? Utilizamos Caché.
Es mas chica, pero mas rápida. 
Cada vez que hago una referencia a la pagina, si esa entrada de la tabla de pagina, no esta cargada en la cache, la cargo, la próxima vez estará lista en la caché.

Esto tiene sentido, porque hay estudios que confirman una presunción, de que, la pagina que voy a acceder, lo mas probable es que sea la misma a la que acabo de acceder o muy cercana. Esto es conocido como "Principio de localidad de referencia".

Si llevo a la cache, algo que seguramente voy a seguir usando, estoy "ganando", tendiendo en cuenta que este comportamiento pasa, y es real, este trabajo tiene sentido, sabiendo de que si hago una referencia a una pagina x, las próximas corran a una cercana.
Si necesito un salto, puedo hacer un swap-in y actualizar las cache, y llevar las entradas de las tablas de pagina y llevar a la cache todo un grupo asociativo de esta pagina.

Cuando tenemos toda las tablas en la memoria principal, todo bien, cuando la mayoría esta en memoria secundaria, es un problema y para eso usamos cache, **TLB**.

**Translation Lookaside Buffer**
"Funciona como una memoria asociativa"

Funciona con todas las entradas a la vez.

En vez de moverse como un vector, y buscar el elemento por selector.
Busco contenido, y el método inspecciona por todos los casilleros del vector de una sola vez.

Ya no necesito un índice, busco por contenido.
"La pagina tal, esta acá?" meto esto en todas las entradas, y el método retorna el valor del frame si esta. 
Esto es caro.

![[Pasted image 20250915163653.png]]
Pregunte por la pagina, y la dirección que lo tiene me lo devuelve.

Termina siendo una decisión de compromiso entre costo, rendimiento y de implementación.

TLB = Translation Lookaside Buffer.
PTE = Entradas de tablas de página.

registro del procesador, que se guarda como contexto en su pcb(?

![[Pasted image 20250915164323.png]]
Dos accesos por cada búsqueda que no este en la caché.

si la tabla de pagina esta en la tabla de memoria secundaria.
haces un swap-in, vas a la tabla de pagina y buscas, ya son 2 búsquedas.

> Por cada acceso, cada referencia, normalmente requerimos 2 accesos, salvo en casos donde esta en la caché.

Todo hasta ahora es de un único nivel.

---

#### Tablas de páginas multinivel
Si los primeros bits de una dirección lógica, si los interpreto como cosas diferentes:
Los de desplazamiento los dejo como están.
Los bits que me indican el numero de pagina, los divido en 2 grupos:

// Numero de Tabla // Numero de Página // Desplazamiento //
 con 2 bits, direcciono los números de pagina - para después ir al desplazamiento.
 
![[Pasted image 20250915165612.png]]
Cada dirección son punteros.
navego a través de la jerarquías, hasta llegar al ultimo nivel, éste ultimo es donde esta el frame. son referencias a una subtabla.
Esto es útil, para hacer mejorar de tablas inmensas.
Solo en el ultimo nivel va a haber contenido real, las intermediarias son punteros, de punteros.

---

#### Tablas de Páginas Invertidas
El objetivo es tratar de arreglar el tema de las tablas inmensas.
Ocupan mucho recurso. Entonces una idea "nueva" son las tablas de paginas "invertidas"

![[Pasted image 20250915170019.png]]
Mapeo la Memoria Física primero. Por eso invertida. con esto en mente, lo que tendré es una única tabla de paginas. que 

La cantidad de memoria física/ El tamaño de pagina= Cantidad de entradas.

Mapeo la memoria física, y tendré tantas entradas como frames tenga la memoria física.
Hay que hacer comparaciones, si hay desbordamiento sigo buscando, pero en cada una hay una comparación. 

Encuentro el frame, tengo que hacer algo mas, chekear que sea del proceso correcto. necesito un atributo que me diga de que proceso es cada pagina de la tabla de pagina invertida. porque ahora tenemos una sola tabla para todo. **Comprar el numero de proceso**.


Páginas compartidas en un sistema de paginación
La posibilidad de compartir en un sistema multiprogramado:
* Reduce la memoria consumida por programas que usan datos o instrucciones comunes.
* Exige que el sistema identifique claramente que páginas pueden compartirse y cuáles no.

En un world compartido, necesito algo distintivo, un programa, cada uno va a tener una parte de datos. que tiene cada 100 instancia del proceso...???
necesito una pcb para cada uno de ellos. para poder compartir el programa, y que condición tiene que cumplir para poder ser compartido?
Tiene que ser programas que no se auto-modifiquen.
Si uno usa el programa, y el programa se cambia, se cambia a todos los programas.

![[Pasted image 20250915171804.png]]


---

## Segmentación

Ahora parte de nuestro programa puede estar en la memoria secundaria.
En segmentación simple, todo el programa esta en la memoria principal, podríamos con particiones dinámicas, sobre todo, yo podría manejar con segmentación un esquema donde podría hablar de segmentación virtual. 
lo mismo que hago con la memoria virtual, tener un sector destinado para las tablas de paginas.
Puedo hacer que segmentos estén en memoria virtual, pero esto en general no ocurre.
Si lo vemos acá porque se combina con paginación. Paginación + Segmentación.
No se hace sola. Se hace swap-in / Swap-Out en un esquema combinado.

### Segmento
● Un bloque de datos o instrucciones de un programa.
● Contiene porciones lógicamente significativas del programa (por ejemplo, procedimientos, arreglos, pila, etc.).
● Consiste de ubicaciones contiguas.
● Los segmentos no necesitan tener todos el mismo tamaño ni deben estar adyacentes en la memoria principal.

> Un proceso puede ejecutarse mientras las instrucciones corrientes y los datos referenciados por ellas se encuentren en segmentos cargados en la memoria principal.



Memoria Lógica: Programa mío que tiene 8 paginas (de la 0 a la 8)

Tabla de Pagina: representa esta situación que dice que la pagina 0 esta cargada en la 4 de a memoria física y que es validad.( Es lo mismo que el bit de presencia.)
La tabla de pagina 1, dice que es invalida, no esta cargada en la memoria principal.
La tabla de pagina 2, esta en la 6 y es valida.
La tabla de pagina 5, esta en la 9 y es valida.

Memoria Física:

La pagina1B, esta en la memoria secundaria., no en la memoria principal.
![[Pasted image 20250915172751.png]]
Con que en la memoria principal haya una pagina de un segmento, ya arranco.
Ese seria el caso extremo. lo que puedo hacer es cargar la primer pagina, o la pagina que tiene, la primero instrucción de mi programa, y a partir de ahí, cada referencia que se produzca..
se produce un page-foult. traer esa pagina en particular que referencie y no esta en la memoria principal. voy a buscar la otra pagina y buscar a cada una de las referencias. y cargo esa única pagina.
Paginación por demanda pura. cuando cargo exclusivamente la pagina que acabo de referenciar y no otra.

una instrucción puede requerir múltiples paginas, por lo cual yo para ejecutar un instrucción debo buscar otras 4 paginas, tengo que ir eventualmente buscar cada pagina y hacerles swap-in a cada una, de a una.

reinicio de instrucción, normalmente por fallo de pagina, busco todos los operandos, y una vez que hice todos las llamadas de los datos, podre hacer por ejemplo una suma
Sumar: A,B.
empieza de nuevo.

pre-paginación. 
Necesitamos soporte hard, para poder hacer esto
un mecanismo de reinicio de instrucciones. cuando tenemos paginación por demanda, necesitamos poder reiniciar la demanda hasta poder completar la instrucción.


#### Manejo de un Fallo de Página:
![[Pasted image 20250915173853.png]]
La pagina no esta en la memoria principal, es una interrupción, el tratamiento del SysOp hace que el sistema operativo valla, la busque, le haga swap-in, para poder cargarla y usarla.

**Load M:** 
Referencia de una variable de mi programa, esa M esta en una pagina de mi programa, 
se produce la referencia. El tema es que en la tabla de pagina no esta. Se produce ese trap, que lo captura el sistema operativo, luego va al almacenamiento secundario, a buscar esa pagina faltante con el contenido M, busca un frame disponible en la memoria y lo carga, luego actualiza la tabla de paginas, diciendo que ahora es valida en tal posición, y finalmente se produce el reinicio de la instrucción.

Performance de baja demanda
Si P = 0, no hay fallo de página.
si es 1, es un fallo de página.

Cual es mi tiempo de acceso efectivo?
quiero saber por cada, cuanto tardo en acceder a la memoria primaria, 

como calculo el tiempo de acceso?
Es: 1-p = Tasa de aciertos = Tasa de Hits.

cuando encuentro que la pagina está, lo multiplico por el tiempo que me toma acceder a la memoria principal + la tasa de fallos * el overhead que me produce el fallo de página, mas una eventual grabación de la pagina, 
Yo hago una referencia a una pagina de memoria, debo seleccionar una candidata en la memoria principal para sacarla, si esta esta modificada, hay que guardarla antes de borrarla.
Hay un montón de tiempos ligados a la sumatoria de cada vez que se produce un fallo de página, es un calculo de probabilidades. 

La probabilidad de que haya hits en la tabla de paginas * Tiempo de acceso a la memoria principal + La probabilidad de que haya un fallo de página +Lo que conlleva que tenga un fallo de página

mili, micro, nano, pico, 
Mili: Una milésima
Micro: Una millonésima
Nano: Son 9 ceros
Pico: Son 12 ceros.

Con esto podemos hacer lo siguiente, aceptamos que vamos a tener fallos de páginas, el tema es hasta cuando acepto fallo de páginas, por eso se dice, por ejemplo:
Si yo acepto hasta una degradación del 10%.

Para obtener una degradación de solo un 10% mi tasa de fallo tiene que ser ínfima.
Si no quiero un tiempo de degradación mayor, necesito una tasa de fallos de página baja.

Yo debo como desarrollador del sistema, debo jugar con esos parámetros.


Siguiente Clase: [[Clase 12]]