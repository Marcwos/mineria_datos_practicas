# 📊 Guía Completa de Pandas para Análisis de Datos

## 📚 Contenido de los Notebooks de Práctica

Esta guía resume todas las funciones y técnicas de pandas utilizadas en las prácticas de minería de datos:
- `practica1.ipynb`: Series y DataFrames básicos
- `practica2.ipynb`: Manipulación avanzada de datos
- `city.ipynb`: Ejercicios con datos de empleados
- `temperaturas.ipynb`: Series y operaciones básicas

---

## 🔰 PARTE 1: Series de Pandas (practica1.ipynb & temperaturas.ipynb)

### ¿Qué es una Serie?
Una Serie es una estructura de datos unidimensional (como una columna de Excel) con índices personalizados.

### Creación de Series
```python
# Serie básica
ventas = pd.Series([5, 10, 15, 30], 
                   name="Ventas", 
                   index=["Camisa", "Pantalon", "Zapatos", "Calcetas"])

temperaturas = pd.Series([28, 30, 27, 29, 31], 
                         name="Temperaturas", 
                         index=["Lunes", "Martes", "Miercoles", "Jueves", "Viernes"])
```

### Operaciones con Series
```python
# Operaciones matemáticas entre Series
total = ventas * cantidad  # Multiplica elemento por elemento
total.name = "Total"       # Asignar nombre a la Serie

# Verificar valores
9 in cantidad.values       # Verifica si 9 está en los valores
```

### Acceso a elementos de Series
```python
# Por índice personalizado
temperaturas["Miercoles"]                    # Un elemento
temperaturas["Lunes":"Miercoles"]            # Rango (inclusivo)
cantidad["Camisa":"Zapatos"]                 # Rango de productos

# Por posición numérica
cantidad[0:3]                                # Primeros 3 elementos (0, 1, 2)

# Por condición
temperaturas[temperaturas > 28]              # Temperaturas mayores a 28
cantidad[cantidad >= 5]                      # Cantidades >= 5
cantidad > 5                                 # Retorna booleanos
```

### Propiedades de Series
```python
cantidad.name          # Nombre de la Serie
cantidad.index         # Índices de la Serie
cantidad.values        # Valores de la Serie
```

### Modificación y eliminación de Series
```python
# Actualizar valores
temperaturas["Miercoles"] = 25

# Eliminar elementos
del temperaturas["Viernes"]
```

### Convertir Serie a DataFrame
```python
df = pd.DataFrame({"temperaturas": temperaturas})
```

---

## 📋 PARTE 2: DataFrames Básicos (practica1.ipynb)

### Creación de DataFrames

#### Método 1: Desde un diccionario de Series
```python
df = pd.DataFrame({
    "ventas": ventas, 
    "cantidad": cantidad, 
    "total": total
}, index=["Camisa", "Pantalon", "Zapatos", "Calcetas"])
```

#### Método 2: Desde una lista de Series
```python
data = [ventas, cantidad, total]
df = pd.DataFrame(data=data)
```

#### Método 3: Desde un diccionario de listas (city.ipynb)
```python
df = pd.DataFrame({
    "Nombres": ["Ana", "Luis", "Carlos", "Maria", "Pedro"],
    "Edad": [23, 25, 22, 24, 26],
    "Cuidad": ["Quito", "Guayaquil", "Cuenca", "Manta", "Quito"],
    "Salario": [1200, 1500, 1100, 1300, 1400]
})
```

### Selección en DataFrames

#### Con loc (por etiquetas)
```python
df.loc[:, ["cantidad", "total"]]              # Todas las filas, columnas específicas
df.loc[df["ventas"] > 20]                     # Filtro por condición
```

#### Con iloc (por posición)
```python
df.iloc[:5, [1, 2]]                           # Primeras 5 filas, columnas 1 y 2
```

### Filtrado avanzado (city.ipynb)
```python
# Filtro simple
empleados_mayores_23 = df.loc[df["Edad"] > 23]

# Filtro con múltiples condiciones (AND)
empleados_quito_mayor_1200 = df.loc[(df["Cuidad"] == "Quito") & (df["Salario"] > 1200)]
```

### Operaciones con columnas
```python
# Multiplicar columna por escalar
salario_anual = df.loc[:, "Salario"] * 12

# Contar elementos que cumplen condición
df.loc[df["ventas"] > 20]["ventas"].count()
```

### Encontrar máximos y mínimos
```python
# Obtener índice del valor máximo y mostrar datos
cuidad_salario_mejor_pagado = df.loc[df["Salario"].idxmax(), ["Cuidad", "Salario"]]
```

---

## 2️⃣ PARTE 3: Manipulación Avanzada (practica2.ipynb)

### Importación de Librerías

```python
import pandas as pd
import numpy as np
```

- **pandas**: Manipulación y análisis de datos tabulares
- **numpy**: Operaciones numéricas y generación de datos aleatorios

### Semilla aleatoria
```python
np.random.seed(42)
```
- Asegura reproducibilidad en números aleatorios

---

## 3️⃣ Creación de DataFrame con Datos Aleatorios

```python
df = pd.DataFrame({
    'producto': ['Laptop', 'Mouse', 'Teclado', 'Monitor'] * 6,
    'precio': np.random.uniform(10, 1000, 24).round(2),
    'cantidad': np.random.randint(1, 50, 24),
    'categoria': ['Tecnologia'] * 24,
    'mes': ['Enero', 'Febrero', ...] * 3,
    'vendedor': np.random.choice(['Juan', 'Maria', 'Pedro'], 24)
})
```

### Funciones para generar datos aleatorios:
- `np.random.uniform(min, max, n)`: Números decimales aleatorios
- `np.random.randint(min, max, n)`: Números enteros aleatorios
- `np.random.choice(lista, n)`: Selección aleatoria de elementos

---

## 4️⃣ Exploración Básica del DataFrame

### Visualización de datos
```python
df.head(10)          # Primeras 10 filas
df.tail(5)           # Últimas 5 filas
df                   # Todo el DataFrame
```

### Información general
```python
df.info()            # Información de datos y valores nulos
df.shape             # Dimensiones (filas, columnas)
df.columns           # Nombres de las columnas
df.dtypes            # Tipos de datos de cada columna
```

### Estadísticas descriptivas
```python
df.describe()                 # Estadísticas de columnas numéricas
df.describe(include='all')    # Estadísticas de todas las columnas
```

---

## 5️⃣ Selección y Filtrado Avanzado de Datos

### Selección de columnas
```python
df['producto']                        # Una columna (Serie)
df.loc[:, ['producto', 'precio']]     # Varias columnas (DataFrame)
```

### Selección de filas
```python
df.iloc[:5]                           # Primeras 5 filas por posición
df.loc[:5, ['producto', 'precio']]    # Primeras 6 filas y columnas específicas
```

### Filtrado por condición
```python
# Filtro simple
df[df['producto'] == 'Laptop']

# Filtros múltiples con AND
df[(df['producto'] == 'Laptop') & (df['cantidad'] > 10) & (df['precio'] > 100)]

# Filtros múltiples con OR
df[(df['mes'] == 'Enero') | (df['mes'] == 'Febrero')]

# Filtro con isin()
df[df['mes'].isin(['Enero', 'Febrero'])]
```

---

## 6️⃣ Valores Únicos y Conteos

```python
df['producto'].unique()      # Valores únicos
df['producto'].nunique()     # Cantidad de valores únicos
df['producto'].count()       # Conteo total de valores
```

---

## 7️⃣ Manejo de Valores Nulos

### Identificar valores nulos
```python
df.isnull()                           # Booleano de valores nulos
df.isnull().sum()                     # Conteo de nulos por columna
df.isnull().sum().sum()               # Total de nulos en el DataFrame
(df.isnull().sum() / len(df)) * 100   # Porcentaje de nulos
```

### Eliminar valores nulos
```python
df.dropna()                           # Elimina filas con valores nulos
df.dropna(subset=['precio'])          # Elimina filas con nulos en columna específica
```

### Rellenar valores nulos
```python
df.fillna('Desconocido')              # Rellena con un valor específico
df['precio'].fillna(df['precio'].mean())  # Rellena con la media
```

---

## 8️⃣ Creación de Nuevas Columnas

### Usando apply() y lambda
```python
df['Descuento'] = df['precio'].apply(lambda precio: precio * 0.10 if precio > 500 else precio * 0.05)
df['Tipo'] = df['precio'].apply(lambda precio: 'Caro' if precio > 500 else 'Barato')
```

### Usando where()
```python
# where() filtra datos basado en condiciones
# Valores que no cumplen la condición se convierten en NaN
# Puedes especificar un valor alternativo en lugar de NaN
```

---

## 9️⃣ Agrupación y Agregación (GroupBy)

### Agrupación simple
```python
df.groupby('producto')['precio'].mean()      # Precio promedio por producto
df.groupby('producto')['cantidad'].sum()     # Cantidad total por producto
```

### Agrupación múltiple
```python
df.groupby(['mes', 'producto'])['cantidad'].mean()  # Promedio por mes y producto
```

### Agregaciones múltiples
```python
df.groupby('producto').agg({
    'precio': ['mean', 'max', 'min'],
    'cantidad': 'sum'
})
```

---

## 🔟 Ordenamiento de Datos

```python
df.sort_values('precio')                                    # Ascendente
df.sort_values('precio', ascending=False)                   # Descendente
df.sort_values(['mes', 'precio'], ascending=[True, False])  # Ordenamiento múltiple
```

---

## 1️⃣1️⃣ Manejo de Duplicados

```python
df.duplicated()                                    # Identifica filas duplicadas
df.duplicated().sum()                              # Cuenta duplicados
df.drop_duplicates()                               # Elimina duplicados
df.drop_duplicates(subset=['producto', 'mes'])     # Elimina basado en columnas
```

---

## 1️⃣2️⃣ Conversión de Tipos de Datos

### Ver tipo de dato
```python
df['mes'].dtype
df.dtypes  # Todos los tipos
```

### Convertir tipos
```python
df['precio'] = df['precio'].astype('float32')     # A float32
df['mes'] = df['mes'].astype('category')          # A categoría
df['fecha'] = pd.to_datetime('2024-01-01')        # A datetime
```

---

## 📝 Conceptos Clave y Diferencias Importantes

### 🔍 Serie vs DataFrame
| Serie | DataFrame |
|-------|-----------|
| Unidimensional (1 columna) | Bidimensional (varias columnas) |
| Tiene índice y valores | Tiene índice, columnas y valores |
| Similar a una lista con índices | Similar a una tabla de Excel |

### 🎯 loc vs iloc
| **loc** | **iloc** |
|---------|----------|
| Selección por **etiquetas** | Selección por **posición numérica** |
| `df.loc["Camisa"]` | `df.iloc[0]` |
| `df.loc[:, "precio"]` | `df.iloc[:, 1]` |
| Inclusivo en rangos: `[0:3]` incluye 0,1,2,3 | Exclusivo en rangos: `[0:3]` incluye 0,1,2 |

### 🔢 Métodos importantes para encontrar valores

```python
# Encontrar índice del máximo/mínimo
df["Salario"].idxmax()        # Índice del salario máximo
df["Salario"].idxmin()        # Índice del salario mínimo

# Obtener el valor máximo/mínimo
df["Salario"].max()           # Valor máximo
df["Salario"].min()           # Valor mínimo

# Obtener toda la fila del máximo
df.loc[df["Salario"].idxmax()]
```

### ⚙️ Operadores para filtros
- **`&`**: AND (Y) - Ambas condiciones deben cumplirse
- **`|`**: OR (O) - Al menos una condición debe cumplirse
- **`~`**: NOT (Negación) - Invierte la condición

**⚠️ IMPORTANTE**: Usa `&` y `|`, NO `and` y `or` en pandas. Siempre usa paréntesis en cada condición.

```python
# ✅ CORRECTO
df[(df["Edad"] > 23) & (df["Salario"] > 1200)]

# ❌ INCORRECTO
df[df["Edad"] > 23 and df["Salario"] > 1200]
```

### 📊 Funciones de agregación comunes
- `mean()`: Media/promedio
- `sum()`: Suma total
- `count()`: Conteo de valores
- `max()`: Valor máximo
- `min()`: Valor mínimo
- `std()`: Desviación estándar
- `var()`: Varianza
- `median()`: Mediana
- `nunique()`: Número de valores únicos
- `unique()`: Lista de valores únicos

### 🎓 Métodos de acceso y modificación en Series

```python
# Acceso por índice personalizado
serie["nombre_indice"]
serie["inicio":"fin"]              # Rango inclusivo

# Acceso por posición
serie[0]                           # Primer elemento
serie[0:3]                         # Primeros 3 elementos (0,1,2)

# Modificación
serie["indice"] = nuevo_valor      # Actualizar valor

# Eliminación
del serie["indice"]                # Eliminar elemento
```

---

## 🎯 Tips y Trucos para el Examen

### ✅ Checklist antes de trabajar con datos
1. **Importar librerías**: `import pandas as pd` y `import numpy as np`
2. **Ver estructura**: `df.head()`, `df.info()`, `df.shape`
3. **Verificar tipos**: `df.dtypes`
4. **Revisar nulos**: `df.isnull().sum()`
5. **Estadísticas**: `df.describe()`

### 🔑 Comandos más usados

```python
# Exploración rápida
df.head()                    # Primeras 5 filas
df.tail()                    # Últimas 5 filas
df.shape                     # (filas, columnas)
df.columns                   # Nombres de columnas
df.info()                    # Resumen completo

# Selección
df['columna']                # Una columna
df[['col1', 'col2']]         # Varias columnas
df.loc[condicion]            # Filtro
df.iloc[0:5]                 # Por posición

# Estadísticas
df['columna'].mean()         # Promedio
df['columna'].sum()          # Suma
df['columna'].max()          # Máximo
df['columna'].idxmax()       # Índice del máximo

# Agrupación
df.groupby('columna').mean()
df.groupby(['col1', 'col2']).sum()
```

### 💡 Errores comunes a evitar

1. **Usar `and`/`or` en lugar de `&`/`|`** en filtros
   ```python
   # ❌ MAL
   df[df['edad'] > 20 and df['edad'] < 30]
   
   # ✅ BIEN
   df[(df['edad'] > 20) & (df['edad'] < 30)]
   ```

2. **Olvidar paréntesis en condiciones múltiples**
   ```python
   # ❌ MAL
   df[df['a'] > 5 & df['b'] < 10]
   
   # ✅ BIEN
   df[(df['a'] > 5) & (df['b'] < 10)]
   ```

3. **Confundir loc e iloc**
   ```python
   df.loc[0]        # Busca índice etiquetado como 0
   df.iloc[0]       # Busca primera fila por posición
   ```

4. **No asignar el resultado de modificaciones**
   ```python
   # ❌ MAL (no guarda cambios)
   df.dropna()
   
   # ✅ BIEN
   df = df.dropna()
   # o usar inplace=True
   df.dropna(inplace=True)
   ```

### 📌 Patrones comunes de ejercicios

#### Patrón 1: Filtrar y contar
```python
# ¿Cuántos productos tienen precio > 500?
df[df['precio'] > 500].shape[0]
# o
df[df['precio'] > 500]['precio'].count()
```

#### Patrón 2: Filtro múltiple y selección
```python
# Empleados de Quito con salario > 1200
resultado = df.loc[(df['Cuidad'] == 'Quito') & (df['Salario'] > 1200)]
```

#### Patrón 3: Operaciones con columnas
```python
# Crear nueva columna calculada
df['salario_anual'] = df['Salario'] * 12
```

#### Patrón 4: Encontrar extremos
```python
# Ciudad del empleado mejor pagado
ciudad = df.loc[df['Salario'].idxmax(), 'Cuidad']
```

#### Patrón 5: Agrupación y estadísticas
```python
# Promedio de ventas por producto
df.groupby('producto')['ventas'].mean()
```

### 🚀 Atajos útiles

```python
# Ver tipos de datos rápidamente
df.dtypes

# Verificar valores únicos
df['columna'].unique()
df['columna'].nunique()

# Verificar si hay nulos
df.isnull().any()           # Por columna
df.isnull().sum()           # Cantidad por columna

# Renombrar columnas rápido
df.columns = ['nuevo1', 'nuevo2', 'nuevo3']

# Reset de índice
df.reset_index(drop=True)
```

---

## 📚 Resumen de Notebooks

### 📓 practica1.ipynb
- ✅ Creación de Series
- ✅ Operaciones entre Series
- ✅ Acceso a elementos por índice y posición
- ✅ Propiedades: name, index, values
- ✅ Creación de DataFrames desde Series
- ✅ Selección con loc e iloc
- ✅ Filtrado básico

### 📓 temperaturas.ipynb
- ✅ Series con índices personalizados
- ✅ Acceso por rango
- ✅ Filtrado por condición
- ✅ Actualización de valores
- ✅ Eliminación de elementos
- ✅ Conversión de Serie a DataFrame

### 📓 city.ipynb
- ✅ DataFrame desde diccionario
- ✅ Filtros con condiciones múltiples
- ✅ Operaciones matemáticas con columnas
- ✅ Uso de idxmax() para encontrar valores máximos
- ✅ Selección de columnas específicas

### 📓 practica2.ipynb
- ✅ Generación de datos aleatorios con numpy
- ✅ Exploración completa de DataFrames
- ✅ Filtrado avanzado con isin()
- ✅ Manejo de valores nulos
- ✅ Creación de columnas con apply() y lambda
- ✅ Agrupación con groupby()
- ✅ Agregaciones múltiples con agg()
- ✅ Ordenamiento
- ✅ Manejo de duplicados
- ✅ Conversión de tipos de datos

---

## 🎯 Tips y Trucos para el Examen

### 🎓 Puntos clave para recordar

1. **Series son unidimensionales**, DataFrames son bidimensionales
2. **loc usa etiquetas**, iloc usa posiciones numéricas
3. **Usar `&` y `|`** para condiciones, NO `and` y `or`
4. **Siempre usar paréntesis** en cada condición de filtros múltiples
5. **`apply()` con lambda`** es muy útil para transformaciones complejas
6. **`groupby()` + `agg()`** para análisis agrupados con múltiples estadísticas
7. **Siempre verificar valores nulos** antes de hacer análisis: `df.isnull().sum()`
8. **`idxmax()` y `idxmin()`** devuelven el índice, no el valor
9. **Los rangos con loc son inclusivos**, con iloc son exclusivos
10. **`inplace=True`** modifica el DataFrame original, sin asignar

---

## 📖 Recursos Adicionales

- [Documentación oficial de Pandas](https://pandas.pydata.org/docs/)
- [Cheat Sheet de Pandas](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- [10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html)

---

## 🧪 Ejercicios de Práctica Rápida

### Ejercicio 1: Series
```python
# Crea una serie de temperaturas y filtra las mayores a 28°C
temps = pd.Series([25, 30, 28, 32, 27], index=['L', 'M', 'X', 'J', 'V'])
resultado = temps[temps > 28]
```

### Ejercicio 2: Filtrado múltiple
```python
# Filtra empleados de Quito con edad > 23
df[(df['Ciudad'] == 'Quito') & (df['Edad'] > 23)]
```

### Ejercicio 3: Agrupación
```python
# Promedio de ventas por producto y mes
df.groupby(['producto', 'mes'])['ventas'].mean()
```

### Ejercicio 4: Nuevas columnas
```python
# Crea columna de bonificación: 10% si salario > 1300, sino 5%
df['bono'] = df['Salario'].apply(lambda x: x * 0.10 if x > 1300 else x * 0.05)
```

---

**¡Buena suerte en tu lección! 🍀📊💪**

_Última actualización: Octubre 2025_
