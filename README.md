# Análisis del Conjunto de Datos de Precios de Aguacate
Este es nuestro proyecto consistente en el análisis del set de datos *Avocado*

## Integrantes del grupo:
- Nelson Morales
- Ivan López

## Planificación

![image](https://github.com/user-attachments/assets/f743eb47-4850-4793-844e-66a9ef4acc4a)


## EDA (Análisis exploratorio de datos)
Comenzamos el análisis realizando un EDA (Exploratory Data Analysis), durante el cual identificamos los siguientes hallazgos:
- El dataset está compuesto por 18,249 filas y 11 columnas.
- Los datos se recopilan semanalmente, lo que equivale a 4 o 5 mediciones por mes.
- La columna 'Date' abarca un rango de fechas desde 2015 hasta 2018, aunque el año 2018 está incompleto, ya que solo incluye datos de enero a marzo.
- Las columnas 'Small Bags', 'Large Bags' y 'XLarge Bags' contienen 159, 2,370 y 12,048 filas con valores de cero (0.0), respectivamente.
- La columna 'Total Bags' presenta 15 filas con valores de cero (0.0), todas correspondientes a aguacates orgánicos.
- La columna 'region' incluye información heterogénea, combinando ciudades, regiones, regiones ampliadas ("greater regions") y datos del total de Estados Unidos (TotalUS).
- La región 'WestNewMexico' tiene 3 filas menos en comparación con el resto de las regiones.
- En las columnas de calibres ('4046', '4225', '4770') encontramos valores igual a cero (0.0): 242 en '4046', 61 en '4225' y 5,497 en '4770'. Todos estos registros corresponden a aguacates orgánicos, excepto uno (df.iloc[2998]), que es de tipo convencional.

Nuestra clasificacion de clases de regiones: ['City' 'Region' 'GreaterRegion' 'TotalUS']
region_classification = {
    'Albany': 'City',
    'Atlanta': 'City',
    'BaltimoreWashington': 'Region',
    'Boise': 'City',
    'Boston': 'City',
    'BuffaloRochester': 'Region',
    'California': 'GreaterRegion',
    'Charlotte': 'City',
    'Chicago': 'City',
    'CincinnatiDayton': 'Region',
    'Columbus': 'City',
    'DallasFtWorth': 'Region',
    'Denver': 'City',
    'Detroit': 'City',
    'GrandRapids': 'City',
    'GreatLakes': 'GreaterRegion',
    'HarrisburgScranton': 'Region',
    'HartfordSpringfield': 'Region',
    'Houston': 'City',
    'Indianapolis': 'City',
    'Jacksonville': 'City',
    'LasVegas': 'City',
    'LosAngeles': 'City',
    'Louisville': 'City',
    'MiamiFtLauderdale': 'Region',
    'Midsouth': 'GreaterRegion',
    'Nashville': 'City',
    'NewOrleansMobile': 'Region',
    'NewYork': 'City',
    'Northeast': 'GreaterRegion',
    'NorthernNewEngland': 'Region',
    'Orlando': 'City',
    'Philadelphia': 'City',
    'PhoenixTucson': 'Region',
    'Pittsburgh': 'City',
    'Plains': 'GreaterRegion',
    'Portland': 'City',
    'RaleighGreensboro': 'Region',
    'RichmondNorfolk': 'Region',
    'Roanoke': 'City',
    'Sacramento': 'City',
    'SanDiego': 'City',
    'SanFrancisco': 'City',
    'Seattle': 'City',
    'SouthCarolina': 'State',
    'SouthCentral': 'GreaterRegion',
    'Southeast': 'GreaterRegion',
    'Spokane': 'City',
    'StLouis': 'City',
    'Syracuse': 'City',
    'Tampa': 'City',
    'TotalUS': 'TotalUS',
    'West': 'GreaterRegion',
    'WestTexNewMexico': 'Region'
}
def get_regions(name):
  cat_region = region_classification.get(name)
  return cat_region

Es por eso que teniendo en cuenta esta classificación, hemos incluido también la siguiente linea de codigo, para filtrar la segmentación de los datos a analizar en cada exploración de los datos:
# Filtrar los datos para en la columna 'region_type'
df_reduced = df.loc[df['region_type'] == 'GreaterRegion'].copy()
df_cities = df.loc[df['region_type'] == 'City'].copy()
df_regions = df.loc[df['region_type'] == 'Region'].copy()

### Análisis de Series Temporales


### Gráficos para Visualización de Datos



### Elasticidad del Precio




### Análisis de Cohortes




### Análisis de Correlación y Regresión
