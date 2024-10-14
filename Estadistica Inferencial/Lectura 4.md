# Capítulo 7: Poder Estadístico

**Apunte: Poder Estadístico y Tamaño del Efecto**

- **Error Tipo I (α):** Rechazar la hipótesis nula (H0) cuando es verdadera. Se controla con el nivel de significación (α).
- **Error Tipo II (β):** No rechazar H0 cuando la hipótesis alternativa (HA) es verdadera.
  
**Relación entre α y β:** Reducir β (error tipo II) incrementa α (error tipo I), especialmente con muestras pequeñas.

### Poder Estadístico
- **Definición:** Probabilidad de rechazar correctamente H0 cuando es falsa (poder = 1 − β).
- **Importancia:** Un alto poder estadístico significa mayor capacidad para detectar un efecto real en lugar de una coincidencia.

### Tamaño del Efecto
- **Definición:** Medida de la magnitud de la diferencia o asociación entre grupos o variables.
- **Tipos de Medición:** Correlación, distancias entre medias, disparidades entre frecuencias.
- **Relevancia:** El tamaño del efecto ayuda a interpretar la importancia práctica de los resultados. Un resultado estadísticamente significativo puede no ser relevante si el tamaño del efecto es pequeño, y un resultado no significativo puede ser importante si el efecto es grande.

### Resumen:
- **Poder estadístico** = Capacidad de detectar un efecto real (evitar error tipo II).
- **Tamaño del efecto** = Magnitud de la diferencia, crucial para la interpretación práctica de los resultados.

## 7.1 Potencia de la Prueba Z

**Apunte: Potencia de la Prueba Z**

- **Diferencia entre medias (δ):** Es la medida del tamaño del efecto en la prueba Z, que permite cuantificar la magnitud de la diferencia entre medias poblacionales.
  
### Ejemplo práctico:
Lola Drones diseña un algoritmo que resuelve problemas de la mochila y realiza una prueba Z con las hipótesis:

- **H₀ (Hipótesis nula):** El tiempo medio de ejecución es 60 segundos (μ = 60).
- **H₁ (Hipótesis alternativa):** El tiempo de ejecución es diferente de 60 segundos (μ ≠ 60).

Lola usa una muestra de 36 instancias, un nivel de significación α = 0.05 y establece las regiones de rechazo en los cuantiles correspondientes. Si el tiempo promedio del nuevo algoritmo es de 55,8 segundos, la diferencia entre las medias sería δ = -4,2, lo que indica un tamaño del efecto.

### Probabilidad de rechazar H₀:
Lola calcula la probabilidad de que su hipótesis nula sea incorrecta, es decir, el poder estadístico de la prueba. El poder es del 55,57%, lo que significa que en ese porcentaje de las pruebas Lola detectaría correctamente la diferencia en el tiempo de ejecución.

### Error Tipo II:
La probabilidad de no detectar la diferencia, es decir, de cometer un error tipo II (β), es del 44,43%. Esto implica que Lola no sería capaz de detectar una diferencia de -4,2 segundos en casi la mitad de las muestras, debido a un bajo poder estadístico.



### 7.1.1 Cálculo del poder usando R

### 7.1.2 Relación entre el poder y el tamaño del efecto

### 7.1.3 Relación entre el poder y el nivel de significación

### 7.1.4 Relación entre el poder y el tamaño de la muestra

### 7.1.5 Ajustando los factores de una prueba de hipótesis

## 7.2 Potencia de la prueba T de student

### 7.2.1 Tamaño del Efecto de la prueba T

## 7.3 Potencia de la prueba de la diferencia de dos proporciones

## 7.4 Consideraciones Finales

## 7.5 Ejercicios Propuestos






# Capítulo 7: Poder Estadístico
## 7.1 Potencia de la Prueba Z

### 7.1.1 Cálculo del poder usando R

### 7.1.2 Relación entre el poder y el tamaño del efecto

### 7.1.3 Relación entre el poder y el nivel de significación

### 7.1.4 Relación entre el poder y el tamaño de la muestra

### 7.1.5 Ajustando los factores de una prueba de hipótesis

## 7.2 Potencia de la prueba T de student

### 7.2.1 Tamaño del Efecto de la prueba T

## 7.3 Potencia de la prueba de la diferencia de dos proporciones

## 7.4 Consideraciones Finales

## 7.5 Ejercicios Propuestos
