\# Credit Risk Analysis | Análisis de Riesgo Crediticio



\*\*Machine Learning · XGBoost · Python · Credit Risk Modeling · Probability of Default\*\*



\## 🇪🇸 Español



\### 1. Descripción del proyecto



Proyecto de análisis de riesgo crediticio mediante técnicas de Machine Learning para estimar la probabilidad de incumplimiento de clientes, clasificarlos según su nivel de riesgo y cuantificar las pérdidas crediticias esperadas.



Se desarrolló un modelo XGBoost con calibración de probabilidades, selección de umbral basada en costos de clasificación y un análisis financiero utilizando los conceptos de PD, LGD y EAD.



\### 2. Objetivos



\- Identificar patrones asociados al incumplimiento crediticio.

\- Estimar la probabilidad de default (PD) de cada cliente.

\- Segmentar la cartera en cuatro niveles de riesgo.

\- Optimizar el umbral de clasificación considerando el costo de los errores.

\- Estimar las pérdidas crediticias esperadas.

\- Generar información útil para la toma de decisiones y la gestión de riesgos.



\### 3. Dataset



Se utilizó el conjunto de datos \*\*Default of Credit Card Clients\*\*, correspondiente a clientes de tarjetas de crédito de Taiwán.



\- 30,000 observaciones originales.

\- 27 variables predictoras después del preprocesamiento.

\- Variable objetivo: `DEFAULT`.

\- Clase 0: cliente que no incumple.

\- Clase 1: cliente que incumple.



Se realizó una división de entrenamiento, validación y prueba, conservando una distribución estratificada de la variable objetivo.



\### 4. Metodología



\*\*Análisis exploratorio y preprocesamiento\*\*

\- Análisis de distribuciones y valores atípicos.

\- Identificación de registros duplicados.

\- Análisis de correlaciones y relaciones entre variables.

\- Tratamiento de variables categóricas.

\- Preparación de los conjuntos de entrenamiento, validación y prueba.



\*\*Modelado predictivo\*\*

\- Entrenamiento de modelos de clasificación.

\- Optimización de hiperparámetros.

\- Implementación de XGBoost.

\- Calibración de probabilidades mediante `CalibratedClassifierCV` con método sigmoid.



\*\*Evaluación\*\*

\- Accuracy.

\- Precision.

\- Recall.

\- F1-score.

\- ROC-AUC.

\- Brier Score.

\- Log Loss.

\- Matriz de confusión.



\### 5. Resultados del modelo



El modelo final se evaluó sobre un conjunto de prueba de 6,000 observaciones.



| Métrica | Resultado |

|---|---:|

| Accuracy | 50.28% |

| Precision | 29.53% |

| Recall | 89.98% |

| F1-score | 44.46% |

| ROC-AUC | 0.7819 |

| Brier Score | 0.1352 |

| Log Loss | 0.4298 |



El modelo presenta una capacidad de discriminación razonable y prioriza la detección de clientes que pueden incumplir sus obligaciones crediticias.



\### 6. Optimización del umbral de decisión



Se seleccionó el umbral mediante el conjunto de validación, considerando un costo relativo de:



\- Falso positivo (FP): 1 unidad.

\- Falso negativo (FN): 10 unidades.



La función de costo utilizada fue:



`Costo = FP + 10 × FN`



El umbral seleccionado fue \*\*0.102\*\*.



En el conjunto de prueba se obtuvieron:



| Indicador | Resultado |

|---|---:|

| Verdaderos positivos (TP) | 1,194 |

| Verdaderos negativos (TN) | 1,823 |

| Falsos positivos (FP) | 2,850 |

| Falsos negativos (FN) | 133 |

| Recall | 89.98% |



Este umbral favorece la detección de incumplimientos, aunque genera un número elevado de falsos positivos. Por ello, una alerta de riesgo no debe interpretarse automáticamente como una decisión de rechazo crediticio.



\### 7. Segmentación de riesgo



Se establecieron cuatro categorías con base en la probabilidad estimada de incumplimiento:



| Nivel | Probabilidad de default |

|---|---|

| Bajo | Menor a 20% |

| Medio | 20% a menos de 40% |

| Alto | 40% a menos de 60% |

| Muy alto | 60% o más |



La distribución obtenida fue:



| Nivel | Clientes | Porcentaje |

|---|---:|---:|

| Bajo | 3,951 | 65.85% |

| Medio | 1,023 | 17.05% |

| Alto | 404 | 6.73% |

| Muy alto | 622 | 10.37% |



\### 8. Análisis financiero: pérdidas esperadas



Se estimaron las pérdidas crediticias esperadas utilizando:



\*\*Expected Credit Loss (ECL)\*\*



`EL = PD × LGD × EAD`



Donde:



\- \*\*PD:\*\* Probability of Default, probabilidad de incumplimiento.

\- \*\*LGD:\*\* Loss Given Default, porcentaje de pérdida en caso de incumplimiento.

\- \*\*EAD:\*\* Exposure at Default, exposición al momento del incumplimiento.



Para este ejercicio se utilizó una LGD del 45% y una aproximación de EAD basada en la información disponible.



\*\*Resultados de la cartera evaluada:\*\*



| Indicador | Resultado |

|---|---:|

| Clientes | 6,000 |

| Exposición total | 310,376,297 |

| Pérdida esperada | 29,200,992.33 |

| Pérdida esperada / Exposición | 9.41% |

| PD promedio | 22.12% |



\*\*Pérdida esperada por segmento:\*\*



| Nivel | Pérdida esperada | Participación |

|---|---:|---:|

| Bajo | 10,568,253.94 | 36.19% |

| Medio | 2,638,022.30 | 9.03% |

| Alto | 3,513,335.13 | 12.03% |

| Muy alto | 12,481,380.96 | 42.74% |



\### 9. Principales hallazgos



\- El segmento de riesgo muy alto representa el 10.37% de los clientes, pero concentra el 42.74% de la pérdida esperada.

\- Los segmentos alto y muy alto concentran conjuntamente el 54.77% de las pérdidas.

\- El segmento de riesgo bajo concentra el 36.19% de las pérdidas debido al volumen de exposición de sus clientes.

\- La probabilidad de incumplimiento no debe analizarse de manera aislada: la exposición crediticia también influye significativamente en la pérdida esperada.

\- La segmentación permite identificar grupos prioritarios para monitoreo y estrategias de mitigación.



\### 10. Dashboard



Se desarrolló un dashboard para visualizar:



\- Distribución de clientes por nivel de riesgo.

\- Exposición crediticia por segmento.

\- Pérdidas esperadas por nivel de riesgo.

\- Concentración acumulada de pérdidas mediante análisis Pareto.



!\[Dashboard de riesgo crediticio](images/dashboard\_riesgo\_final.png)



\### 11. Tecnologías utilizadas



\- Python

\- Pandas

\- NumPy

\- Matplotlib

\- Seaborn

\- Scikit-learn

\- XGBoost

\- Jupyter Notebook



\### 12. Limitaciones



\- Los resultados corresponden al conjunto de prueba y no representan necesariamente el comportamiento de toda una cartera bancaria.

\- La LGD del 45% es un supuesto ilustrativo, no una estimación empírica.

\- La EAD es una aproximación basada en las variables disponibles.

\- La función de costos utilizada para seleccionar el umbral es hipotética.

\- Las cantidades financieras conservan las unidades del dataset original; no deben interpretarse como pesos mexicanos.

\- Para una aplicación productiva sería necesario validar el modelo con datos adicionales, revisar la estabilidad temporal, optimizar la selección de hiperparámetros y evaluar posibles sesgos.



\### 13. Conclusión



Este proyecto integra análisis exploratorio, Machine Learning, calibración de probabilidades, optimización de umbrales y estimación de pérdidas crediticias esperadas.



El resultado es una herramienta analítica que permite transformar datos históricos de clientes en indicadores de riesgo y estimaciones financieras que pueden apoyar la toma de decisiones en instituciones financieras.



\---



\## 🇬🇧 English



\### 1. Project Overview



This project develops a credit risk analysis framework using Machine Learning techniques to estimate customers' probability of default, classify them into risk segments, and quantify expected credit losses.



An XGBoost model was developed alongside probability calibration, cost-sensitive threshold selection, and financial risk analysis using PD, LGD, and EAD.



\### 2. Project Objectives



\- Identify patterns associated with credit default.

\- Estimate each customer's Probability of Default (PD).

\- Segment customers into four risk categories.

\- Optimize the classification threshold based on error costs.

\- Estimate expected credit losses.

\- Generate actionable insights to support credit risk management.



\### 3. Dataset



The project uses the \*\*Default of Credit Card Clients\*\* dataset from Taiwan.



\- 30,000 original observations.

\- 27 predictor variables after preprocessing.

\- Target variable: `DEFAULT`.

\- Class 0: No default.

\- Class 1: Default.



The data was split into training, validation, and test sets using stratified sampling.



\### 4. Methodology



\*\*Exploratory Data Analysis and Preprocessing\*\*

\- Distribution and outlier analysis.

\- Duplicate record identification.

\- Correlation analysis.

\- Categorical variable treatment.

\- Dataset preparation.



\*\*Predictive Modeling\*\*

\- Classification model training.

\- Hyperparameter optimization.

\- XGBoost implementation.

\- Probability calibration using `CalibratedClassifierCV` with sigmoid calibration.



\*\*Model Evaluation\*\*

\- Accuracy.

\- Precision.

\- Recall.

\- F1-score.

\- ROC-AUC.

\- Brier Score.

\- Log Loss.

\- Confusion Matrix.



\### 5. Model Performance



The final model was evaluated on a test set of 6,000 observations.



| Metric | Result |

|---|---:|

| Accuracy | 50.28% |

| Precision | 29.53% |

| Recall | 89.98% |

| F1-score | 44.46% |

| ROC-AUC | 0.7819 |

| Brier Score | 0.1352 |

| Log Loss | 0.4298 |



The model prioritizes the detection of potential credit defaults, achieving a high recall at the expense of precision.



\### 6. Decision Threshold Optimization



The classification threshold was selected using the validation set and an illustrative cost function:



\- False Positive (FP): 1 cost unit.

\- False Negative (FN): 10 cost units.



`Total Cost = FP + 10 × FN`



The selected threshold was \*\*0.102\*\*.



Test set results:



| Indicator | Result |

|---|---:|

| True Positives | 1,194 |

| True Negatives | 1,823 |

| False Positives | 2,850 |

| False Negatives | 133 |

| Recall | 89.98% |



The selected threshold favors default detection, although it generates a considerable number of false positives.



\### 7. Risk Segmentation



Customers were classified into four categories based on their estimated probability of default:



| Risk Level | Probability of Default |

|---|---|

| Low | Below 20% |

| Medium | 20% to below 40% |

| High | 40% to below 60% |

| Very High | 60% or higher |



| Risk Level | Customers | Portfolio Share |

|---|---:|---:|

| Low | 3,951 | 65.85% |

| Medium | 1,023 | 17.05% |

| High | 404 | 6.73% |

| Very High | 622 | 10.37% |



\### 8. Financial Analysis: Expected Credit Loss



Expected Credit Loss (ECL) was estimated using:



`ECL = PD × LGD × EAD`



Where:



\- \*\*PD:\*\* Probability of Default.

\- \*\*LGD:\*\* Loss Given Default.

\- \*\*EAD:\*\* Exposure at Default.



An illustrative LGD assumption of 45% was used, while EAD was approximated using available dataset information.



\*\*Portfolio Results:\*\*



| Indicator | Result |

|---|---:|

| Customers | 6,000 |

| Total Exposure | 310,376,297 |

| Expected Credit Loss | 29,200,992.33 |

| ECL / Exposure | 9.41% |

| Average PD | 22.12% |



\### 9. Key Business Insights



\- The very-high-risk segment represents 10.37% of customers but accounts for 42.74% of expected credit losses.

\- High- and very-high-risk segments jointly account for 54.77% of expected losses.

\- The low-risk segment accounts for 36.19% of expected losses due to its larger exposure volume.

\- Credit risk assessment should consider both default probability and financial exposure.

\- Risk segmentation can help prioritize monitoring and credit risk mitigation strategies.



\### 10. Dashboard



The project includes a dashboard showing:



\- Customer distribution by risk level.

\- Credit exposure by risk segment.

\- Expected credit losses by risk level.

\- Cumulative loss concentration through Pareto analysis.



!\[Credit Risk Dashboard](images/dashboard\_riesgo\_final.png)



\### 11. Technologies



\- Python

\- Pandas

\- NumPy

\- Matplotlib

\- Seaborn

\- Scikit-learn

\- XGBoost

\- Jupyter Notebook



\### 12. Limitations



\- Results are based on the test dataset and may not represent an entire banking portfolio.

\- The 45% LGD is an illustrative assumption, not an empirically estimated value.

\- EAD is an approximation based on available variables.

\- The classification cost function is hypothetical.

\- Financial amounts retain the original dataset's units and should not be interpreted as Mexican pesos.

\- Production deployment would require additional validation, temporal stability testing, hyperparameter selection safeguards, and bias assessment.



\### 13. Conclusion



This project combines exploratory data analysis, Machine Learning, probability calibration, threshold optimization, and expected credit loss estimation.



It demonstrates how historical customer data can be transformed into credit risk indicators and financial estimates to support data-driven decision-making in financial institutions.



\---



\*\*Author:\*\* José Luis Serrano Ricardo  

\*\*Field:\*\* Mathematics, Statistics \& Data Analytics  

\*\*Project:\*\* Credit Risk Analysis

