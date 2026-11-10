# Credit Risk Analysis | Análisis de Riesgo Crediticio

**Machine Learning · Credit Risk Modeling · XGBoost · Python · Probability of Default**

<img width="1589" height="1082" alt="dashboard_riesgo_calibrado" src="https://github.com/user-attachments/assets/2de7aba7-911d-43ba-905d-7880a07f4bdd" />


---

# 🇪🇸 Español

## 1. Descripción del proyecto

Proyecto de análisis de riesgo crediticio mediante técnicas de análisis estadístico y Machine Learning, cuyo objetivo es estimar la probabilidad de incumplimiento de clientes, identificar los principales patrones asociados al default, segmentar la cartera según su nivel de riesgo y cuantificar las pérdidas crediticias esperadas.

El proyecto integra análisis exploratorio de datos, evaluación de variables demográficas y financieras, comparación de diferentes algoritmos de clasificación, calibración de probabilidades y análisis financiero mediante los conceptos de Probability of Default (PD), Loss Given Default (LGD) y Exposure at Default (EAD).

Se desarrolló un proceso progresivo de modelado, comenzando con regresión logística, continuando con Random Forest y finalizando con XGBoost calibrado.

## 2. Objetivos

- Identificar patrones demográficos, financieros y de comportamiento de pago asociados al incumplimiento crediticio.
- Analizar la relación entre variables como edad, sexo, educación, estado civil, historial de pagos y exposición crediticia con la probabilidad de default.
- Comparar diferentes algoritmos de clasificación.
- Estimar la probabilidad de incumplimiento (PD) de cada cliente.
- Calibrar las probabilidades para obtener estimaciones más representativas del riesgo.
- Optimizar el umbral de clasificación considerando los costos de los errores.
- Segmentar la cartera en diferentes niveles de riesgo.
- Estimar las pérdidas crediticias esperadas y generar indicadores financieros para apoyar la toma de decisiones.

## 3. Dataset

Se utilizó el conjunto de datos **Default of Credit Card Clients**, correspondiente a clientes de tarjetas de crédito de Taiwán.

Características principales:

- 30,000 observaciones originales.
- 27 variables predictoras después del preprocesamiento.
- Variable objetivo: `DEFAULT`.
- Clase 0: cliente que no incumple.
- Clase 1: cliente que incumple.

El conjunto contiene información demográfica, características del crédito, historial de pagos, montos facturados y pagos realizados.

### Variables analizadas

| Categoría | Variables | Descripción |
|---|---|---|
| Demográficas | `AGE`, `SEX`, `EDUCATION`, `MARRIAGE` | Edad, sexo, educación y estado civil |
| Crédito | `LIMIT_BAL` | Límite de crédito |
| Historial de pagos | `PAY_0` a `PAY_6` | Comportamiento de pago y retrasos |
| Facturación | `BILL_AMT1` a `BILL_AMT6` | Montos facturados |
| Pagos realizados | `PAY_AMT1` a `PAY_AMT6` | Montos pagados |

## 4. Análisis exploratorio de datos (EDA)

Se realizó un análisis exploratorio para comprender la estructura de la cartera, identificar patrones de incumplimiento y evaluar la relación entre las variables predictoras y la variable objetivo.

### 4.1 Análisis demográfico

Se analizaron las tasas de incumplimiento según:

- Edad de los clientes.
- Sexo.
- Nivel educativo.
- Estado civil.

Se calcularon tasas de incumplimiento por grupos y se compararon las distribuciones de las variables entre clientes que incumplen y aquellos que cumplen sus obligaciones.

### 4.2 Análisis financiero y comportamiento de pago

Se estudió la relación entre el incumplimiento y:

- Límite de crédito (`LIMIT_BAL`).
- Historial de retrasos en pagos (`PAY_0` a `PAY_6`).
- Montos facturados (`BILL_AMT1` a `BILL_AMT6`).
- Montos pagados (`PAY_AMT1` a `PAY_AMT6`).

También se analizaron distribuciones, valores atípicos, correlaciones y tasas de incumplimiento por categorías de variables relevantes.

### 4.3 Principales enfoques del análisis

El análisis permitió estudiar cómo las características demográficas, la exposición crediticia y, especialmente, el historial de pagos se relacionan con el comportamiento de incumplimiento.

Estas relaciones se interpretaron como asociaciones estadísticas y no como relaciones causales.

## 5. Preprocesamiento de datos

Se realizaron las siguientes actividades:

- Revisión de valores faltantes.
- Identificación de registros duplicados.
- Análisis y tratamiento de valores atípicos.
- Revisión de categorías y codificación de variables.
- Selección de variables predictoras.
- División de los datos en entrenamiento, validación y prueba.
- Muestreo estratificado para conservar la proporción de incumplimientos.

La división inicial contempló 24,000 observaciones para entrenamiento y 6,000 para prueba. Posteriormente, el conjunto de entrenamiento se subdividió para realizar la selección del umbral mediante validación.

## 6. Desarrollo y comparación de modelos

Se siguió un proceso progresivo para evaluar diferentes algoritmos de clasificación y mejorar la estimación del riesgo crediticio.

### 6.1 Regresión logística

Se comenzó con un modelo de regresión logística como línea base (*baseline*).

Este modelo permitió establecer una primera aproximación a la clasificación de clientes y estudiar la relación entre las variables predictoras y la probabilidad de incumplimiento.

Su implementación proporcionó un punto de referencia para comparar modelos de mayor complejidad.

### 6.2 Random Forest

Posteriormente, se implementó Random Forest, un algoritmo de aprendizaje basado en conjuntos de árboles de decisión.

Se utilizó para explorar relaciones no lineales entre las variables, capturar interacciones y comparar su capacidad predictiva frente al modelo inicial.

### 6.3 XGBoost

Finalmente, se trabajó con XGBoost, un algoritmo de Gradient Boosting basado en árboles de decisión.

Se realizó optimización de hiperparámetros para mejorar el desempeño predictivo y obtener una mejor aproximación a la probabilidad de incumplimiento.

### 6.4 Calibración de probabilidades

Debido a que el objetivo del proyecto no era únicamente clasificar clientes, sino estimar probabilidades de incumplimiento utilizables en el análisis financiero, se incorporó una etapa de calibración.

Se utilizó:

`CalibratedClassifierCV(method='sigmoid', cv=5)`

La calibración sigmoid permitió ajustar las probabilidades estimadas por el modelo para mejorar su correspondencia con las frecuencias observadas de incumplimiento.

**Modelo final:** XGBoost calibrado.

## 7. Evaluación del modelo final

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

El Recall de 89.98% indica que el modelo identifica aproximadamente nueve de cada diez incumplimientos reales. Sin embargo, la precisión de 29.53% refleja que existe una cantidad considerable de falsos positivos.

## 8. Optimización del umbral de decisión

En problemas de riesgo crediticio, el umbral convencional de 0.50 no necesariamente representa la mejor decisión de negocio.

Por ello, se evaluaron diferentes umbrales utilizando el conjunto de validación y una función de costos ilustrativa:

- Falso positivo (FP): 1 unidad de costo.
- Falso negativo (FN): 10 unidades de costo.

La función utilizada fue:

`Costo_Total = FP + 10 × FN`

El umbral que minimizó el costo dentro del rango evaluado fue:

**Umbral seleccionado: 0.102**

La evaluación final en el conjunto de prueba produjo:

| Indicador | Resultado |
|---|---:|
| Verdaderos positivos (TP) | 1,194 |
| Verdaderos negativos (TN) | 1,823 |
| Falsos positivos (FP) | 2,850 |
| Falsos negativos (FN) | 133 |
| Recall | 89.98% |

La selección de este umbral favorece la detección de incumplimientos, reduciendo los falsos negativos a costa de incrementar los falsos positivos.

Una clasificación de riesgo no debe interpretarse automáticamente como una decisión de rechazo crediticio: en un entorno real se requerirían políticas adicionales de evaluación y autorización.

## 9. Segmentación de riesgo

A partir de las probabilidades de incumplimiento estimadas por el modelo final, se establecieron cuatro categorías:

| Nivel de riesgo | Probabilidad de default |
|---|---|
| Bajo | Menor a 20% |
| Medio | 20% a menos de 40% |
| Alto | 40% a menos de 60% |
| Muy alto | 60% o más |

Distribución de los clientes en el conjunto de prueba:

| Nivel | Clientes | Porcentaje |
|---|---:|---:|
| Bajo | 3,951 | 65.85% |
| Medio | 1,023 | 17.05% |
| Alto | 404 | 6.73% |
| Muy alto | 622 | 10.37% |
| **Total** | **6,000** | **100%** |

Esta segmentación permite diferenciar grupos de clientes según su probabilidad estimada de incumplimiento y facilita la priorización de estrategias de seguimiento y gestión de cartera.

## 10. Análisis financiero: pérdidas esperadas

Se estimaron las pérdidas crediticias esperadas utilizando la metodología:

**Expected Credit Loss (ECL)**

`EL = PD × LGD × EAD`

Donde:

- **PD (Probability of Default):** probabilidad de incumplimiento.
- **LGD (Loss Given Default):** porcentaje de exposición que se perdería en caso de incumplimiento.
- **EAD (Exposure at Default):** exposición crediticia al momento del incumplimiento.

Para este ejercicio se utilizó una LGD del 45% y una aproximación de EAD basada en la información disponible.

### 10.1 Resultados generales

| Indicador | Resultado |
|---|---:|
| Clientes evaluados | 6,000 |
| Exposición total (EAD) | 310,376,297 |
| Pérdida esperada (EL) | 29,200,992.33 |
| Pérdida esperada / Exposición | 9.41% |
| PD promedio | 22.12% |

### 10.2 Pérdida esperada por segmento

| Nivel de riesgo | Pérdida esperada | Participación |
|---|---:|---:|
| Bajo | 10,568,253.94 | 36.19% |
| Medio | 2,638,022.30 | 9.03% |
| Alto | 3,513,335.13 | 12.03% |
| Muy alto | 12,481,380.96 | 42.74% |
| **Total** | **29,200,992.33** | **100%** |

## 11. Principales hallazgos de negocio

- El segmento de riesgo muy alto representa el 10.37% de los clientes, pero concentra el 42.74% de la pérdida esperada.
- Los segmentos alto y muy alto representan conjuntamente el 17.10% de los clientes y concentran el 54.77% de las pérdidas.
- El segmento de riesgo bajo concentra el 36.19% de las pérdidas debido al volumen de exposición de sus clientes.
- La probabilidad de incumplimiento no debe analizarse de manera aislada: la exposición crediticia también influye significativamente en la pérdida esperada.
- El análisis demográfico y financiero permite explorar qué características están asociadas con un mayor incumplimiento.
- La segmentación de riesgo permite identificar grupos prioritarios para monitoreo y estrategias de mitigación.

## 12. Dashboard

Se desarrolló un dashboard para visualizar los principales indicadores de la cartera:

- Distribución de clientes por nivel de riesgo.
- Exposición crediticia por segmento.
- Pérdidas esperadas por nivel de riesgo.
- Concentración acumulada de pérdidas mediante análisis Pareto.

![Dashboard de riesgo crediticio](images/dashboard_riesgo_final.png)

## 13. Tecnologías utilizadas

- **Lenguaje:** Python.
- **Análisis y manipulación de datos:** Pandas, NumPy.
- **Visualización:** Matplotlib, Seaborn.
- **Machine Learning:** Scikit-learn.
- **Modelos:** Regresión logística, Random Forest y XGBoost.
- **Calibración:** CalibratedClassifierCV.
- **Entorno de desarrollo:** Jupyter Notebook.

## 14. Limitaciones

- Los resultados corresponden al conjunto de prueba y no representan necesariamente el comportamiento de toda una cartera bancaria.
- La LGD del 45% es un supuesto ilustrativo, no una estimación empírica.
- La EAD es una aproximación basada en las variables disponibles.
- La función de costos utilizada para seleccionar el umbral es hipotética.
- Las cantidades financieras conservan las unidades del dataset original; no deben interpretarse como pesos mexicanos.
- Las relaciones identificadas entre variables demográficas y default son asociaciones estadísticas, no evidencia de causalidad.
- Para una aplicación productiva sería necesario validar el modelo con datos adicionales, revisar la estabilidad temporal, reforzar la independencia entre selección de hiperparámetros y validación, y evaluar posibles sesgos.

## 15. Conclusión

Este proyecto integra análisis exploratorio de datos, estadística aplicada, comparación de algoritmos de Machine Learning, calibración de probabilidades, optimización de umbrales y estimación de pérdidas crediticias esperadas.

El proceso permitió pasar de un modelo inicial de regresión logística a modelos más complejos como Random Forest y XGBoost, incorporando finalmente una etapa de calibración para obtener probabilidades más útiles en la evaluación financiera del riesgo.

El resultado es una herramienta analítica que transforma datos históricos de clientes en indicadores de riesgo y estimaciones financieras que pueden apoyar la toma de decisiones en instituciones financieras.

---

# 🇬🇧 English

## 1. Project Overview

This project develops a credit risk analysis framework using statistical analysis and Machine Learning techniques to estimate customers' probability of default, identify patterns associated with credit default, segment customers by risk level, and quantify expected credit losses.

The project combines exploratory data analysis, demographic and financial variable analysis, model comparison, probability calibration, and financial risk assessment using Probability of Default (PD), Loss Given Default (LGD), and Exposure at Default (EAD).

A progressive modeling approach was followed, starting with Logistic Regression, moving to Random Forest, and finally developing a calibrated XGBoost model.

## 2. Project Objectives

- Identify demographic, financial, and payment behavior patterns associated with credit default.
- Analyze the relationship between variables such as age, sex, education, marital status, payment history, and credit exposure and the probability of default.
- Compare different classification algorithms.
- Estimate each customer's Probability of Default (PD).
- Calibrate predicted probabilities to improve their reliability.
- Optimize the classification threshold based on error costs.
- Segment customers into different risk categories.
- Estimate expected credit losses and generate financial indicators to support decision-making.

## 3. Dataset

The project uses the **Default of Credit Card Clients** dataset, which contains information about credit card customers in Taiwan.

- 30,000 original observations.
- 27 predictor variables after preprocessing.
- Target variable: `DEFAULT`.
- Class 0: No default.
- Class 1: Default.

The dataset includes demographic information, credit characteristics, payment history, bill amounts, and previous payment amounts.

### Analyzed Variables

| Category | Variables | Description |
|---|---|---|
| Demographic | `AGE`, `SEX`, `EDUCATION`, `MARRIAGE` | Age, sex, education, and marital status |
| Credit | `LIMIT_BAL` | Credit limit |
| Payment history | `PAY_0` to `PAY_6` | Payment behavior and delays |
| Billing | `BILL_AMT1` to `BILL_AMT6` | Bill amounts |
| Payments | `PAY_AMT1` to `PAY_AMT6` | Previous payment amounts |

## 4. Exploratory Data Analysis (EDA)

An exploratory analysis was conducted to understand the portfolio structure, identify default patterns, and evaluate the relationship between predictor variables and the target variable.

### 4.1 Demographic Analysis

Default rates were analyzed across:

- Customer age.
- Sex.
- Education level.
- Marital status.

Default rates were calculated across different groups, and variable distributions were compared between customers who defaulted and those who did not.

### 4.2 Financial and Payment Behavior Analysis

The relationship between default and the following variables was explored:

- Credit limit (`LIMIT_BAL`).
- Payment delay history (`PAY_0` to `PAY_6`).
- Bill amounts (`BILL_AMT1` to `BILL_AMT6`).
- Previous payment amounts (`PAY_AMT1` to `PAY_AMT6`).

The analysis also included distributions, outliers, correlations, and default rates across relevant variable categories.

### 4.3 Main Analytical Focus

The analysis explored how demographic characteristics, credit exposure, and particularly payment history relate to default behavior.

These findings were interpreted as statistical associations rather than causal relationships.

## 5. Data Preprocessing

The following activities were performed:

- Missing value inspection.
- Duplicate record identification.
- Outlier analysis and treatment.
- Categorical variable review and encoding.
- Predictor variable selection.
- Training, validation, and test data splitting.
- Stratified sampling to preserve the target class distribution.

The initial split consisted of 24,000 training observations and 6,000 test observations. The training set was subsequently divided to perform threshold selection using validation data.

## 6. Model Development and Comparison

A progressive modeling approach was used to evaluate different classification algorithms and improve credit default probability estimation.

### 6.1 Logistic Regression

Logistic Regression was implemented as the initial baseline model.

It provided a first approach to customer classification and helped establish a reference point for evaluating more complex models.

### 6.2 Random Forest

Random Forest was subsequently implemented as an ensemble learning algorithm based on decision trees.

It was used to explore nonlinear relationships and interactions between predictor variables and compare its predictive capabilities against the baseline model.

### 6.3 XGBoost

Finally, XGBoost was implemented using gradient boosting decision trees.

Hyperparameter optimization was performed to improve predictive performance and obtain more accurate default probability estimates.

### 6.4 Probability Calibration

Since the project's objective was not limited to customer classification but also involved estimating probabilities for financial risk analysis, a probability calibration stage was incorporated.

The following method was used:

`CalibratedClassifierCV(method='sigmoid', cv=5)`

Sigmoid calibration was applied to adjust the model's predicted probabilities and improve their alignment with observed default frequencies.

**Final model:** Calibrated XGBoost.

## 7. Final Model Evaluation

The final model was evaluated on a test set containing 6,000 observations.

| Metric | Result |
|---|---:|
| Accuracy | 50.28% |
| Precision | 29.53% |
| Recall | 89.98% |
| F1-score | 44.46% |
| ROC-AUC | 0.7819 |
| Brier Score | 0.1352 |
| Log Loss | 0.4298 |

The model achieves reasonable discrimination and prioritizes the detection of customers who may default on their credit obligations.

The 89.98% Recall indicates that the model identifies approximately nine out of ten actual defaults. However, the 29.53% Precision reflects a considerable number of false positives.

## 8. Decision Threshold Optimization

In credit risk problems, the conventional 0.50 threshold does not necessarily represent the optimal business decision.

Therefore, different thresholds were evaluated using the validation set and an illustrative cost function:

- False Positive (FP): 1 cost unit.
- False Negative (FN): 10 cost units.

The cost function was:

`Total Cost = FP + 10 × FN`

The selected threshold was:

**0.102**

The final evaluation on the test set produced:

| Indicator | Result |
|---|---:|
| True Positives (TP) | 1,194 |
| True Negatives (TN) | 1,823 |
| False Positives (FP) | 2,850 |
| False Negatives (FN) | 133 |
| Recall | 89.98% |

This threshold prioritizes default detection by reducing false negatives at the expense of increasing false positives.

A risk classification should not automatically be interpreted as a credit rejection decision. Real-world credit approval requires additional underwriting and policy considerations.

## 9. Risk Segmentation

Customers were classified into four categories based on their estimated probability of default:

| Risk Level | Probability of Default |
|---|---|
| Low | Below 20% |
| Medium | 20% to below 40% |
| High | 40% to below 60% |
| Very High | 60% or higher |

Test set distribution:

| Risk Level | Customers | Portfolio Share |
|---|---:|---:|
| Low | 3,951 | 65.85% |
| Medium | 1,023 | 17.05% |
| High | 404 | 6.73% |
| Very High | 622 | 10.37% |
| **Total** | **6,000** | **100%** |

This segmentation helps distinguish customers according to their estimated default probability and supports portfolio monitoring and risk mitigation strategies.

## 10. Financial Analysis: Expected Credit Loss

Expected credit losses were estimated using:

**Expected Credit Loss (ECL)**

`ECL = PD × LGD × EAD`

Where:

- **PD (Probability of Default):** Probability that a customer will default.
- **LGD (Loss Given Default):** Percentage of exposure expected to be lost in the event of default.
- **EAD (Exposure at Default):** Credit exposure at the time of default.

An illustrative LGD assumption of 45% was used, while EAD was approximated using available dataset information.

### 10.1 Overall Results

| Indicator | Result |
|---|---:|
| Customers evaluated | 6,000 |
| Total Exposure (EAD) | 310,376,297 |
| Expected Credit Loss (ECL) | 29,200,992.33 |
| ECL / Exposure | 9.41% |
| Average PD | 22.12% |

### 10.2 Expected Loss by Risk Segment

| Risk Level | Expected Loss | Share |
|---|---:|---:|
| Low | 10,568,253.94 | 36.19% |
| Medium | 2,638,022.30 | 9.03% |
| High | 3,513,335.13 | 12.03% |
| Very High | 12,481,380.96 | 42.74% |
| **Total** | **29,200,992.33** | **100%** |

## 11. Key Business Insights

- The very-high-risk segment represents 10.37% of customers but accounts for 42.74% of expected credit losses.
- High- and very-high-risk segments jointly represent 17.10% of customers and account for 54.77% of expected losses.
- The low-risk segment accounts for 36.19% of expected losses due to its larger credit exposure.
- Credit risk assessment should consider both default probability and financial exposure.
- Demographic and financial analysis helps explore which characteristics are associated with higher default rates.
- Risk segmentation supports the identification of priority groups for monitoring and mitigation strategies.

## 12. Dashboard

A dashboard was developed to visualize the main portfolio indicators:

- Customer distribution by risk level.
- Credit exposure by risk segment.
- Expected credit losses by risk level.
- Cumulative loss concentration through Pareto analysis.

![Credit Risk Dashboard](images/dashboard_riesgo_final.png)

## 13. Technologies Used

- **Programming Language:** Python.
- **Data Analysis:** Pandas, NumPy.
- **Data Visualization:** Matplotlib, Seaborn.
- **Machine Learning:** Scikit-learn.
- **Models:** Logistic Regression, Random Forest, and XGBoost.
- **Probability Calibration:** CalibratedClassifierCV.
- **Development Environment:** Jupyter Notebook.

## 14. Limitations

- Results are based on the test dataset and may not represent an entire banking portfolio.
- The 45% LGD is an illustrative assumption, not an empirically estimated value.
- EAD is an approximation based on available variables.
- The classification cost function is hypothetical.
- Financial amounts retain the original dataset's units and should not be interpreted as Mexican pesos.
- Relationships between demographic variables and default are statistical associations, not evidence of causality.
- Production deployment would require additional validation, temporal stability testing, stronger safeguards against information leakage during model selection, and bias assessment.

## 15. Conclusion

This project combines exploratory data analysis, applied statistics, Machine Learning model comparison, probability calibration, threshold optimization, and expected credit loss estimation.

The modeling process progressed from an initial Logistic Regression baseline to more complex algorithms such as Random Forest and XGBoost, finally incorporating probability calibration to obtain estimates more suitable for financial risk analysis.

The result is an analytical framework that transforms historical customer data into credit risk indicators and financial estimates to support data-driven decision-making in financial institutions.

---

**Author:** José Luis Serrano Ricardo  
**Field:** Mathematics, Statistics & Data Analytics  
**Project:** Credit Risk Analysis
