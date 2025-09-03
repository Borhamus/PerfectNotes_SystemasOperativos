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