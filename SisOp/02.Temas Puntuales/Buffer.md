**Buffer**  
En sistemas operativos, un **buffer** es una región de memoria temporal utilizada para almacenar datos mientras se trasladan entre dos dispositivos o entre un proceso y un dispositivo. Su función principal es **amortiguar** las diferencias de velocidad o tamaño de transferencia entre el productor de datos (por ejemplo, la CPU o un programa) y el consumidor de datos (por ejemplo, un dispositivo de E/S).

Los controladores de dispositivos suelen implementar sus propios buffers internos para optimizar el flujo de datos y minimizar el tiempo de espera de la CPU. Cuando un programa solicita una operación de entrada/salida, es posible que el dispositivo no pueda recibir o entregar toda la cantidad de datos de una sola vez. El sistema operativo utiliza buffers para:

1. **Compensar diferencias de velocidad** entre dispositivos rápidos (como la memoria principal o la CPU) y dispositivos lentos (como discos duros, impresoras, o redes).
    
2. **Reducir la latencia** percibida por el programa, permitiendo que la CPU continúe ejecutando otras tareas mientras se completa la E/S.
    
3. **Agrupar o fragmentar transferencias** de datos para que se adapten al tamaño de bloque o al protocolo del dispositivo.
    
4. **Sincronizar** procesos productores y consumidores, evitando pérdida de datos en situaciones de desbordamiento o subalimentación.
    

En términos técnicos, el buffer actúa como **memoria intermedia** que permite desacoplar las tasas de producción y consumo, evitando cuellos de botella y mejorando la eficiencia global del sistema.