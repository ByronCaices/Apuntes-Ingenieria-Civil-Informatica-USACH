# Capítulo 5: Inferencia con medias muestrales

## 5.1 Prueba Z

## 5.2 Prueba T de student

### 5.2.1 Prueba T para una muestra

### 5.2.2 Prueba T para dos muestras pareadas

### 5.2.3 Prueba T para dos muestras independientes
## 5.3 Ejercicios Propuestos

# Capítulo 6: Inferencia con proporciones muestrales

## 6.1 Método de Wald

### 6.1.1 Método de Wald para una proporción
### 6.1.2 Método de Wald para dos proporciones

## 6.2 Método de Wilson

## 6.3 Ejercicios propuestos


¡Claro! Puedo complementar y enriquecer la información que has proporcionado, agregando descripciones más detalladas y orientadas para alguien que está iniciando en estadística inferencial.

---

### **Capítulo 5: Inferencia con Medias Muestrales**

La inferencia estadística con medias muestrales nos permite hacer conclusiones sobre una población basándonos en una muestra de datos. Es fundamental cuando queremos saber si una media poblacional difiere de un valor específico o si hay diferencias entre las medias de dos poblaciones.

#### **5.1 Prueba Z**

La **prueba Z** se utiliza para determinar si hay una diferencia significativa entre la media de una muestra y la media de la población. Esta prueba es apropiada cuando:

- La **desviación estándar de la población $\sigma$ es conocida**.
- El **tamaño de la muestra es grande** (generalmente $n > 30$), lo que permite que la distribución de la media muestral se aproxime a una distribución normal gracias al Teorema del Límite Central.

**Fórmula de la prueba Z:**

$$
Z = \frac{\bar{x} - \mu}{\frac{\sigma}{\sqrt{n}}}
$$

Donde:

- $\bar{x}$: Media muestral (promedio de los datos en la muestra).
- $\mu$: Media poblacional (valor hipotético o conocido de la población).
- $\sigma$: Desviación estándar de la población.
- $n$: Tamaño de la muestra.

**¿Cómo se interpreta el estadístico Z?**

El valor de Z nos indica cuántas desviaciones estándar está la media muestral $\bar{x}$ por encima o por debajo de la media poblacional $\mu$. Un valor de Z grande en valor absoluto sugiere que es poco probable que la diferencia observada sea por azar.

**Pasos para realizar una prueba Z:**

1. **Formular las hipótesis:**

   - **Hipótesis nula $H_0$**: La media muestral es igual a la media poblacional $\bar{x} = \mu$.
   - **Hipótesis alternativa $H_a$**: La media muestral es diferente de la media poblacional $\bar{x} \neq \mu$.

2. **Elegir el nivel de significancia $\alpha$**: Comúnmente se usa 0.05 (5%).

3. **Calcular el estadístico Z** usando la fórmula.

4. **Determinar el valor crítico o el p-valor** correspondiente al estadístico Z.

5. **Tomar una decisión**: Si el p-valor es menor que $\alpha$, se rechaza $H_0$; de lo contrario, no se rechaza $H_0$.

**Ejemplo sencillo:**

Supongamos que queremos saber si la altura promedio de los estudiantes de una universidad $\bar{x}$ es diferente de la altura promedio nacional $\mu$ que es de 170 cm, y conocemos la desviación estándar de la población $\sigma = 6$  cm.

#### **5.2 Prueba T de Student**

La **prueba T de Student** se utiliza cuando:

- La **desviación estándar de la población $\sigma$ es desconocida**.
- El **tamaño de la muestra es pequeño** (generalmente $n < 30$).

Esta prueba toma en cuenta la variabilidad adicional que se introduce al estimar la desviación estándar a partir de la muestra.

##### **5.2.1 Prueba T para una muestra**

**Fórmula de la prueba T:**

$$
T = \frac{\bar{x} - \mu}{\frac{s}{\sqrt{n}}}
$$

Donde:

- $s$: Desviación estándar de la muestra.

**Pasos para realizar una prueba T para una muestra:**

1. **Formular las hipótesis $H_0$ y $H_a$**.

2. **Elegir el nivel de significancia $\alpha$**.

3. **Calcular el estadístico T** usando la fórmula.

4. **Determinar los grados de libertad $df = n - 1$**.

5. **Encontrar el valor crítico o el p-valor** correspondiente al estadístico T y $df$.

6. **Tomar una decisión**: Comparar el p-valor con $\alpha$ o el estadístico T con el valor crítico.

**Ejemplo sencillo:**

Un investigador quiere saber si el tiempo promedio que tardan los estudiantes en resolver un examen es diferente de 60 minutos. Toma una muestra de 10 estudiantes (n = 10) y registra sus tiempos. Como \( \sigma \) es desconocida, usa la prueba T.

##### **5.2.2 Prueba T para dos muestras pareadas**

Esta prueba es adecuada cuando las muestras están relacionadas o emparejadas. Por ejemplo, mediciones antes y después de un tratamiento en los mismos sujetos.

**Fórmula de la prueba T para muestras pareadas:**

$$
T = \frac{\bar{d}}{\frac{s_d}{\sqrt{n}}}
$$

Donde:

- $\bar{d}$: Media de las diferencias entre los pares.
- $s_d$: Desviación estándar de las diferencias.

**Pasos para realizar una prueba T para muestras pareadas:**

1. **Calcular las diferencias** entre cada par de observaciones.

2. **Calcular la media $\bar{d}$ y la desviación estándar $s_d$ de las diferencias**.

3. **Formular las hipótesis**: Por ejemplo, $H_0: \bar{d} = 0$.

4. **Calcular el estadístico T**.

5. **Determinar los grados de libertad $df = n - 1$**.

6. **Tomar una decisión**.

**Ejemplo sencillo:**

Un nutricionista quiere evaluar si una dieta específica reduce el peso. Mide el peso de 15 pacientes antes y después de seguir la dieta durante un mes y aplica la prueba T para muestras pareadas.

##### **5.2.3 Prueba T para dos muestras independientes**

Esta prueba se utiliza para comparar las medias de dos muestras independientes, es decir, cuando no hay relación entre las observaciones de una muestra y la otra.

**Casos según la igualdad de varianzas:**

- **Varianzas iguales:** Se asume que las poblaciones tienen la misma varianza.
  
  **Estadístico T:**

  $$
  T = \frac{\bar{x}_1 - \bar{x}_2}{s_p \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}
  $$

  Donde:

  - $s_p$: Desviación estándar combinada (ponderada).

  $$
  s_p = \sqrt{\frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2}}
  $$

- **Varianzas desiguales:** No se asume igualdad de varianzas (prueba de Welch).

  **Estadístico T:**

  $$
  T = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}
  $$

  Los grados de libertad se calculan con una fórmula más compleja.

**Pasos para realizar una prueba T para muestras independientes:**

1. **Formular las hipótesis $H_0$ y $H_a$**.

2. **Realizar una prueba de igualdad de varianzas** (por ejemplo, prueba de F o de Levene).

3. **Calcular el estadístico T** utilizando la fórmula adecuada.

4. **Determinar los grados de libertad**.

5. **Tomar una decisión**.

**Ejemplo sencillo:**

Se quiere comparar el rendimiento académico promedio de estudiantes de dos métodos de enseñanza diferentes. Se toma una muestra de estudiantes de cada método y se aplica la prueba T para muestras independientes.

#### **5.3 Ejercicios Propuestos**

Esta sección incluye problemas prácticos que te permiten aplicar las pruebas Z y T en diversas situaciones. Practicar con estos ejercicios te ayudará a comprender mejor cómo y cuándo utilizar cada prueba, así como a interpretar los resultados.

---

### **Capítulo 6: Inferencia con Proporciones Muestrales**

Cuando trabajamos con datos categóricos (por ejemplo, éxito/fracaso, sí/no), nos interesan las proporciones. La inferencia con proporciones muestrales nos permite estimar proporciones poblacionales y comparar proporciones entre grupos.

#### **6.1 Método de Wald**

El **método de Wald** es una técnica clásica para estimar intervalos de confianza y realizar pruebas de hipótesis sobre proporciones. Es más adecuado cuando el tamaño de la muestra es grande.

##### **6.1.1 Método de Wald para una proporción**

**Estimación de la proporción poblacional $p$:**

- **Proporción muestral $\hat{p}$ **: Número de éxitos dividido por el tamaño de la muestra $\hat{p} = \frac{x}{n}$.

**Error estándar de la proporción:**

$$
SE(\hat{p}) = \sqrt{\frac{\hat{p}(1 - \hat{p})}{n}}
$$

**Intervalo de confianza:**

$$
\hat{p} \pm z^* \cdot SE(\hat{p})
$$

Donde $z^*$ es el valor crítico de la distribución normal estándar para el nivel de confianza deseado (por ejemplo, 1.96 para un 95% de confianza).

**Ejemplo sencillo:**

En una encuesta de 200 personas, 60 dicen preferir el producto A. Estimamos la proporción poblacional que prefiere el producto A y construimos un intervalo de confianza.

##### **6.1.2 Método de Wald para dos proporciones**

**Comparación de dos proporciones muestrales $\hat{p}_1$ y $\hat{p}_2$:**

**Error estándar de la diferencia de proporciones:**

$$
SE(\hat{p}_1 - \hat{p}_2) = \sqrt{\frac{\hat{p}_1(1 - \hat{p}_1)}{n_1} + \frac{\hat{p}_2(1 - \hat{p}_2)}{n_2}}
$$

**Estadístico Z para comparar proporciones:**

$$
Z = \frac{\hat{p}_1 - \hat{p}_2}{SE(\hat{p}_1 - \hat{p}_2)}
$$

**Ejemplo sencillo:**

Se quiere saber si hay diferencia en la proporción de éxito entre dos tratamientos médicos. Se compara la proporción de pacientes que mejoraron con el tratamiento A (\( \hat{p}_1 \)) y con el tratamiento B (\( \hat{p}_2 \)).

#### **6.2 Método de Wilson**

El **método de Wilson** mejora la estimación del intervalo de confianza, especialmente cuando la proporción está cerca de 0 o 1, o cuando el tamaño de la muestra es pequeño.

**Intervalo de confianza de Wilson:**

$$
\hat{p}_{\text{ajustada}} = \frac{\hat{p} + \frac{z^2}{2n}}{1 + \frac{z^2}{n}}
$$

**Error estándar ajustado:**

$$
SE_{\text{ajustada}} = \sqrt{\frac{\hat{p}(1 - \hat{p})}{n} + \frac{z^2}{4n^2}}
$$

**Intervalo de confianza:**

$$
\hat{p}_{\text{ajustada}} \pm z^* \cdot SE_{\text{ajustada}}
$$

**Ventajas del método de Wilson:**

- Proporciona intervalos más precisos y evita problemas del método de Wald en muestras pequeñas o proporciones extremas.

**Ejemplo sencillo:**

En un estudio con 20 pacientes, solo 2 mostraron una reacción adversa. Usando el método de Wilson, estimamos el intervalo de confianza para la proporción de reacciones adversas en la población.

#### **6.3 Ejercicios Propuestos**

Los ejercicios en esta sección te ayudarán a practicar la aplicación de los métodos de Wald y Wilson en la estimación y comparación de proporciones. Te enfrentarás a situaciones donde tendrás que decidir qué método es más adecuado y cómo interpretar los resultados.

---

**Consejos para principiantes:**

- **Comprende los conceptos básicos:** Antes de aplicar fórmulas, asegúrate de entender qué es una media, una proporción, la desviación estándar, y qué representan en tu contexto.

- **Sigue un enfoque paso a paso:** Al realizar pruebas estadísticas, sigue un proceso estructurado: formular hipótesis, elegir el nivel de significancia, calcular el estadístico, tomar decisiones.

- **Familiarízate con las distribuciones:** Conoce las características de la distribución normal y la distribución t de Student, y cuándo se utilizan.

- **Practica con datos reales:** Aplicar estos métodos a ejemplos del mundo real te ayudará a comprender mejor su utilidad y limitaciones.

- **Utiliza herramientas y tablas:** Las tablas de valores críticos y las calculadoras estadísticas pueden ser de gran ayuda.

- **No dudes en revisar conceptos:** Si algo no queda claro, revisa materiales introductorios o busca explicaciones adicionales. La estadística es un campo acumulativo; los conceptos se construyen unos sobre otros.

---

Espero que esta información ampliada y detallada te sea de gran ayuda en tu aprendizaje de la inferencia estadística. Si tienes más preguntas o necesitas aclaraciones adicionales, ¡no dudes en consultarme!