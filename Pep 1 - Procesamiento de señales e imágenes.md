
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
- *Ejemplo: Si $H(135)=69$ en la imagen existen 69 pixels con un tono menor que 135*

- Binarizacion, filtrado, deteccion de bordes, mejoramiento del contraste, morfología matemática y segmentación

#### s2-cat1:

- Operaciones T
- Operaciones de punto: Negativo, Blending, Binarizacion*
- Algoritmo de Otsu para binarizar
- Isodata
- Binarizacion Adaptativa

#### s2-cat2:

- Filtrado Espacial
- Filtros Lineales
- Nucleo de Convolucion (Máscara, kernel)
- Convolucion y correlación
- Propiedades de la convolución
- Filtros de Suavizamiento
- Ruidos: Sal-pimienta, de impulso y gaussiano
- Filtros Lineales de suavizamiento:
	-  Filtro Promedio (BOX FILTER)
	- Filtro promedio ponderado
	- Filtro Gaussiano
	- Filtro Promedio/Rango
- Filtros Lineales de realce:
	- Filtros de paso alto
	- Filtro de enfases en altas frecuencias
- Filtros NO lineales:
	- Filtro mediana
	- Difusion anisotrópica

#### s3-cat1:

- Deteccion de bordes
- Caracterizacion de un borde
- Gradiente de una imagen
- Magnitud y angulo del gradiente
- Operadores de primer orden:
	- Operador de Roberts
	- Operador de Prewitt
	- Operador de Sobel
	- Método de Canny (histéresis?)
- Operadores de segundo orden:
	- Zero-Crossing?
	- Operador Laplaciano
	- Laplaciano de Gaussiano
	- Operadores de Kirsch

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
