18-08-2025 Lunes Agosto. Horacio: Teoría.
clase anterior: [[Clase 3]]


## Administración de procesos

Ideas generales de los procesos, nociones básicas.
en que estados se pueden encontrar.

Tiempos de respuesta

maximizando el uso del cpu, 
asegurando tiempo de respuestas razonables,

sistema multiprogramado.
	Conceptos

✔ Estados

✔ Estructuras de datos

✔ Cambios de modo y proceso

✔ Diseño y modos de ejecución del SO

✔ Ejemplo

✔ Claves y Conclusiones

el tiempo desde que tocas una tecla hasta que es mostrada en pantalla, es un tiempo de respuesta del sistema.

Tiempo de respuesta, métrica que tiene que ver con el usuario. tiempos razonables.

Puede haber T.R. 
estimulas al sistema, y hasta la respuesta, pasa un tiempo medible. 

Dar una buena respuesta a los Usuarios Vs Uso eficiente de los recursos.

Asignar recursos a los procesos, evitando bloqueos o inanición, pide/libera y el so es el que se los asigna.

---
Bien, tomemos tu texto y lo desarrollemos como si fuera un fragmento de clase de **Sistemas Operativos**. Te lo explico en versión extendida, con ejemplos y contexto de libros de referencia (Tanenbaum, Silberschatz, Stallings).

---

### 📘 Desarrollo del Texto

En el estudio de los sistemas operativos, una de las métricas fundamentales para evaluar su desempeño es el **tiempo de respuesta**.

🔹 **Definición básica:**  
El tiempo de respuesta es el intervalo que transcurre desde que un usuario realiza una acción —por ejemplo, presionar una tecla— hasta que el sistema refleja esa acción en pantalla. Es decir, desde el **estímulo** al sistema hasta la **respuesta observable**.

En términos más generales, el tiempo de respuesta se aplica a cualquier interacción entre un usuario y un sistema de cómputo: ejecutar un comando en la consola, abrir un archivo, cargar una página web, etc.

---

### 📊 Tiempo de respuesta como métrica orientada al usuario

A diferencia de otras métricas del sistema operativo (como **throughput**, o cantidad de procesos completados por unidad de tiempo, que está más ligada al rendimiento global), el tiempo de respuesta está íntimamente relacionado con la **percepción del usuario**.

Un sistema puede ser muy eficiente en términos de utilización de CPU, pero si los tiempos de respuesta son demasiado altos, el usuario lo percibe como “lento” o “ineficiente”.

Por eso, en el diseño de sistemas operativos modernos, se busca un **equilibrio**:

- **Dar una buena respuesta al usuario** (tiempos razonables).
    
- **Mantener el uso eficiente de los recursos** (CPU, memoria, disco, red).
    

---

### ⚖️ El equilibrio: satisfacción del usuario vs eficiencia del sistema

Este equilibrio es clave. Por ejemplo:

- Si el sistema operativo dedicara todos los recursos a un único proceso para darle la máxima velocidad, los demás procesos podrían quedar **bloqueados** o incluso sufrir **inanición** (starvation).
    
- Por otro lado, si los recursos se reparten de manera perfectamente equitativa pero sin atender la urgencia de ciertas tareas, los usuarios percibirán **respuestas lentas** incluso para operaciones simples.
    

El sistema operativo resuelve este problema implementando **algoritmos de planificación (scheduling)** que asignan recursos a los procesos de forma inteligente.

---

### 🖥️ Ejemplo práctico

- **Escenario 1:** un usuario escribe en un procesador de texto. Si cada vez que presiona una tecla tarda medio segundo en aparecer en pantalla, el sistema es inútil para esa tarea.
    
- **Escenario 2:** un servidor procesa cientos de peticiones web. El sistema operativo debe decidir qué procesos priorizar para que la mayoría de usuarios perciba tiempos de respuesta bajos, sin que el servidor se “atasque” en atender a unos pocos.
    

---

### 🔑 Conceptos asociados

- **Asignación de recursos:** el SO otorga CPU, memoria y dispositivos a los procesos según algoritmos definidos.
    
- **Bloqueos (deadlocks):** situación en la que un conjunto de procesos queda esperando recursos entre sí y nunca avanza.
    
- **Inanición (starvation):** un proceso queda indefinidamente postergado porque otros procesos acaparan los recursos.
    
- **Planificación justa y eficiente:** los algoritmos del SO (Round Robin, SJF, Prioridades, Multinivel, etc.) intentan balancear eficiencia con tiempos de respuesta razonables.
    

---

### 📌 Resumen final para repasar

- **Tiempo de respuesta:** intervalo entre estímulo (acción del usuario) y respuesta visible del sistema.
    
- Es una **métrica centrada en el usuario** (percepción de rapidez).
    
- Requiere equilibrio entre:
    
    - **Satisfacción del usuario** (respuesta rápida).
        
    - **Uso eficiente de los recursos** (evitar bloqueos, inanición, desperdicio).
        
- El **SO asigna y libera recursos** a los procesos mediante algoritmos de planificación para optimizar ese equilibrio.
    


---

Creación de procesos

● Nuevo trabajo batch

● Login interactivo

● Creado por el SO para proveer un servicio

● Creado por un proceso existente


Perfecto, vamos a desarrollar el tema **Creación de procesos** como si fuera explicado en una clase universitaria de **Sistemas Operativos**.

---

## 📘 Creación de procesos en un Sistema Operativo

Un **proceso** es un programa en ejecución, que incluye no solo el código del programa, sino también su estado actual (variables, memoria asignada, registros de CPU, recursos abiertos, etc.).  
El sistema operativo es el encargado de **crear, administrar y finalizar procesos**, asegurando que tengan acceso justo y seguro a los recursos del sistema.

La **creación de procesos** puede darse en diferentes situaciones, que corresponden a las siguientes categorías:

---

### 🔹 1. Nuevo trabajo batch

En los sistemas antiguos de procesamiento por lotes (**batch systems**), los usuarios entregaban sus trabajos en tarjetas perforadas o cintas. El sistema operativo creaba un proceso cada vez que recibía un **nuevo trabajo** de este lote.

📌 Ejemplo actual:  
Un script o programa enviado a un **servidor de colas de impresión** o a un **sistema de procesamiento por lotes en la nube** (ej. ejecución de jobs en Hadoop o Spark). Cada job se convierte en un proceso independiente.

---

### 🔹 2. Login interactivo

En sistemas **interactivos** (como Unix, Linux o Windows), un proceso se crea cuando un usuario inicia sesión.  
El **login shell** o **entorno de escritorio** que aparece luego del inicio de sesión es en sí mismo un proceso creado por el sistema operativo.

📌 Ejemplo:

- Cuando entrás en Linux con tu usuario, el SO crea el proceso `bash` (o `zsh`, u otro shell).
    
- En Windows, al iniciar sesión, se ejecutan procesos como `explorer.exe` que brindan la interfaz gráfica.
    

---

### 🔹 3. Creado por el SO para proveer un servicio

El propio sistema operativo puede crear procesos de manera **automática** para brindar servicios esenciales al usuario o al hardware.

Estos procesos se conocen como **procesos del sistema**, **daemons** en Unix/Linux o **servicios** en Windows.  
No dependen de la acción directa del usuario, sino que son iniciados para mantener al sistema operativo funcional.

📌 Ejemplo:

- En Linux: `sshd` (para conexiones remotas), `cron` (para tareas programadas).
    
- En Windows: `svchost.exe` (hospeda servicios del sistema), `winlogon.exe` (gestiona inicio de sesión).
    

---

### 🔹 4. Creado por un proceso existente

Un proceso en ejecución puede crear **otros procesos hijos**.  
Esto se da a través de **llamadas al sistema**:

- En Unix/Linux se utiliza `fork()` (duplica el proceso padre) y `exec()` (cambia la imagen del proceso).
    
- En Windows se usa `CreateProcess()`.
    

De esta forma, se construye un **árbol de procesos**, donde cada proceso puede ser padre de otros.

📌 Ejemplo:

- En Linux, cuando abrís Firefox desde la terminal:
    
    - El shell (proceso padre) ejecuta un `fork()` y `exec()` para crear el proceso `firefox`.
        
- En Windows, cuando un programa lanza un instalador externo, ese programa actúa como **padre** del proceso de instalación.
    

---

## 📌 Resumen para repasar

- **Nuevo trabajo batch:** procesos creados a partir de trabajos enviados en lote (batch jobs).
    
- **Login interactivo:** al iniciar sesión, el SO crea procesos para manejar la sesión (shell, escritorio, etc.).
    
- **SO crea procesos de servicio:** demonios, servicios y procesos de sistema que garantizan funcionalidades básicas.
    
- **Procesos crean procesos:** un proceso padre puede lanzar procesos hijos mediante llamadas al sistema (`fork`, `exec`, `CreateProcess`).
    

---

El so tiene que ser capas de crear un batch, o con un login interactivo. 
Interactivo, como una pc con una app. y no interactivo, como una actualización de una base de datos.

Los **Interactivos**, son con Users.
Los **No-Interactivos**, los manipula el SO.

Un proceso puede ser creado por otro proceso. *Es lo que normalmente ocurre*.

> Ejemplo
	En C llamo a una librería y hacer un fork, genera una copia limpia de un proceso que se esta ejecutando. 

son 4 vias. lol, me quede con 3 creo. ree-ver.

siempre el so crea los procesos. uno puede programar cosas pero el sistema finalmente crea los procesos y determina sus caracteristicas y como y cuando se termina.

---

## Terminación de procesos

#### Terminación normal

#### Terminación anormal:

	● Excede tiempo límite
	● Excede memoria disponible
	● Violación de memoria
	● Error de protección
	● Error aritmético
	● Fallo de I/O
	● Instrucción inválida
	● Instrucción privilegiada
	● Datos
	● Operador u OS
	● Terminado por el padre
	● Terminación del padre

---

## Comportamiento

tiene que ver con la vida de un proceso.
Siempre para cada programa que quiero ejecutar.

●El procesador ejecuta las instrucciones señaladas por el PC

●Para cada programa que se ejecuta se crea al menos un proceso

●Comportamiento de un proceso: la secuencia en la que se ejecutan las instrucciones de ese proceso (traza)

●Comportamiento del procesador: la intercalación de las trazas de varios procesos

tasa de 

siempre tenemos que tener en cuenta las 2 visiones, que pasa en los procesos
y en el ámbito de una cpu, en el ámbito de multiprogramado.

---
Perfecto, desarrollemos este tema como si fuera explicado en una clase de **Sistemas Operativos** sobre el **comportamiento de los procesos y del procesador**.

---

# 📘 Comportamiento de los procesos y del procesador

Cuando hablamos de **comportamiento** en sistemas operativos, nos referimos a la **vida de un proceso**: cómo nace, se ejecuta y termina.  
Siempre que queremos ejecutar un programa, el sistema operativo crea al menos un proceso que representa esa ejecución.

---

## 🔹 1. Ejecución de instrucciones (visión del proceso)

El procesador (**CPU**) ejecuta instrucciones una a una siguiendo lo que indica el **contador de programa (Program Counter, PC)**.

- Cada proceso tiene su **traza de ejecución**, que es la **secuencia ordenada de instrucciones** que ese proceso va realizando.
    
- La traza es única para cada proceso y define su “comportamiento” individual.
    

📌 Ejemplo:  
Si abrís una calculadora y haces una operación, la CPU ejecuta una serie de instrucciones específicas (cargar operandos, sumar, mostrar en pantalla). Esa serie ordenada es la **traza del proceso calculadora**.

---

## 🔹 2. Multiprogramación (visión del procesador)

En un sistema multiprogramado, la CPU no ejecuta un único proceso de principio a fin, sino que **intercala la ejecución de varios procesos**.

Esto significa que:

- El **comportamiento del procesador** es la **intercalación de trazas** de distintos procesos.
    
- La CPU cambia rápidamente de un proceso a otro mediante mecanismos de **planificación y cambio de contexto (context switch)**.
    

📌 Ejemplo:

- En una computadora con un procesador y varios programas abiertos (navegador, música, procesador de texto), la CPU ejecuta pequeñas partes de cada uno, alternándolos.
    
- Para el usuario parece que todos corren al mismo tiempo, pero en realidad la CPU está **compartiendo el tiempo** entre ellos.
    

---

## 🔹 3. Visión dual: proceso vs procesador

Cuando estudiamos sistemas operativos, debemos tener en cuenta **dos perspectivas complementarias**:

1. **Qué pasa en un proceso en particular** (su traza, su comportamiento individual).
    
    - Ejemplo: el proceso del navegador cargando una página web.
        
2. **Qué pasa en la CPU en un sistema multiprogramado** (cómo intercalamos múltiples procesos).
    
    - Ejemplo: la CPU alternando entre el navegador, el reproductor de música y el editor de texto.
        

La combinación de ambas visiones permite entender cómo el sistema operativo administra los recursos para que:

- Cada proceso tenga la ilusión de correr de forma independiente.
    
- El procesador sea utilizado de manera eficiente, sin tiempos muertos.
    

---

## 📌 Resumen para repasar

- **Cada programa → al menos un proceso**.
    
- **Comportamiento de un proceso:** secuencia de instrucciones ejecutadas (traza).
    
- **Comportamiento del procesador:** intercalación de múltiples trazas en un sistema multiprogramado.
    
- Siempre debemos analizar desde dos ángulos:
    
    - La vida de un proceso individual.
        
    - La organización global del procesador al manejar varios procesos.
        

---

Hacer uso eficiente de los recursos y darle un buen servicio a los usuarios ( dando buenos tiempos de respuesta.)

el so trata de que el tiempo de respuesta sea lo mejor posible. para dar un buen servicio.

**Un proceso:** se ejecutan ráfagas de Entrada/Salida
Estados posibles: **Ejecutando** o **No-Ejecutando**

**Estados**

● La principal responsabilidad del sistema operativo es controlar la ejecución de los procesos

● Asignar recursos

● Intercalarlos en el ejecución (asignar la CPU)

● Modelo de dos estados: Ejecutando / No Ejecutando


Perfecto, avancemos con el tema de **Estados de los procesos**, que es central en la materia.

---

# 📘 Estados de los procesos

Uno de los roles principales del **sistema operativo (SO)** es **controlar la ejecución de los procesos**.  
Esto implica tres grandes tareas:

1. **Asignar recursos** (CPU, memoria, archivos, dispositivos).
    
2. **Organizar la ejecución** de múltiples procesos en un sistema multiprogramado.
    
3. **Decidir qué proceso ejecuta la CPU en cada momento**, mediante algoritmos de planificación (scheduling).
    

Para poder cumplir con estas funciones, el SO representa a cada proceso dentro de un **modelo de estados**.

---

## 🔹 Modelo de dos estados (visión básica)

El modelo más simple para describir el ciclo de vida de un proceso distingue solo **dos estados posibles**:

1. **Ejecutando (Running):**
    
    - El proceso tiene el control de la CPU y está ejecutando sus instrucciones.
        
    - Solo **un proceso por CPU** puede estar en este estado al mismo tiempo.
        
2. **No ejecutando (Not Running):**
    
    - El proceso existe, pero **no tiene asignada la CPU**.
        
    - Puede estar listo para ejecutarse (**ready**) o esperando algún recurso (**waiting**, por ejemplo entrada/salida).
        

📌 Ejemplo:

- Cuando estás escribiendo en Word, ese proceso está en **ejecutando** mientras la CPU le dedica tiempo.
    
- Cuando la CPU cambia a reproducir música en Spotify, el proceso Word pasa a **no ejecutando**, pero puede volver a ejecutarse más tarde.
    

---

## 🔹 Limitación del modelo de dos estados

Aunque este modelo es útil para entender la idea básica de **ejecutar vs no ejecutar**, resulta demasiado **simplista** para sistemas reales.  
En la práctica, se utilizan **modelos con más estados** (por ejemplo, el clásico de 5 estados: nuevo, listo, ejecutando, bloqueado, terminado).

Sin embargo, el modelo de dos estados es el **punto de partida didáctico**:

- Sirve para introducir la noción de **intercalación** de procesos en la CPU.
    
- Muestra cómo el SO alterna entre **darle la CPU a un proceso** y **retirársela para asignársela a otro**.
    

---

## 📌 Resumen para repasar

- **Responsabilidad del SO:** controlar la ejecución de procesos, asignar recursos y decidir la planificación de la CPU.
    
- **Modelo de dos estados:**
    
    - **Ejecutando:** el proceso tiene la CPU.
        
    - **No ejecutando:** el proceso no tiene la CPU (puede estar listo o esperando).
        
- Aunque es un modelo simplificado, ayuda a comprender cómo el SO **intercala procesos** para compartir la CPU.
    

---

![[Modelo de 2 estados.png]]
---

No alcanza, es demasiado elemental.

![[Modelo de 5 estados.png]]
Mientras transcurre ese tiempo, que el proceso no esta listo para ejecutarse, ese proceso esta en estado "nuevo" se le da paginación, direcciones, estructuras de datos, registros para el proceso.
pasa un buen tiempo creándose el proceso.

Además, chekea que tenga los recursos. una ves listo, se toma como "listo/ready"

En exit hay que desarmarlo, desasignando sus espacios, sus archivos hay que cerrarlos, hay que matar a los hijos si corresponde, hay que registrar en una memoria, en unas tablas del so cuanto del procesador utilizo, cuanto e/s utilizo, información contable, llevar la contabilidad del proceso. marcar la memoria como limpia.


los bloqueados no tienen posibilidad de ejecutarse.

---
Otro modelo de proceso:
necesitamos que se pueda poner suspender (un estado adicional)

![[Modelo de 6 estados.png]]
El estado suspendido no esta en la memoria principal 
y entonces vamos a otro modelo:
![[Modelo de 7 estados.png]]Queda guardado en la memoria principal volátil.
La guardo en disco, sacando una foto antes de hacer el swap.

**Existen tablas para**:
*Memory
Devices
Files
Procesos

Un proceso es una construcción virtual. pero tiene esta forma concreta.

![[Diseño de proceso.png]]

Lo que movemos de un lado a otro, es una imagen del proceso.

requisitos para mover la imagen:
programa del usuario
armar pilas para que el programa a lo algo de su ejecución, guarde sus referencias de sus rutinas y subrutinas.
armar la pcb de un proceso (contexto de ejecución)

**Libros:**
1 Opción: Stallings
2 Opción: Silberschatz
3 Opción: Tanenbaum

Recomendación del profe leer el capitulo de procesos.

Próxima Clase: [[Clase 5]]