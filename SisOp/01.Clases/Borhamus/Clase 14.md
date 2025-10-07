06/10/2025 - Teoría Sys Op - Horacio Pendenti.

Clase Anterior: [[Clase 13]]

---

![[Pasted image 20251006162502.png]]

Logical I/O + Basic I/O Supervisor + Basic File System= 
Te permite pasa de números de registros a bloques

la aplicación te pide registros, y los bloques

métodos de acceso. es lo que tenemos arriba.
los archivos, hay distintos datos, y formas de organizarse.

un archivo puede estar organizado, de varias formas
vamos a estudiar 5:

Tipo Pila.
Tipo Secuencial.
Tipo Secuencial Indexado.
Tipo Indexado.
Tipo Indexado Hasheado.

al sistema operativo le interesan los bloques, a los programas los registros.

siempre hablamos de registros, los usuarios.

### Funciones del Administrador

● Identificar y localizar un archivo determinado
● Usar un directorio para describir la ubicación de los archivos y sus atributos
● En un sistema compartido controlar el acceso de los usuarios
●Bloquear y desbloquear los datos
●Asignar los archivos a bloques libres en la memoria secundaria
● Administrar el espacio libre

### Criterios para organizar archivos

● Velocidad de acceso

	● Necesario cuando se accede a un único registro
	
	● No tan importante en el acceso secuencial

● Facilidad de actualización

● Economía de almacenamiento

	● Implica mínima redundacia de los datos
	
	● Pero la redundancia puede ser útil para obtener 
	velocidad de acceso (por ejemplo, un índice)

● Facilidad de mantenimiento

● Confiabilidad

---

### Organización Pila

● Los datos son coleccionados en el orden en el que arriban.
● El propósito es acumular los datos y conservarlos.
● Los registros pueden tener estructuras diferentes o ninguna estructura.
● El acceso a los datos es por búsqueda exhaustiva.

![[Pasted image 20251006163414.png]]

---
### Organización Secuencial

● El archivo está formado por registros
● Los registros tienen un formato fijo (estructura del registro) : Tipo tabla.
● Registros de longitud fija (Stallings)
● Todos los campos iguales (orden y longitud)
● Eventualmente hay un pequeño número de tipos de registros
	● El tipo de registro se identifica al comienzo del registro
● Los nombres de los campos y sus longitudes son atributos del archivo
● Un campo es el campo clave (key field)
	● Identifica en forma única a cada registro (que normalmente están almacenados en secuencia de clave)
● Los registros nuevos son colocados en un archivo de log o de transacciones
● La actualización es realizada en forma batch, mezclando el archivo de transacciones con el maestro


>**Dato**: Un archivo extra se crea para actualizar la tabla, y trabaja con punteros. 
   Esto es gestionado por el Sistema Operativo.
   Te permite actualizar los punteros.

**Dato2**: Sirve para hacer actualizaciones masivas de registros.

![[Pasted image 20251006163923.png]]
### Casos de uso:
el acceso secuencial es útil cuando debo recorrer todos los registros para hacer algo en concreto.

si necesito buscar 1 solo registro, esta estructura no me sirve.


---

### Organización Secuencial Indexada

● Los índices proveen una capacidad de búsqueda que permite alcanzar rápidamente la vecindad de un registro deseado
	● Contienen un campo de clave y un puntero al archivo principal
	● Se busca en el índice hasta encontrar el primer valor de la clave que es mayor que la del registro deseado
	● La búsqueda continúa en el archivo principal en forma secuencial a partir de la ubicación señalada por el puntero

● **Ejemplo comparado**
	● Sobre un archivo con 1 millón de registros se crea un índice con 1.000 entradas. Se necesitará un promedio de 500 accesos para encontrar la entrada y 500 accesos para
	encontrar el registro en el archivo principal, es decir, 1.000 accesos (contra 500.000 en tratamiento secuencial)
● Al agregar
	● Los registros se agregan a un archivo de overflow (que periódicamente puede ser
	 mezclado con el principal)
	● El registro que precede al que está en overflow contiene un puntero


> **Dato**: Estos 3 datos pueden estar en un solo archivo de mi file system.

> **Dato2**: No necesariamente deben tener la misma longitud.

![[Pasted image 20251006165340.png]]
**Índice exhaustivo:** Que hay un índice por cada registro. 
normalmente los índices parciales hay por cada índice, varios registros.

Ejemplo:
Por cada 1000 registros, se crea un índice.

Ejemplo:
Tengo una lista índice de 100 y cada puntero apunta a una lista de 1000 registros. 

---

### Organización Indexada

● Se utilizan múltiples índices para diferentes campos de clave
● Los índices pueden ser exhaustivos (contienen una entrada para cada registro en el archivo) o parciales (sólo referencian algunos registros) 
![[Pasted image 20251006170059.png]]

---

### Organización Directa o Hashed

● Accede directamente a un registro conociendo su dirección
● Se requiere un campo de clave para cada registro que
	● Lo identifique
	● Sirva de base para calcular la dirección
● Como en el caso de secuencial indexado no todos los registros se ubican en el lugar al que lleva el cálculo de dirección de modo que hay necesidad de campos de overflow y punteros para redirigir el direccionamiento

>**Dato**: Es la forma mas rápida que hay.

---

**Organizaciones:** (Estructura interna de los archivos)
● Pila
● Secuencial
● Secuencial Indexado
● Indexado
● Hash

**Modo de Acceso:** (Como voy a acceder a los registros)
● Secuencial
● Indexado
● Directo

**Método de Locación:** (Como esta dispuesto en memoria secundaria el archivo)
● Contigua
● Encadenada
● Indexada


**Recordatorio:**
>**Secuencial**: Acceder de a uno, hasta cierto punto o hasta el final. 
> **Indexado**: Necesito que el archivo tenga un indice. Puedo acceder a un registro particular con un indice, y luego avanzo secuencialmente.
> **Directo**: Hashing es directo, tiene una búsqueda de 1.

**Que es una carpeta?**
	Los directorios son Carpetas, los directorios son archivos.
Es un archivo que podría ser secuencial o secuencial indexado.
El nombre es el nombre de la carpeta, pero el contenido, es cada uno de los archivos que tenés dentro.
Junto con otros datos, entre otros, la FAT.

**Que es La FAT?**
Es el archivo que me dice donde  
file alocation table, tabla de alocación de archivos, me dice donde esta la memoria secundaria el archivo que estas buscando.

**Ejemplo de sistema operativo antiguo.**
1 Directorio de módulos.
2 Nivel de directorios.
3 Archivos.

que es importante en Directorios:

Como y donde
El espacio disponible lo tengo que  xxx también

asignación de espacios, y pree

cuando vamos a crear un archivo, tenemos que dejarle un espacio para poder trabajar, preasignación, cuanto tamaño/Bloques va a tener es archivo.

como lo voy a disponer en el disco

el mas simple es:

---

### Alocación Dinámica Contigua

● Un conjunto único de bloques es asignado al archivo al momento de la creación (preasignación)
● Produce una única entrada en la tabla de asignación de archivos (FAT) (bloque de inicio y longitud del archivo)
● Es buena para archivos secuenciales
● Es buena para archivos secuenciales indexados: una fórmula simple permite encontrar el bloque n
● Puede producir fragmentación externa
● Periódicamente puede compactarse el disco para recuperar los fragmentos no utilizados

![[Pasted image 20251006172049.png]]

---

### Asignación dinámica encadenada

● La asignación es sobre la base de bloques individuales
● Cada bloque contiene un puntero al próximo bloque en la cadena
● La tabla de asignación de archivos (FAT) contiene una entrada con un puntero al primer bloque y la longitud de la cadena
● No hay fragmentación externa
● Es mejor para archivos secuenciales, pero es buena para otros tipos de archivos
● El principio de localidad no es aprovechado
● Periódicamente el disco puede consolidarse para poner todos los bloques de un archivo en forma contigua (y aprovechar el principio de localidad)

![[Pasted image 20251006172419.png]]

> **FAT** = File Alocation Table 

---

### Asignación dinámica indexada

● La tabla de asignación de archivos (FAT) contiene un índice de un nivel para cada archivo
● El índice tiene una entrada para cada porción asignada al archivo
● La FAT contiene el número de bloque del índice

![[Pasted image 20251006172754.png]]

Esta es la forma mas básica de asignación indexada, donde el archivo B esta apuntado en el bloque indice 24. el bloque contiene punteros a otros bloques que si tienen datos.

![[Pasted image 20251006172947.png]]
En este diseño cambia la FAT

Empieza en el bloque 1, durante 3 bloques contiguos, luego, en el 28 por 4 bloques contiguos, y finalmente del 14 por 1 largo.


**Esto hay que tener en cuenta:**

Pila con contigua: SI
Pila con Encadenado: Si, pero es medio malo
Pila con Indexada: No.

Secuencial con contigua: 
Secuencial con Encadenado:
Secuencial con Indexada:

Secuencial Indexado con contigua: 
Secuencial Indexado con Encadenado:
Secuencial Indexado con Indexada:

Indexado con contigua: 
Indexado con Encadenado: no son compatibles.
Indexado con Indexada:

Hash con contigua: 
Hash con Encadenado: no son compatibles.
Hash con Indexada:

Los bloques de disco, pueden contener, mas de un registro, pueden tener pedazos de registros. el file system se encarga con la aritmética, calcular cual bloque es el correcto.

Muchos sistemas operativos lo que haces en usar cada bloque, un espacio para punteros y un espacio para datos.





---
Siguiente Clase: [[Clase 15]]