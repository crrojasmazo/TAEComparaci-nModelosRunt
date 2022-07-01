# Competencia de modelos de Predicción para el número de vehículos registrados en el sistema RUNT

<div style="text-align:center"><img src ="https://www.ipsenvigado.com/wp-content/uploads/2020/03/image001.jpg" /></div>



## Integrantes
- Cristian Alejandro Rojas Mazo 
- Sebastian Lopez Mazo 
- Kevin Danilo Arias Buitrago 
- Santiago Carvajal Torres
- Juan David Pino Ramirez

<p > Semestre 1 Año 2022, Cuarta Entrega</p>

# Descripción

<p align = "justify"> Según la página del RUNT ¨Se define como un sistema de información que permite registrar y mantener actualizada, centralizada, autorizada y validada la misma sobre los registros de automotores, conductores, licencias de tránsito, empresas de transporte público, infractores, accidentes de tránsito, seguros, remolques y semirremolques, maquinaría agrícola y de construcción autopropulsada y de personas naturales o jurídicas que prestan servicio al sector. (art. 8 y 9 de la Ley 769 de 2002 y la parte pertinente de la Ley 1005 de 2006). ¨ </p>

<p align = "justify"> Este sistema de información juega un gran papel dentro de los beneficios de los poseedores de un automotor, esto porque según el RUNT, su sistema posee 3 beneficios principales, estos:  </p>

<p> - Para mayor confiabilidad al momento de realizar un trámite usted se identificará con su firma y huella. </p>
<p> - Contará con la garantía de que, en caso de un accidente, las autoridades podrán consultar en línea y en tiempo real la legalidad de un SOAT y Revisión Técnico-Mecánica. </p>
<p> - Su información personal y la de su vehículo estarán protegidas por el RUNT, además podrá visualizar los cinco últimos trámites que haya realizado. </p>

<p align = "justify">  Dada la importancia del RUNT dentro del día a día de los ciudadanos poseedores de un automotor, plantear un modelo que tenga la capacidad de predecir la cantidad de vehículos registrados en el sistema diariamente traería consigo un impacto positivo para el RUNT y los ciudadanos, esto porque se podrían realizar una planeación bien organizada para ciertas fechas del año donde los registros sean más frecuentas, reducir costos operacionales y hacer más eficiente el sistema de información a través de la predicción.   </p>

# Justificación de las Variables.

<p align = "justify"> Con el objetivo de encontrar patrones en los datos relacionados con el RUNT se analizó la base de datos "registros_autos_entrenamiento.xlsx" la cual tenía la siguiente composición. </p>

![Image text](https://github.com/crrojasmazo/TAEComparaci-nModelosRunt/blob/main/imagen_2022-07-01_134950043.png)

En esta solo de dan los datos de la fecha y las unidades. Se entienden las unidades como la cantidad de automóviles a los cuales se les sacó RUNT por lo que se puede decir que son vehículos recien vendidos, por lo que se puede entrar a analizar los movimientos de las ventas de los carros, sin embargo, tenemos un problema y es la falta de variables para poder plantear cualquier modelo, por lo que basados en la fecha optamos por sacar estas variables.
* NonBussinessDay: 
* Day: 
* Dayweek:
* Month:
* Year:
* Holidays:

Explicación de las variables Dummies sacadas a partir de la columna Dayweek

Finalmente se elimina Dayweek y la fecha inicial, pues ya se descompuso, para quedar con 12 varibles o columnas.


# Metodologías Utilizadas.

Después de la creación de variables y el refinamiento de la base de datos inicial, los se pasan por la función "setup" de la librería PyCaret

La función setup lo que hace es iniciar un ambiente de entranamiento y crea un proceso de transformación de las variables del modelo, esta función es el primer paso para la función "compare_models" la cual es muy importante pues entrena y evalúa el rendimiento de todos los estimadores disponibles en la librería (que ya se verán cuales son) usando validación cruzada. La tabla arrojada por "compare_models" es la siguiente: 

![Image_text](https://github.com/crrojasmazo/TAEComparaci-nModelosRunt/blob/main/2%20TAE.png)

Aunque se puede ver que el modelo sugerido por la tabla es el lightgbm, para el desarrollo del trabajo se escogió el modelo rf osea Random Forest Regressor

teniendo que el modelo se hará con el random forest regressor, se ajustan los parámetros y se escogen los parámetros que mejor ajustan el modelo (mejor basado en métricas)




# Métricas de Error Conseguidas.
  Luego de estimar los mejores parámetros para el modelo, se les pasan los datos de entrenamiento y testeo y se sacan métricas de desempéño del modelo, para este caso R2 para el entreenamiento y otro para el testeo.
  
  
  Finalmente se obtienen las predicciones con el modelo ya entrenado y testeado.





## Cibergrafía
  - https://www.runt.com.co/sobre-runt/que-es-runt
  - https://pycaret.gitbook.io/docs/learn-pycaret/official-blog/announcing-pycaret-1.0#9.-predict-model
  - https://www.runt.com.co/node/2892
  - https://pycaret.gitbook.io/docs/get-started/quickstart#setup
