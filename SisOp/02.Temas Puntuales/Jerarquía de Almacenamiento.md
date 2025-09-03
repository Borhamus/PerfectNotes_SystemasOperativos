

La **jerarquía de almacenamiento** es la organización de los distintos tipos de memoria y dispositivos de almacenamiento de un sistema computacional, ordenados según:

1. **Velocidad de acceso** (rápida en la cima, lenta en la base).
    
2. **Costo por bit** (caro arriba, barato abajo).
    
3. **Capacidad de almacenamiento** (baja arriba, alta abajo).
    

---

### 📊 **Estructura típica** (de arriba hacia abajo)

| Nivel                                  | Tipo de memoria                   | Velocidad               | Capacidad          | Costo/bit | Volatilidad |
| -------------------------------------- | --------------------------------- | ----------------------- | ------------------ | --------- | ----------- |
| **Registro de CPU**                    | Dentro del procesador             | Nanosegundos            | Bytes              | Muy alto  | Volátil     |
| **Cache L1 / L2 / L3**                 | En o cerca de la CPU              | Nanosegundos            | KB–MB              | Alto      | Volátil     |
| **Memoria principal (RAM)**            | DRAM                              | Decenas de ns           | GB                 | Medio     | Volátil     |
| **Almacenamiento secundario**          | SSD / HDD                         | Micro–milisegundos      | Cientos de GB – TB | Bajo      | No volátil  |
| **Almacenamiento terciario / offline** | Cintas magnéticas, discos ópticos | Milisegundos – segundos | TB–PB              | Muy bajo  | No volátil  |

---

### 🔍 **Características clave**

- **Principio de localidad**: La jerarquía aprovecha que los programas tienden a acceder repetidamente a un conjunto pequeño de direcciones en un corto período de tiempo (_localidad temporal_) y a direcciones cercanas (_localidad espacial_).
    
- **Transferencia por bloques**: Los datos suelen moverse en bloques desde niveles más lentos hacia niveles más rápidos para anticipar accesos futuros.
    
- **Intercambio automático**: Las capas superiores y medias suelen manejarse mediante mecanismos de _cache_ y _swap_ controlados por hardware y/o el SO.
    

---

### 📌 En el contexto de un SO

El Sistema Operativo:

- Gestiona la **memoria principal** y la asignación de espacio en dispositivos de almacenamiento.
    
- Implementa mecanismos como **memoria virtual** para extender la capacidad aparente de la RAM usando almacenamiento secundario.
    
- Optimiza el uso de caches de disco y búferes para reducir accesos a dispositivos lentos.
    
