# 📊 Análisis de Fraude de tarjetas de crédito con Power BI

Dashboard interactivo desarrollado en Power BI para analizar el comportamiento del fraude en transacciones con tarjeta de crédito, identificar patrones de riesgo, medir su impacto económico y facilitar la toma de decisiones basada en datos.

El análisis se enfoca en cuánto fraude existe, cuándo ocurre, dónde se concentra y bajo qué condiciones, utilizando métricas claras y visualizaciones orientadas al negocio.

<img width="1472" height="806" alt="image" src="https://github.com/user-attachments/assets/ef8d506d-9857-4217-9964-a042f0812a30" />


## 📌 Objetivo del proyecto

El objetivo del proyecto es analizar y caracterizar el fraude en transacciones con tarjeta de crédito, identificando patrones relevantes según el monto, el momento de la transacción, la ubicación, el tipo de operación y el nivel de riesgo asociado.

A través del uso de métricas clave y visualizaciones interactivas, el dashboard permite:

Medir la tasa de fraude y su impacto económico.

Detectar segmentos de mayor riesgo.

Analizar el comportamiento del fraude en distintas dimensiones temporales y operativas.

Facilitar la detección temprana y el análisis exploratorio para la toma de decisiones.

El enfoque del proyecto es analítico y descriptivo, orientado a convertir datos transaccionales en insights accionables.

El análisis se construyó a partir de un dataset transaccional (Kaggle) y abarca todo el ciclo típico del trabajo de un Analista de Datos: exploración, limpieza, modelado, creación de métricas, visualización y storytelling.

https://www.kaggle.com/datasets/miadul/credit-card-fraud-detection-dataset

## 🧠 Preguntas clave que responde el dashboard

El dashboard fue diseñado para responder, entre otras, las siguientes preguntas:

¿Cuál es la cantidad total de transacciones fraudulentas y cuál es su impacto económico?

¿Qué porcentaje del total de transacciones corresponde a fraude?

¿En qué rangos de monto se concentran la mayor cantidad de fraudes?

¿Cómo se distribuyen los fraudes según la velocidad de transacciones en las últimas 24 horas?

¿Existen horarios del día con mayor incidencia de fraude?

¿Qué categorías de comercio presentan mayor cantidad de fraudes y mayor tasa relativa?

¿Cómo varía el fraude según la ubicación de la transacción?

¿Qué relación existe entre la puntuación de confianza del dispositivo y la ocurrencia de fraude?

¿Cómo se distribuyen los fraudes según los niveles de riesgo definidos?

¿Qué patrones permiten identificar comportamientos potencialmente sospechosos?

Estas preguntas estructuran el diseño visual del dashboard y guían el análisis exploratorio de los datos.

## 🗂️ Dataset utilizado

Origen: Kaggle – Credit Card Fraud Detection Dataset

Tipo de datos: transaccionales

Volumen: miles de registros

Variables analizadas:

is_fraud

amount

transaction_hour

merchant_category

foreign_transaction

location_mismatch

velocity_last_24h

device_trust_score

A partir de estos datos se agregó la columna "risk_categories" que categoriza las transacciones mediante una fórmula SWITCH en la cual según ciertos parámetros, se dividen las categorías de riesgo en "Normal", "Riesgo Bajo", "Riesgo Medio" y "Riesgo Alto"; y se calcularon las siguientes métricas que fueron ingresadas en una tabla aparte para una mejor práctica:

Amount frauds

Amount legitimate transactions

Average fraud ticket

Average legitimate ticket

F1 Score

False negative

False positive

Fraud percentage

Precision

Recall

Total frauds

Total legitimate transactions

Total transactions

True negatives

True positive

El volumen y la granularidad del dataset permiten realizar análisis:

comparativos

estructurales

exploratorios

## 🔧 Proceso de análisis

1️⃣ Limpieza y preparación de datos

Corrección de tipos de datos (fechas, numéricos y categóricos).

Eliminación de valores inconsistentes.

Creación de columnas calculadas.

Validación de integridad de los datos.

2️⃣ Modelado y métricas (DAX)

Creación de medidas clave:

Cantidad total de fraudes

Monto total fraudulento

Porcentaje de fraude sobre el total de transacciones

Métricas segmentadas por categoría, hora, tipo de transacción, riesgo, tipo de dispositivo y comportamiento

Uso de funciones DAX como:

CALCULATE

DIVIDE

COUNT

SUM

IF

SWITCH

FILTER

3️⃣ ## 🧮 Sistema de Scoring de Riesgo

Para clasificar las transacciones según su nivel de riesgo, se diseñó un **sistema de scoring aditivo** que asigna puntos según señales de fraude conocidas:

### Variables y pesos utilizados:

| Variable | Condición | Puntos |
|----------|-----------|--------|
| **Transacción internacional** | foreign_transaction = 1 | +30 |
| **Discrepancia de ubicación** | location_mismatch = 1 | +20 |
| **Velocidad alta** | velocity_last_24h ≥ 5 | +30 |
| **Velocidad media** | velocity_last_24h ≥ 3 | +15 |
| **Velocidad baja** | velocity_last_24h ≥ 2 | +5 |
| **Dispositivo sospechoso** | device_trust_score ≤ 30 | +30 |
| **Dispositivo de riesgo** | device_trust_score ≤ 45 | +20 |
| **Dispositivo no confiable** | device_trust_score ≤ 60 | +5 |
| **Monto elevado** | amount > $30,000 | +10 |

### Categorización por umbrales:

- **Alta sospecha** (≥85 puntos): Múltiples señales fuertes → Revisión inmediata
- **Riesgo Alto** (≥70 puntos): 2-3 señales importantes → Revisión prioritaria
- **Riesgo Medio** (≥55 puntos): 1-2 señales moderadas → Monitoreo
- **Riesgo Bajo** (≥40 puntos): Señal débil → Seguimiento rutinario
- **Normal** (<40 puntos): Sin señales de alerta

### Resultados del modelo:

| Categoría | Transacciones | Fraudes | Tasa de fraude | Acción |
|-----------|---------------|---------|----------------|--------|
| Alta sospecha | 23 | 14 | **60.9%** | 🔴 Bloqueo/Revisión |
| Riesgo Alto | 87 | 47 | **54.0%** | 🟠 Revisión manual |
| Riesgo Medio | 388 | 51 | **13.1%** | 🟡 Monitoreo |
| Riesgo Bajo | 928 | 33 | **3.6%** | 🟢 Seguimiento |
| Normal | 8,249 | 3 | **0.04%** | ✅ Aprobado |

**Métricas de rendimiento:**
- **Precision: 22.5%** → De cada 100 alertas, 22 son fraudes reales
- **Recall: 75.7%** → Se detecta el 76% de los fraudes
- **F1 Score: 34.7%** → Balance razonable entre precisión y cobertura

Este enfoque permite **reducir en 94% el volumen de transacciones a revisar manualmente** (de 9,675 a 498), manteniendo una tasa de detección del 76%.

## 🛠️ Herramientas utilizadas

Power BI

DAX

Power Query

Google sheets (exploración inicial)

## 📈 Dashboard – Principales visualizaciones

🔑 KPIs principales

En la parte superior del dashboard se presentan los indicadores clave:

Cantidad total de fraudes

Monto total asociado a transacciones fraudulentas

Porcentaje de fraudes sobre el total de transacciones

👉 Estos KPIs permiten obtener una visión inmediata de la magnitud y el impacto económico del fraude, y funcionan como referencia para interpretar el resto de las visualizaciones.

📈 Análisis descriptivo del fraude

Estas visualizaciones permiten comprender cómo se distribuye el fraude según distintas dimensiones operativas:

Fraudes por rangos de monto
Permite identificar si el fraude se concentra en montos bajos, medios o altos.

Fraudes por categoría comercial
Analiza qué tipos de comercios presentan mayor cantidad de fraudes y su peso relativo.

Fraudes por hora del día
Permite detectar patrones temporales y posibles horarios de mayor riesgo.

Este bloque responde principalmente a la pregunta:
👉 ¿Cómo se distribuye el fraude en términos generales?

🧠 Análisis de comportamiento y riesgo

Este bloque profundiza en patrones asociados al comportamiento transaccional y señales de riesgo:

Fraudes por velocidad de transacciones (últimas 24 hs)
Analiza la relación entre la frecuencia de transacciones y la ocurrencia de fraude.

Fraudes por discrepancia de ubicación
Permite identificar comportamientos sospechosos vinculados al desajuste entre la facturación y la ubicación de la transacción

Fraudes por tipo de transacción
Evalúa si incidencia de fraude si la transacción es internacional o no.

Fraudes según nivel de riesgo
Muestra cómo se distribuyen las transacciones fraudulentas entre los distintos niveles de riesgo definidos.

👉 Este conjunto de visualizaciones permite detectar patrones potencialmente anómalos y segmentar transacciones según su nivel de exposición al fraude.

## 🎯 Decisiones de diseño

Se priorizó el uso de gráficos claros y comparables, evitando sobrecargar el dashboard.

El uso de colores consistentes facilita la interpretación rápida de los datos.

La disposición visual permite un análisis progresivo:
contexto → distribución → comportamiento → riesgo.

El dashboard fue pensado para ser explorable, permitiendo al usuario filtrar y analizar distintos escenarios sin perder contexto.

## 🚀 Conclusiones principales

Una gran proporción de fraudes se concentra en montos bajos y medios, lo que sugiere intentos de pasar desapercibidos. Es muy importante tener en cuenta que casi el 40% de los fraudes (59 sobre 148 fraudes en total) se dan en montos inferiores a $5884

La categoría comercial de "Grosery" presenta mayor tasa de fraude con un 2,01%. Entre "Food" y "Grosery" se concentran un 49,3% del total de casos de fraudes

Los horarios donde se presentan picos claros de actividad fraudulenta son entre las 00 hs y las 03 hs acumulando el 86,48% del total de fraudes.

La combinación de múltiples señales de riesgo como el tipo de transacción, la ubicación, la velocidad el puntaje del dispositivo y el monto de la operación, mejora significativamente la detección de fraudes.
Debido a las limitaciones del análisis, hay variables no consideradas que ayudarían a una mejor precisión del modelo como historial del cliente, patrón de gasto habitual o ubicación geográfica
Los pesos asignados en el sistema de scoring fueron definidos analíticamente. En un contexto real, deberían ajustarse con:
   - Machine Learning (modelos supervisados)
   - Feedback del equipo de prevención de fraude
   - Análisis de costos de falsos positivos vs falsos negativos

📌 Notas finales

Este dashboard fue diseñado como pieza de portfolio profesional, simulando un caso real de análisis en una empresa del sector financiero.
