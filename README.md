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

Una vez  hecha la classificación, añadimos una columna con categorización de City/Region/GreaterRegion/TotalUS así:
![image](https://github.com/user-attachments/assets/755d56cd-8ab6-4d2d-b4b8-e49bd3270354)


Es por eso que teniendo en cuenta esta classificación, hemos incluido también la siguiente linea de codigo, para filtrar la segmentación de los datos a analizar en cada exploración de los datos:

![image](https://github.com/user-attachments/assets/d698ac9c-c4f1-42f3-aae0-b39876377355)


### Análisis de Series Temporales
Descomposición de Serie Temporal del precio promedio de los aguacates, analizado con precios semanales.

En el gráfico siguiente, se puede observar claramente, que anualmente se repiten una serie de fluctuaciones en el "AveragePrice" como que, si nos centramos en el gráfico de Estacionalidad, o en el gráfico de Observado, podemos visualizar unos picos de máximos relativos en los meses de octubre y noviembre, así como una bajada en el precio medio de los aguacates en el mes de febrero.

Tras una búsqueda para recolectar información que nos pudiese indicar el motivo de estas fluctuaciones, hemos determinado que dos de los factores más determinantes para la bajada del precio de los aguacates en los meses de febrero, son, en primer lugar que en invierno, las bajas temperaturas en gran parte del país tienden a disminuir el interés en comidas frescas o veraniegas, como ensaladas o guacamole, que son formas comunes de consumir aguacates, además por ese mismo cambio en las temperaturas, hay mucha exportación de aguacates de México cosa que ayuda a mantener los precios bajos, y además, y el motivo que creemos que es más determinante en este caso, en enero y principios de febrero, el Super Bowl genera un aumento significativo en el consumo de aguacates debido a su popularidad como ingrediente principal del guacamole. Después del evento, el entusiasmo por este tipo de consumo disminuye, lo que puede explicar la caída en la demanda y consecuentemente el precio.

También hemos comprobado que en septiembre se empieza a acabar la temporada de cosecha del aguacate, y por eso, al disminuir la oferta, pero mantenerse la demanda, puede subir el precio en octubre y noviembre, otro factor, el cual consideramos como claramente muy determinante, es que en noviembre hay la fiesta nacional de  Acción de Gracias donde es muy común el uso del aguacate para hacer Guacamole

![image](https://github.com/user-attachments/assets/4194c701-eb6d-496e-b779-5b11e88b52f9)


Análisis de Estacionalidad por Región de la variación de Precios de Aguacates por Grandes Regiones.
![image](https://github.com/user-attachments/assets/27530520-2e29-4806-a270-6bb0739fd699)

En este gráfico se puede ver un claro incremento en el precio medio de los aguacates por Grandes Regiones, sobre todo hay dos claros repuntes como son, durante los meses previos al inicio de 2017 y hacia los meses finales de ese mismo año.

Tras una investigación, hemos asociado estos picos a las siguientes razones clave:

1. En primer lugar, y como motivo principal, la disminución en la Producción Global, puesto que México, el principal exportador de aguacates hacia los Estados Unidos (aproximadamente el 80% de los aguacates consumidos en EE.UU.), enfrentó una caída en la producción debido a factores climáticos adversos, como fueron las sequías y heladas, que afectaron sus cosechas en 2016 y 2017.

2. Y en segundo lugar, debido a un incremento en la Demanda Internacional, a causa de la creciente popularidad del aguacate, no solo en Estados Unidos, sino también en mercados emergentes como Asia y Europa. Presionó la oferta disponible, especialmente en temporadas donde la producción ya era limitada, lo cual ocasionó un claro incremento en los precios del aguacate.

### Gráficos para Visualización de Datos



### Elasticidad del Precio




### Análisis de Cohortes




### Análisis de Correlación y Regresión
