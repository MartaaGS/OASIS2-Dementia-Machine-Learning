\# ¿Puede el Machine Learning anticipar la demencia?



\### Un estudio exploratorio con datos longitudinales de OASIS-2



!\[Cabecera del proyecto](images/header.png)



> Este proyecto comenzó intentando responder si el Machine Learning podía ayudar a detectar el Alzheimer antes de la aparición de los síntomas. El análisis de los datos obligó a reformular esa pregunta y terminó convirtiéndose en un estudio sobre las posibilidades —y las limitaciones— de los modelos clásicos de Machine Learning para identificar patrones asociados a la conversión posterior a demencia.





\## 🧠 Motivación y pregunta de investigación



Este proyecto nace de una motivación personal. Una persona muy cercana a mí fue diagnosticada de Alzheimer y, al mismo tiempo que intentaba comprender mejor la enfermedad, surgió una pregunta relacionada con mi formación en Ciencia de Datos:



> \*\*¿Podría el Machine Learning ayudar a detectar el Alzheimer antes de la aparición de los síntomas?\*\*



La idea inicial era estudiar si sería posible identificar señales que permitieran anticipar la enfermedad varios años antes de su manifestación clínica.



Sin embargo, al comenzar a trabajar con \*\*OASIS-2\*\* y comprender mejor la estructura del dataset, quedó claro que los datos disponibles no permitían responder de forma rigurosa a esa pregunta. El tamaño de la muestra, las variables disponibles y el diseño longitudinal del estudio hacían necesario reformular el objetivo.



En lugar de forzar los datos para responder a la pregunta inicial, el proyecto evolucionó hacia una cuestión más ajustada a la información disponible:



> \*\*¿Hasta qué punto pueden los modelos clásicos de Machine Learning, utilizando las variables disponibles en OASIS-2, ayudar a diferenciar a los pacientes que permanecen sin demencia de aquellos que posteriormente presentan conversión a demencia?\*\*



A partir de esta pregunta, el proyecto se desarrolló en dos perspectivas complementarias: analizar la información disponible en la \*\*visita inicial (baseline)\*\* y estudiar posteriormente la \*\*evolución longitudinal\*\* de los pacientes.





\## 📊 El dataset: OASIS-2



Para este proyecto se utilizó \*\*OASIS-2 (Open Access Series of Imaging Studies – Longitudinal)\*\*, un conjunto de datos longitudinal que permite estudiar la evolución de los participantes a lo largo de varias visitas.



El dataset contiene \*\*150 participantes y 373 sesiones\*\*, con entre 2 y 5 visitas por participante. Esta estructura permite abordar el problema desde dos perspectivas: analizar la información disponible en la visita inicial y estudiar posteriormente cómo evolucionan determinadas variables durante el seguimiento.



Los participantes se clasifican en tres grupos:



\- \*\*Nondemented:\*\* participantes que permanecen sin demencia durante el seguimiento.

\- \*\*Demented:\*\* participantes clasificados con demencia.

\- \*\*Converted:\*\* participantes inicialmente sin demencia que evolucionan hacia una clasificación de demencia durante el seguimiento.



OASIS-2 incluye información demográfica, cognitiva, clínica y medidas derivadas de resonancia magnética. Entre las variables utilizadas en el proyecto se encuentran la edad, el sexo, la educación, el nivel socioeconómico, MMSE, CDR y medidas como eTIV y nWBV.



La naturaleza longitudinal de OASIS-2 fue especialmente relevante para este proyecto, ya que permitió comparar qué información aportaba la \*\*situación inicial del paciente\*\* frente a su \*\*evolución a lo largo del tiempo\*\*.



> \*\*Nota:\*\* el dataset original no se incluye en este repositorio. El acceso a OASIS-2 está sujeto a las condiciones de uso establecidas por OASIS. Las instrucciones para solicitar los datos se detallan en la sección \[Acceso a los datos](#-acceso-a-los-datos).





\## 🔬 Metodología



El análisis se desarrolló de forma progresiva, comenzando por la comprensión de los datos antes de aplicar técnicas de Machine Learning:



\*\*Comprensión de OASIS-2 → EDA baseline → EDA longitudinal → Machine Learning baseline → Machine Learning longitudinal\*\*



\### 1. Comprensión y exploración inicial



Se estudió la estructura de OASIS-2, el significado de las variables, la calidad de los datos y su carácter longitudinal. Esta primera etapa permitió conocer las posibilidades y limitaciones del dataset y reformular la pregunta inicial del proyecto.



\### 2. Análisis exploratorio baseline



Se analizó la primera visita de cada participante para estudiar las diferencias entre los grupos \*\*Nondemented, Demented y Converted\*\*, combinando análisis visual y pruebas estadísticas.



\### 3. Análisis exploratorio longitudinal



Se estudió la evolución de los participantes durante el seguimiento, prestando especial atención a los cambios en variables cognitivas y estructurales como \*\*MMSE y nWBV\*\*.



\### 4. Machine Learning baseline



Para estudiar la posible conversión futura a demencia se compararon únicamente \*\*Nondemented y Converted\*\*, utilizando información disponible en la visita inicial.



Se evaluaron tres modelos clásicos:



\- \*\*Regresión Logística\*\*

\- \*\*Random Forest\*\*

\- \*\*Support Vector Machine (SVM)\*\*



Debido al desbalance entre ambas clases, se compararon modelos estándar y balanceados y se utilizaron distintas métricas de evaluación, evitando depender únicamente de la accuracy.



\### 5. Machine Learning longitudinal



Finalmente, se incorporó información sobre la evolución de \*\*MMSE y nWBV\*\* para estudiar si las trayectorias longitudinales permitían diferenciar mejor a los participantes Converted de los Nondemented.



Este último análisis se interpreta como una \*\*clasificación retrospectiva de trayectorias y no como predicción precoz\*\*, ya que utiliza información obtenida durante el seguimiento.





\## 📈 Principales resultados



\### 1. La visita inicial muestra un importante solapamiento entre Nondemented y Converted



El análisis exploratorio mostró diferencias claras entre los participantes que ya presentaban demencia y aquellos que permanecían sin demencia. Sin embargo, los grupos \*\*Nondemented y Converted eran mucho más similares en la visita inicial\*\*.



Variables como MMSE o nWBV, que permiten observar diferencias entre Demented y Nondemented, no mostraron una separación suficientemente clara entre quienes permanecerían sin demencia y quienes posteriormente presentarían conversión.



Este resultado anticipaba una de las principales dificultades del problema de Machine Learning: \*\*identificar la conversión futura utilizando únicamente la información disponible al inicio del seguimiento\*\*.



\### 2. Una accuracy elevada no implicaba una buena capacidad predictiva



La cohorte utilizada para Machine Learning estaba fuertemente desbalanceada: \*\*72 participantes Nondemented frente a 14 Converted\*\*.



Los modelos sin balancear alcanzaban accuracies cercanas al \*\*83 %\*\*, pero prácticamente no identificaban participantes Converted. Por este motivo, la evaluación se centró también en métricas como Recall, Precision, F1-score, ROC-AUC y PR-AUC.



Entre las configuraciones evaluadas, el \*\*SVM balanceado sin CDR ni MMSE\*\* ofreció uno de los mejores compromisos:



| Métrica | Resultado aproximado |

|---|---:|

| Recall | 0.61 |

| Precision | 0.23 |

| F1-score | 0.33 |

| ROC-AUC | 0.65 |

| PR-AUC | 0.42 |



El modelo consiguió detectar una mayor proporción de Converted, pero a costa de un número considerable de falsos positivos y con una elevada variabilidad entre las particiones de validación.



\### 3. La información longitudinal tampoco produjo una separación robusta



En el análisis longitudinal, el \*\*cambio anual de MMSE\*\* mostró diferencias más claras entre Converted y Nondemented que el cambio anual de nWBV.



Sin embargo, al incorporar información sobre la evolución de los pacientes al modelo, el rendimiento continuó siendo moderado:



| Métrica | SVM longitudinal balanceado |

|---|---:|

| Recall | 0.55 |

| Precision | 0.26 |

| F1-score | 0.34 |

| ROC-AUC | 0.67 |

| PR-AUC | 0.46 |



Por tanto, la incorporación de información longitudinal \*\*no produjo una mejora sustancial ni una clasificación suficientemente estable\*\*.



!\[Comparación de resultados baseline y longitudinal](images/comparacion\_ml\_baseline\_longitudinal.png)



> \*\*Resultado principal:\*\* con la muestra y las variables estructuradas utilizadas en este proyecto, los modelos evaluados encontraron cierta señal relacionada con la conversión a demencia, pero no alcanzaron una capacidad suficientemente robusta para realizar una predicción individual fiable.





\## 💡 Conclusiones



Este proyecto comenzó con una pregunta ambiciosa: \*\*¿puede el Machine Learning anticipar la demencia?\*\*



Los resultados obtenidos muestran que la respuesta no es sencilla. Con la muestra y las variables estructuradas disponibles en OASIS-2 utilizadas en este estudio, los modelos clásicos de Machine Learning evaluados \*\*no mostraron una capacidad suficientemente robusta y estable para identificar de forma fiable qué pacientes desarrollarían posteriormente demencia\*\*.



Esto no significa que el Machine Learning no pueda contribuir a la detección precoz de enfermedades neurodegenerativas. Más bien pone de manifiesto que la capacidad de un modelo depende en gran medida de la \*\*calidad y cantidad de los datos, de las variables disponibles y del diseño del estudio\*\*.



La dificultad encontrada para anticipar la conversión a partir de la información disponible también sugiere que un problema clínico tan complejo probablemente requiera conjuntos de datos más amplios y una combinación más rica de información clínica, cognitiva, de neuroimagen y otros posibles biomarcadores.



Por tanto, más que obtener un modelo predictivo final, este proyecto ha permitido explorar de forma crítica \*\*hasta dónde podemos llegar con los datos disponibles y dónde aparecen sus límites\*\*.





\## ⚠️ Limitaciones



Los resultados de este proyecto deben interpretarse teniendo en cuenta varias limitaciones:



\- \*\*Tamaño de la muestra:\*\* la cohorte utilizada para Machine Learning contiene únicamente 86 participantes, de los cuales solo 14 pertenecen al grupo Converted. Esto limita la capacidad de los modelos para aprender patrones generalizables y contribuye a la elevada variabilidad observada.



\- \*\*Desbalance de clases:\*\* la diferencia entre el número de participantes Nondemented y Converted dificulta especialmente la identificación de la clase minoritaria.



\- \*\*Información disponible:\*\* el proyecto utiliza las variables estructuradas proporcionadas por OASIS-2. No se analizaron directamente las imágenes de resonancia magnética ni se incorporaron otras fuentes de información como biomarcadores, genética o PET.



\- \*\*Seguimiento longitudinal variable:\*\* los participantes presentan diferente número de visitas y duración del seguimiento. Aunque se utilizaron tasas de cambio anualizadas para reducir este efecto, esta heterogeneidad continúa siendo una limitación.



\- \*\*Ausencia de validación externa:\*\* los modelos no han sido evaluados en una cohorte independiente, por lo que los resultados deben considerarse exploratorios y no pueden generalizarse a otras poblaciones.



> \*\*Este proyecto tiene una finalidad exclusivamente exploratoria y educativa. Los modelos desarrollados no constituyen una herramienta diagnóstica ni tienen aplicación clínica.\*\*





\## 🧠 Qué he aprendido con este proyecto



Más allá de los resultados obtenidos, el desarrollo de este proyecto me ha permitido extraer varios aprendizajes importantes sobre el análisis de datos aplicado a problemas de salud:



\- \*\*Comprender el problema y los datos debe preceder al modelado.\*\* La pregunta inicial del proyecto tuvo que evolucionar cuando comprendí qué podía responder realmente OASIS-2.



\- \*\*Una buena métrica no siempre significa un buen modelo.\*\* En un problema desbalanceado, una accuracy elevada puede ocultar una capacidad prácticamente nula para identificar la clase que realmente nos interesa.



\- \*\*Significación estadística y capacidad predictiva no son lo mismo.\*\* Encontrar diferencias entre grupos no implica necesariamente poder clasificar correctamente a un paciente individual.



\- \*\*Hay que vigilar especialmente el data leakage y la circularidad.\*\* En datos clínicos, algunas variables pueden estar estrechamente relacionadas con la propia definición del resultado que intentamos predecir.



\- \*\*La información longitudinal no equivale automáticamente a predicción precoz.\*\* Utilizar datos obtenidos durante el seguimiento puede ayudar a caracterizar la evolución de los pacientes, pero no significa que esa información estuviera disponible en el momento inicial.



\- \*\*La complejidad del algoritmo no compensa las limitaciones de los datos.\*\* Antes de buscar modelos más sofisticados, es fundamental preguntarse si la muestra y las variables contienen suficiente información para responder al problema planteado.



En conjunto, el proyecto me ha permitido recorrer un flujo de trabajo completo de Data Science aplicado a salud: desde la formulación y reformulación de la pregunta de investigación hasta el análisis exploratorio, la evaluación estadística, el modelado y, especialmente, la interpretación crítica de los resultados.





\## 📓 Estructura del proyecto



El proyecto está organizado en cinco notebooks que siguen el orden en el que se desarrolló el análisis:



| Notebook | Contenido |

|---|---|

| \[01 - Comprensión y exploración inicial de OASIS-2](notebooks/01\_Understanding\_and\_Initial\_EDA\_OASIS2.ipynb) | Comprensión del dataset, estructura longitudinal, variables y primeras exploraciones. |

| \[02 - EDA Baseline](notebooks/02\_EDA\_Baseline.ipynb) | Análisis de la visita inicial y comparación entre Nondemented, Demented y Converted. |

| \[03 - EDA Longitudinal](notebooks/03\_EDA\_Longitudinal.ipynb) | Estudio de la evolución de los participantes y de los cambios en MMSE y nWBV. |

| \[04 - Machine Learning Baseline](notebooks/04\_ML\_Baseline.ipynb) | Comparación de Regresión Logística, Random Forest y SVM para estudiar la conversión futura utilizando información de la visita inicial. |

| \[05 - Machine Learning Longitudinal](notebooks/05\_ML\_Longitudinal.ipynb) | Evaluación de la información longitudinal para diferenciar las trayectorias de Converted y Nondemented. |



Los notebooks están documentados con el objetivo de explicar no solo el código, sino también las decisiones tomadas durante el análisis y la interpretación de los resultados.





\## 📂 Acceso a los datos



El dataset \*\*OASIS-2 no se distribuye junto con este repositorio\*\*.



Para acceder a los datos es necesario solicitar el acceso a través de la página oficial de \*\*Open Access Series of Imaging Studies (OASIS)\*\*, completando el formulario correspondiente:



\*\*OASIS Datasets:\*\*  

https://sites.wustl.edu/oasisbrains/datasets/



Como parte del proceso de acceso, el usuario debe aceptar y firmar el \*\*OASIS Data Use Agreement\*\*, comprometiéndose a cumplir las condiciones establecidas para el uso, almacenamiento y tratamiento de los datos.



Por este motivo, los datos originales utilizados en este proyecto no se incluyen ni se redistribuyen en este repositorio. Cualquier persona interesada en reproducir el análisis deberá solicitar su propio acceso a OASIS-2 y aceptar las condiciones de uso correspondientes.





\## 🔁 Reproducibilidad



Para reproducir los análisis de este proyecto:



1\. Solicita acceso a \*\*OASIS-2\*\* siguiendo las indicaciones de la sección anterior.

2\. Crea una carpeta `data` en la raíz del proyecto y guarda en ella el archivo utilizado para el análisis con el nombre:



&#x20;  ```

&#x20;  oasis\_2.xlsx

&#x20;  ```



3\. Instala las dependencias necesarias:



&#x20;  ```bash

&#x20;  pip install -r requirements.txt

&#x20;  ```



4\. Ejecuta los notebooks en orden, comenzando por `01` y continuando hasta `05`.



Los notebooks están configurados para cargar el dataset desde:



```text

../data/oasis\_2.xlsx

```



El archivo `requirements.txt` contiene las principales librerías de Python necesarias para ejecutar los análisis.



> Los datos originales de OASIS-2 no forman parte del repositorio y deben obtenerse directamente a través de OASIS.





\## 📚 Agradecimientos y referencias



\### Acknowledgments



“Data were provided \[in part] by OASIS \[insert appropriate OASIS source info]”



b. OASIS-2: Longitudinal: Principal Investigators: D. Marcus, R, Buckner, J. Csernansky, J. Morris; P50 AG05681, P01 AG03991, P01 AG026276, R01 AG021910, P20 MH071616, U24 RR021382



\### Citation



b. OASIS-2: Longitudinal: https://doi.org/10.1162/jocn.2009.21407





\## 👩‍💻 Autora



\*\*Marta Gan Sáez\*\*



Proyecto desarrollado como parte de mi formación y especialización en Ciencia de Datos e Inteligencia Artificial aplicada a salud.

