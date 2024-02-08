<a target="_blank" href="https://colab.research.google.com/github/PabloOrazi/fed-sentiment-analysis/">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Un modelo de predicción de Política Monetaria enriquecido por análisis de sentimiento de las minutas de la Reserva Federal

En las últimas décadas, el aspecto de la comunicación por parte de los bancos centrales ha cobrado mayor preponderancia a medida que se evoluciona hacia una mayor transparencia. Este cambio no solo responde a razones de legitimidad democrática y responsabilidad, sino también a la búsqueda de una política monetaria más efectiva. Los bancos centrales emplean diversos canales de comunicación, que incluyen declaraciones a los medios, conferencias de prensa, discursos, informes y minutas. Las declaraciones tienen como objetivo explicar la acción política realizada y transmitir la perspectiva futura en cuanto a la política monetaria. Por otro lado, las minutas proporcionan información más detallada sobre las opiniones de los miembros del Comité, abarcando la postura política adecuada, la perspectiva económica de EE. UU. y la inclinación de la política monetaria a corto plazo.

En este contexto, los inversores encuentran valiosa información en las minutas, revelando argumentos, datos, riesgos y expectativas de la Fed sobre el dinero, el crédito, el empleo, la inflación y el crecimiento. El análisis meticuloso de las minutas se convierte en una herramienta clave para los inversores, permitiéndoles detectar señales sobre el futuro comportamiento de la Reserva Federal y ajustar sus inversiones de manera anticipada.

En este repositorio mostramos un modelo de predicción de decisiones de política monetaria enriquecido por un modelo de análisis de sentimiento, mediante el cual buscamos que se evalúe las minutas de manera objetiva, realizando evaluaciones oración por oración y asignando clasificaciones basadas en los niveles de Hawkish, Dovish o Neutral. El gráfico 1 muestra la capacidad del modelo de análisis de sentimiento para identificar de manera coherente un tono dovish en las minutas durante períodos de recesión económica, así como un tono Hawkish cuando la inflación supera el objetivo establecido del 2%. Este enfoque proporciona una valiosa herramienta para anticipar y comprender las posibles respuestas de la Reserva Federal en diferentes condiciones económicas en el intento de evitar posibles sesgos de comportamiento de los mercados. 


                                                                  # Gráfico 1


![grafico_sentimiento](https://github.com/PabloOrazi/fed-sentiment-analysis/blob/main/img/grafico_sentimiento.jpg?raw=true)

A la información recopilada a partir del análisis de las minutas, hemos incorporado las tasas de interés a tres meses y la Tasa de Referencia (Federal Fund Rate) con el objetivo de anticipar el comportamiento que la Reserva Federal podría adoptar en su próxima decisión. Con este fin, hemos diseñado cuatro modelos, consistiendo en dos Regresiones Logísticas y dos Redes neuronales, cada una con y sin el análisis de sentimiento. De esta manera, podemos evaluar cómo la información derivada de las minutas y la utilización de modelos más sofisticados que los lineales contribuyen a mejorar la precisión de las predicciones.
--------------------------------------
Para entrenar los modelos decidimos dividir la informacion de las minutas y las tasas en 3 diferentes datasets el primero, se utilizar para entrenar a los modelos y  es el X_train e y_train que van desde 1995 hasta diciembre 2016. Para la validacion en las redes neuronales usamos los datos que van desde enero 2017 hasta diciembre 2017, y desde enero 2018 hasta la actualidad lo utilizamos para el testeo del mismo. 

En el primer modelo utiliza Logistic Regression y solamente se nutre con información de las tasas. A la hora de pronosticar, su rendimiento es extremadamente pobre, acierta el 33,33% de las veces, lo que significa que no es mejor que el azar. Si analizamos otros indicadores podemos ver que recall (la proporción de casos positivos que fueron correctamente identificados por el modelo) fue de 50% y precision (la proporción de casos positivos identificados correctamente por el modelo respecto a todos los casos identificados como positivos) fue solamente del 19.13%. Extremadamente bajos. 

Ahora bien, si al mismo modelo le agregamos la información de las minutas 

![alt text](https://github.com/[PabloOrazi]/[fed-sentiment-analysis]/blob/main/descarga.jpg?raw=true)

