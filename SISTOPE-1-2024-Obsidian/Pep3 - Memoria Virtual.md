
# Requerimientos de un Sistema de Administración de Memoria

## 1. Re-ubicación: Capacidad del proceso para moverse entre memoria física. 
- La memoria virtual permite la traducción de las direcciones de memoria para poder almacenar en memoria principal o secundaria (Por confirmar con rannou)
## 2. Protección: Ningún proceso puede acceder/modificar mis datos o código si yo no lo permito.
- Chequeo de direcciones físicas se hace en tiempo de ejecución
- Hardware provee los mecanismos de protección ¿Cómo?


Preguntas para final de la clase
¿Se podría decir que:  La memoria virtual permite la traducción de las direcciones de memoria para poder almacenar en memoria principal o secundaria?

## 3. Compartición:

## 4. Organización Local

## 5. Organización Física

# Esquemas de particionamiento de memoria física RAM

## Particionamiento Fijo
- La memoria se divide en particiones del **mismo tamaño**.
- Si el _tamaño_proceso < tamaño_partición_ y existe una partición libre entonces el proceso puede ser cargado en memoria física.
- Si todas las particiones están ocupadas, el SO podría swapear a disco un proceso.
- Problemas:
	- ¿Qué pasa si el proceso no cabe?
		- Overlays
		- Particiones de distinto tamaño pero fijas
	- **Fragmentación Interna:** Espacio dentro de la partición no usada por el proceso
- Particionamiento fijo de la MF sin MV no es usado en sistemas modernos
## Particionamiento dinámico
- Procesos van ocupando solo el espacio que necesitan, pero se va generando **fragmentación externa**
- Se asume que se carga el proceso completo en memoria
- ![[Pasted image 20240730142131.png]]
### Algoritmos de Posicionamiento en Particionamiento dinámico

#### 1. Best-fit: 

- Usa el bloque de memoria (partición) más pequeño entre los suficientemente grandes para alojar el proceso
- Peor rendimiento, genera alta fragmentación externa
#### 2. Worst-fit:

- Usa el bloque de memoria (partición) más grande entre los suficientemente grandes para alojar el proceso

#### 3. First-fit:

- Busca desde el comienzo la primera partición que pueda alojar el proceso.
- El más veloz, generalmente produce los mejores resultados

#### 4. Next-fit: 

- Busca desde el _último espacio alocado_ la primera partición que pueda alojar el proceso.
- Rendimiento marginalmente peor que First Fit


# Método Buddy

- Genera fragmentación interna
- ![[Pasted image 20240730145622.png]]
- ![[Pasted image 20240730145633.png]]
- 