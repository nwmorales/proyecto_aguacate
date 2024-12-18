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
#### Descomposición de Serie Temporal del precio promedio de los aguacates, analizado con precios semanales.

En el gráfico siguiente, se puede observar claramente, que anualmente se repiten una serie de fluctuaciones en el "AveragePrice" como que, si nos centramos en el gráfico de Estacionalidad, o en el gráfico de Observado, podemos visualizar unos picos de máximos relativos en los meses de octubre y noviembre, así como una bajada en el precio medio de los aguacates en el mes de febrero.

Tras una búsqueda para recolectar información que nos pudiese indicar el motivo de estas fluctuaciones, hemos determinado que dos de los factores más determinantes para la bajada del precio de los aguacates en los meses de febrero, son, en primer lugar que en invierno, las bajas temperaturas en gran parte del país tienden a disminuir el interés en comidas frescas o veraniegas, como ensaladas o guacamole, que son formas comunes de consumir aguacates, además por ese mismo cambio en las temperaturas, hay mucha exportación de aguacates de México cosa que ayuda a mantener los precios bajos, y además, y el motivo que creemos que es más determinante en este caso, en enero y principios de febrero, el Super Bowl genera un aumento significativo en el consumo de aguacates debido a su popularidad como ingrediente principal del guacamole. Después del evento, el entusiasmo por este tipo de consumo disminuye, lo que puede explicar la caída en la demanda y consecuentemente el precio.

También hemos comprobado que en septiembre se empieza a acabar la temporada de cosecha del aguacate, y por eso, al disminuir la oferta, pero mantenerse la demanda, puede subir el precio en octubre y noviembre, otro factor, el cual consideramos como claramente muy determinante, es que en noviembre hay la fiesta nacional de  Acción de Gracias donde es muy común el uso del aguacate para hacer Guacamole

![image](https://github.com/user-attachments/assets/4194c701-eb6d-496e-b779-5b11e88b52f9)


#### Análisis de Estacionalidad por Región de la variación de Precios de Aguacates por Grandes Regiones.
![image](https://github.com/user-attachments/assets/27530520-2e29-4806-a270-6bb0739fd699)

En este gráfico se puede ver un claro incremento en el precio medio de los aguacates por Grandes Regiones, sobre todo hay dos claros repuntes como son, durante los meses previos al inicio de 2017 y hacia los meses finales de ese mismo año.

Tras una investigación, hemos asociado estos picos a las siguientes razones clave:

1. En primer lugar, y como motivo principal, la disminución en la Producción Global, puesto que México, el principal exportador de aguacates hacia los Estados Unidos (aproximadamente el 80% de los aguacates consumidos en EE.UU.), enfrentó una caída en la producción debido a factores climáticos adversos, como fueron las sequías y heladas, que afectaron sus cosechas en 2016 y 2017.

2. En segundo lugar, debido a un incremento en la Demanda Internacional, a causa de la creciente popularidad del aguacate, no solo en Estados Unidos, sino también en mercados emergentes como Asia y Europa. Presionó la oferta disponible, especialmente en temporadas donde la producción ya era limitada, lo cual ocasionó un claro incremento en los precios del aguacate.

#### Tendencia de Ventas de Aguacates a lo largo del Tiempo
![image](https://github.com/user-attachments/assets/ad237578-c0e2-40b9-b6ff-9c01bdffdb98)
En este gráfico se puede observar de forma muy clara el suceso que afirmábamos al resaltar el primer gráfico de descomposición de Serie Temporal del precio promedio de los aguacates, puesto que exactamente los mismos picos de máximos relativos que tiene este gráfico en las tendencias de venta, aparecen como mínimos relativos en ese gráfico, meramente por el índice compuesto por Oferta/Demanda, con la afectación que tiene sobre el precio.


### Gráficos para Visualización de Datos
#### Gráfico de violín de los datos del volumen total por 'región'
![image](https://github.com/user-attachments/assets/8cba89ac-465c-4877-9301-f88989a9509d)
En este gráfico de violín del volumen total de consumo de aguacates, ordenado por grandes regiones, hemos podido ver algunas regiones como "West", "California" y "SouthCentral" con dispersiones pronunciadas, y, por otro lado, en otras regiones como, la región "Plains", que tienen un comportamiento bastante más uniforme.

#### Boxplot Comparativo de Precios entre Años
![image](https://github.com/user-attachments/assets/f502b12a-894b-4dc9-b269-b14b8ef6544d)

Este gráfico se revela que, entre 2015 y 2017, parece existir una tendencia al alza en el precio promedio de los aguacates, alcanzando su punto más alto en 2017.

En 2018, el precio promedio muestra una disminución en este promedio, lo que sugiere que el mercado pudo haberse estabilizado o que hubo una mayor disponibilidad de aguacates.

El año 2017 destaca por una mayor variabilidad en los precios promedio en comparación con los demás años, reflejada en la amplitud de la caja y en la cantidad de valores atípicos. Esto indica que 2017 fue un período marcado por inestabilidad en los precios de los aguacates. En contraste, 2018 presenta una menor variabilidad y un número reducido de outliers, lo que sugiere precios más estables y consistentes durante ese año.

Además, se identifican numerosos valores atípicos en 2016 y 2017, lo que podría ser indicativo de la influencia de factores externos, como variaciones climáticas o un aumento en la demanda, que impactaron significativamente los precios durante esos períodos.

#### Gráfico de ventas por Tipo de Bolsa
En el siguiente grafico podemos observar el análisis de las ventas según el tamaño de las bolsas, el cual revela que las bolsas pequeñas (Small Bags) tienen una mayor demanda en comparación con las bolsas grandes (Large Bags) y las bolsas extragrandes (XLarge Bags). Este comportamiento se puede observar claramente en la gráfica presentada, donde las Small Bags destacan como el formato más popular entre los consumidores, siempre sin tener en cuenta el apartado de Total Bags, el cual únicamente expresa el sumatorio de las ventas de todas las bolsas de forma común.

Esta preferencia podría estar relacionada con diversos factores, como la comodidad para el transporte, su asequibilidad o una mayor adecuación a las necesidades de los hogares promedio. En contraste, las Large Bags y XLarge Bags parecen dirigirse a un segmento más específico del mercado, como restaurantes, mayoristas o familias numerosas.  

La diferencia en las ventas también podría reflejar patrones de consumo ligados a la frecuencia de compra, con las Small Bags siendo ideales para consumidores que prefieren adquirir productos frescos en cantidades más pequeñas de manera regular. Este patrón subraya la importancia de entender cómo el tamaño del empaque influye en las decisiones de compra y el comportamiento del mercado.
![image](https://github.com/user-attachments/assets/48a0141e-6e93-47e1-8d96-62c79d877cf5)



### Elasticidad del Precio

#### Elasticidad Precio-Demanda por Año

![image](https://github.com/user-attachments/assets/70acd10c-09e9-4ca4-a7a7-3da8b4b0da18)
Podemos observar que la elasticidad mejora en todas las categorías de 2015 a 2016

City tiene la elasticidad más baja, lo que sugiere que en entornos urbanos, el precio no afecta significativamente la demanda. 

GreaterRegion y TotalUS muestran una tendencia general de mejora hasta 2017, pero sufren un retroceso en 2018

#### Elasticidad a Nivel de Tipo de Bolsa

![image](https://github.com/user-attachments/assets/6a310e70-951c-493d-8770-7c924899947d)

![image](https://github.com/user-attachments/assets/25420982-cc75-4a00-8eab-73861e94285d)

![image](https://github.com/user-attachments/assets/534db5d0-8a1e-4563-8239-d7be784cbd00)

En las gráficas se puede observar que las Small Bags tienen elasticidades negativas, lo cual es común porque la demanda disminuye con el aumento de precios.

Las Large Bags muestran variaciones drásticas: en "GreaterRegion" hay alta sensibilidad negativa, mientras que en "City" y "Region" la elasticidad es positiva.

Las XLarge Bags presentan un comportamiento inconsistente, positivo en "GreaterRegion" y "City", pero muy negativo en "Region". Estas diferencias podrían deberse a preferencias locales, factores económicos específicos o condiciones del mercado en cada región.

#### Elasticidad Precios-Ventas (Relación General)

![image](https://github.com/user-attachments/assets/bf8aedce-cbe5-416f-8fd6-5a07d7b61dd2)

Observamos que los Aguacates Convencionales tienen Alta elasticidad de precio, donde un aumento en el precio reduce significativamente las ventas.

También que los Aguacates Orgánicos tienen una Baja elasticidad, ya que los precios altos no afectan drásticamente las ventas, aunque el volumen total de ventas sigue siendo bajo.

Esto refleja que los aguacates convencionales tienen mayor demanda general, mientras que los orgánicos atraen un nicho específico dispuesto a pagar más.


### Análisis de Cohortes
#### Cohortes Basadas en Precios Promedios Trimestrales
![image](https://github.com/user-attachments/assets/7f276e48-0983-40f3-9292-45538036a847)

Como se puede observar en la gráfica 1 hay fluctuación en el precio promedio del aguacate a lo largo del tiempo, el precio del aguacate varía de manera cíclica con picos y caídas claras, mostrando una ligera tendencia al alza a lo largo del tiempo hasta Q3 de 2017. 

En la gráfica 2 a lo largo del tiempo, el volumen total de ventas presenta subidas y bajadas marcadas y el volumen de ventas fluctúa estacionalmente, con caídas en ciertos trimestres y una tendencia de recuperación posterior. 

Hay relación entre ambas gráficas que sería cuando el precio promedio sube (Q3 de 2017), parece que el volumen total de ventas tiende a disminuir ligeramente en períodos cercanos (como Q3 de 2017) y Las bajas en precios (Q1 de 2016 y Q1 de 2017) coinciden con altos volúmenes de ventas, sugiriendo una posible relación inversa entre precio y ventas.


#### Cohortes por Región y Fecha
![image](https://github.com/user-attachments/assets/abc8f6db-0cc9-4c12-a5fb-8b66df9b02ee)   ![image](https://github.com/user-attachments/assets/2bfe3349-68d4-4977-92c7-0bb3eadd800a)

Como podemos observar West y California son las regiones más destacadas, con precios más altos y volúmenes de ventas elevados, esto sugiere que estas regiones lideran el mercado tanto en demanda como en capacidad de pago.

Regiones como Midsouth, Plains y Southeast tienen volúmenes de ventas bajos y precios más accesibles. Estas podrían ser áreas con potencial de crecimiento en demanda

Los picos de precios y volúmenes en 2017 podrían deberse a un aumento en la demanda global o condiciones de oferta limitada.


#### Análisis de Cohortes en Función del Tipo de Bolsa
![image](https://github.com/user-attachments/assets/e566e121-2365-4cdd-969b-ac78ab96aa9c)
![image](https://github.com/user-attachments/assets/ee69f287-5831-4385-a445-6cee327372b2)


En esta gráfica podemos observar que las Small Bags son el motor principal de las ventas de aguacates, tanto en la categoría convencional como en la orgánica.

Las ventas totales tienden a crecer con el tiempo, con picos estacionales.

Las Large Bags tienen un rol secundario pero muestran crecimiento, especialmente en bolsas orgánicas.

Las XLarge Bags representan una fracción muy pequeña y su impacto es insignificante en comparación con las otras categorías


#### Cohortes de Clientes Basadas en Ventas
![image](https://github.com/user-attachments/assets/e14f10f5-fe58-4059-93f4-c628f0dc5ccb)
En la gráfica podemos observar que West lidera el volumen de ventas, con un crecimiento marcado entre 2015 y 2017.

California ocupa una posición sólida con ventas consistentes

Regiones como Southeast y Plains destacan por un crecimiento notable, mostrando oportunidades en estas áreas.

Las regiones con bajo volumen de ventas se mantienen constantes y no muestran cambios significativos, lo que sugiere mercados menos activos o con menor demanda.


### Análisis de Correlación y Regresión
#### Matriz de Correlación de las Variables Numéricas surgidas del Análisis de Correlación y Regresión
![image](https://github.com/user-attachments/assets/8da35913-768d-4315-ac32-6748f7225943)
Teniendo en cuenta y utilizando, todas las variables numéricas del DataFrame, podemos hacer un gráfico de tipo heatmap para la matriz de correlación entre esos datos.

Para este gráfico, puesto que, como ya hemos indicado en un apartado anterior, sabemos que Total Bags es la combinación de Small Bags, Large Bags i XLarge Bags, y por lo tanto en el grafico de la matriz de correlación, podemos simplificar el heatmap y dejar sólo Total Bags.

Dicho esto, al analizar el gráfico, observamos que Total Volume muestra una alta correlación con Total Bags y con las columnas que representan los calibres 4046 y 4225 (que representan los tipos de aguacate). Esto sugiere que las ventas de aguacates de estos calibres son los principales contribuyentes al volumen total de ventas.

Es importante tener en cuenta que esta alta correlación entre variables puede impactar negativamente en el análisis, especialmente al usar modelos de regresión lineal. Las correlaciones fuertes entre las variables independientes pueden llevar a problemas de multicolinealidad, lo que a su vez puede hacer que los modelos sean inestables, generen errores numéricos y ofrezcan un rendimiento de predicción deficiente.


### Análisis de Dispersión entre Variables Clave
Estos graficos ilustran el diagrama de dispersión que hemos realizado, implementando regresión lineal y polinómica.
Realizando un analisis por cada grupo de regiones que hemos creado siendo estas:
#### Greater Reagions:
![image](https://github.com/user-attachments/assets/f7fa3f12-ea18-4527-94c3-1b61136a9904)

### Cities:
![image](https://github.com/user-attachments/assets/87889af0-34f0-4787-abac-d2c3a498cae6)

### Regions:
![image](https://github.com/user-attachments/assets/56d00783-7ced-4549-8f96-0eb845ffaf26)

### TotalUS:
![image](https://github.com/user-attachments/assets/26de5589-0ccc-413a-b743-e1cec783189c)

Al analizar la dispersión entre las variables clave AveragePrice y Total Volume, se observa una concentración de puntos cerca del valor 0, lo que indica que los volúmenes de venta de aguacates orgánicos son notablemente más bajos que los convencionales.

Aun con eso, mediante los gráficos resultantes, podríamos concluir que la regresión polinómica de grado 2 es algo más ajustada. Sin embargo, la aproximación no es buena por el acúmulo de puntos cercanos a 0.

Además, al realizar el análisis por grupos, hemos observado, que la segmentación impacta de forma directa a la dispersión, de forma que en el nivel TotalUS, y de forma menos clara en Grandes Regiones, los datos están más agregados y muestran una tendencia global estable, pero, en cambio, a nivel de Regiones y Ciudades, la dispersión es mayor, lo que podría sugerir que los factores regionales y locales (como oferta, demanda o distribución) influyen más en la relación precio-volumen.


### Predicciones Mensuales Usando Datos Trimestrales
Si realizamos predicciones mensuales del **'AveragePrice'** utilizando datos trimestrales a través de una regresión lineal, empleando los dos primeros meses para predecir el tercero, obtenemos estos valores:
![image](https://github.com/user-attachments/assets/71c67231-eae9-42a7-b325-b7ed8f44f4d0)

Y la siguiente gráfica:

![image](https://github.com/user-attachments/assets/d019f553-1879-4c45-8fab-2a1e37912961)

El conglomerado inicial probablemente se debe al menor volumen de aguacates orgánicos en comparación con los convencionales.  

Esto sugiere la necesidad de realizar predicciones por separado para los aguacates orgánicos y convencionales.

Y por eso hemos separado el grafico anterior en estos dos graficos:

![image](https://github.com/user-attachments/assets/ffc4d825-1ad4-4495-a8ae-8ccb18e49b6f)

En el cual hemos podido estimar estos valores:
![image](https://github.com/user-attachments/assets/34f1d486-8f26-4f97-a8be-7b1ddba4c2be)

Lamentablemente tal y como ya se observa en la gráfica, el modelo creado no es demasiado bueno.

Y sospechamos que se debe a que nuestro modelo está sobre ajustado.


### Desarrollo y analisis de Modelos de Regresión Múltiple

Realizamos un modelo de regresión múltiple usando las mismas variables numéricas que las implementadas en graficos anteriores, como por ejemplo en la matriz de correlació, siendo estas variables: 'Total Volume', '4046', '4225', '4770', y 'Total Bags', todo ello para obtener unos valores menos ajustados de la evaluación del 'AveragePrice':

![image](https://github.com/user-attachments/assets/eaa9b7b1-e661-4043-8106-d7b4aa40f88f)

Así como los coeficientes obtenidos para el modelo lineal y polinómico:

![image](https://github.com/user-attachments/assets/c007b7a2-3872-4819-872f-5c2595a5141a)


### Analisis de la influencia de las Ventas Totales sobre el Precio Promedio
![image](https://github.com/user-attachments/assets/bc45b469-508e-4dca-a3a4-966a773c4b82)

En este gráfico, podemos observar el resultado grafico de la influencia que ejercen las ventas totales (Total Volume) en el precio promedio (AveragePrice), al aplicar los modelos: lineal y polinómico.

Entendiendo que, la relación entre Total Volume y AveragePrice es negativa, puesto que como muestra claramente el grafico, el precio promedio de los aguacates disminuye con el aumento del volumen total.


## Temas a intentar mejorar en un futuro:

El apartado principal que no hemos realizado y desearíamos poder haberlo trabajado de mejor manera, sería el haber logrado un modelo predictivo que realizase de forma correcta, regresiones y proyecciones a futuro de los datos faltantes en la base de datos de avocados.

Creemos que este era uno de los temas más atractivos de este proyecto, pero lamentablemente por falta de tiempo, falta de conocimientos, y sinceramente una possible mala planificación de nuestros tiempos en el proyecto, no nos ha sido posible realizarlo.

![image](https://github.com/user-attachments/assets/3cd1f7fa-e8bd-48ee-82fd-36badeef6105)
