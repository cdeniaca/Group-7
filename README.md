# 📊 Análisis de la Población Activa, Teletrabajo, Salarios y Gastos en España 🏠💼💶


_______________________________________________________________________________________________________

# Introducción 🚀

Este proyecto analiza la situación laboral y económica de la población activa en España, con un enfoque en la distribución y crecimiento del teletrabajo, los salarios y los gastos en las distintas comunidades autónomas. Usamos Python y bibliotecas de análisis de datos para descubrir tendencias y patrones relevantes en el mercado laboral español.

_______________________________________________________________________________________________________

# Datos Utilizados 📑

Para el análisis, empleamos los siguientes conjuntos de datos:

- Población Activa: Datos sobre ocupación, desempleo, inactividad y la tasa de actividad por comunidad autónoma y año.
- Teletrabajo: Información sobre teletrabajo distribuida en categorías de personas que teletrabajan, las que podrían teletrabajar pero no lo hacen, y quienes no pueden teletrabajar.
- Salarios y Gastos: Información sobre salarios promedio y gastos de los hogares en cada comunidad.

_______________________________________________________________________________________________________

# Comentarios sobre los Datos 📋

- Fortalezas: Datos completos y recientes por región, ideales para observar el impacto del teletrabajo, aunque también al analizar dentro de INE.es mismas muestras nos encontramos con errores de muestreo, por lo que los totales no coincidian en un 100%.
- Desafíos: Las diferencias de tamaño de población entre comunidades pueden sesgar los resultados si no se normalizan.
- Debilidades: Al analizar promedios, perdemos la variabilidad dentro de cada comunidad, lo que limita el análisis a generalizaciones.

_______________________________________________________________________________________________________

# Preguntas de Investigación y Conclusiones 🧐

1. ¿Cuál es la proporción de teletrabajo en cada comunidad autónoma? 🖥️
Conclusión: Las comunidades con mayores tasas de teletrabajo (Madrid y Cataluña) suelen tener economías orientadas a servicios y mayor digitalización. En cambio, las comunidades con economías más tradicionales muestran tasas menores.
2. ¿Cómo ha evolucionado la población activa en los últimos años? 📈
Conclusión: La mayoría de las comunidades autónomas han visto un crecimiento sostenido en su población activa, especialmente en regiones con un crecimiento económico más dinámico como Madrid y Cataluña.
3. ¿Cuál es la relación entre los salarios promedio y los gastos en cada comunidad? 💸
Conclusión: En áreas urbanas, el aumento de los salarios no ha seguido el mismo ritmo que los gastos, lo que indica una mayor presión económica. Madrid, Cataluña y el País Vasco muestran las mayores brechas entre salarios y gastos promedio.

_______________________________________________________________________________________________________

# Metodología ⚙️

Para desarrollar este análisis, seguimos los pasos siguientes:

- Paso 1: Carga de Datos 🔄

Cargamos los datos desde archivos CSV en Python utilizando pandas. A continuación, un ejemplo de la carga de datos:


```python
import pandas as pd

Cargar el dataset de Población Activa
url_poblacion = 'https://raw.githubusercontent.com/cdeniaca/Group-7/refs/heads/main/Poblacion_Agrupado_Limpia.csv'

poblacion_agrupada_df = pd.read_csv(url_poblacion)

Cargar el dataset de Teletrabajo
url_teletrabajo = 'https://raw.githubusercontent.com/cdeniaca/Group-7/refs/heads/main/Poblacion_Teletrabajo_Limpia.csv'

poblacion_teletrabajo_df = pd.read_csv(url_teletrabajo)

Cargar el dataset de Salarios y Gastos
url_salarios_gastos = 'https://example.com/Salarios_Gastos.csv' 

salarios_gastos_df = pd.read_csv(url_salarios_gastos)
```


- Paso 2: Limpieza de Datos 🧹

Convertimos columnas de años a tipo numérico y aseguramos coherencia en los nombres de columnas para facilitar el análisis y la combinación de datos:


```python
Convertir columna de año a tipo entero
for df in [poblacion_agrupada_df, poblacion_teletrabajo_df, salarios_gastos_df]:
    df['AÑO'] = df['AÑO'].astype(int)

Tratamiento de valores nulos
poblacion_agrupada_df.fillna(0, inplace=True)
poblacion_teletrabajo_df.fillna(0, inplace=True)
salarios_gastos_df.fillna(0, inplace=True)
```



- Paso 3: Integración de Datos 📊

Usamos las columnas Comunidad autónoma y AÑO para fusionar los tres DataFrames en un solo conjunto de datos consolidado:


```python
Fusión de los datos de población activa y teletrabajo
df_merged = pd.merge(poblacion_agrupada_df, poblacion_teletrabajo_df, on=['Comunidad autónoma', 'AÑO'])

Incorporación de datos de salarios y gastos
df_final = pd.merge(df_merged, salarios_gastos_df, on=['Comunidad autónoma', 'AÑO'], how='inner')
```

- Paso 4: Análisis y Visualización 📉

Para identificar tendencias, utilizamos Seaborn y Matplotlib para visualizaciones, con especial enfoque en las diferencias regionales en teletrabajo, salario y gasto.

Ejemplo de visualización de la evolución del teletrabajo en diferentes comunidades:


```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(12, 6))
sns.lineplot(data=df_final, x='AÑO', y='Han teletrabajado', hue='Comunidad autónoma')
plt.title("Evolución del Teletrabajo en España por Comunidad Autónoma")
plt.xlabel("Año")
plt.ylabel("Personas que teletrabajaron (en miles)")
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
plt.show()
```


_______________________________________________________________________________________________________

# Conclusiones Principales 📌

1. Teletrabajo: El teletrabajo ha crecido en comunidades con economías digitalizadas, destacándose Madrid y Cataluña en adopción de esta modalidad.

2. Desempleo: Aunque el desempleo ha disminuido en varias regiones, persisten diferencias significativas entre comunidades.

3. Salarios y Gastos: En algunas regiones, el gasto supera el crecimiento de los salarios, destacando una presión económica mayor en áreas urbanas como Madrid y el País Vasco.

_______________________________________________________________________________________________________

# Preguntas Futuras 🔍

A partir de este análisis, surgen preguntas adicionales como:

- ¿Qué impacto ha tenido la expansión del teletrabajo en la productividad y satisfacción laboral en cada región?
- ¿Cómo influye el tipo de industria y el costo de vida en la viabilidad del teletrabajo en diferentes comunidades?
- ¿Existe alguna relación entre el crecimiento de los salarios, el teletrabajo y la migración hacia áreas urbanas?

_______________________________________________________________________________________________________

# Fuentes de Datos 🔗
- Población de 16 o más años de edad por comunidad autónoma -> [
](https://www.ine.es/jaxiT3/Tabla.htm?t=66266)
- Uso de productos TIC por las personas de 16 a 74 años -> [
](https://www.ine.es/jaxi/Tabla.htm?tpx=60861&L=0 )
- Coste laboral por trabajador, comunidad autónoma, sectores de actividad -> [
](https://www.ine.es/jaxiT3/Tabla.htm?t=6061)
- [
](


_______________________________________________________________________________________________________
