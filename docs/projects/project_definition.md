


# Proyecto Final

## Introducción

El propósito de este proyecto es introducir a los estudiantes en el análisis y predicción de **series de tiempo multivariadas**, trabajando con uno de los desafíos más emblemáticos de Kaggle: el M5 Forecasting - Accuracy. Este proyecto combina técnicas de preprocesamiento, análisis exploratorio, visualización, selección de variables y modelamiento de datos temporales.

## Descripción del Proyecto

El desafío M5 Forecasting se basa en datos reales de ventas minoristas de Walmart. El objetivo es **predecir la demanda diaria de productos** en distintos estados y tiendas durante un período determinado. Este tipo de pronóstico es fundamental para la planificación logística, el manejo de inventario y la toma de decisiones comerciales.

Los estudiantes deberán construir modelos predictivos que logren estimar la demanda futura basándose en patrones históricos, variables categóricas y exógenas como precios o eventos especiales.

> Dataset oficial: [M5 Forecasting - Accuracy](https://www.kaggle.com/competitions/m5-forecasting-accuracy)

## Evaluación

El proyecto consta de dos componentes principales:

* **Parte Técnica**: Desarrollo completo en Jupyter Notebook.
* **Presentación Final**: Exposición de resultados con foco en visualización, interpretación y propuesta de solución.



### Parte Técnica

Debe incluir las siguientes secciones:

1. **Definición del problema**

     * Importancia del forecasting en el retail.
     * Objetivo del análisis y justificación del enfoque adoptado.

2. **Exploración de datos**

     * Revisión de los archivos `sales_train_validation.csv`, `calendar.csv`, `sell_prices.csv`.
     * Comprensión del significado de `d_1` a `d_1913`, y variables clave (`item_id`, `store_id`, `state_id`, etc.).

3. **Visualización**

     * Tendencias de ventas por producto, tienda o estado.
     * Cambios de precio, patrones semanales, eventos especiales.
     * Exploración de estacionalidades y anomalías.

4. **Preprocesamiento**

     * Transformación del dataset a formato largo (`melt`) para modelamiento.
     * Incorporación de variables exógenas (precios, eventos).
     * Agregación de features: medias móviles, lags, rolling statistics, etc.

5. **Modelamiento**

     * Se deben comparar al menos **cuatro modelos** diferentes:
         * Modelos clásicos (ARIMA/SARIMA)
         * Modelos con regresores (LinearRegression, XGBoost, LightGBM)
         * Modelos multivariados como `Facebook Prophet` o `VAR`
         * Opcional: redes neuronales (`LSTM`, `RNN`) si se justifican adecuadamente.
  
     * Se recomienda usar validación tipo **backtesting** o **walk-forward**.

6. **Evaluación**

     * Métricas requeridas: RMSE, MAE, RMSSE.
     * Visualización de predicciones vs. reales.
     * Análisis de errores y comparación entre modelos.

7. **Conclusiones**

     * Reflexión sobre los resultados obtenidos.
     * Recomendaciones para implementación o mejoras futuras.



### Presentación de Resultados

* La presentación consta de 10–20 minutos.
* Utilizar diapositivas con [BEAMER](https://www.dropbox.com/s/ol38qwzacgwzud7/Beamer.rar). Se deja el siguiente [tutorial](https://www.youtube.com/watch?v=rx7wwtmFlD8&t=792s&ab_channel=Dr.TreforBazett) a modo de ejemplo.
* La presentación debe alojarse en su **Portafolio Personal** del curso (`.pdf`).



## Información Importante

* **Plazo**: 25 de Noviembre del 2025.
* Esto corresponde a un desafío de Kaggle ([link](https://www.kaggle.com/competitions/m5-forecasting-accuracy/)).
* El conjunto de datos puede descargarse desde la sección [Data](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data).
* Como inspiración, pueden revisar notebooks de Kaggle en la sección [Code](https://www.kaggle.com/competitions/m5-forecasting-accuracy/code).

