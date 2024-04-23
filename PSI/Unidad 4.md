
# s5-cat2
# Transformaciones Geométricas

Corresponden a transformaciones espaciales, es decir, no cambian los pixels sino las coordenadas $(x,y)$ de la imagen

 
¿Para que queremos hacer esto? Por ejemplo 
- Para alinear imágenes en fotografías panorámicas
- Tomar fotos desde orientaciones incorrectas y quiero que parezca tomada de frente

$$u = f_1(x,y)$$
$$v = f_2(x,y)$$Buscamos hacer una transformación mediante el cambio de coordenadas
 (X,Y) -> (U,V)
![[Pasted image 20240418114648.png]]
Una transformación geométrica transforma una imagen I a una nueva imagen I' modificando las coordenadas de los pixels de la imagen

Interpolación: Para discretizar* los valores de las nuevas coordenadas

(\*): creo que ese termino es incorrecto para este caso

Transformación geométrica consiste de:
- Transformación de coordenadas
- Interpolación de intensidades

### Tipos de transformaciones geométricas

- Traslación
- Escalamiento (Contraer o Estirar):
	- Escalamiento uniforme: Cuando $s_x$ y $s_y$ son iguales

- Shearing o afinamiento: Lineas verticales se "acuestan" 
- Rotación

#### Clasificación de transformaciones

- **Transf. Euclidiana** = rotación + traslación
	- (11) El 1 de abajo se conoce como la coordenada homogénea, solo existe para que nos permita realizar la operación de multiplicación entre matrices
	- invariante a
- **Transf. de similitud:** Escalamiento + rotación + traslación
	- Ángulos, lineas paralelas, razón entre longitudes, razón entre áreas de objetos
- **Transf. Afín:** Escalamiento no isométrico + rotación + traslación
	- colinealidad de puntos: si un punto esta antes que otro o después, esto se mantiene
- **Transf de proyección:** Deforma al objeto y solo mantiene la colinealidad
	- Sirve para cambios de perspectiva
	- Stitching

Grados de libertad:
	menos grados -> menos se va a distorsionar la forma de objetos
	mas grados -> mas se va a distorsionar la forma de los objetos
### Coordenadas Homogéneas

**Como encontrar la tranformación**
(29) Voy eligiendo puntos de interés entre las imágenes y los coloco en las matrices P Y Q.

**Interpolación**
- **Forward Mapping:** Tomo mi imagen original y para cada pixel en esa imagen original, calcularé la nueva imagen y luego tomo el color imagen original y lo pongo en la imagen de salida
- **Inverse Mapping:** Para cada pixel de I' qué color le pongo en base a lo que tengo en I

# s6-cat1
# Transformada de Hough

## Detección de líneas

- Busca las lineas rectas, pq? porque los objetos están caracterizados por rectas, su forma. ¿Porque no uso detectores de bordes? Cuando usamos estos a ellos no le importa si es una linea o circunferencia, solo ve un cambio de brusco de tonalidad y detecta el borde pero no verifica qué es.

- Según cant de puntos puedo saber cuantas lineas hay. Hough toma puntos detectados 
- Entrada: Una imagen de bordes binaria (Sobel, canny)
- Ecuación de recta:
- $$y = kx + d$$
- Todos los puntos $(x,y)$ que cumplen con una pendiente $k$ e intercepto $d$
- Por cada punto cualquiera pueden pasar multiples lineas, pero por cada cual participe tendrá una pendiente e intercepto diferente ¿Como asignamos a la linea que corresponde? **Trasladamos a espacio de parámetros de hough**
- $(x,y) \rightarrow(pendiente, intercepto)$
- Un punto aqui representa una linea por allá
- Si yo tengo muchos puntos de borde, de cada uno puedo sacar las lineas que corresponden en el espacio de hough
- Muchas intercepciones en hough = muchos votos -> puedo dibujar en la imagen todos los $(x,y)$ con $(pendiete,intercepto)$ con más votos
- Problemas con lineas rectas verticales -> debemos usar coordenadas polares ya que las pendientes en coordenadas cartesianas pueden generar pendientes indeterminadas
$$x = r \cdot \cos{\theta}$$
$$y = r \cdot \sin{\theta}$$
- $(x,y) \rightarrow (\theta,r)$ de punto a sinusoidal (en vez de recta)
- Si 2 sinusoidal interceptan -> hay dos (x,y) en recta en la imagen
- Se traduce a matriz acumuladora
### Algoritmo de transformada de Hough para detectar líneas rectas

```
//Inicializar con ceros matriz acumuladora
H[d,theta] = 0
For cada punto borde en la imagen:
	for theta = 0 to 180:
		d = x*cos(theta)-y*sin(theta)
		H[d,theta] += 1
Find the value(s) of (d,theta) where H[d,theta] is maximum
Te quedas con las N lineas maximas y pintas esos puntos en la imagen original
```
- Una línea cartesiana por cada intercepción en el espacio polar de Hough
-  


## Detección de círculos

$$ (x_i - a)² + (y_i - b)² = r²$$
- Tenemos dos métodos, sabiendo el radio o no
- A partir de la dirección del gradiente puedo identificar el radio
```
For every edge pixel:
	For each possible radius value:
		For each possible gradient direction
		//or use estimated gradient
			a = ...
			
```
