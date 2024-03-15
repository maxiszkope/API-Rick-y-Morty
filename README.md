# API-Rick-y-Morty
![] (rick.png)

### Resumen:
Este framework proporciona un conjunto de herramientas para interactuar con la API de Rick and Morty, obtener datos de personajes y realizar análisis exploratorios sobre estos datos de manera eficiente y efectiva.

### Requisitos:
- Python 3.x
- Bibliotecas Python: `requests`, `pandas`, `numpy`, `plotly`

### Uso del Framework:

1. **Obtención de Datos de Personajes:**
   - Utiliza la función `obtener_datos_personajes()` para obtener datos de personajes de la API de Rick and Morty.
   - **Detalles de la Función:**
     - La función emplea la biblioteca `requests` para realizar solicitudes GET a la API de Rick and Morty.
     - Inicia un bucle while que solicita datos de personajes en páginas sucesivas hasta que no haya más datos disponibles.
     - Devuelve una lista de personajes en formato JSON que incluye información como nombre, estado, especie, género, origen, ubicación, episodios en los que aparece, etc.
   - **Ejemplo de Uso:**
     ```python
     data_personajes = obtener_datos_personajes()
     ```

2. **Procesamiento de Datos:**
   - Los datos obtenidos se cargan en un DataFrame de Pandas para facilitar el análisis.
   - Se eliminan las columnas innecesarias (`image`, `url`, `created`, `id`, `type`) para mejorar la legibilidad y el rendimiento.
   - Se realiza limpieza en las columnas `origin` y `location` para extraer solo el nombre del lugar.
   - **Ejemplo de Uso:**
     ```python
     import pandas as pd
     df = pd.DataFrame(data_personajes)
     ```

3. **Análisis Exploratorio de Datos:**
   - Se realizan varios análisis visuales utilizando la biblioteca Plotly.

   - **Gráfico de Barras para las Especies Más Comunes:**
     - **Función:**
       - Utiliza `plotly.express.bar()` para crear un gráfico de barras.
       - Muestra las especies más comunes entre los personajes.
     - **Ejemplo de Uso:**
       ```python
       import plotly.express as px

       fig_bar = px.bar(x=df['species'].value_counts().head(15).index, 
                        y=df['species'].value_counts().head(15).values)
       fig_bar.show()
       ```

   - **Gráfico de Pastel para la Proporción de Géneros:**
     - **Función:**
       - Utiliza `plotly.graph_objects.Pie()` para crear un gráfico de pastel.
       - Muestra la proporción de géneros entre los personajes.
     - **Ejemplo de Uso:**
       ```python
       import plotly.graph_objects as go

       proporcion = df["gender"].value_counts()

       fig_pie = go.Figure(data=[go.Pie(labels=(proporcion/len(df * 100)).index, 
                                        values=(proporcion/len(df * 100)).values, 
                                        text=proporcion.index)])
       fig_pie.show()
       ```

   - **Gráficos 3D, Polares y de Barras Polares para Visualización Detallada:**
     - **Funciones:**
       - Utiliza `plotly.express.scatter_3d()`, `plotly.express.scatter_polar()` y `plotly.express.bar_polar()` respectivamente.
       - Visualiza la distribución de especies de manera más detallada.
     - **Ejemplo de Uso:**
       ```python
       especies = df['species'].value_counts()

       # Gráfico 3D
       px.scatter_3d(x=especies, y=especies, z=especies, color=especies.index)

       # Gráfico Polar
       px.scatter_polar(r=especies, theta=especies.index, size=especies, color=especies.index)

       # Gráfico de Barras Polares
       px.bar_polar(r=especies, theta=especies.index, color=especies.index)
       ```

   - **TreeMap para Visualizar el Tamaño de las Especies:**
     - **Función:**
       - Utiliza `plotly.express.treemap()` para crear un TreeMap.
       - Visualiza el tamaño de las especies en relación con el número de personajes de cada especie.
     - **Ejemplo de Uso:**
       ```python
       px.treemap(especies, path=[especies.index], values=especies, height=700, 
                  title='Tamaño de las especies', color_discrete_sequence=px.colors.qualitative.Dark2)
       ```

   - **Gráfico de Dispersión para Mostrar la Relación entre Especies y Nombres de Personajes:**
     - **Función:**
       - Utiliza `plotly.express.scatter()` para crear un gráfico de dispersión.
       - Muestra la relación entre las especies y los nombres de los personajes.
     - **Ejemplo de Uso:**
       ```python
       fig_scatter = px.scatter(df.head(30), x="species", y="name", color="species")
       fig_scatter.show()
       ```

### Instalación:
1. Asegúrate de tener Python 3.x instalado en tu sistema.
2. Instala las bibliotecas requeridas ejecutando `pip install requests pandas numpy plotly`.

### Ejecución:
1. Ejecuta el script en un entorno de Python.
2. Los gráficos generados se mostrarán en la interfaz de usuario.

### Contribuciones:
- Siéntete libre de contribuir agregando más análisis o características al framework.
- Puedes sugerir mejoras en el código o informar sobre problemas encontrados.

### Notas:
- Asegúrate de no hacer solicitudes excesivas a la API para evitar sobrecargar el servidor.
- Ten en cuenta que este framework asume la disponibilidad y estructura actual de la API de Rick and Morty. Los cambios futuros en la API pueden afectar su funcionamiento.

¡Disfruta explorando los datos de Rick and Morty con este framework!
