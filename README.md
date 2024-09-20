# Tarea 3: Metaheurísta de Trayectoria

## Requerimientos
Alguna versión de python superior a la 3.1, la paquetería ´pandas´, ´numpy´, ´time´, ´request´

## Funciones
### Para descargar los archivos de los ejemplares en Google colab se tiene que ejecutar la celda:

!wget https://raw.githubusercontent.com/FridaVargas/tsp/main/pr152.tsp

!wget https://raw.githubusercontent.com/FridaVargas/tsp/main/eil51.tsp

!wget https://raw.githubusercontent.com/FridaVargas/tsp/main/ch130.tsp

!wget https://raw.githubusercontent.com/FridaVargas/tsp/main/berlin52.tsp

!wget https://raw.githubusercontent.com/mastqe/tsplib/refs/heads/master/pr76.tsp

### para descargarlo en VSC o algún otro IDE:

´import requests

urls = [
    "https://raw.githubusercontent.com/FridaVargas/tsp/main/pr152.tsp",
    
    "https://raw.githubusercontent.com/FridaVargas/tsp/main/eil51.tsp",
    
    "https://raw.githubusercontent.com/FridaVargas/tsp/main/ch130.tsp",
    
    "https://raw.githubusercontent.com/FridaVargas/tsp/main/berlin52.tsp",
    
    "https://raw.githubusercontent.com/mastqe/tsplib/refs/heads/master/pr76.tsp]
    
for url in urls:

    filename = url.split("/")[-1]
    
    response = requests.get(url)
    
    with open(filename, 'wb') as f:
    
        f.write(response.content)
        
    print(f"Archivo {filename} descargado.")´
    
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

### 7. `busqueda_por_vecindades(solucionInicial, tipoVecindad)`

- **Descripción**: Busca la mejor solución explorando vecindades de una solución inicial.
- **Parámetros**:
  - `solucionInicial`: Lista que representa la solución inicial.
  - `tipoVecindad`: Tipo de vecindad a utilizar (ej. "CambioConsecutivo").
- **Retorno**: Mejor solución y su evaluación.

### 8. `perturbacion_estocastica(s)`

- **Descripción**: Aplica una perturbación estocástica a una solución dada.
- **Parámetros**:
  - `s`: Lista que representa la solución a perturbar.
- **Retorno**: Solución modificada.

## Ejemplo de Uso

python
# Cargar un ejemplar y generar una solución aleatoria
ejemplar = 'ch130.tsp'
solucion = generar_sol_aleatoria(ejemplar)

# Evaluar la solución
costo = evaluar_sol(ejemplar, solucion)
print(f"Costo de la solución: {costo}")

# Buscar mejor solución
mejor_solucion, mejor_valor = busqueda_por_vecindades(solucion, "CambioConsecutivo")
print("Mejor solución:", mejor_solucion)
print("Mejor valor:", mejor_valor)

## Esquemas disponibles: 
'ch130.tsp', 'pr152', 'berlin52', 'eil51.tsp', 'pr71.tsp'. Aunque cualquier archivo de un ejemplar con el formato de [TSPLIB] (http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/tsp95.pdf) puede ser cargado y leído.

