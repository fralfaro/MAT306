# Proyecto Final

## Overview

### Objetivo 

**Diseñar, validar y comunicar** un **sistema estadístico** para resolver un desafío de Kaggle (p. ej., *M5 Forecasting – Accuracy*), maximizando el desempeño predictivo, la **reproducibilidad** (código y reporte) y la **interpretabilidad** de los resultados mediante un proceso riguroso de EDA, ingeniería de *features*, modelado comparativo y validación robusta.

### Objetivos específicos

1. Realizar **EDA** y diagnóstico de calidad (faltantes, outliers, estacionalidad/tendencias si aplica).
2. Implementar **preprocesamiento** y **feature engineering** trazable (pipelines).
3. Comparar **familias de modelos** (baselines y avanzados) con **búsqueda de hiperparámetros**.
4. Definir y ejecutar **validación robusta** (K-fold estratificado o *walk-forward* en series) con reporte de **media ± DE**/IC.
5. Entregar **interpretabilidad** (importancias, SHAP/PD) y **análisis de errores** por subgrupos.
6. Comunicar resultados en **notebook ejecutable** (Colab), **presentación BEAMER** y **informe**.

### Alcance del Proyecto

* Uso del **dataset oficial de Kaggle** (p. ej., M5: ventas, calendario, precios) sin agregar datos sensibles.
* **Comparación de modelos** con métricas adecuadas (p. ej., RMSSE/MAPE/RMSE en series; AUC/F1/LogLoss en clasificación).
* **Validación** correcta al tipo de problema (K-fold o *walk-forward*) y reporte de incertidumbre (**media ± DE** / *bootstrap*).
* **Materiales reproducibles**: repositorio GitHub (notebook Colab, scripts/pipelines, `requirements.txt`), **PDF BEAMER** y **informe**.
* **Formulación del proyecto**: cuestionario guiado (objetivos/hipótesis/impacto), **carta Gantt** y **planilla de costos** coherentes con el plan de trabajo.

>**Fuera de alcance del proyecto:**
despliegue/MLOps (APIs, CI/CD) ni integraciones externas; recolección de datos privados adicionales a Kaggle; automatización de decisiones sin supervisión humana en entornos reales.

### Entregables

Todos los artefactos del proyecto (notebooks, PDFs, planillas, etc.) deben publicarse en el **repositorio personal** de cada estudiante, dentro de la carpeta **`project/`**. Usa nombres de archivos claros y añade un **`README.md`** con instrucciones de ejecución y enlace al informe final.

### Información importante

* **Plazo de entrega:** **25 de noviembre de 2025** (hora local Chile).
* **Competencia base:** Kaggle — *M5 Forecasting – Accuracy* ([ver competencia](https://www.kaggle.com/competitions/m5-forecasting-accuracy/)).
* **Datos:** descarga el dataset desde la pestaña **Data** ([enlace directo](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data)).
* **Referencias:** usa como inspiración los **notebooks** de la pestaña **Code** ([explorar ejemplos](https://www.kaggle.com/competitions/m5-forecasting-accuracy/code)).
* **Presentación**: Utilizar diapositivas con [BEAMER](https://www.dropbox.com/s/ol38qwzacgwzud7/Beamer.rar). Se deja el siguiente [tutorial](https://www.youtube.com/watch?v=rx7wwtmFlD8&t=792s&ab_channel=Dr.TreforBazett) a modo de ejemplo.

> **Sugerencia**: asegúrate de tener cuenta en Kaggle para habilitar la descarga de datos.



## Parte Técnica + Presentación (70%)

### Objetivo

Construir y justificar un **sistema de pronóstico de demanda diaria** para M5 (nivel ítem/tienda/estado) con **pipeline reproducible**, **modelamiento comparativo** y **validación walk-forward**, reportando **RMSSE** (obligatoria) y **RMSE/MAE**, con resultados **interpretables** y **accionables**.

### Entregables (obligatorios)

* **Notebook ejecutable (Google Colab)**, que corra *end-to-end*: 
    * datos → EDA → *features* → modelos → validación → interpretabilidad → tablas/figuras
* **Presentación Beamer (PDF)**, 10–20 min, centrada en hallazgos clave



#### Secciones mínimas del Notebook

1. **Definición del problema**

     * Relevancia del *forecasting* en retail (inventario, logística, decisiones).
     * **Objetivo técnico** y **unidad de modelado** (ítem/tienda/estado o agregaciones) con justificación.

2. **Exploración de datos (EDA)**

     * Archivos: `sales_train_validation.csv`, `calendar.csv`, `sell_prices.csv`.
     * Entender `d_1 … d_1913` y claves (`item_id`, `store_id`, `state_id`, etc.).
     * Calidad: faltantes, ceros, rupturas; primeras correlaciones y patrones.

3. **Visualización**

     * Tendencias y estacionalidad por producto/tienda/estado.
     * Cambios de precio, patrones semanales, eventos especiales.
     * Anomalías y comparación de subgrupos (*top sellers* vs *long tail*).

4. **Preprocesamiento**

     * **Reformateo a largo** (melt) para *lags/rollings*.
     * **Regresores exógenos**: precios (niveles/variaciones), eventos/feriados (`calendar`).
     * **Feature engineering (mínimos)**:

       * *Lags* (7, 28, …), *rolling means/std* (7/28/56), calendario (`dow`, `month`, fin de semana, proximidad a evento).
       * Codificación categóricas (one-hot/target) evitando **leakage**.
     * **Pipelines** (`sklearn`): imputación, escala, codificación y selección integradas.

5. **Modelamiento (comparativa ≥ 4)**

     * **Baselines**: Naive / SNaive (estacional) o media móvil.
     * **Clásicos**: ARIMA/SARIMA/ETS (por unidad o segmentos).
     * **Regresión con lags**: Linear/Elastic Net y **Gradient Boosting** (XGBoost/LightGBM/CatBoost).
     * **Multivariados**: Prophet (con regresores) o VAR (si agrupas pocas series correlrelacionadas).
     * **Opcional**: LSTM/RNN/DeepAR/Temporal Fusion (si justificas costo y comparas).

6. **Validación**

     * **Backtesting / walk-forward** con **origen rodante** y ventana creciente.
     * Explicitar **fechas** de *train/validation* por *split* y mantener causalidad temporal.
     * *Grid/random/Optuna* **dentro** del esquema temporal (sin mirar el futuro).

7. **Evaluación**

     * **Métricas**: **RMSSE** (M5), **RMSE**, **MAE**.
     * **Reporte**: tabla **media ± DE** por modelo y por *split*.
     * **Gráficos**: pred vs real (casos típicos y difíciles), residuales, error por subgrupos (tienda/estado/categoría).
     * **Ablation** breve: impacto de *features* clave (precio/eventos).

8. **Interpretabilidad y análisis de error**

     * Importancias (gain/perm) y **SHAP**/**Partial Dependence** en 1–2 modelos top.
     * **≥ 2 insights accionables** (sensibilidad a precio, efecto calendario/feriados).

9. **Conclusiones técnicas**

     * **Modelo recomendado** + justificación: métrica principal, estabilidad, costo/tiempo.
     * **Limitaciones** y **próximos pasos** (nuevas *features*, segmentación, mejor *tuning*).



#### Secciones mínimas del Beamer

* **Duración**: 10–20 minutos.
* **Contenido mínimo**: problema → datos/EDA → método/validación → resultados (tabla + gráficos) → interpretabilidad → limitaciones → próximos pasos.
* **Formato**: PDF **Beamer** (subir al Portafolio).


**Recomendación para el cierre** (últimas 2–3 diapositivas)

1. **Conclusión ejecutiva (1 slide)**

     * *Modelo elegido* + **RMSSE** (y RMSE/MAE) con **media ± DE**.
     * 1 gráfico clave (pred vs real) y una frase de **valor práctico**.
2. **Limitaciones y riesgos (1 slide)**

     * 2–3 puntos concretos (datos, horizonte, complejidad) y cómo afectan el uso.
3. **Próximos pasos / llamada a la acción (1 slide)**

     * Qué **mejorarías** (feature/segmentación/validación), costo estimado y **beneficio esperado**.
     * Link al **repo** y al **notebook Colab** para reproducir.





## Formulación del Proyecto (30%)

#### Objetivos de esta parte

**Objetivo general**
Estructurar el trabajo como **proyecto estadístico aplicado**, definiendo objetivos medibles, plan de trabajo (Gantt), presupuesto y criterios de éxito coherentes con la Parte Técnica.

**Objetivos específicos**

1. Formular **OG y OE** medibles con métricas/umbrales y alcance explícito.
2. Responder un **cuestionario guiado** (estilo ANID) que cubra problema, hipótesis, metodología, riesgos, ética e impacto.
3. Elaborar una **Carta Gantt** con hitos, tareas, responsables, dependencias y criterios de finalización.
4. Construir un **presupuesto** trazable por rubros (personal, infraestructura, difusión, misceláneos), con supuestos y tasas documentadas.

**Entregables**

* **Informe de Formulación** (PDF o Markdown).
* **Carta Gantt** (Excel).
* **Planilla de costos** (Excel).


### Cuestionario guiado (responder en el informe)

#### A. Contenido científico/tecnológico

1. **Problema y oportunidad**: ¿qué necesidad resuelve el pronóstico M5 y por qué ahora?
2. **Resultados previos**: ¿qué baselines/EDA ya tienes y qué aprendiste?
3. **Hipótesis** (1–3, contrastables): p. ej., “incluir *lags* 28 y eventos reduce RMSSE ≥ X%”.
4. **Estado del arte**: ¿qué enfoques comparables tomas como referencia y cómo te diferencias?
5. **Criterios de éxito**: métrica principal (RMSSE) + umbral esperado; métricas secundarias.

#### B. Estrategia de desarrollo e impacto

6. **Producto final**: repo reproducible + informe + póster/diapositivas. ¿Para qué decisiones sirve?
7. **Usuarios/beneficiarios**: ¿quién lo usaría (curso/industria) y cómo?
8. **Ventajas**: reproducibilidad, claridad, costo-tiempo, interpretabilidad.
9. **Impacto esperado**: técnico (lecciones/benchmark) y aplicado (decisiones de inventario, etc.).

#### C. Capacidades y organización

10. **Equipo y roles**: quién lidera EDA, modelado, validación, documentación y presentación.
11. **Coordinación**: ¿cómo gestionarán issues, branches, *reviews*?

#### D. Objetivos y métricas

12. **OG** del proyecto (1) y **OE** (4–6) con métrica y umbral cada uno.
13. **Alineación**: explicar cómo validación y métricas permiten verificar cada OE.

#### E. Metodología

14. **Validación**: por qué *walk-forward* es adecuado; detalle de *splits* y fechas.
15. **Métricas**: RMSSE (principal) + RMSE/MAE; cómo estimar incertidumbre (media ± DE, bootstrap).
16. **Interpretabilidad**: qué técnicas (importancias, SHAP/PD) y cómo se usarán para decisiones.
17. **Sesgos y leakage**: riesgos y mecanismos de prevención.

#### F. Ética, permisos y datos

18. **Datos**: naturaleza pública del M5; ausencia de datos sensibles; licencias/notebooks citados.
19. **Uso responsable**: límites de aplicación fuera del entorno académico.

#### G. Resultados e hitos

20. **Resultados**: R1 informe, R2 repo, R3 póster (y links).
21. **Hitos**: H1…H5 con entregables verificables.



### Carta Gantt — temas mínimos (qué debe contener)

**Horizonte sugerido**: 8 semanas (ajustable).
**Hitos y tareas base (ejemplo)**

| Fase | Hito / Tarea                   | Descripción                             | Responsable    | Inicio | Fin | Depende de | Entregable                        | Criterio de finalización   |
| ---- | ------------------------------ | --------------------------------------- | -------------- | ------ | --- | ---------- | --------------------------------- | -------------------------- |
| H1   | EDA + limpieza                 | Calidad de datos, visuales clave        | Analista       | S1     | S2  | —          | Notebook EDA                      | Checklist EDA completo     |
| H2   | *Features* + baselines         | Lags/rollings, calendario; Naive/SNaive | Analista       | S3     | S4  | H1         | Notebook *features*               | Tabla baselines            |
| H3   | Modelos + *tuning*             | ARIMA/SARIMA/ETS + GBMs                 | Analista       | S5     | S6  | H2         | Notebook modelos                  | CV temporal implementado   |
| H4   | Validación + interpretabilidad | Walk-forward, SHAP/PD, subgrupos        | Líder/Analista | S7     | S7  | H3         | Figuras y tabla **media ± DE**    | Reproducible y documentado |
| H5   | Informe + BEAMER + repo        | Redacción y slides finales              | Autor/Líder    | S8     | S8  | H4         | PDF informe + PDF Beamer + README | Checklist de entrega       |

**Incluir en tu Gantt**

* Responsable por tarea, dependencias, entregables y **criterio de salida**.
* **Riesgos** por fase (p. ej., sobretiempos en *tuning*) y plan de contingencia.
* Marcar **hitos** (diamante) y **tareas** (barras) si usas diagrama.

> **Consejo**: alinear las fechas del Gantt con las fechas de *splits* del *walk-forward* para que la validación quede calendarizada y auditable.



### Presupuesto — estructura y supuestos

**Rubros mínimos**

1. **Personal**: horas y rol (Líder, Analista, Autor/a del informe/póster).
2. **Infraestructura**: cómputo (CPU/GPU/TPU), almacenamiento.
3. **Difusión**: impresión de póster, insumos de presentación.
4. **Misceláneos/contingencias**: transporte, imprevistos menores.

**Plantilla de tabla (resumen por ítem)**

| Categoría       | Ítem              |       UM | Cantidad | Costo unitario | Periodo | Notas                | Subtotal |
| --------------- | ----------------- | -------: | -------: | -------------: | ------- | -------------------- | -------: |
| Personal        | Líder de proyecto |     hora |       20 |         35.000 | S1–S8   | Revisión/seguimiento |       $… |
| Personal        | Analista de datos |     hora |       80 |         25.000 | S1–S8   | EDA/modelado         |       $… |
| Infraestructura | Cómputo nube      |     hora |       30 |          1.800 | S3–S6   | Entrenamiento/tuning |       $… |
| Difusión        | Impresión póster  |   unidad |        1 |         45.000 | S8      | A0 satinado          |       $… |
| Misceláneos     | Contingencias     | lump-sum |        1 |         30.000 | S1–S8   | Varios               |       $… |

**Totales**

* **Subtotal** = Σ Subtotales
* **IVA** (ej. 19%, si aplica)
* **Contingencia** (ej. 10%, configurable)
* **TOTAL** = Subtotal + IVA + Contingencia

**Supuestos (dejar explícitos en el informe)**

* Tarifas por hora y disponibilidad del equipo.
* Cantidad de horas de cómputo estimadas según *tuning* y tamaño de muestra.
* Necesidad de impresión del póster (o solo digital).
* Tasas de IVA/contingencia y política de redondeo.

> **Tip**: vincula cada **ítem de costo** a un **hito/tarea** de la carta Gantt.

