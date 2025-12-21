# 📊 Análisis de Fraude de tarjetas de crédito con Power BI
🧠 Descripción general

Este proyecto presenta un dashboard de análisis de fraude con tarjetas de crédito, desarrollado solamente en Power BI, con el objetivo de identificar patrones de comportamiento fraudulento, medir su impacto económico y facilitar la toma de decisiones basada en datos.

El análisis se construyó a partir de un dataset transaccional (Kaggle) y abarca todo el ciclo típico del trabajo de un Analista de Datos: exploración, limpieza, modelado, creación de métricas, visualización y storytelling.

🎯 Objetivos del proyecto

Identificar patrones de fraude en transacciones con tarjeta.

Analizar la tasa de fraude y su evolución según distintas variables.

Evaluar el impacto económico del fraude.

Segmentar transacciones por niveles de riesgo.

Construir un dashboard claro, accionable y orientado a negocio.

🗂️ Dataset

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

🔧 Proceso de análisis
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

3️⃣ Segmentación de riesgo

Se construyó una clasificación de riesgo combinando variables clave:

Transacción internacional

Discrepancia de ubicación

Velocidad de transacciones en las últimas 24 hs

Niveles definidos:

Normal

Riesgo Bajo

Riesgo Medio

Alta Sospecha

📈 Dashboard – Principales visualizaciones

El dashboard incluye:

KPIs principales:

Cantidad de fraudes

Monto total de fraudes

Porcentaje de fraude

Análisis descriptivo:

Fraudes por rango de monto

Fraudes por categoría comercial

Fraudes por hora del día

Análisis de comportamiento:

Fraudes por velocidad de transacciones (últimas 24 hs)

Fraudes por discrepancia de ubicación

Fraudes por tipo de transacción

Fraudes por puntuación de confianza del dispositivo

Análisis por riesgo:

Cantidad de fraudes según nivel de riesgo

Monto total involucrado por nivel de riesgo

💡 Insights destacados

Una gran proporción de fraudes se concentra en montos bajos y medios, lo que sugiere intentos de pasar desapercibidos.

Determinadas categorías comerciales presentan mayor tasa de fraude relativa pero son muy parejas y las diferencias porcentuales son mínimas.

Existen horarios con picos claros de actividad fraudulenta.

La combinación de múltiples señales de riesgo mejora significativamente la detección.

🛠️ Herramientas utilizadas

Power BI

DAX

Power Query

Google sheets (exploración inicial)

🎯 Perfil profesional

Este proyecto refleja habilidades propias de un Analista de Datos:

Pensamiento analítico

Enfoque orientado a negocio

Capacidad de transformar datos en insights

Construcción de dashboards claros y accionables

📌 Notas finales

Este dashboard fue diseñado como pieza de portfolio profesional, simulando un caso real de análisis en una empresa del sector financiero.
