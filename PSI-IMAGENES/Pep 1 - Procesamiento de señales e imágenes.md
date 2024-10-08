
## Conceptos:

#### s1-cat1:

- **Procesamiento de imágenes:** Disciplina de la ciencia de computación que tiene como objetivo mejorar de algún modo la calidad de una imagen de entrada a través de operaciones de modo que facilite su análisi posterior

- **Análisis de Imágenes:** Aplicación de operaciones de nivel medio una vez que la imagen ya ha sido procesada, el análisis extrae información importante de ella

- **Reconocimiento de patrones:** Clasificar patrones presentes en una imagen como un elemento de un conjunto finito de posibles categorias

- **Visión por Computadora:** Describir el mundo que nos rodea mediante una o más imágenes

- **PAI y VC:** Son tareas difíciles debido a:
	1. Pérdida de informacion 3d->2d
	2. Interpretación
	3. Ruido e Incertidumbre
	4. Muchos datos
	5. Vista parcial de un mundo complejo


#### s1-cat2:

- **Señal:** Es una función que representa el comportamiento de algún fenómeno.

- **Formación de la imágen real:** La retina

- **Conos, bastones, punto ciego:** Conos se encargan de percibir los colores y los bastones tonos de grises, son altamente sensibles a ambientes oscuros

- **Errores de percepcion humana**
	- **Contraste simultáneo:** Un mismo color puede parecer más oscuro o claro dependiendo del color que lo rodee

	- **Ilusion Optica:** Percepciones visuales que difieren de la realidad. Estas pueden surgir debido a la forma en que el sistema visual interpreta el color, la luz, las sombras, las dimensiones y la perspectiva.

	- **Ambigüedad óptica:** Se refiere a imágenes o situaciones visuales que pueden ser interpretadas de dos o más maneras distintas. A diferencia de las ilusiones ópticas que "engañan" al cerebro para ver algo que difiere de la realidad, las imágenes ambíguas genuinamente contienen múltiples interpretaciones posibles, ninguna de las cuales es incorrecta.

- **Imagen Digital:** tonos de grises y color
	- El ojo humano es más sensible al verde>rojo>azul
	- **Filtro de Bayer**: el filtro se compone de una matriz de filtros de color rojo, verde y azul (RGB) colocados sobre el sensor de imagen. Este diseño aprovecha la mayor sensibilidad del ojo humano al verde, asignando el doble de píxeles a este color y 1/4 al rojo y azul. El filtro de Bayer es fundamental en la fotografía digital ya que permite a las cámaras con sensores de imagen en blanco y negro capturar imágenes a color sin necesidad de componentes adicionales o más complejos
	- **Imagen digital:** Matriz nxm que codifica una representación visual de una imagen real en forma de una matriz bidimensional en donde cada casilla de la matriz representa un pixel de la imagen donde se indica su intensidad de luz y color, si corresponde.
	- **RGB -> GRAY:** 
$$
GRAY = 0.299\cdot RED + 0.587 \cdot GREEN + 0.114 \cdot BLUE
$$
- **Muestreo y Cuantizacion:**

	
	- ￼￼Angulo del gradiente:￼￼ ￼
 
￼
	
	- Muestreo:  Discretiza el dominio de la función imagen. Define número de filas M y columnas N de la grilla. La interseccion se conoce como PIXEL (picture element)
	- Cuantización: Discretiza el rango de la función. Determina el número de niveles de intensidad de luz (niveles de voltaje L)
	- $L = 2^{8bits}=256$
	- $$ MUESTRO + CUANTIZACION = IMAGEN DIGITAL$$
- **Imagenes según espectro electromagnético:**
- **Histograma:** Frecuencia de ocurrencia de las intensidades de grises en una imagen. Es un arreglo de largo 256 en donde cada casilla corresponde a una intensidad de luz, el numero de cada casilla son las ocurrencias de dicha tonalidad.
- **Probabilidad de ocurrencia:** Probabilidad de que un pixel de cierta tonalidad esté en la imagen digital
- $$p(x)=\dfrac{\text{ocurrencias de x}}{\text{nro pixeles}}$$
- **Acumulacion de la imagen:**
- $$H(\lambda) = \sum_{j=0}^{\lambda-1} h(j)$$
- $H(\lambda):$ Frencuencia de aparicion de ciertos tonos de gris en la imagen menores que el tono $\lambda$ 
- *Ejemplo: Si $H(135)=69$ en la imagen existen 69 pixels con un tono menor que 135
```
histograma_acumulado histogramaAcumulado(imagen I):
	histA = crearArreglo(256)
	hist = histograma(I)
	histA[0] = hist[0]
	para j = 1 hasta largo(hist)-1:
		histA[j] = histA[j-1] + hist[j-1]
	retornar histA
```
- 

- Binarizacion, filtrado, deteccion de bordes, mejoramiento del contraste, morfología matemática y segmentación

#### s2-cat1:

**Operaciones T:** Operaciones sobre una imagen I que permiten generar otra imagen G procesando los pixeles de I (Puntual, Local Global)

- ##### Operaciones de punto: Negativo, Blending, Binarizacion

-  **Negativo:**  $G(x) = M - I(x)$ con $M=255$ (o máximo del espectro)

- **Blending:** Se ponderan los pixeles de cada imagen $G(x) = \alpha \cdot I_1 + (1-\alpha)\cdot I_2(x)$

- **Binarizacion(Thresholding):**

	- Objetivo: Separar el objeto de interés del fondo de la imagen. Genera GRAY -> B&W
	- 1 si supera umbral sino, 0
	
	- **Algoritmo de Otsu para binarizar:** Requiere o se parte desde el supuesto de que nuestra imagen tiene un histograma bimodal
	
		- **Objetivo:** Maximizar varianza entre clases
		
			- **Umbral:** valor que minimiza la dispersión intra-clase y maximiza la dispersion entre clases.
			
		- El algoritmo de Otsu es un método de umbralización automática que se basa en la variabilidad de los niveles de intensidad para separar una imagen en primer plano y fondo. Calcula el umbral que minimiza la varianza intraclase o maximiza la varianza entre clases asumiendo un histograma bimodal. La principal ventaja de Otsu es que no requiere intervención humana y es efectivo cuando hay una clara distinción entre los objetos y el fondo. Sin embargo, es sensible a las variaciones de iluminación y a las sombras, lo que puede resultar en un umbral menos óptimo cuando las condiciones de iluminación no son uniformes. Además, en histogramas con múltiples modas o ruido excesivo, su rendimiento puede disminuir significativamente, ya que su premisa se basa en la presencia de dos clases predominantes.
	- **Isodata**
	- **Binarizacion Adaptativa**: varianza y media local; niblack; savuola

| Característica                | Otsu                                            | ISODATA                                                                                    | Binarización Adaptativa                                        |
| ----------------------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------- |
| **Principio**                 | Maximizar la varianza entre clases              | Iterativo, busca el umbral que minimiza la varianza dentro de cada clase                   | Umbral local en función de las condiciones de la vecindad      |
| **Tipo de umbral**            | Global                                          | Global                                                                                     | Local                                                          |
| **Selección del umbral**      | Automática                                      | Automática, inicialmente puede ser manual                                                  | Automática                                                     |
| **Histograma**                | Bimodal                                         | Puede manejar más de dos modas                                                             | No se basa en el histograma                                    |
| **Sensibilidad a la luz**     | Sensible a variaciones globales                 | Menos sensible que Otsu, pero todavía afectado por condiciones de iluminación no uniformes | Alta adaptabilidad a variaciones de luz                        |
| **Ruido**                     | Sensible al ruido                               | Moderadamente sensible al ruido                                                            | Resistente al ruido local                                      |
| **Velocidad**                 | Rápido                                          | Más lento que Otsu debido a la iteración                                                   | Variable, depende del tamaño de la ventana de análisis         |
| **Aplicaciones típicas**      | Imágenes con buena separación de fondo y objeto | Imágenes con variaciones de intensidad y posiblemente múltiples modos                      | Imágenes con iluminación no uniforme o variabilidad de fondo   |
| **Complejidad computacional** | Baja                                            | Moderada                                                                                   | Alta (dependiendo del método de cálculo del umbral adaptativo) |

#### s2-cat2:

- **Filtrado Espacial**
	- **Objetivo:** Acentuar o disminuir características mediante la convolución. Requiere una vecindad definida alrededor de un punto y una operación que se realice en tal vecindad

| Característica                    | Correlación $\otimes$                                                                  | Convolución $\circledast$                                                                                 |
| --------------------------------- | -------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Definición**                    | Medida de similitud entre dos señales.                                                 | Operación matemática que combina dos funciones para formar una tercera función.                           |
| **Rotación de Kernel**            | No se rota el kernel antes de aplicarlo.                                               | El kernel se rota 180 grados antes de aplicarlo.                                                          |
| **Propósito en Imágenes**         | Comúnmente usada para coincidencia de patrones y detección de características.         | Utilizada para aplicar efectos como desenfoque, realce de bordes, entre otros.                            |
| **Resultado**                     | Alto cuando hay un fuerte parecido entre el kernel y la imagen en la región analizada. | El resultado depende de cómo el kernel modifica la región subyacente de la imagen.                        |
| **Uso en Aprendizaje Automático** | Menos común, pero puede usarse para comparar características.                          | Fundamental en redes neuronales convolucionales para aprendizaje de características.                      |
| **Invarianza**                    | Directamente dependiente de la forma del kernel y la señal de entrada.                 | Propiedad de invarianza espacial (las características se detectan independientemente de donde aparezcan). |
| **Simetría**                      | La operación es directa, sin cambios en la orientación del kernel.                     | Incorpora una simetría debido a la rotación del kernel.                                                   |
| **Enfoque**                       | Coincidencia directa y comparación de señales.                                         | Filtrado y transformación de señales.                                                                     |

- **Obs:** Si el filtro es simétrico tanto correlación como convolución generan el mismo resultado
- **Filtrado en extremos:** Existen alternativas como agregar un valor constante $k$ en los bordes del kernel que salgan de la imagen, replicar el borde de la imagen $xxy$, reflejar el borde de la imagen $xyx$, "envolver" los bordes de la imagen $zxxy..z$

- **Propiedades de la convolución:** Conmutativa, Asociativa, Linealidad

- **Filtros de Suavizamiento:** Permiten eliminar detalles y reducir ruido en imágenes

- **Ruidos:** Sal-pimienta (b&w), de impulso (w) y gaussiano (gray)

- **Filtros Lineales de suavizamiento:**

	- **Filtro Promedio (BOX FILTER):** Suma todos los pixels de la vecindad, promedia la suma y reemplaza el valor resultante en el pixel central. Ideal para ruido sal y pimienta.
	
	- **Filtro promedio ponderado:** Aplica un kernel cuyos valores varian espacialmente. Se pondera por el peso total del kernel
	
	- **Filtro Gaussiano:** Aplica un kernel que sigue una distribucion gaussiana y se pondera por el peso total del kernel.
	
	- **Filtro Promedio/Rango:** Promedia los pixels dentro del kernel que esten dentro de un rango determinado (El kernel va variando)

- **Filtros Lineales de Realce:** Kernel debe tener valores positivos cerca del centro y negativos lejos de este

	- **Filtro de Paso Alto:** El filtro de paso alto es un tipo de filtro que atenúa las bajas frecuencias y permite que las altas frecuencias pasen. En el contexto de las imágenes, las bajas frecuencias corresponden a áreas de cambio gradual en la intensidad (como regiones lisas o uniformes), mientras que las altas frecuencias corresponden a cambios abruptos (como bordes o detalles finos). El resultado de aplicar un filtro de paso alto es una imagen que tiene un aspecto más "nítido", con los bordes y detalles resaltados. 
	
	- $ORIGINAL = PASO\_ALTO + PASO\_BAJO$
	
		- **El procedimiento típico para aplicar un filtro de paso alto incluye:**
		
			- Definir un kernel que tenga valores positivos en el centro y negativos alrededor o viceversa, **asegurando que la suma de todos los valores sea cero o se acerque a cero**.
			
			- Convolucionar este kernel con la imagen.
			
			- Ajustar el resultado para evitar valores negativos de píxeles, generalmente sumando un valor constante o escalando el resultado.
			
	- **Filtro de Enfasis en Altas Frecuencias:** Este filtro es una variación del filtro de paso alto. No solo permite que pasen las altas frecuencias, sino que también las amplifica ($A$) para aumentar el contraste entre las áreas con altas frecuencias y el resto de la imagen. Este tipo de filtro puede diseñarse para controlar la cantidad de realce que se aplica a las altas frecuencias.
	- $$EAF = A \cdot ORIGINAL-PASO\_BAJO$$
	- $$EAF = (A-1) \cdot ORIGINAL + PASO\_ALTO$$
		- **El proceso de aplicación de un filtro de énfasis en altas frecuencias podría ser:**
		
			- Crear un kernel que, además de tener un diseño de paso alto, incluye un término adicional que amplifica las frecuencias altas.
			
			- Aplicar este kernel mediante convolución a la imagen.
			
			- Al igual que con el filtro de paso alto, realizar ajustes en la imagen resultante para asegurar que los valores de los píxeles son válidos.
			
	- *Una consecuencia de su aplicación es que también pueden realzar el ruido, por lo que a veces se utilizan en combinación con técnicas de suavizado para contrarrestar este efecto.*

- **Filtros NO lineales:**
	- Filtro mediana
	- Difusion anisotrópica

| Filtro                | Descripción y Funcionamiento                                                                                                                                                       | Eficacia contra Ruido Sal-Pimienta | Eficacia contra Ruido Gaussiano | Eficacia contra Ruido de Impulso |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|---------------------------------|----------------------------------|
| Mediana               | Reemplaza cada píxel por la mediana de su vecindad. Ordena los valores de intensidad dentro de una ventana y utiliza el valor mediano para suavizar la imagen.                        | Muy alta. Elimina eficazmente valores extremos. | Moderada. Puede suavizar pero hay filtros más adecuados. | Muy alta. Similar a la eficacia con ruido sal-pimienta. |
| Difusión Anisotrópica | Difunde los valores de píxeles basándose en un tensor de difusión que limita la difusión en los bordes. Permite más difusión en áreas homogéneas y menos en zonas con altos gradientes. | Alta. Limita la difusión alrededor de píxeles extremos preservando bordes. | Alta. Suaviza áreas homogéneas mientras preserva los bordes. | Alta. Restringe la difusión en áreas con altos gradientes. |

#### s3-cat1:

- **Deteccion de bordes:** Identificar cambios repentinos o discontinuidades en una imagen $GRAY \rightarrow GRAY$ 

	- Se generan por discontinuidad de la normal de la superficie, de profundidad, de color, de iluminación.

- **Caracterizacion de un borde:** Un borde se detecta en el lugar de *rápido* cambio de intensidad den la imagen -> derivada 
	
	- **Gradiente de una imagen:**  $\nabla I = [g_x,g_y]^T = [\frac{\partial I}{\partial x},\frac{\partial I}{\partial y}]^T$
	
	- **Magnitud del gradiente:** $mag(\nabla I) = \sqrt{g_x^2+g_y^2} \approx |g_x|+|g_y|$
	
	- **Angulo del gradiente:** $\alpha(x,y) = \tan^{-1}[\frac{g_y}{g_x}]$
	
	- *Dirección del cambio (gradiente) es perpendicular al borde* 
	
	- **Derivada parcial discretizada:** $$\frac{\partial f(x,y)}{\partial x} \approx \frac{f(x+1,y)-f(x+y)}{1}$$
		- $G_x = 0 \cdot (x-1,y) + (-1) \cdot I(x,y) + 1 \cdot I(x+1,y)$
		- $G_y = 0 \cdot (x,y-1) + (-1) \cdot I(x,y) + 1 \cdot I(x,y+1)$
		
		- Se puede resumir la detección de bordes en la convolución de una imagen con determinados kernels que aproximan las derivadas parciales en las direcciones horizontal y vertical
	
		- **Kernel en Gx:** $$G_x = [0,-1,1]$$
		- **Kernel en Gy:** $$G_y = [0,-1,1]^T$$
		- **Luego la imagen G resulta como:** $$mag(\nabla I) = \sqrt{g_x^2+g_y^2} \approx |g_x|+|g_y|$$
		- *G tiene los bordes en blanco por lo que se puede aplicar un negativo para dejar los bordes negros y lo demás blanco*
	
- ### Operadores de primer orden:

	- #### Operador de Roberts:
	
		- **Características**: Utiliza cálculo de diferencias diagonales para estimar la magnitud del gradiente en una imagen. Se caracteriza por ser especialmente sensible a bordes diagonales.
		
		- **Kernels:**
			- $$ G_x = \begin{bmatrix} +1 & 0 \\ 0 & -1 \end{bmatrix} $$
			- $$ G_y = \begin{bmatrix} 0 & +1 \\ -1 & 0 \end{bmatrix} $$
		- **Aplicación**: Convoluciona estos kernels con la imagen para detectar cambios en la diagonal. Es menos robusto al ruido y generalmente produce bordes menos definidos en comparación con otros operadores más modernos.
		- **Observaciones:** 
			- Pocos pixeles en la vecindad -> **muy sensible al ruido**
			- Máscara de 2x2 -> aproximación de $(i,j)$ en $(i+1/2$,$j+1/2)$

	- #### Operador de Prewitt:
	
		- **Características**: Similar al operador de Sobel, pero utiliza pesos uniformes en sus kernels, lo que le confiere menos sensibilidad a las variaciones de dirección en los bordes.
		
		- **Kernels**:
			- $$ G_x = \begin{bmatrix} -1 & 0 & 1 \\ -1 & 0 & 1 \\ -1 & 0 & 1 \end{bmatrix} $$
			  - $$ G_y = \begin{bmatrix} -1 & -1 & -1 \\ 0 & 0 & 0 \\ 1 & 1 & 1 \end{bmatrix} $$
		- **Aplicación**: Se utiliza para detectar bordes verticales y horizontales, siendo útil en imágenes donde los bordes son más rectos y menos variados.
		
		- **Observaciones:** Menos sensible al ruido en comparación con Roberts

	- #### Operador de Sobel
	
		- **Características**: Proporciona una mayor ponderación a los píxeles centrales de la región siendo evaluada, lo que resulta en una mayor precisión en la detección de bordes comparado con Prewitt y Roberts.
		- *Sobel=prewitt+f.gaussiano?*
		
		- **Kernels**:
			- $$ G_x = \begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix} $$
			- $$ G_y = \begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ 1 & 2 & 1 \end{bmatrix} $$
		- **Aplicación**: Sobel es ampliamente utilizado debido a su efectividad en resaltar tanto bordes verticales como horizontales en presencia de ruido. Es uno de los métodos preferidos para tareas de detección de bordes en imágenes en muchos campos, incluidos el médico y el industrial.
		
		- **Observaciones:** Sobel tiende a producir bordes más gruesos y precisos.

	- #### Método de Canny (histéresis?)
		1. **Detección Óptima:** Reducir respuesta al ruido -> Suavizado para reducir el ruido y variaciones de intensidad que pueden llevar a detecciones falsas.
		2. **Buena localización:** Aplicacion del operador de Sobel para determinar potenciales bordes
		3. **Respuesta única:** 
			1. **Supresión de No-Máximos**: Este paso implica la revisión de la imagen para asegurarse de que solo se conserven los máximos locales en la magnitud del gradiente de la imagen, lo cual es esencial para la "buena localización" del borde. Cualquier píxel que no sea un máximo local (es decir, si su magnitud no es mayor que la de sus vecinos en la dirección del gradiente) se suprime, lo que reduce potencialmente el grosor de los bordes a un píxel.
    
			2. **Histéresis**: Este proceso se refiere a la decisión de qué bordes son verdaderamente significativos basados en dos umbrales de magnitud del gradiente, denominados TH_HIGH (umbral alto) y TH_LOW (umbral bajo), y se realiza en tres pasos:
    
			    - **Fuerte**: Si la magnitud del gradiente en un píxel es mayor que el umbral alto (TH_HIGH), entonces el píxel se considera como parte de un borde fuerte.
			    - **Débil**: Si la magnitud del gradiente está entre los dos umbrales (TH_LOW y TH_HIGH), el píxel se considera como parte de un borde débil.
			    - **No Borde**: Si la magnitud del gradiente es menor que el umbral bajo (TH_LOW), el píxel no se considera como parte de un borde.
			1. **Conexión de Bordes Débiles y Fuertes**: Un borde débil se considera válido y se convierte en fuerte si está conectado a un borde fuerte, lo que significa que se puede trazar una línea de píxeles de borde fuerte hasta el borde débil en cuestión. Esto asegura que los bordes continuos no se interrumpan por fluctuaciones menores en la intensidad del gradiente.
    
			1. **Definición del Borde Final**: Los bordes finales se definen por los puntos fuertes, ya sean aquellos identificados directamente por superar el umbral alto o aquellos bordes débiles que están conectados a ellos. Esto garantiza que los bordes en la imagen final sean claros y representen con precisión las formas reales en la imagen.

### Operadores de segundo orden:
- #### Zero-Crossing
	- **Descripción**: Se basa en encontrar los cambios de signo en los valores de la imagen que indican la presencia de un borde. Típicamente, esto se utiliza después de aplicar un filtro que resalta las áreas donde se esperan cambios de intensidad, como el Laplaciano de Gaussiano.
	- **Kernel**: No utiliza un kernel específico por sí mismo, pero se aplica después de usar un operador que produce una salida donde los cruces por cero son significativos.

- #### Operador Laplaciano
	- **Descripción**: Es un operador de segundo orden que mide la segunda derivada de la imagen, capturando regiones donde hay una rápida transición de intensidades. Es isotrópico, reaccionando igualmente a bordes de todas las orientaciones.
	- **Kernel**: El Laplaciano puede tener varias formas, pero un ejemplo común es:
	- $$
  \begin{bmatrix}
  0 & 1 & 0 \\
  1 & -4 & 1 \\
  0 & 1 & 0
  \end{bmatrix}
  $$
  o, para tomar en cuenta las diagonales:
	- $$
  \begin{bmatrix}
  1 & 1 & 1 \\
  1 & -8 & 1 \\
  1 & 1 & 1
  \end{bmatrix}
  $$

- #### Laplaciano de Gaussiano (LoG)

	- **Descripción**: Este operador combina la detección de bordes del Laplaciano con el suavizado del filtro Gaussiano. El filtro Gaussiano se aplica primero para reducir el ruido y luego se aplica el Laplaciano para detectar los bordes.
	- **Kernel**: El LoG tiene un kernel que es la convolución de un Laplaciano con un Gaussiano, y su forma depende del tamaño del filtro y la desviación estándar del Gaussiano. No tiene una forma fija, ya que el filtro Gaussiano varía.

- #### Operadores de Kirsch
	- **Descripción**: Son un conjunto de 8 posibles convoluciones que responden a bordes en diferentes orientaciones. Se basan en la detección de máximos en la dirección del gradiente.
	- **Kernels**: Cada uno de los 8 kernels de Kirsch detecta bordes en una dirección diferente. Por ejemplo, uno de ellos es en cero grados es:
	- $$
  \begin{bmatrix}
  -1 & -1 & -1 \\
  0 & 0 & 0 \\
  1 & 1 & 1
  \end{bmatrix}
  $$
  Se rotan estos pesos para crear los 4 kernels, cada uno enfocándose en una orientación específica (Norte, Sur, Este, Oeste)

- Los operadores de segundo orden suelen ser más sensibles al ruido en comparación con los operadores de primer orden (como Sobel o Prewitt), por lo que el preprocesamiento con suavizado es comúnmente utilizado antes de aplicarlos. Los resultados de estos operadores no solo indican la presencia de un borde, sino también la naturaleza de la transición en intensidad en el borde, lo que puede ser beneficioso para ciertas aplicaciones que requieren una comprensión más detallada de la estructura de los bordes en la imagen.
#### s3-cat2:

- Mejoramiento del contraste
- Correccion Gamma
- Escalamiento Lineal
- Ecualización de Histograma
- Adaptive Histogram Equalization

#### s4-cat1:

- **Morfología matemática:** Simplificar/ destacar estructura de objetos en imagenes **conservando características de forma** GRAY->B&W

- Usos de la MM

- **Elemento Estructural:** Es una forma o nucleo que define la forma en que voy a procesar la foto. (4) Solo me interesan los pixels que están en gris y descarto los blancos "Extraigo objetos de la imagen"
	- Diferentes nucleos implican diferentes resultados, mascaras de unos (me importan) y ceros (no me importan)
	- (5) Busca representar discos de diferentes radios
	- **Objetos:** Conjunto de pixels blancos en una imagen
	- **Elemento estructural:** Conjunto de puntos que definen la forma del nucleo, puede contener elementos que no me importan (ceros)
	
- **Morfología Binaria**
	- **Dilatacion Binaria:** Expandir una imagen usando un elemento estructural dado. (7) Cada vez que $\cdot$ (centro del elemento estructural) caiga en parte del objeto de la imagen lo voy a copiar completo.
		- G comienza negra

	- **Erosión Binaria:** Reducción de una imagen I usando un elemento estructural E. Cada vez que el ES quepa completo en el objeto copio **solo el centro del objeto** a la imagen de salida

	- *La magia viene en elegir correctamente la forma y tamaño del elemento estructural*
	- Apertura = E + D (Puede eliminar objetos no deseados como "agujeros" en la imagen)
	- Clausura = D + E (Puede completar objetos incompletos como "agujeros")
	- *mnemotecnia: vocal con vocal, consonante con consonante*
	- Dualidad = Se utiliza de a dos *(como en slide 22)*
	- ¿Cómo extraer bordes con morfología? 
		- original-erosionado=borde
		- dilatacion-imagen=borde externo
		- dilatacion-erosion = borde morfologico
	- Adelgazar->Erosion; Engrosar->Dilatacion
	- Quitar Cachitos->Clausura
	- Operaciones de M.M son muy rápidas
	- Componentes convexos en lab s4
	- (24) Borde morfológico
	- (25) Buscar elemento mayor, quita puntos negros dentro de los main puntos blancos
- **Morfología en tonos de gris:** Fondo oscuro~0 y objeto claro~255
	- Si quiero ver un objeto claro y quiero expandirlo necesito que los pixels que lo rodeen se vuelvan mas claros
	- Elemento Estructural: Vecindad
	
	- Dilatacion: 
	- Erosion
	- Apertura
	- Clausura


