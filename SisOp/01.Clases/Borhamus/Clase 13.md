29/09/2025 - Teoría Sys Op - Horacio Pendenti.

Clase Anterior: [[Clase 12]]

---
El concepto de "working set. Investigar.


**Este jueves, 2/10 a las 16hs. Examen.**

### Sobrepaginación

A mayor grado de multiprogramación, si me excedo, ocurre "Thrashing", que es admitir muchos procesos, no es capas de que el sistema operativo lo use eficientemente.

Baja abruptamente al aumentar el grado de multiprogramación, se quedo sin recursos y esta muy sobrecargado haciendo mucho trabajo de swap out de paginas y swap in.

Es excesivo en tiempo no util. Si el sistema Operativo no puede detectar estas dos variables, podemos estar en una **Hiperpaginación** sin solución.

El Thrashing es un efecto no deseado, es: 
El exceso de transferencia de pagina entre los dos niveles de memoria.

Se trata de evitarlo por todos los medios, **modelo de localidad de referencia**, sirve para esto. Hay que diseñar un mecanismo que no permita que suceda el Thrashing.

![[Pasted image 20250929161849.png]]
Y: Referencias a paginas.
X: El eje del tiempo.

Un grupo de paginas es una **LOCALIDAD**.
Ejemplo de la 18 a la 24 hay una **LOCALIDAD**.

Se dice que la localidad migro a otro grupo de paginas.

Un LRU podría hacerlo un OPTIMO no existe. (Organizar cual están libres y cuales no)

TENEMOS QUE ESTUDIAR EL MODELO DEL CONJUNTO DE TRABAJO.
El "Resident Set", es el conjunto de paginas de un proceso que esta cargado en la memoria principal.

todas las paginas que están cargadas en memoria principal = "Resident Set"
conjunto de paginas que si se están usando = "Working set"



Entonces:
En la historia reciente, cual se venían usando?

tomamos esta experiencia pasada e intentamos predecir algo
lo que quiero saber es cuales de todas las paginas del residen set del proceso son las que se estuvieron usando?
en unas ventanas de tiempo.
no solo en términos de reloj, sino que lo puedo definir en tiempos de ticks, o de referencias.

"las ultimas xxxx referencias..."

"el marco de observación sobre un grafico"

![[Pasted image 20250929163456.png]]


En el delta 1 {1,2,5,6,7} son usadas, en el delta2, {3,4} por lo que hubo un cambio de localidad de paginas.

si mi delta es pequeño, no seré capas de abarcar toda la localidad.

Si Δ(Delta) es: 
	Demasiado pequeño no podrá abarcar toda la localidad.
	Demasiado grande puede superponer localidades.

si el working set es igual al resident set, te quedas sin memoria.
Esta mal.


D = Σ WSS_i (Demanda total de marcos)

Si D > el total de marcos disponibles (m) tendremos Sobrepaginación.

Política: Si D > m suspender o sacar de memoria algún proceso.

Entonces el tema esta en poder determinar el delta. que no es un trabajo sencillo.


![[Pasted image 20250929164936.png]]

#### Modelo por Frecuencia de Fallos de página
En vez de determinar cual es el conjunto de trabajo apropiado, lo que hago es definir unas bandas
Establezco un limite superior e inferior. si mi tasa de fallos de pagina es muy alta, le asigno mas memoria. 
Y si baja demasiado, le estoy dando demasiada memoria a ese proceso entonces le quito memoria.

Esta pensado para un remplazo global de paginas.

![[Pasted image 20250929165325.png]]



---
---
## File Management

windows era un sistema orientado a manejar los archivos.
DOS, 

DrDoS <- Digital Reserve. 

necesitamos una forma conveniente para organizar cada dato que tenemos
el tratamiento de archivos es un tema central y de hecho dio origen a Windows.


conjuntos de llamadas al sistema, estándar, que podían cubrir las necesidades de cualquier programa.

Para efectuar operaciones sobre archivos:
Crear registros, editar registros guardar registros, etc...

Algunas operaciones:
● Retrieve All.
● Retrieve One.
● Retrieve Next.
● Retrieve Previous.
● Insert One.
● Delete One.
● Update One.
● Retrieve according hot specific criteria.

Siempre pasamos por el Sistema Operativo

Tiene que haber una jerarquía en la pc, para que no se pisen las prioridades de uso.

**Este gestor de archivos tiene algunas funciones, objetivos a cumplir:**
● Satisfacer las necesidades del administrador y los requerimientos del usuario.
● Garantizar la integridad de los datos.
● Minimizar la potencial pérdida de datos.
● Optimizar performance.
● Proveer soporte de I/O para un variedad de dispositivos de almacenamiento.
● Proveer un conjunto estandarizado de rutinas de I/O.
● Proveer soporte de I/O para usuarios múltiples.


**Requerimientos mínimos**
●Un usuario debería ser capaz de:
● Crear, borrar, leer y modificar archivos
● Tener acceso controlado a los archivos de otros usuarios
● Controlar que tipo de acceso está permitido a sus archivos (leer, escribir, ejecutar, …)
● Reestructurar los archivos del usuario en una forma adecuada al problema
● Mover datos entre archivos
● Resguardar (back up) y restaurar sus archivos en caso de daño
● Acceder a sus archivos utilizando nombres simbólicos







---
Siguiente Clase: [[Clase 14]]