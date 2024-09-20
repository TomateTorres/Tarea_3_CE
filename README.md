# Tarea 3: Metaheurísta de Trayectoria

**Para cargar los archivos en google colab ejecutar la siguiente línea**:
      !wget https://raw.githubusercontent.com/FridaVargas/tsp/main/pr152.tsp
      !wget https://raw.githubusercontent.com/FridaVargas/tsp/main/eil51.tsp
      !wget https://raw.githubusercontent.com/FridaVargas/tsp/main/ch130.tsp
      !wget https://raw.githubusercontent.com/FridaVargas/tsp/main/berlin52.tsp
      !wget https://raw.githubusercontent.com/mastqe/tsplib/refs/heads/master/pr76.tsp
**Para cargarlos en VSC:**
      import requests

        urls = [
            "https://raw.githubusercontent.com/FridaVargas/tsp/main/pr152.tsp",
            "https://raw.githubusercontent.com/FridaVargas/tsp/main/eil51.tsp",
            "https://raw.githubusercontent.com/FridaVargas/tsp/main/ch130.tsp",
            "https://raw.githubusercontent.com/FridaVargas/tsp/main/berlin52.tsp",
            "https://raw.githubusercontent.com/mastqe/tsplib/refs/heads/master/pr76.tsp"
        ]
        
        for url in urls:
            filename = url.split("/")[-1]
            response = requests.get(url)
            with open(filename, 'wb') as f:
                f.write(response.content)
            print(f"Archivo {filename} descargado.")

## Ejemplares que se van a descargar:
'ch130.tsp', 'pr152.tsp', 'pr71.tsp', 'eil51.tsp', 'berlin52.tsp'

## Requisitos: 
Se necesita una versión de python posterior a la 3.5, y tener las librerías ´pandas´, ´numpy´, ´time´ e ´import´

## Funciones

### 1. `lectura_TSP(ejemplar, imprimir=False)`

- **Descripción**: Lee un archivo TSP y devuelve un diccionario con sus atributos y un DataFrame con las coordenadas de las ciudades.
- **Parámetros**:
  - `ejemplar`: Ruta del archivo TSP.
  - `imprimir`: Booleano para decidir si imprimir el nombre y la dimensión del ejemplar.
- **Retorno**: Diccionario de datos y DataFrame de coordenadas.

### 2. `matriz_distancias(ejemplar)`

- **Descripción**: Calcula la matriz de distancias entre las ciudades de un ejemplar TSP.
- **Parámetros**:
  - `ejemplar`: Ruta del archivo TSP.
- **Retorno**: Matriz de distancias.

### 3. `generar_sol_aleatoria(ejemplar)`

- **Descripción**: Genera una solución aleatoria para el problema TSP.
- **Parámetros**:
  - `ejemplar`: Ruta del archivo TSP.
- **Retorno**: Lista que representa la solución.

### 4. `evaluar_sol(ejemplar, solucion)`

- **Descripción**: Evalúa el costo de una solución dada.
- **Parámetros**:
  - `ejemplar`: Ruta del archivo TSP.
  - `solucion`: Lista que representa la solución a evaluar.
- **Retorno**: Costo total de la solución.

### 5. `arista_mayor(ejemplar)`

- **Descripción**: Encuentra la arista de mayor peso en el TSP.
- **Parámetros**:
  - `ejemplar`: Ruta del archivo TSP.
- **Retorno**: Tupla con los índices de las ciudades y el valor de la arista.

### 6. `leer_sol(archivo_sol, imprimir=False)`

- **Descripción**: Lee una solución desde un archivo.
- **Parámetros**:
  - `archivo_sol`: Ruta del archivo con la solución.
  - `imprimir`: Booleano para decidir si imprimir la solución.
- **Retorno**: Lista de la solución leída.

### 7. `evaluar(ejemplar, solucion)`

- **Descripción**: Evalúa una solución.
- **Parámetros**:
  - `ejemplar`: Ruta del archivo TSP.
  - `solucion`: Lista que representa la solución a evaluar.
- **Retorno**: Costo total de la solución.

### 8. `perturbacion_estocastica(s)`

- **Descripción**: Aplica una perturbación estocástica a una solución dada.
- **Parámetros**:
  - `s`: Lista que representa la solución a perturbar.
- **Retorno**: Solución modificada.

### 9. `primVecinoMejorar(solucionInicial, vecinos)`

- **Descripción**: Busca el mejor vecino que mejore la solución inicial.
- **Parámetros**:
  - `solucionInicial`: Lista que representa la solución inicial.
  - `vecinos`: Lista de vecinos a evaluar.
- **Retorno**: Mejor vecino encontrado.

### 10. `busqueda_por_vecindades(solucionInicial, tipoVecindad)`

- **Descripción**: Busca la mejor solución explorando vecindades de una solución inicial.
- **Parámetros**:
  - `solucionInicial`: Lista que representa la solución inicial.
  - `tipoVecindad`: Tipo de vecindad a utilizar (ej. "CambioConsecutivo").
- **Retorno**: Mejor solución y su evaluación.

### 11. `generar_vecindades_CambioConsecutivo(solucion_inicial, operadorCambioConsecutivo)`

- **Descripción**: Genera diferentes tamaños de vecindades utilizando el operador de cambio consecutivo.
- **Parámetros**:
  - `solucion_inicial`: Lista que representa la solución inicial.
  - `operadorCambioConsecutivo`: Función para generar cambios consecutivos.
- **Retorno**: Lista de vecindades.

### 12. `generar_vecindades_NoConsecutivo(solucion_inicial, OperadorNoConsecutivo)`

- **Descripción**: Genera diferentes tamaños de vecindades utilizando el operador de cambio no consecutivo.
- **Parámetros**:
  - `solucion_inicial`: Lista que representa la solución inicial.
  - `OperadorNoConsecutivo`: Función para generar cambios no consecutivos.
- **Retorno**: Lista de vecindades.

### 13. `generar_vecindades_InvParticion(solucion_inicial, OperadorInvParticion)`

- **Descripción**: Genera diferentes tamaños de vecindades utilizando el operador de inversión por partición.
- **Parámetros**:
  - `solucion_inicial`: Lista que representa la solución inicial.
  - `OperadorInvParticion`: Función para realizar inversiones por partición.
- **Retorno**: Lista de vecindades.

### 14. `generarVecindadGeneral(solucionInicial, tipoVecindad)`

- **Descripción**: Genera vecindades según el tipo de vecindad solicitado.
- **Parámetros**:
  - `solucionInicial`: Lista que representa la solución inicial.
  - `tipoVecindad`: Tipo de vecindad a utilizar.
- **Retorno**: Lista de vecindades generadas.

## Ejemplo de Uso

python
#### Cargar un ejemplar y generar una solución aleatoria
ejemplar = 'ch130.tsp'
solucion = generar_sol_aleatoria(ejemplar)

#### Evaluar la solución
costo = evaluar_sol(ejemplar, solucion)
print(f"Costo de la solución: {costo}")

#### Buscar mejor solución
mejor_solucion, mejor_valor = busqueda_por_vecindades(solucion, "CambioConsecutivo")
print("Mejor solución:", mejor_solucion)
print("Mejor valor:", mejor_valor)


