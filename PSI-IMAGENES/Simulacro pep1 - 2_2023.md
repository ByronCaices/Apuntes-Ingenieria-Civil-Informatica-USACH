
#### Pregunta 1:
*Discutir, en general, cuál sería el efecto en el histograma de una imagen si se ponen en cero si se ponen en cero los bits menos significativos de cada pixel. Y si en cambio se ponen en cero los bits más significativos*

**Poner en cero el LSB**
Sea por ejemplo las tonalidades de grises 10, 150 y 250

Que en binario se verían como:

- 128+64+32+16+8+4+2+1
	- 10 = (0000 1010)
	- 150 = 128+0+0+16+0+4+2+0 = 1001 0110
	- 250 = 128+64+32+16+4+2+1 = 1111 1010

y notamos que si ponemos en cero su bit menos significativo no ocurren cambios, esto ya que son numeros pares pero en el caso de un número impar como el 251 = 1111 1011 por ejemplo, ocurre que si el bit menos significativo lo dejamos en cero sería equivalente a restarle 1 pasando a ser este bit de intensidad 251 a 250. Si aplicamos esto a todas las intensidades de gris de un histograma tendremos como resultados que todos los pixels con intensidad impar pasaran a tener intensidad par por 1 unidad menos. 

Lo que visualizaríamos en el histograma de la imagen es que tiene espacios vacíos o cortes denotados por 0 ya que no hay pixels con intensidad impar y visualmente la imagen no variaría mucho, solo tendería a disminuir su intensidad de blancos levemente. Al ojo humano le cuesta diferenciar entre una intensidad 251 y 250 hasta diría que no nota la diferencia pero el histograma nos serviría para evidenciar este hecho

**Poner en cero el MSB**

Tomando como ejemplo las tonalidades anteriormente mencionadas pero agregando el 127

- 10 = (0000 1010)
- 127 = (0111 1111)
- 150 = 128+0+0+16+0+4+2+0 = (1001 0110)
- 250 = 128+64+32+16+4+2+1 = (1111 1010)
- 251 = 128+64+32+16+4+2+1 = (1111 1011)

Modificar el MSB solo afecta a intensidades mayores o iguales a 128 ya que es el primero en tener un 1 en el bit más significativo siendo (1000 0000) luego afecta también al 129 siendo (1000 0001) y así en adelante, entonces si ponemos en cero el MSB ocurrirá que para toda intensidad de gris mayor o igual a 128 se le restarán 128 unidades de intensidad, así el 128 = 1000 0000 pasaria a ser 0, el 129 = 1001 0001 pasaría a ser 1, y así con todos los demás pixeles dentro de este conjunto.

En el histograma visulizaríamos que a partir del 128 en adelante no tenemos presencia de intensidades y se agruparían a la izquierda del histograma las intensidades. Visualmente la imagen se oscurecería y carecería de tonalidades claras, predominando solo las tonalidades negras a grises.

![[pregunta3.png]]
