**Definición más formal**  
Según **Silberschatz, Galvin & Gagne**, un **Sistema Operativo** es un programa que actúa como intermediario entre el usuario y el hardware, y que coordina el uso de los recursos del sistema. Una de sus características clave es que está diseñado como un **sistema impulsado por interrupciones** (_interrupt-driven system_).

Esto significa que el SO normalmente **no ejecuta continuamente un bucle de espera activa** revisando si un evento ocurrió (lo que sería ineficiente). En su lugar:

1. **Estado inactivo o ejecución de usuario**  
    El SO permite que la CPU ejecute programas de usuario o permanezca en espera mientras no haya eventos que requieran atención.
    
2. **Eventos externos o internos generan interrupciones**
    
    - **Hardware interrupts**: señales del hardware (ej. un dispositivo de E/S terminó su tarea, llegada de un paquete de red, fin de temporizador).
        
    - **Software interrupts** (o _traps_): invocaciones de sistema hechas por programas (ej. `read()`, `write()`, manejo de errores).
        
3. **Cambio de contexto y atención al evento**  
    Cuando ocurre una interrupción, el flujo normal de ejecución se detiene, la CPU guarda su estado (_contexto_) y transfiere el control a la rutina de servicio de interrupción (ISR) del SO.
    
4. **Retorno a la tarea anterior**  
    Una vez atendida la interrupción, el SO restaura el contexto y continúa la ejecución del proceso que estaba corriendo o despacha otro según la planificación.
    

---

💡 **Por qué es importante que sea interrupt-driven**

- Permite **multitarea eficiente**: el SO no desperdicia ciclos de CPU revisando constantemente el estado de los dispositivos.
    
- Favorece la **respuesta rápida** a eventos externos.
    
- Es esencial para **sincronizar** hardware y software.
    
- Minimiza la **latencia** en operaciones de entrada/salida.