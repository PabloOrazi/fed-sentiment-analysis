<a target="_blank" href="https://colab.research.google.com/github/PabloOrazi/fed-sentiment-analysis/">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# ¿Puede la Inteligencia Artificial anticipar al mercado?
## Leyendo el mensaje de la Fed con Inteligencia Artificial

## Introducción

En las últimas décadas, el aspecto de la comunicación por parte de los bancos centrales ha cobrado mayor preponderancia a medida que se evoluciona hacia una mayor transparencia. Este cambio no solo responde a razones de legitimidad democrática y responsabilidad, sino también a la búsqueda de una política monetaria más efectiva. Los bancos centrales emplean diversos canales de comunicación, que incluyen declaraciones a los medios, conferencias de prensa, discursos, informes y minutas. Las declaraciones tienen como objetivo explicar la acción política realizada y transmitir la perspectiva futura en cuanto a la política monetaria. En EE.UU., por ejemplo, las minutas proporcionan información más detallada sobre las opiniones de los miembros del Comité de la Reserva Federal (*Fed*), abarcando la postura política adecuada, la perspectiva económica de EE. UU. y la inclinación de la política monetaria a corto plazo.

En este contexto, los inversores encuentran valiosa información en las minutas, revelando argumentos, datos, riesgos y expectativas de la Fed sobre el dinero, el crédito, el empleo, la inflación y el crecimiento. El análisis meticuloso de las minutas se convierte en una herramienta clave para los inversores, permitiéndoles detectar señales sobre el futuro comportamiento de la Reserva Federal y ajustar sus inversiones de manera anticipada.

## Datos y Modelos

Con el propósito de destacar las capacidades de la inteligencia artificial, a la hora de interpretar las minutas, creamos este repositorio que cuenta con cuatro modelos: dos Regresiones Logísticas y dos Redes Neuronales. Estos modelos se emplean para predecir las decisiones de política monetaria por parte de la Fed. Estas decisiones pueden ser:

    - Mantener las tasas de referencia sin cambios
   
    - Subir las tasas de referencia

    - Bajar las tasas de referencia


La Regresión Logística es un modelo estadístico que se emplea para predecir la probabilidad de un evento, como determinar si un correo electrónico es spam, si un cliente realizará una compra, o en nuestro caso, si la Fed mantendrá, subirá o bajará la tasa de interés. Este modelo utiliza una función logística para establecer la relación entre las variables de entrada y la probabilidad del resultado.

Por otro lado, las Redes Neuronales son modelos de *Machine Learning* (ML) denominados de aprendizaje profundo compuestos por capas de nodos interconectados que procesan la información de entrada para producir una salida. Cada neurona aplica transformaciones no lineales a los datos y transmite los resultados a las neuronas de la siguiente capa. Estas redes tienen la capacidad de aprender patrones complejos y características de los datos a través del proceso de entrenamiento.

Los insumos que usamos en los modelos para la predicción de la decisión de la Fed son tres -el análisis de sentimiento de las minutas, las tasas de interés a tres meses y la Tasa de Referencia-.  

En el análisis del sentimiento de las minutas, utilizamos un modelo de inteligencia artificial desarrollado con el fin de evaluarlas de manera objetiva. Este modelo realiza evaluaciones oración por oración, asignando clasificaciones basadas en cuán *Hawkish* (sesgo monetario contractivo), *Dovish* (sesgo monetario expansivo) o *Neutral* (sesgo monetario sin definición clara) son. Para llevar a cabo este análisis, hemos utilizado un modelo de inteligencia artificial de código abierto, específicamente del repositorio de la página Hugging Face.

Ejemplo de los análisis de las minutas:

![sentimiento-oracion](https://github.com/PabloOrazi/fed-sentiment-analysis/assets/44901407/367ccf47-a653-4473-8717-d674263fedc1)


Este análisis se realiza con todas las oraciones que conforman las minutas, calculando un promedio de todas ellas para obtener un único dato que represente la evaluación de la respectiva minuta.

El siguiente gráfico muestra la capacidad del modelo de análisis de sentimiento para identificar de manera coherente un tono *dovish* en las minutas durante períodos de recesión económica, así como un tono *Hawkish* cuando la inflación supera el objetivo establecido del 2%. Este enfoque proporciona una valiosa herramienta para anticipar y comprender las posibles respuestas de la Reserva Federal en diferentes condiciones económicas en el intento de evitar posibles sesgos de comportamiento de los mercados. 
                                                             
![grafico_sentimiento](https://github.com/PabloOrazi/fed-sentiment-analysis/assets/44901407/74b1eb85-8657-42f3-ad8b-d69ef1c7ba12)

Para medir la efectividad de nuestro análisis de sentimiento de las minutas, hemos utilizado dos modelos de Regresión Logística y dos Redes Neuronales. A un modelo de Regresión Logística le incorporamos la información de las minutas y el otro no. Del mismo modo, desarrollamos dos Redes Neuronales, una con los datos de las minutas y otra sin ellos. Este enfoque nos permite evaluar si la información que obtenemos de las minutas es útil para predecir las decisiones de política monetaria.

Para entrenar los modelos decidimos dividir la informacion de las minutas y las tasas en 3 diferentes datasets. El primero, se utiliza para entrenar a los modelos que van desde 1995 hasta diciembre 2016. El segundo se utiliza para la validación de las redes neuronales usando los datos que van desde enero 2017 hasta diciembre 2017, y por último,  utilizamos para el testeo del mismo los datos que van desde enero 2018 hasta la actualidad.

## Resultados

En el primer modelo utiliza una regresión logística (*logistic regression*) y solamente se nutre con información de las tasas. A la hora de pronosticar, su rendimiento es extremadamente pobre, acierta el 33,33% de las veces, lo que significa que no es mejor que el azar. Si analizamos otros indicadores podemos ver que recall (la proporción de casos positivos que fueron correctamente identificados por el modelo) fue de 50% y precision (la proporción de casos positivos identificados correctamente por el modelo respecto a todos los casos identificados como positivos) fue solamente del 19.13%. Extremadamente bajos. 

Ahora bien, si al mismo modelo le agregamos la información de las minutas, las mejoras son sustanciales. Los tres indicadores mejoran, pasando el accuracy a 79,5%, el recall a 68,0% y el precision a 69,8%. Estas mejoras nos permiten percibir de manera clara que al analizar las minutas hay indicios claros de los futuros pasos de la Reserva Federal. A continuación vemos las diferentes métricas y como mejoran una vez que al dataset de las tasas le agregamos la información de las minutas.  

![modelos_logistic_regression](https://github.com/PabloOrazi/fed-sentiment-analysis/assets/44901407/781c34cc-8247-4fee-baef-89f58b3b89b6)

Además de *recall, accuracy* y *precision*, el gráfico también muestra el *F1 score, roc_auc_score* y *log_loss*, esenciales para evaluar de manera completa el desempeño de un modelo de machine learning. El F1 score combina precision y recall en una sola métrica, siendo ideal para conjuntos de datos desbalanceados. El roc_auc_score mide la capacidad de clasificación del modelo, mientras que log_loss evalúa la certeza de las probabilidades de las predicciones, siendo menor su valor cuando las predicciones son más certeras.

A la hora de analizar otro tipo de modelos como una Red Neuronal, cuando analizamos el mismo tipo de data, nos damos cuenta de que son mejores que la Regresión Logística. Las redes neuronales sin la información de las minutas, es decir, prediciendo la futura decisión de la Fed solamente con el movimiento de las tasas de interés, tienen un accuracy del 64,1%, casi el doble que la Regresión Logística con el mismo dataset. En cuanto a recall y precision, son del 61,7% y el 75,1%, respectivamente. Sin embargo, la Regresión Logística con la información de las minutas muestra un recall y un accuracy superiores (aunque con una precisión ligeramente inferior). En efecto, el mejor modelo es una Red Neuronal entrenada con la información de tasas y las minutas. Este modelo, nuestro modelo final, es superior a todos los demás modelos. El accuracy es del 82,0%, con un recall del 81,7% y una precisión del 85,7%, respectivamente. 

En machine learning, la matriz de confusión es una herramienta que nos permite evaluar el desempeño de un modelo predictivo. Esta matriz muestra de manera concisa la cantidad de predicciones correctas e incorrectas realizadas por el modelo en comparación con los valores reales. En la matriz, las filas representan los valores reales, mientras que las columnas representan las clases predichas por el modelo. Así, la diagonal principal contiene los casos en los que el modelo acertó, mientras que las celdas fuera de esta diagonal indican los errores de predicción. 

Mostramos la matriz de confusión de nuestro modelo seleccionado. 

![matriz confusion rn + minutas](https://github.com/PabloOrazi/fed-sentiment-analysis/assets/44901407/892d85e3-03e6-4b6a-997c-e1fb1111228c)


## Comparación final de los cuatro modelos

Los modelos que empleamos, la regresión logística y las redes neuronales, ofrecen enfoques distintos en el campo del machine learning. La regresión logística, un modelo más simple y fácil de interpretar, se utiliza para problemas de clasificación al calcular la probabilidad de que una instancia pertenezca a una clase específica utilizando una función logística. Por otro lado, las redes neuronales, son estructuras de aprendizaje que pueden aprender patrones y relaciones complejas en los datos a través de capas de nodos interconectados que procesan información.

En este cuadro, se muestra la comparación de las principales métricas de los modelos seleccionados. Podemos observar que las redes neuronales, con la misma información, son superiores a la Regresión Logística, pero lo que marca la diferencia son las minutas; los modelos con esa información son ampliamente superiores a los que no la tienen.   

![comparacion 4 modelos](https://github.com/PabloOrazi/fed-sentiment-analysis/assets/44901407/d8d717c1-c7dc-408c-a904-fc4d49c82066)


![Log_loss](https://github.com/PabloOrazi/fed-sentiment-analysis/assets/44901407/beae2241-e94e-40ab-80a2-f8febd39c885)
