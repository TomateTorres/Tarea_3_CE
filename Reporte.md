# Ejercicio 1
## 1. Codificación de ejemplares y soluciones
#### - Considerando el formato especificado en TSPLIB, implementa un algoritmo que lea un archivo con ejemplares para el TSP.
  Empleando la documentación de la librería [TSPLIB](http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/tsp95.pdf)nos basamos en el formato de los archivos para su lectura en _python_; cada archivo consiste en una parte de especificaciones y una parte para los datos. 
  
  La primera parte especifica las características del ejemplar con el formato _palabra clave : valor_, donde todas las palabras claves que se pueden utilizar, son: 
  - NAME
  - TYPE
  - COMMENT
  -  DIMENSION
  -  CAPACITY
  -  EDGE_WEIGHT_TYPE
  -  EDGE_WEIGHT_FORMAT
  -   NODE_COORD_TYPE
  -   DISPLAY_DATA_TYPE
  -   EOF
    
Entre otros que pueden ser opcionales según el ejemplar. Por lo tanto, observamos que dependiendo del archivo pueden variar los atributos que se vean mencionados, entonces no podemos empezar a leer el archivo desde una línea en particular. Sin embargo, notemos que cada una de estas palabras clave tiene un caracter en común, ":". Nos basamos en esta observación para almacenar las características del ejemplar en un diccionario, pues al momento de leer el archivo, si encuentra el caracter ":", va a dividir la cadena que esté leyendo en dos: lo que haya antes de los dos puntos (la palabra clave) y lo que exista después (el valor asociado a este atributo). La función que devuelve los datos del ejemplar es `lectura_archivo()` y además imprime en pantalla los atributos de interés, que son los que corresponden al nombre, dimensión del ejemplar.

En la sección de datos, las primeras columnas que tenemos corresponden al _número de nodo_,y sus coordenadas. Los ejemplares utilizados fueron definidos en $\mathbb{R}^{2}$, por lo que sus coordenadas son en _x_ y en _y_. En otros ejemplares da información adicional. Entonces con la librería `pandas` guardamos la información mencionada en un _DataFrame_. 

A partir de los _n_ nodos y sus coordenadas, calculamos las distancias de _i_ a _j_ $d_{ij}$ para cualesquiera dos nodos de la gráfica, y las almacenamos en una matriz de $ n \cdot n$ que es la _matriz de distancias_; es importante guardarla en una función para llamarla las veces necesarias y no realizar los cálculos una y otra vez, sino que sólo los consultaríamos, esta matriz estará disponible con la función `matriz_distancias()`, cuya métrica será la euclidiana en $\mathbb{R}^{2}$, pues así lo especifican los ejemplares.

### - Implementa un algoritmo para generar soluciones aleatorias para el TSP, utilizando algún esquema de codificación basado en permutaciones

Para el ejemplar con _n_ nodos (ciudades), las soluciones se codificarán como vectores de n entradas. Donde los elementos en el arreglo son el número que identifica a cada uno de los nodos (ciudad) en el ejemplar y sus posiciones en el vector corresponden al orden en el cual se recorrerán las ciudades. 

Por otra parte, en un ejemplar de tamaño _n_ se tienen $n!$ permutaciones, para reducir este espacio fijamos a la primera ciudad (que se identifica con el _nodo 1_) y ya sólo tendríamos $(n-1)!$ permutaciones posibles. Observemos que entre más grande sea $n$ menos posibilidades hay que un programa te devuelva la misma permutación dos o más veces. 

Se utilizó la función _permutation()_ de la librería `numpy` para obtener permutaciones entre los números del 2 a _n_.

### - Implementa un algoritmo para evaluar una solución (permutación).

Dada una solución al ejemplar, en el esquema de codificación anterior y empezando el recorrido desde la ciudad 1; Obtenemos la distancia del nodo 1 a la ciudad con el índice que corresponde al número que ocupa el segundo lugar en el arreglo. Después la distancia de la segunda en el arreglo con la tercera y así sucesivamente hasta encontrar la distancia de la ciudad con índice el último número del arreglo hacia la ciudad 1 (Para cerrar el ciclo). 

Recordemos que estos datos de distancias no los tenemos que calcular cada vez que se ejecute el programa, sino que los podemos consultar en la matriz de distancias.

Por ejemplo si el ejemplar contiene 3 ciudades: $c_1, c_2,c_3$ y la solución generada aleatoriamente es 1,3,2 entonces de la ciudad uno se visitará la ciudad tres, de la tres a la dos y de la ciudad dos volvemos a la ciudad 1. La distancia total de este recorrido será:

$$
d_{Total} = d(c_1, c_3) + d(c_3 , c_2) + d(c_2,c_1)
$$

con:

$$
d(c_i , c_j ) = \sqrt{(x_i - x_j )^2 + (y_i - y_j)^2}
$$

La implementación de este algoritmo se encuentra en la función `evaluar_sol()` que recibe de parámetros el archivo con el ejemplar y una solución para éste en forma de una lista (vector) de números naturales.

## Para probar las implementaciones, deberán generar dos programas (ejecutables desde consola)
#### Programa que reciba como parámetros (en la misma línea de ejecución):
- Nombre del archivo con los datos del 
- Semilla del generador de aleatorio
- Nombre del archivo con los datos de la solución generada 

#### Como salida, deberá imprimir algunos datos generales del ejemplar leído. Por ejemplo:
- Nombre del ejemplar (archivo)
- Tamaño del ejemplar (número de ciudades)
- Arista de mayor peso (o distancia más grande)
- Ejemplo de solución (solo los primeras y los últimas 3 elementos de la permutación)
- En caso de que se haya indicado, se deberá escribir en un archivo de texto la solución generada (completa)

Para esta función llamada `lectura_ejemplar()` necesitamos de los parámetros: el nombre del archivo con el ejemplar, una semilla para generar la solución aleatoria y un nombre para el archivo donde se guardará la solución generada. Los parámetros de semilla y nombre del archivo con la solución son opcionales, de no ser especificados los valores por default que tomarán será el número aleatorio basado en la fecha, generado por la función `time.time()` de la librería `time`. 

Luego, dentro de este mismo archivo se llamarán a las funciones `lectura_archivo()`, `matriz_distancias()`, `np.permutation()` y `evaluar_sol()`. 

* `lectura_archivo()`: Utilizamos esta función y con el diccionario creado se imprimen en pantalla los valores de las palabras clave _NAME_ y _DIMENSION_, especificando que corresponden al nombre del ejemplar y a su número de ciudades.
* `matriz_distancias()`: Esta la utilizaremos para encontrar la arista de mayor peso; buscamos $ max\{ d_{ij} : i,j=1, \ldots, n \}$ que es la entrada ij-ésima de la matriz, esto se obtuvo con `np.max()` Luego de identificar este valor encontramos de qué fila y columna se obtuvo
* `np.permutation()`
* `evaluar_sol()`

# Ejercicio 2:

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
