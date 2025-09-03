## 📚 **1. Paginación con segmentación**

La paginación y la segmentación son dos técnicas distintas de gestión de memoria.  
En **paginación con segmentación** se combinan para aprovechar ventajas de ambas:

- **Paginación**: divide la memoria física en marcos de tamaño fijo, y la memoria lógica en páginas del mismo tamaño.
    
- **Segmentación**: divide el espacio lógico en segmentos que representan unidades lógicas de un programa (código, datos, pila).
    

💡 **Cómo se combinan**

- Cada **segmento** se divide internamente en **páginas**.
    
- Cada segmento tiene su **tabla de páginas** correspondiente.
    
- La dirección lógica se especifica como:
    
    ```
    (número de segmento, número de página, desplazamiento)
    ```
    
- El sistema usa la **tabla de segmentos** para localizar la **tabla de páginas** correcta, y luego la tabla de páginas para encontrar el marco físico.
    

**Ventajas**:

- Flexibilidad lógica de segmentación + control simple de fragmentación de la paginación.
    
- Permite protección y compartición a nivel de segmento.
    

---

## 📚 **2. Tablas de páginas invertidas**

- En paginación tradicional, cada proceso tiene su propia tabla de páginas, lo que consume mucha memoria si el espacio de direcciones es grande.
    
- En una **tabla de páginas invertida**, hay **una sola tabla global para todo el sistema**, con **una entrada por cada marco de memoria física**, no por cada página lógica.
    
- Cada entrada indica **qué página de qué proceso** está ocupando ese marco.
    
- Para traducir una dirección lógica → física:
    
    1. Se busca en la tabla invertida (normalmente usando un _hash_) el marco que corresponde a `(id_proceso, num_página)`.
        
    2. Se obtiene el marco físico y se suma el desplazamiento.
        

**Ventajas**: ahorro de memoria en la tabla.  
**Desventaja**: traducción más lenta, requiere búsquedas y TLB eficientes.

---

## 📚 **3. Memoria virtual**

- **Concepto**: La memoria virtual es una abstracción que permite a un proceso tener un espacio de direcciones lógico mucho mayor que la memoria física real.
    
- Permite que los programas se carguen parcialmente en memoria y el resto permanezca en almacenamiento secundario, trayendo las partes necesarias bajo demanda.
    
- Se implementa mediante **paginación bajo demanda** o **segmentación bajo demanda**.
    

**Objetivos**:

1. Ejecutar programas más grandes que la memoria física.
    
2. Aislar procesos entre sí (protección).
    
3. Optimizar uso de memoria física.
    

---

## 📚 **4. Swapping**

- **Definición**: Técnica donde **un proceso completo** se copia temporalmente desde la memoria principal a almacenamiento secundario (por ejemplo, disco), para liberar memoria para otros procesos.
    
- Cuando el proceso necesita ejecutarse nuevamente, se trae de vuelta a memoria.
    
- Puede ocurrir:
    
    - **Total**: el proceso entero se mueve.
        
    - **Parcial**: solo algunas partes (páginas o segmentos).
        
- El área de disco usada para esto se llama **área de swapping** o _swap space_.
    

**Diferencia clave con paginación bajo demanda**:

- En _swapping_ tradicional se mueven bloques grandes (todo el proceso).
    
- En _paginación bajo demanda_ solo se cargan páginas necesarias.
    