## Ejercicio 2:

Primero, implementamos un operador de intercambio de dos elementos consecutivos para permutaciones:
1. Definimos una función llamada `operadorCambioConsecutivo()` que recibe como parámetros una permutación (en formato de lista) y un índice.
2. Creamos una nueva copia de la lista `permutacion` para no modificar la original y la guardamos en `nuevaPermutación`.
3. Si el índice proporcionado no es válido, se retorna simplemente la copia de la lista original.
4. Si el índice proporcionado es válido, intercambiamos el elemento al que corresponde el índice con el siguiente en la lista y retornamos la lista modificada. 

