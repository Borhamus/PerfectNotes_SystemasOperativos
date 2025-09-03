# Algoritmo de Envejecimiento (Aging) / Promediación Exponencial

El **algoritmo de envejecimiento** es una técnica de planificación de CPU utilizada en sistemas operativos con **prioridades dinámicas**. Su objetivo principal es **prevenir la inanición (starvation)** de procesos de baja prioridad, asegurando que eventualmente tengan acceso a la CPU.

---

## 1. Problema que resuelve

En sistemas de **planificación por prioridad**:

- Los procesos de **alta prioridad** siempre se ejecutan antes que los de baja prioridad.  
- Esto puede causar **inanición**, es decir, que los procesos de baja prioridad **nunca lleguen a ejecutarse**.  

**Envejecimiento (Aging)** incrementa progresivamente la prioridad de los procesos que llevan mucho tiempo esperando, asegurando que todos tengan oportunidad de ejecutarse.

---

## 2. Concepto básico

Cada proceso tiene:

- **Prioridad base**: prioridad inicial asignada al proceso.  
- **Tiempo de espera**: cuánto tiempo ha estado en la cola de listos sin ejecutarse.  

La prioridad se **actualiza periódicamente** según el tiempo de espera.

### Fórmula de envejecimiento simple:

$$
\text{Prioridad}_{\text{nueva}} = \text{Prioridad}_{\text{actual}} + \alpha \cdot t_{\text{espera}}
$$

Donde:

- \( \alpha \) es el **factor de envejecimiento**, que controla la velocidad de incremento de prioridad.  
- La prioridad máxima está limitada para que un proceso de baja prioridad no sobrepase indefinidamente a los de alta prioridad.

---

## 3. Algoritmo paso a paso

1. **Inicialización:** Asignar **prioridad base** a cada proceso al crearlo.  
2. **Cola de listos:** Mantener los procesos ordenados por **prioridad actual**.  
3. **Recalcular prioridades periódicamente:** Cada quantum de CPU o intervalo de tiempo:

$$
\text{Prioridad}_{\text{nueva}} = \text{Prioridad}_{\text{actual}} + \alpha \cdot t_{\text{espera}}
$$

4. **Ejecutar proceso con mayor prioridad:** Elegir el proceso con **mayor prioridad actual** para la CPU.  
5. **Repetir el ciclo:** Cada intervalo se recalculan prioridades y se selecciona el próximo proceso.

---

## 4. Envejecimiento con Promediación Exponencial

En sistemas más avanzados, se combina el envejecimiento con **promedio exponencial** para estimar el **tiempo de uso futuro de CPU** de un proceso. Esto se usa especialmente en **planificación predictiva** (ej. SJF dinámico).

### Fórmula de promedio exponencial:

$$
\tau_{n+1} = \alpha \cdot t_n + (1 - \alpha) \cdot \tau_n
$$

Donde:

- \( \tau_{n+1} \) = tiempo estimado de CPU para el próximo burst.  
- \( t_n \) = duración real del último burst de CPU.  
- \( \tau_n \) = estimación previa del burst de CPU.  
- \( \alpha \) = factor de ponderación (0 < α < 1), regula el peso del último burst vs el historial.

**Interpretación:**

- Si \( \alpha \) cercano a 1 → ajuste rápido a los cambios recientes.  
- Si \( \alpha \) pequeño → suaviza la estimación, da más peso al historial.

---

## 5. Ejemplo práctico

Supongamos tres procesos con prioridad base:

| Proceso | Prioridad Base | Tiempo Espera (ms) |
|---------|----------------|------------------|
| P1      | 5              | 10               |
| P2      | 3              | 20               |
| P3      | 1              | 30               |

Con \( \alpha = 0.1 \), el envejecimiento simple recalcula:

$$
\begin{align*}
P1 &: 5 + 0.1 \cdot 10 = 6 \\
P2 &: 3 + 0.1 \cdot 20 = 5 \\
P3 &: 1 + 0.1 \cdot 30 = 4
\end{align*}
$$

**Resultado:**  

- P1 sigue siendo el de mayor prioridad,  
- P2 y P3 **suben prioridad progresivamente**, evitando starvation.

---

## 6. Resumen

- **Envejecimiento (Aging):** previene la **inanición** de procesos de baja prioridad.  
- **Prioridad dinámica:** se ajusta según **tiempo de espera**.  
- **Fórmula de envejecimiento:**

$$
\text{Prioridad}_{\text{nueva}} = \text{Prioridad}_{\text{actual}} + \alpha \cdot t_{\text{espera}}
$$

- **Promediación exponencial:** predice tiempo de CPU o ajusta prioridad suavemente:

$$
\tau_{n+1} = \alpha \cdot t_n + (1 - \alpha) \cdot \tau_n
$$

- **Ventaja:** asegura que todos los procesos sean atendidos, evitando starvation.  
- **Aplicación:** sistemas de **prioridad dinámica**, **SJF estimado**, **sistemas de tiempo compartido**.
