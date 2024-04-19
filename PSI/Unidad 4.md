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