**Definición**  
Según _Silberschatz, Galvin & Gagne_ y _Tanenbaum_, el **DMA** es un mecanismo de hardware (un módulo o controlador) que permite que ciertos dispositivos de E/S transfieran datos directamente hacia o desde la memoria principal **sin la intervención continua de la CPU**.

El **módulo DMA** actúa como un “miniprocesador especializado” que:

1. **Recibe de la CPU** la información necesaria para la transferencia:
    
    - Dirección de origen y destino en memoria.
        
    - Cantidad de datos a transferir.
        
    - Dirección o puerto del dispositivo.
        
    - Dirección de control (lectura o escritura).
        
2. **Se comunica directamente con el controlador del dispositivo**  
    Una vez configurado, el DMA maneja la transferencia bloque a bloque o palabra a palabra, sincronizándose con el dispositivo de E/S.
    
3. **Libera a la CPU**  
    La CPU no necesita copiar cada byte/palabra; puede dedicarse a ejecutar otros procesos mientras el DMA se encarga de mover los datos.
    
4. **Interrumpe a la CPU solo al finalizar**  
    Cuando la transferencia termina (o si hay un error), el DMA envía una **interrupción** para informar al sistema operativo que la operación ha concluido.
    

---

### 🔍 **¿Qué problemas resuelve?**

- **Reduce carga de CPU**: sin DMA, la CPU tendría que mover datos uno por uno mediante instrucciones de E/S.
    
- **Mejora el rendimiento** en transferencias masivas (discos, redes, audio, video).
    
- **Permite paralelismo**: CPU ejecuta tareas mientras DMA mueve datos.
    

---

### 📊 **Flujo típico de operación DMA**

1. CPU configura el módulo DMA con parámetros de transferencia.
    
2. DMA solicita el control del bus (arbitraje con la CPU).
    
3. DMA transfiere datos entre memoria y el dispositivo.
    
4. DMA libera el bus.
    
5. DMA genera una interrupción a la CPU para informar finalización.
    

---

💡 **Importante**:  
El **DMA** no es un _trap_ (trampa por software), porque no es una interrupción generada por código, sino un módulo de hardware que eventualmente **genera una interrupción** al terminar, pero su operación es independiente de la CPU.