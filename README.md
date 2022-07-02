# Competencia de modelos de Predicción para el número de vehículos registrados en el sistema RUNT

<div style="text-align:center"><img src ="https://www.ipsenvigado.com/wp-content/uploads/2020/03/image001.jpg" /></div>



## Integrantes:
- Cristian Alejandro Rojas Mazo.
- Sebastian Lopez Mazo. 
- Kevin Danilo Arias Buitrago. 
- Santiago Carvajal Torres.
- Juan David Pino Ramirez.

<p > Semestre 1 Año 2022, Cuarta Entrega</p>

# Descripción.

<p align = "justify"> Según la página del RUNT ¨Se define como un sistema de información que permite registrar y mantener actualizada, centralizada, autorizada y validada la misma sobre los registros de automotores, conductores, licencias de tránsito, empresas de transporte público, infractores, accidentes de tránsito, seguros, remolques y semirremolques, maquinaría agrícola y de construcción autopropulsada y de personas naturales o jurídicas que prestan servicio al sector. (art. 8 y 9 de la Ley 769 de 2002 y la parte pertinente de la Ley 1005 de 2006). ¨ </p>

<p align = "justify"> Este sistema de información juega un gran papel dentro de los beneficios de los poseedores de un automotor, esto porque según el RUNT, su sistema posee 3 beneficios principales, estos:  </p>

<p> - Para mayor confiabilidad al momento de realizar un trámite usted se identificará con su firma y huella. </p>
<p> - Contará con la garantía de que, en caso de un accidente, las autoridades podrán consultar en línea y en tiempo real la legalidad de un SOAT y Revisión Técnico-Mecánica. </p>
<p> - Su información personal y la de su vehículo estarán protegidas por el RUNT, además podrá visualizar los cinco últimos trámites que haya realizado. </p>

<p align = "justify">  Dada la importancia del RUNT dentro del día a día de los ciudadanos poseedores de un automotor, plantear un modelo que tenga la capacidad de predecir la cantidad de vehículos registrados en el sistema diariamente traería consigo un impacto positivo para el RUNT y los ciudadanos, esto porque se podrían realizar una planeación bien organizada para ciertas fechas del año donde los registros sean más frecuentas, reducir costos operacionales y hacer más eficiente el sistema de información a través de la predicción.   </p>

# Justificación de las Variables.

<p align = "justify"> Con el objetivo de encontrar patrones en los datos relacionados con el RUNT se analizó la base de datos "registros_autos_entrenamiento.xlsx" la cual tenía la siguiente composición. </p>

![Image text](https://github.com/crrojasmazo/TAEComparaci-nModelosRunt/blob/main/imagen_2022-07-01_134950043.png)

<p align = "justify"> En esta solo de dan los datos de la fecha y las unidades. Se entienden las unidades como la cantidad de automóviles a los cuales se les sacó RUNT en la respectiva fecha por lo que se puede decir que son vehículos recién vendidos, con esto se puede entrar a analizar los movimientos de las ventas de los carros, sin embargo, tenemos un problema y es la falta de variables para poder plantear cualquier modelo, por lo que basados en la fecha optamos por sacar las siguientes variables.
</p>

* <p align = "justify"> NonBussinessDay: ayudados de una base de datos extra que nos dice que días son sábados, domingos y festivos en Colombia se hizo una variable indicadora (0 o 1) la cual es 0 si la fecha corresponde a un día de semana y 1 si corresponde a un día del fin de semana o festivo, los cuales son días no laborales normalmente. </p>
* Day: el número del día sacado de la fecha.
* <p align = "justify"> Dayweek: dice el día (entre monday y sunday) al que corresponde el día (esto sirve para los NonBussinessDay). </p>
* <p align = "justify"> Month: el número del mes sacado de la fecha original. </p>
* <p align = "justify"> Year: el número del año sacado de la fecha original. </p>
* <p align = "justify"> Holidays: es una variable indicadora (0 o 1) la cual no dice si el mes corresponde a un mes que comúnmente es de vacaciones (Enero, Junio, Julio, Noviembre, Diciembre) o algún otro mes, esto es importante pues basados en la página carroya se encontró que en los meses de vacaciones las personas tienden a comprar más vehículos, por lo que se hizo interesante analizar si está premisa es verdadera. </p>

<p align = "justify"> Como se tenía el dayweek en formato String, la mejor opción fue convertir esta columna en 7 (una por cada día de la semana), la cual sería una variable indicadora, así, si el día es lunes, en la columna dayweek_monday habrá un 1 y en las demás columnas habrá ceros, esto facilita el análisis de las variables y de la base de datos pues ahora todos nuestro datos son numéricos. </p>

<p align = "justify"> Finalmente se elimina Dayweek y la fecha inicial, pues esta ayudo con la creación de las variables día, mes y año y ya no es necesaria, para quedar con 12 variables o columnas. </p>

<p align = "justify"> Habiendo hecho todo el preprocesamiento y la elección de variables se pueden analizar un poco los datos con estadística descriptiva. Para esto tenemos las dos siguientes gráficas. </p>

![Image text](https://github.com/crrojasmazo/TAEComparaci-nModelosRunt/blob/main/imagen_2022-07-01_215342619.png)

<p align = "justify"> En la gráfica anterior se puede observar el comportamiento de la inscripción de vehículos según el día de la semana, además se tiene la comparativa de cómo ha cambiado con los años el comportamiento, vemos que a lo largo de los años la inscripción ha estado hasta cierto punto constante, empezando a caer las ventas desde el 2014 hasta la actualidad, esto para todos los días, por otro lado podemos notar que el sábado y el domingo la inscripción baja mucho, esto se puede explicar porque el sábado las jornadas laborales son más cortas, y el domingo por que en la mayoría de las oficinas no se presta servicio al público, aparte de esto el lunes tienen cierto comportamiento interesante, pues se venden muchos menos vehículos que los otros "días laborales" que igual se puede explicar ya que en Colombia la mayoría de festivos son lunes y son bastantes festivos al año. </p>


![Image text](https://github.com/crrojasmazo/TAEComparaci-nModelosRunt/blob/main/imagen_2022-07-01_215408393.png)


<p align = "justify"> En esta gráfica podemos notar un comportamiento que ya se sospechaba y es que en el mes de diciembre que también puede ser considerado un mes de vacaciones se venden más vehículos que en todos los otros meses, comportamiento que se ha repetido durante todos los años del estudio. Además de esto podemos decir que el comportamiento de todos los otros meses es normal, aproximándose a un comportamiento constante, sin embargo se vuelve a notar que desde el año 2014 la inscripción de vehículos ha disminuido, esto se podría explicar por el mercado tan grande de vehículos de "segunda mano" o por que la capacidad adquisitiva de las personas ha bajado por lo que comprar un vehículo ha quedado fuera de los alcances. </p>


# Metodologías Utilizadas.

<p align = "justify"> Después de la creación de variables y el refinamiento de la base de datos inicial, los datos se pasan por la función "setup" de la librería PyCaret. </p>

<p align = "justify"> La función setup lo que hace es iniciar un ambiente de entrenamiento y crea un proceso de transformación de las variables del modelo, esta función es el primer paso para la función "compare_models" la cual es muy importante pues entrena y evalúa el rendimiento de todos los estimadores disponibles en la librería (que ya se verán cuáles son) usando validación cruzada. La tabla arrojada por "compare_models" es la siguiente:  </p>

![Image_text](https://github.com/crrojasmazo/TAEComparaci-nModelosRunt/blob/main/2%20TAE.png)

<p align = "justify"> Aunque se puede ver que el modelo sugerido por la tabla es el lightgbm, para el desarrollo del trabajo se escogió el modelo rf esto quiere decir Random Forest Regressor, esto por el siguiente análisis de las métricas de desempeño de cada modelo. </p>

Que significa cada métrica dada.
* <p align = "justify"> MAE: error absoluto medio, mientras más alejado de cero (0) sea el número el modelo hará peores ajustes. </p>
* <p align = "justify"> MSE: error cuadrático medio, mientras más alejado de cero (0) sea el número el modelo hará peores ajustes. </p>
* <p align = "justify"> RMSE: raiz del error cuadrático medio, mientras más alejado de cero (0) sea el número el modelo hará peores ajustes. </p>
* <p align = "justify"> R2: 0 indica que el modelo no sirve mientras 1 indica que es el modelo perfecto. </p>
* <p align = "justify"> RMSLE: raiz del error cuadrático logarítmico medio, mientras más alejado de cero (0) sea el número el modelo hará peores ajustes.  </p>
* <p align = "justify"> MAPE: error porcentual absoluto medio. Mide el tamaño del error en términos porcentuales. </p>

<p align = "justify"> Nuestro modelo escogido (Random forest) gana en el MAE, en el RMSLE y en el MAPE, además en los que no gana tiene una diferencia mínima con respecto al que si gana. </p>
Para el caso particular del R2 fuimos más allá y llevamos a cabo la ejecución del modelo con rf, el ajuste al modelo se hizo por lotes de datos y uno de ellos dio un R2 de 0.8728 (como se muestra en la tabla de abajo), que es incluso mayor al R2 de los dos modelos que supuestamente le gana en esta métrica (se recuerda además que los parámetros para el modelo RF se calculan con base a ese lote que tuvo mejor R2), por lo que ahora con más seguridad se trabajará con este modelo. </p>

![image_text](https://github.com/crrojasmazo/TAEComparaci-nModelosRunt/blob/main/imagen_2022-07-01_173728009.png)

<p align = "justify"> Ahora, un random forest regressor o regresor de bosque aleatorio es un meta estimador que ajusta un número de árboles de decisión clasificatorios en varias submuestras del conjunto de datos y utiliza el promedio para mejorar la precisión predictiva y controlar el sobreajuste. </p>

<p align = "justify"> Teniendo que el modelo se hará con el random forest regressor, se corren varios modelos por lotes de datos y se escogen los parámetros que mejor ajustan el modelo (mejor basado en métricas como el R2). </p>




# Métricas de Error Conseguidas.

  <p align = "justify"> Luego de estimar los mejores parámetros para el modelo, se les pasan los datos de entrenamiento y testeo y se sacan métricas de desempeño del modelo, para este caso R2 para el entrenamiento y otro para el testeo. </p>
  
* <p align = "justify"> Para el dataset de entrenamiento se obtuvo un r cuadrado de 0,96 lo que nos indica que el modelo se ajusta en un 96% y se mantiene alto el nivel de precisión y bajo el nivel de sesgo del modelo. </p>
* <p align = "justify"> Para el dataset de prueba también se obtiene un determinante prometedor 0,85 nuevamente indicándonos que el modelo se ajusta en un 85% mantenido alto el nivel de precisión y bajo el nivel de sesgo del modelo. </p>
  

<p align = "justify"> Finalmente se obtienen las predicciones con el modelo ya entrenado y testeado. </p>



# Conclusiones.

* <p align = "justify"> Teniendo en cuenta los valores obtenidos al realizar el determinante o R cuadrado con los dataset de entrenamiento y test, 96% y 85% respectivamente podemos concluir que los niveles de precisión y sesgo del modelo frente a los datos reales se mantiene altos y bajos respectivamente lo cual indica que el modelo ajusta bastante bien a los resultados, además al comprar con el resto de modelos y sus determinantes el random forest regressor se mantiene como uno de los modelos con r cuadrado mas alto, lo cual se corrobora con los determinantes de que arrojo el dataset de entrenamiento y prueba. </p>
 
* <p align = "justify"> Se espera que el modelo prediga muy bien sobre todos los datos que se le pongan, esto debido a la uniformidad de las observaciones, pues a lo largo de los años no se ha visto gran variación en el comportamiento del mercado. </p>

* <p align = "justify"> El modelo funciona muy bien para condiciones normales, aunque no se tienen datos de este periodo, se espera que para los años denominados de pandemia la dinámica del mercado haya cambiado un poco, por lo que no se recomienda hacer predicciones de estos años, pues se espera que no sean tan precisas ya que no hablamos de unas condiciones en el mercado normales o comunes debido a el cambio de dinámica que trajo la pandemia. </p>


## Cibergrafía
  - https://www.runt.com.co/sobre-runt/que-es-runt
  - https://pycaret.gitbook.io/docs/learn-pycaret/official-blog/announcing-pycaret-1.0#9.-predict-model
  - https://www.runt.com.co/node/2892
  - https://pycaret.gitbook.io/docs/get-started/quickstart#setup
  - https://support.numxl.com/hc/es/articles/215969423-MAE-Error-medio-absoluto
  - https://aprendeia.com/evaluando-el-error-en-los-modelos-de-regresion/
  - https://www.gestiondeoperaciones.net/proyeccion-de-demanda/error-porcentual-absoluto-medio-mape-en-un-pronostico-de-demanda/
- https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html
- https://www.carroya.com/noticias/guias-de-compra-y-venta/las-mejores-fechas-para-comprar-carro-4411
- https://sitiobigdata.com/2018/08/27/machine-learning-metricas-regresion-mse/#:~:text=MSE%20b%C3%A1sicamente%20mide%20el%20error,valor%2C%20peor%20es%20el%20modelo

