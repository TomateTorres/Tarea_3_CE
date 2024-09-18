## Ejercicio 1
### 1. Codificación de ejemplares y soluciones
#### - Considerando el formato especificado en TSPLIB, implementa un algoritmo que lea un archivo con ejemplares para el TSP.
  Empleando la documentación de la librería [TSPLIB] http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/tsp95.pdf nos basamos en el formato de los archivos para su lectura en _python_; cada archivo consiste en una parte de especificaciones y una parte para los datos. 
  La primera parte especifica las características del ejemplar con el formato _palabra clave : valor_, donde todas las palabras claves que se pueden utilizar, son: NAME, TYPE, COMMENT, DIMENSION, CAPACITY, EDGE_WEIGHT_TYPE, EDGE_WEIGHT_FORMAT, NODE_COORD_TYPE, DISPLAY_DATA_TYPE, EOF, entre otros que pueden ser opcionales según el ejemplar. Por lo tanto, observamos que dependiendo del archivo pueden variar los atributos que se vean mencionados, entonces no podemos empezar a leer el archivo desde una línea en particular. Sin embargo, notemos que cada una de estas palabras clave tiene un caracter en común, ":". Nos basamos en esta observación para almacenar las características del ejemplar en un diccionario, pues al momento de leer el archivo, si encuentra el caracter ":", va a dividir la cadena que esté leyendo en dos: lo que haya antes de los dos puntos (la palabra clave) y lo que exista después (el valor asociado a este atributo)
## Ejercicio 2:

Primero, implementamos un operador de intercambio de dos elementos consecutivos para permutaciones:
1. Definimos una función llamada `operadorCambioConsecutivo()` que recibe como parámetros una permutación (en formato de lista) y un índice.
2. Creamos una nueva copia de la lista `permutacion` para no modificar la original y la guardamos en `nuevaPermutación`.
3. Si el índice proporcionado no es válido, se retorna simplemente la copia de la lista original.
4. Si el índice proporcionado es válido, intercambiamos el elemento al que corresponde el índice con el siguiente en la lista y retornamos la lista modificada. 

Luego, implementamos un operador de intercambio de dos elementos no necesariamente consecutivos:
1. Definimos una función llamada `OperadorNoConsecutivo()` que toma una lista `permutacion` y dos números (`indice1` y `indice2`).
2. Creamos una nueva copia de la lista `permutacion` para no modificar la original y la guardamos en `nuevaPermutación`.
3. Si alguno de los índices proporcionados no es válido o estos son iguales, se retorna simplemente la copia de la lista original.
4. Si los índices proporcionados son válidos y distintos, se intercambian los elementos correspondientes a los índices y se retorna la lista modificada.

Finalmente, implementamos un operador que parte a la lista en dos partes y las intercambia:
1. Definimos una función llamada `OperadorInvParticion()` que recibe como parámetros una permutación (en formato de lista) y un índice.
2. Creamos una nueva copia de la lista `permutacion` para no modificar la original y la guardamos en `nuevaPermutación`.
3. Si el índice proporcionado no es válido, se retorna simplemente la copia de la lista original.
4. Si el índice proporcionado es válido, dividimos la lista en dos partes: la primera parte va desde el primer elemento (que tiene índice `0`) hasta el índice dado y la segunda desde `indice + 1` al final de la lista. Se retorna la lista modificada.
