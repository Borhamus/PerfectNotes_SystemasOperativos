## 📚 **Definición**

Un **bus** es un conjunto de líneas de comunicación físicas y protocolos asociados que permiten transferir datos, direcciones y señales de control entre los diferentes componentes de un sistema de cómputo.

Cuando se usa para concurrencia, el concepto clave es que:

- El bus **no es paralelo en uso**: aunque varios dispositivos pueden necesitarlo simultáneamente, solo **uno** puede tener control del bus en un instante dado.
    
- Esto introduce **competencia** (contention) y la necesidad de **arbitraje** para decidir quién lo usa y cuándo.
    

---

## 🔍 **Concurrencia en el bus**

En un sistema real, pueden coexistir varios “maestros” del bus:

- CPU (cuando accede a memoria o dispositivos)
    
- Controladores DMA (cuando transfieren datos)
    
- Otros coprocesadores o controladores inteligentes
    

Todos ellos **pueden solicitar acceso al bus de manera concurrente**. El problema de concurrencia es que:

- Si dos o más lo solicitan a la vez, hay que decidir **cuál tiene prioridad**.
    
- Si no se gestiona bien, puede haber **esperas largas** o **injusticia** (starvation).
    

---

## ⚙ **Mecanismos para manejar concurrencia en el bus**

1. **Arbitraje centralizado**  
    Un controlador de bus decide a quién se le concede acceso según prioridades predefinidas.
    
2. **Arbitraje distribuido**  
    Cada dispositivo participa en un protocolo de decisión para resolver conflictos sin un árbitro único.
    
3. **Priorización y fairness**
    
    - _Prioridad fija_: ciertos dispositivos siempre ganan (rápido pero puede causar starvation).
        
    - _Rotación (round-robin)_: turnos equitativos.
        
    - _Prioridad dinámica_: prioridades cambian según uso o antigüedad en la cola.
        

---

## 📌 En relación con Sistemas Operativos

- El SO debe **coordinar el acceso al bus** indirectamente, asegurando que las operaciones de E/S, memoria y DMA no generen cuellos de botella.
    
- El bus es un ejemplo de **recurso crítico**: no puede ser usado por más de un maestro a la vez, lo que lo convierte en un caso claro para aplicar **principios de sincronización y concurrencia** que también se usan en procesos e hilos.
