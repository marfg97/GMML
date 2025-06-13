---
title: "Análisis predictivo para la gestión estratégica de abastecimiento"
author: "Martin Augusto Rosales Figueroa"
date: "2025"
geometry: margin=2.5cm
fontsize: 12pt
header-includes:
   - \usepackage[spanish]{babel}
   - \usepackage{booktabs}
---
# UNIVERSIDAD ESAN

![Logo ESAN](images/caratula.png) <!-- Si necesitas insertar el logo -->

# TRABAJO DE INVESTIGACIÓN

**Tema de investigación:**
Análisis predictivo para la gestión estratégica de abastecimiento: Proyección de la demanda agrícola en el Gran Mercado Mayorista de Lima (2020-2024)


| **Campo**       | **Detalle**                      |
| --------------- | -------------------------------- |
| **CURSO**       | METODOLOGIA DE LA INVESTIGACION  |
| **PROFESOR**    | RABÍ HIRATA KARIM YADALLAH      |
| **SECCIÓN**    | S - 004                          |
| **INTEGRANTES** | ROSALES FIGUEROA, MARTIN AUGUSTO |

**LIMA-PERÚ**
**2025**

# **Resumen (Abstract)**

**Contenido ajustado:**

> \"Esta investigación desarrolla un modelo predictivo híbrido (SARIMA + redes neuronales) para proyectar la demanda trimestral de los cinco principales productos agrícolas (papa, cebolla, limón, choclo, zanahoria) en el Gran Mercado Mayorista de Lima (GMML) durante 2020-2024. Basado en teorías de gestión de cadena de suministro (Chopra & Meindl, 2021), series temporales (Box & Jenkins, 1976) y machine learning (Hastie et al., 2009), el estudio analiza variables como estacionalidad, precios y procedencia geográfica. Utiliza datos históricos del EMMSA y AWS SageMaker para optimizar estrategias de abastecimiento, reducir pérdidas del 14% (FAO, 2023) y mitigar la volatilidad de precios ( +93% en papa Yungay, 2021-2022). Los hallazgos buscan mejorar la eficiencia operativa del GMML.

**Palabras clave:**

* Modelo predictivo híbrido
* Demanda agrícola
* Gran Mercado Mayorista de Lima

# **Situación Problemática**

**Contexto global:**

La gestión de cadenas de suministro agrícola enfrenta desafíos críticos a nivel mundial. Según la FAO (2023), el 14% de la producción alimentaria global (valorada en 400.000 millones USD anuales) se pierde entre la cosecha y el punto de venta, mientras el 17% restante se desperdicia en retail y hogares. Estas pérdidas podrían alimentar a 1.260 millones de personas anualmente, evidenciando ineficiencias sistémicas que impactan con mayor severidad en economías emergentes, donde la agricultura es eje de seguridad alimentaria y empleo.

(FAO, 2023)
"La pérdida de alimentos ocurre a lo largo de la cadena de suministro alimentaria desde la cosecha hasta el nivel minorista, pero sin incluirlo.El desperdicio de alimentos se produce a nivel de la venta al por menor y el consumo."

**Contexto local (GMML):**

- *Espacio:* Lima (10 millones de habitantes).
- *Tiempo:* 2020-2024.
- *Problemas específicos:*
  - **Variabilidad oferta:** -3.7% volumen total (2021-2022).
  - **Estacionalidad no gestionada:** Picos de 8,367 ton (jueves) vs. 3,280 ton (miércoles).
  - **Impacto geográfico:** 85% limón de Piura (vulnerable a lluvias).

#### **Variabilidad en la oferta:**

Entre 2021 y 2022, el volumen total de productos ingresados al GMML disminuyó un 3.7% (de 584,888 a 563,126 toneladas), con caídas significativas en productos clave como:

- Papa: -2.1% (164,887 a 161,437 toneladas).
- Cebolla: -4.6% (58,992 a 56,263 toneladas).
- Limón: -13.8% (41,689 a 35,941 toneladas) (Boletín GMML, 2022).

#### **Estacionalidad no gestionada:**

Los días jueves y sábados registran picos de ingreso (8,367 toneladas el 04/08/2022), mientras que los miércoles son los de menor actividad (3,280 toneladas el 21/07/2022). Esta irregularidad genera congestión logística y sobrecostos operativos.

#### **Impacto geográfico:**

El 85% del limón proviene de Piura, y el 28.2% de la papa de Junín (Boletín GMML, 2022). Eventos climáticos en estas regiones (lluvias intensas en Piura en 2023) interrumpen abruptamente el suministro, como ocurrió con el limón en 2022 (-14% volumen, +32% precio).

"La procedencia geográfica es un predictor subutilizado en la planificación de abastecimiento" **(Gómez et al., 2020).**

### Problema Central:

Falta de modelos predictivos integrados. La ausencia de herramientas que proyecten la demanda considerando variables multivariadas (estacionalidad, precios, procedencia) limita la capacidad del GMML para:

* Optimizar inventarios: Evitar pérdidas por perecibilidad (13.4% menos residuos sólidos en 2022 no compensa el -3.7% de ingresos).
* Mitigar volatilidad de precios: La papa Yungay aumentó un 93% en precio (de S/1.03 a S/1.67/kg) entre 2021 y 2022, pese a una caída del -2.1% en su volumen **(EMMSA, 2025).**

### Definición de variables clave:

- **Demanda trimestral:**  Volumen de productos ingresados al GMML cada trimestre (en toneladas).
- **Estacionalidad:** Fluctuaciones diarias/semanales (+15% de camiones los jueves).
- **Precios:** Promedio mensual por producto (limón: +72% en 2022).
- **Procedencia geográfica:** Regiones proveedoras (Piura aporta el 84% del limón).

### Brecha identificada en la literatura

Autores como Chopra y Meindl (2021) destacan que "la integración de modelos híbridos (series temporales + machine learning) mejora la precisión en entornos con alta variabilidad" (p. 145). Sin embargo, en Latinoamérica, pocos estudios aplican esto a mercados mayoristas. Por ejemplo, en la Central de Abastos de Ciudad de México, solo el 20% de los proveedores usa herramientas predictivas **(Gómez et al., 2020)**, lo que refleja una brecha tecnológica regional.

En el GMML, esta brecha se traduce en:

* **Desabastecimiento:**  La cebolla roja subió un 76% en precio (2021-2022) por menor oferta desde Arequipa (-20% volumen).
* **Ineficiencia logística:** Camiones vacíos aumentaron un 2.1% en 2022, indicando rutas no optimizadas **(EMMSA, 2025).**

### Consecuencias del problema

* **Para agricultores:** Pérdidas por precios bajos en temporadas de sobreproducción (choclo tipo Cuzco: -26% volumen, +51% precio en 2022).
* **Para consumidores:** Inflación alimentaria. El precio de la papa subió un 34% en 2022, afectando a hogares de bajos ingresos.
* **Para el GMML:** Costos operativos elevados. La congestión en días pico incrementa un 18% el tiempo de descarga.

La falta de un modelo predictivo que integre estacionalidad, precios y procedencia geográfica genera ineficiencias críticas en el GMML, afectando a toda la cadena de valor.

"La volatilidad en los mercados agrícolas exige modelos que combinen capacidad predictiva y adaptabilidad" **(FAO, 2023, p. 22).**

"Estudios previos han destacado el potencial de la IA y el análisis de big data para mejorar las predicciones de la producción agrícola en toda África, identificar los desiertos alimentarios, corregir las ineficiencias de la cadena de suministro y predecir la inseguridad alimentaria."**(Tamasiga et al., 2023).**

Desarrollar una herramienta con enfoque híbrido (SARIMA + Redes Neuronales) no sólo resolvería esta brecha, sino que serviría como referente para mercados mayoristas en Latinoamérica.

# **Formulación del Problema**

### **Preguntas y objetivos alineados:**


| **Preguntas**                             | **Objetivos**                                                 |
| ----------------------------------------- | ------------------------------------------------------------- |
| ¿Cómo desarrollar un modelo predictivo? | *Desarrollar* un modelo híbrido (SARIMA + redes neuronales). |
| ¿Factores que explican variaciones?      | *Identificar* impacto de estacionalidad, precios y clima.     |
| ¿Incidencia de procedencia geográfica?  | *Evaluar* correlación entre región proveedora y oferta.     |
| ¿Estrategias operativas?                 | *Proponer* optimización de rutas y almacenamiento.           |
|                                           |                                                               |


## **Justificación de la Investigación**

### **1. Conveniencia: Abordaje de necesidades concretas**

La investigación **resuelve una brecha operativa crítica** en el GMML, donde la ausencia de modelos predictivos integrados genera pérdidas del 13.4% por perecibilidad y volatilidad de precios (papa Yungay: +93% en 2021-2022) [citation:9][citation:8]. El modelo híbrido (SARIMA + redes neuronales) propuesto:

* **Optimiza inventarios** mediante pronósticos trimestrales basados en estacionalidad, precios y procedencia geográfica [citation:10].
* **Mitiga riesgos climáticos** en regiones proveedoras clave (Piura y Junín), responsables del 85% del limón y 28.2% de la papa [citation:8].
  Como señala la FAO (2023), *"la transformación de sistemas agroalimentarios exige localizar soluciones técnicas en realidades territoriales"* [citation:9], especialmente en economías emergentes donde el 78% de mercados carece de estas herramientas **12**.


### **2. Relevancia social: Beneficiarios y proyección**

#### **Beneficiarios directos:**

* **Agricultores:** Reduce pérdidas por sobreproducción no anticipada (ej.: choclo Cuzco: -26% volumen, +51% precio) [citation:8].
* **Consumidores:** Mitiga la inflación alimentaria (papa +34% en 2022) que afecta a hogares de bajos ingresos [citation:9].
* **GMML:** Disminuye costos logísticos (18% menos tiempo de descarga) y residuos sólidos (13.4%) [citation:8].

#### **Proyección social:**

El modelo servirá como **referente para mercados latinoamericanos**, donde solo el 20% de proveedores usa herramientas predictivas [citation:10]. Su escalabilidad permitirá replicarlo en contextos con vulnerabilidades similares, como la Central de Abastos de Ciudad de México o mercados de Colombia, alineándose con el llamado de Tamasiga et al. (2023) a *"incorporar vulnerabilidades climáticas e informales propias del Global South"* [citation:17].


### **3. Valor práctico: Solución a problemas sectoriales**

* **Para el sector público:** Ofrece un protocolo para gestionar estacionalidad agrícola (+15% ingresos los jueves) y desastres climáticos (lluvias en Piura: -14% oferta de limón) [citation:8]**14**.
* **Para empresas privadas:** Reduce costos de logística inversa (2.1% menos camiones vacíos) mediante rutas optimizadas con GIS [citation:10].
* **Para políticas alimentarias:** Contribuye a la seguridad alimentaria en Lima, donde el GMML abastece al 65% de la población [citation:8].
  La integración con **AWS SageMaker** garantiza acceso a tecnologías asequibles (*cloud computing*), superando limitaciones de *hardware* obsoleto **8**1.



### **4. Aporte teórico-metodológico**

#### **Innovación teórica:**

* **Precisión en variables:** Combina teorías de cadena de suministro (Chopra & Meindl), series temporales (Box & Jenkins) y *machine learning* (Hastie et al.) para modelar no-linealidades ignoradas en estudios previos (ej.: impacto de El Niño) **13**[citation:13].
* **Originalidad metodológica:** Emplea **redes LSTM** para procesar datos multivariados (clima, precios, procedencia), reduciendo el MAPE a <8.5% como en Abbasimehr et al. (2020) **1**8.

#### **Replicabilidad metodológica:**

* **Protocolo escalable:** El uso de **PySpark para ETL** y **APIs de AWS** permite adaptar el modelo a otros mercados mayoristas **8**.
* **Enfoque transferible:** Como demostró **Hyperplan (Francia)** con datos satelitales **1**, la metodología es aplicable a cadenas agroalimentarias de economías emergentes con alta informalidad (30% en Lima) [citation:10].

---

### **Síntesis de contribuciones**


| **Dimensión**        | **Aporte clave**                                                   | **Evidencia**                                             |
| --------------------- | ------------------------------------------------------------------ | --------------------------------------------------------- |
| **Conveniencia**      | Reduce pérdidas del 13.4% en GMML mediante pronósticos precisos. | Datos EMMSA (2025) y FAO (2023) [citation:8][citation:9]. |
| **Relevancia social** | Beneficia a 10 millones de limeños con estabilidad de precios.    | CEPES (2024) y Gómez et al. (2020)**12**[citation:10].   |
| **Valor práctico**   | Protocolo replicable para mercados latinoamericanos.               | Tamasiga et al. (2023) [citation:17].                     |
| **Aporte teórico**   | Modelo híbrido que integra no-linealidades climáticas.           | Abbasimehr et al. (2020) y Damari et al. (2024)**1**14.   |

**Conclusión:**
Esta investigación trasciende el ámbito académico al ofrecer una **herramienta cuantificable** para la toma de decisiones en cadenas agroalimentarias. Como advierte Marwala (2024), *"la IA puede transformar la seguridad alimentaria global si se alinea con las necesidades del Global South"*. Su implementación en el GMML sentará las bases para una nueva generación de modelos predictivos contextualizados en realidades latinoamericanas.

## **Viabilidad de la investigación**

### **Recursos Materiales**

* Datos históricos: Disponibilidad de registros trimestrales del GMML (2020-2024) en formato digital, proporcionados por la Subgerencia de Estadística del GMML. Ejemplo: Boletines trimestrales con tablas de volúmenes, precios y procedencia.
* Validación de Datos: Los datos del EMMSA son oficiales y auditados por la Subgerencia de Estadística del GMML, garantizando confiabilidad.

### **Infraestructura Técnica**

#### Software:

* Python: Librerías como Pandas (procesamiento), Statsmodels (análisis estadístico), TensorFlow/Keras (redes neuronales) y Prophet (pronóstico).
* R: Paquetes como forecast (series temporales) y caret (machine learning).
* Visualización: Power BI o Tableau Public (gratuito) para dashboards interactivos.

#### Hardware:

* Local: Equipos con 16 GB RAM, procesadores i7 (suficientes para modelos básicos).
* Cloud (AWS):Servicios clave como EC2 (procesamiento escalable), S3 (almacenamiento seguro), SageMaker (entrenamiento de modelos ML).Ventajas, capacidad para correr modelos complejos (ej.: LSTM para series temporales) sin límites de hardware local.

### **Viabilidad Técnica**

* [ ]  Procesamiento de Datos

* Limpieza: Uso de Pandas para manejar valores faltantes o outliers (ej.: precios atípicos por crisis sanitarias).

#### Modelado

* Series temporales: ARIMA/SARIMA para pronósticos de demanda.
* Machine Learning: Random Forest para identificar patrones ocultos en la oferta-demanda.
* Deep Learning: Redes neuronales recurrentes (RNN) en AWS SageMaker para predicciones no lineales.

#### Escalabilidad

* AWS Auto-Scaling: Ajusta automáticamente recursos según la carga de trabajo (ej.: picos en procesamiento durante la temporada alta de productos).

### Riesgos y Mitigación

* Datos incompletos: Imputación mediante métodos como K-NN o algoritmos de interpolación.
* Sesgos en modelos: Técnicas de cross-validation y métricas como MAPE (Error Porcentual Absoluto Medio).
* Costos AWS: Uso de instancias Spot (hasta 90% más económicas) y monitoreo con AWS Cost Explorer.

### Cronograma

* Fase 1 (2 meses): Extracción y limpieza de datos (EMMSA + AWS S3).
* Fase 2 (3 meses): Modelado en AWS SageMaker y validación estadística.
* Fase 3 (1 mes): Visualización de resultados en dashboards y redacción del informe final.

## Deficiencias en el conocimiento del problema

* **Falta de detalle en variables clave:** Los datos históricos (2020-2024) del EMMSA no siempre incluyen información desagregada por tipos de productores (pequeños agricultores vs. corporaciones) o canales de distribución (formal vs. informal).
* **Variables ausentes:** No se registran datos sobre costos logísticos (transporte,    almacenamiento) o pérdidas poscosecha, variables críticas para modelar la oferta-demanda.
* **Dependencia de supuestos simplificadores:** Los modelos de series temporales (ARIMA, Prophet) asumen linealidad en patrones estacionales, ignorando perturbaciones abruptas (fenómenos climáticos como El Niño o crisis políticas).
* **Sobreajuste (overfitting):** Uso de algoritmos complejos (RNN en AWS SageMaker) con datos insuficientes (solo 4 años de historial), lo que genera predicciones poco generalizables.
* **Impacto de la economía informal:** El GMML coexiste con mercados informales que influyen en precios y volúmenes, pero estos no están registrados en el EMMSA.
* **Factores socioambientales omitidos:** No se integran datos sobre cambio climático (fenómeno del niño, sequías, heladas, etc) o conflictos sociales (paros agrarios) que alteran la cadena de suministro.

### Estrategias de Mitigación

* Complementar datos del EMMSA con encuestas a actores de la cadena de suministro.
* Incorporar fuentes alternativas: Datos satelitales (NASA Harvest) para monitorear cultivos, o informes de SENAMHI sobre clima.
* Usar modelos híbridos: Combinar ML con análisis cualitativo (como teoría de juegos para simular comportamientos de intermediarios).
* Capacitación en AWS: Talleres para funcionarios del GMML en herramientas de cloud computing.
* Fuentes alternativas (SENAMHI, NASA Harvest).

# Marco Teorico

## **Bases Teóricas**

### **1. Teoría de Cadena de Suministro (Chopra & Meindl)**

* La cadena de suministro es una **red integrada** que abarca proveedores, fabricantes, distribuidores y clientes, donde el éxito depende de la interrelación eficiente entre eslabones para reducir incertidumbres mediante pronósticos.
* Según Chopra y Meindl (2006), incluye funciones como "desarrollo de productos, operaciones, distribución y servicio al cliente", con énfasis en la coordinación de flujos de materiales, información y capital.
* **Modelo SCOR (Supply Chain Operations Reference):**

  * Estandariza métricas para optimizar fases críticas: *aprovisionamiento, producción, distribución y comercialización*.
  * Ejemplo: En el GMML, aplicaría métricas para reducir pérdidas por perecibilidad (13.4%) y ajustar inventarios ante caídas de oferta (-3.7% en volumen total).

**Aplicación en el GMML:**

* **Optimización de inventarios:**
  * Uso de pronósticos integrados para gestionar estacionalidad (ej.: picos de 8,367 ton los jueves) y mitigar congestión logística (+18% tiempo de descarga).
* **Mitigación de riesgos geográficos:**
  * Coordinación con proveedores de Piura (limón) y Junín (papa) para anticipar disrupciones climáticas, usando datos del Boletín GMML (2022).

**Limitaciones:**

* Depende de la integración de actores informales (30% del comercio en Lima, GRADE 2022), lo que exige complementar datos con encuestas a agricultores.

## **Gestión de Cadenas de Suministro: Estrategia, Planificación y Operación**

### **Enfoque y Metodología**

Chopra y Meindl (2006) establecieron un marco conceptual para entender las cadenas de suministro con énfasis en lograr un ajuste estratégico entre la estrategia competitiva de una empresa y la estrategia de cadena de suministro utilizando los impulsores clave del desempeño[7][8]. Su filosofía se basa en que inventario, transporte, instalaciones e información constituyen impulsores clave del desempeño de la cadena de suministro[8].

### **Instrumentos y Población/Muestra**

Los autores utilizaron ejemplos de cadenas de suministro exitosas de la vida real de Wal-Mart, Dell Computers, 7-Eleven Japan y otras organizaciones para presentar conceptos y motivar a los lectores[8]. El libro aborda cinco cadenas de suministro ejemplo en el Capítulo 1 y plantea preguntas sobre el diseño, planificación y operación de cadenas de suministro[8].

### **Resultados Principales**

El marco teórico demostró que la gestión efectiva de cadenas de suministro puede mejorar significativamente la calidad de vida de los ciudadanos mundiales[8]. Los conceptos presentados han sido ampliamente adoptados en universidades e industrias globalmente, proporcionando una mezcla óptima de conceptos de gestión de cadenas de suministro con énfasis en la estrategia y aspectos cuantitativos[8].


### **2. Teoría de Series Temporales (Box & Jenkins)**

* Modelos **ARIMA/SARIMA** para analizar patrones temporales con componentes estacionales, usando descomposición de series en: *tendencia, estacionalidad y ruido* **9**.
* **Metodología:**
  1. *Identificación*: Diagnóstico de autocorrelación (ACF/PACF).
  2. *Estimación*: Ajuste de parámetros (p, d, q).
  3. *Validación*: Residuales deben ser estacionarios.

**Aplicación en el GMML:**

* **Pronóstico de demanda diaria:**
  * Predicción de picos los jueves (+15% ingresos) y valles los miércoles (3,280 ton), optimizando rutas de transporte y almacenamiento.
* **Manejo de estacionalidad agrícola:**
  * Modelado de caídas abruptas (limón: -14% volumen en 2022 por lluvias en Piura) mediante componentes SARIMA para eventos recurrentes.

**Limitaciones:**

* Asume patrones lineales, por lo que ignora perturbaciones no lineales como El Niño. Se recomienda combinar con *machine learning* (ej.: redes neuronales)

## 4. **Metodología Box-Jenkins para Análisis de Series Temporales**

### **Enfoque y Metodología**

Box et al. (2016) establecieron la metodología fundamental para análisis de series temporales, proporcionando un enfoque sistemático que comprende identificación del modelo, estimación de parámetros y verificación diagnóstica[6]. La metodología se enfoca en modelos ARIMA y SARIMA que ayudan a incorporar varios componentes de datos de series temporales, incluyendo tendencia, estacionalidad y ruido[6].

### **Instrumentos y Población/Muestra**

La metodología Box-Jenkins utiliza funciones de autocorrelación (ACF) y autocorrelación parcial (PACF) para la identificación del modelo, seguido de métodos estadísticos para estimar parámetros del modelo[6]. La validación se realiza mediante análisis de residuales para asegurar que el modelo capture efectivamente la estructura subyacente de los datos[6].

### **Resultados Principales**

Los modelos validados pueden utilizarse para generar pronósticos que ayudan a las empresas en la toma de decisiones estratégicas relacionadas con gestión de inventarios, presupuestación y asignación de recursos[6]. La metodología ha demostrado particular efectividad en pronósticos de ventas y demanda basados en datos históricos[6].

### **3. Machine Learning en Demanda Agrícola (Hastie et al.)**

**Fuente principal:** *Hastie, Tibshirani y Friedman (2009)* en *The Elements of Statistical Learning*.
**Definición y Fundamentos:**

* **Algoritmos no lineales** (Random Forest, LSTM) para capturar interacciones complejas en datos multivariados. Según Hastie et al., "el *bagging* y *boosting* mejoran precisión en entornos de alta varianza".
* **Enfoque híbrido:**
  * Combina fortalezas de modelos estadísticos (SARIMA) y ML (Random Forest) para predecir variables como precios o impacto climático.

**Aplicación en el GMML:**

* **Predicción de volatilidad por clima:**
  * Random Forest analiza correlación entre lluvias en Piura (variable climática) y precios de limón (+72% en 2022), usando datos históricos del SENAMHI.
* **Reducción de sesgos:**
  * *Cross-validation* y métricas (MAPE) para evitar sobreajuste en datos limitados (2020-2024).

**Limitaciones:**

* Riesgo de sobreajuste (*overfitting*) con pocos datos. Solución: Uso de AWS SageMaker para entrenar modelos con *regularización*

**Tabla: *Componentes teóricos y su aplicación en el GMML***


| **Teoría**                                | **Aportes clave**                                                                                | **Aplicación en GMML**                                                                | **Limitaciones**                                                |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **Cadena de Suministro (Chopra & Meindl)** | Red integrada de proveedores-distribuidores-clientes para reducir incertidumbres.                | Optimización de inventarios ante estacionalidad (picos de 8,367 ton jueves).          | Depende de integración de actores informales (30% en Lima).    |
| **Series Temporales (Box & Jenkins)**      | Modelos SARIMA para patrones estacionales (descomposición en tendencia, estacionalidad, ruido). | Pronóstico de demanda diaria y manejo de caídas abruptas (limón: -14% por lluvias). | Asume linealidad; ignora perturbaciones no lineales (El Niño). |
| **Machine Learning (Hastie et al.)**       | Algoritmos no lineales (Random Forest, LSTM) para datos multivariados.                           | Predicción de volatilidad por clima (lluvias en Piura vs. precios de limón).         | Riesgo de*overfitting* con pocos datos.                         |

# **Antecedentes de Investigación**

## 1. **Modelos Predictivos con Redes Neuronales LSTM para Pronóstico de Demanda**

### **Enfoque y Metodología**

Abbasimehr et al. (2020) desarrollaron un modelo optimizado usando redes neuronales LSTM multicapa para pronóstico de demanda, implementando una metodología que utiliza el método de búsqueda *grid search* para seleccionar automáticamente la mejor combinación de hiperparámetros para series temporales específicas[1]. El enfoque se fundamenta en la capacidad de las redes LSTM para capturar patrones no lineales en datos de series temporales, considerando las características inherentes de datos no estacionarios[1].

###  **Instrumentos y Población/Muestra**

La investigación utilizó datos históricos de demanda de una empresa de muebles, comparando el modelo LSTM propuesto con métodos establecidos de pronóstico de series temporales tanto estadísticos como de inteligencia computacional[1]. Los métodos de comparación incluyeron ARIMA (autoregresivo integrado de media móvil), suavizado exponencial (ETS), redes neuronales artificiales (ANN), K-vecinos más cercanos (KNN), redes neuronales recurrentes (RNN), máquinas de vectores de soporte (SVM) y LSTM de una sola capa[1].

### **Resultados Principales**

Los resultados experimentales demostraron que el método propuesto fue superior entre todos los métodos evaluados en términos de medidas de rendimiento[1]. En aplicaciones posteriores del modelo LSTM multicapa, estudios como el de El Filali et al. (2022) reportaron un RMSE de 4487.32 y SMAPE de 0.026, significativamente mejor que los obtenidos por otros modelos como ETS, ARIMA y RNN[2]. La metodología LSTM demostró particular fortaleza en capturar características no lineales existentes en datos de series temporales comparado con métodos conocidos derivados de enfoques estadísticos y de machine learning[2].

## 2. **Pronóstico y Planificación en Cadenas de Suministro Alimentarias Durante Crisis**

### **Enfoque y Metodología**

Aljuneidi et al. (2025) propusieron un enfoque de dos etapas para la planificación de cadenas de suministro de carne durante la pandemia COVID-19[3]. En la primera etapa, identificaron el modelo más adecuado para predecir la demanda y el suministro, mientras que en la segunda etapa desarrollaron un modelo de programación entera mixta multi-período y multi-producto que considera características clave de la cadena de suministro de carne[3].

### **Instrumentos y Población/Muestra**

La validación de la propuesta teórica se realizó mediante un estudio de caso de una cadena de suministro de carne real durante la segunda y primera ola de COVID-19 bajo diferentes condiciones[3]. El estudio se enfocó en la cadena de suministro de carne como componente clave del sector de infraestructura crítica 'Alimentación y Agricultura' según la clasificación CISA[3].

### **Resultados Principales**

Los resultados demostraron que el pronóstico preciso de demanda y suministro, junto con el recurso al enfoque de planificación de horizonte rodante, permite satisfacer la demanda y mantener la rentabilidad de la cadena de suministro de carne en períodos de turbulencia[3]. Estos hallazgos pueden considerarse como palancas para la resiliencia de la cadena de suministro, reduciendo el desabastecimiento en un 30% durante períodos críticos[3].

## 3. **Plataformas de Inteligencia Artificial para Prevención de Desperdicios en Redes Alimentarias**

### **Enfoque y Metodología**

Birkmaier et al. (2023) presentaron una arquitectura de plataforma para el pronóstico impulsado por IA basado en big data heterogéneo para prevenir desperdicios en redes de suministro alimentarias[4]. La metodología integra tecnologías de IA como modelos de machine learning, análisis predictivo y algoritmos avanzados para predecir el deterioro de alimentos con alta precisión[5].

### **Instrumentos y Población/Muestra**

La investigación se apoyó en estudios de caso de soluciones impulsadas por IA de empresas como Shelf Engine y Afresh, analizando sistemas de detección temprana de indicadores de deterioro, algoritmos dinámicos para condiciones óptimas de almacenamiento y modelos predictivos para pronóstico de desperdicios basados en datos ambientales en tiempo real[5].

### **Resultados Principales**

Los resultados mostraron una reducción del 14.8% en desperdicios de alimentos por tienda, con una reducción asociada de 26,705 toneladas de emisiones de CO₂[5]. De manera similar, IKEA logró una reducción del 30% en desperdicios de alimentos de cocina en un año utilizando sistemas de monitoreo impulsados por IA[5].


##  **4. Pronóstico de Series Temporales Heterogéneas Mediante Promediado**

### **Enfoque y Metodología**

Neubauer y Filzmoser (2025) propusieron un marco general que utiliza una medida de similitud en Dynamic Time Warping para encontrar series temporales similares y construir vecindarios de manera k-Nearest Neighbor, mejorando pronósticos de modelos posiblemente simples mediante promediado[9]. La metodología permite el pronóstico de un conjunto de series temporales posiblemente muy heterogéneas utilizando una gama de modelos locales y agregándolos de manera apropiada[9].

### **Instrumentos y Población/Muestra**

El estudio se aplicó específicamente a pronósticos de demanda alimentaria, utilizando series temporales con diferentes propiedades como longitud variable[9]. La metodología se validó mediante herramientas de diagnóstico que permiten una comprensión profunda del procedimiento[9].

### **Resultados Principales**

Los argumentos teóricos subrayaron la utilidad del promediado para pronósticos, demostrando que cada serie temporal en un conjunto de datos puede modelarse mediante un modelo local[9]. Para cada serie temporal, se obtiene un conjunto de pronósticos utilizando los modelos estimados de sus series temporales vecinas, realizando un tipo de promediado de modelos para mejorar sus pronósticos[9].

##  **5. Inteligencia Artificial y Big Data en Cadenas de Valor Alimentarias**

### **Enfoque y Metodología**

Tamasiga et al. (2023) realizaron un análisis bibliométrico y cientométrico sobre el papel de la IA y análisis de big data para pronosticar disrupciones en cadenas de valor alimentarias globales[10]. La metodología se enfocó en identificar cómo la IA puede abordar la inseguridad alimentaria mediante análisis predictivo avanzado[10].

### **Instrumentos y Población/Muestra**

El estudio utilizó análisis bibliométrico para examinar la literatura existente sobre aplicaciones de IA en sistemas alimentarios, con particular énfasis en países del Global South que enfrentan vulnerabilidades climáticas e informales[10]. La investigación abarcó múltiples bases de datos académicas para proporcionar una visión integral del campo[10].

### **Resultados Principales**

Los hallazgos destacaron que los modelos para economías emergentes deben incorporar vulnerabilidades climáticas e informales propias del Global South[10]. El estudio identificó que la IA tiene potencial significativo para mejorar la eficiencia de cadenas de suministro alimentarias mediante análisis predictivo, especialmente en regiones con alta variabilidad climática[10].

## **6. Aplicaciones de Machine Learning en Selección de Proveedores**

### **Enfoque y Metodología**

ul Husna et al. (2025) desarrollaron técnicas de machine learning y programación multiobjetivo para seleccionar los mejores proveedores y determinar órdenes óptimas[11]. La metodología integra enfoques de programación multiobjetivo como método para selección de proveedores en entornos just-in-time (JIT)[11].

### **Instrumentos y Población/Muestra**

El estudio se basó en un caso de estudio que desarrolló un modelo de selección de proveedores JIT que permite intercambios simultáneos de criterios de precio, entrega y calidad[11]. El análisis se realizó en un entorno de sistema de soporte a decisiones[11].

### **Resultados Principales**

El sistema de programación multiobjetivo de soporte a decisiones demostró ser ventajoso porque permite juicio en la toma de decisiones mientras simultáneamente intercambia criterios clave de selección de proveedores[11]. Una flexibilidad adicional del modelo es que permite un número variable de proveedores en la solución y proporciona asignación de volumen sugerida por proveedor[11].

## **7. Implementación de Sistemas de Planificación de Demanda con Información de Órdenes Anticipadas**

### **Enfoque y Metodología**

Haberleitner et al. (2010) demostraron la aplicación exitosa de un sistema de pronóstico de cadena de suministro en la industria refractaria que integra el conocimiento de información de demanda anticipada parcialmente conocida[12]. La metodología implementa el "algoritmo aditivo" que añade un pronóstico de órdenes aún no conocidas a las órdenes ya reservadas (conocidas)[12].

### **Instrumentos y Población/Muestra**

El sistema se aplicó en la industria refractaria utilizando datos históricos de órdenes de clientes y información de fin de período, integrando atributos de datos maestros actuales y estructuras organizacionales[12]. La validación se realizó mediante comparación con pronósticos convencionales para horizontes de tiempo a corto plazo[12].

### **Resultados Principales**

Los resultados demostraron que el uso de información de órdenes anticipadas ayudó a estimar el impacto y efectos de la crisis económica para problemas en varias áreas funcionales dentro de la cadena de suministro[12]. El algoritmo aditivo claramente superó a los pronósticos convencionales para horizontes de tiempo a corto plazo y para la mayoría de segmentos de planificación[12]. Las decisiones basadas en pronósticos recuperaron la inversión en pocos meses[12].

## **8. Pronóstico de Demanda Alimentaria Sostenible**

### **Enfoque y Metodología**

Damari et al. (2024) desarrollaron un enfoque para pronóstico de demanda alimentaria futura sostenible integrando consideraciones sociales, de salud y ambientales[3]. La metodología se enfoca en incorporar factores socioambientales en pronósticos para elevar la sostenibilidad de cadenas alimentarias[3].

### **Instrumentos y Población/Muestra**

El estudio utilizó una metodología que integra múltiples dimensiones de sostenibilidad en modelos de pronóstico, considerando aspectos como impacto ambiental, salud pública y equidad social[3]. La investigación se basó en datos representativos de sistemas alimentarios contemporáneos[3].

### **Resultados Principales**

Los hallazgos demostraron que la integración de factores sociales y ambientales en pronósticos de demanda alimentaria puede contribuir significativamente a la sostenibilidad de cadenas alimentarias[3]. El modelo propuesto mostró capacidad para proyectar escenarios de demanda que consideran tanto viabilidad económica como impacto ambiental[3].

La revisión de estos antecedentes evidencia un creciente interés en la aplicación de modelos predictivos avanzados, particularmente redes neuronales LSTM y enfoques híbridos, para optimizar cadenas de suministro alimentarias. Los estudios convergen en la necesidad de integrar múltiples variables (climáticas, económicas, sociales) para desarrollar sistemas de pronóstico más precisos y resilientes, especialmente en contextos de economías emergentes donde la seguridad alimentaria representa un desafío crítico.

# **Contexto de Investigación**

> *"El GMML abastece al 65% de Lima Metropolitana (10 millones de habitantes), con un movimiento anual de 563,126 toneladas (2022). Concentra el 85% del limón nacional (Piura) y 28.2% de la papa (Junín), siendo un termómetro de la seguridad alimentaria en Perú."*


**El GMML como eje estratégico**

El Gran Mercado Mayorista de Lima abastece al 65% de Lima Metropolitana (10 millones de habitantes), con un movimiento anual de 563,126 toneladas (2022). Concentra el 85% del limón nacional (Piura) y 28.2% de la papa (Junín), siendo un termómetro de la seguridad alimentaria en Perú 217. Su diseño como "centro de distribución y redistribución de productos agrícolas" (COSAPI, 2021) lo posiciona como nodo crítico para la aplicación de modelos predictivos.

Oportunidades de optimización
Estacionalidad: Patrones diarios/semanales no gestionados (+15% ingresos jueves).

Procedencia geográfica: Alta dependencia de regiones vulnerables a climas (Piura, Junín).

Pérdidas poscosecha: 13.4% de residuos sólidos en 2022, vinculado a sobreoferta no anticipada


## Segmento Seleccionado para la Investigación

La presente investigación se centra en el **Gran Mercado Mayorista de Lima (GMML)**, el principal centro de abastecimiento agrícola de Lima Metropolitana y una pieza clave en la cadena alimentaria urbana del Perú. Este mercado abastece aproximadamente al 65% de la población limeña, que asciende a cerca de 10 millones de habitantes, y moviliza diariamente más de 6 mil toneladas de productos agrícolas a través de aproximadamente 1,200 comerciantes mayoristas (EMMSA, 2025).

## Relevancia del Grupo Seleccionado

### Importancia Económica y Social

El GMML es un nodo estratégico para la seguridad alimentaria de Lima y, por extensión, del país. Según el Centro Peruano de Estudios Sociales (CEPES, 2024), más del 78% de los mercados mayoristas peruanos carece de herramientas predictivas integradas para la gestión eficiente del abastecimiento, lo que genera pérdidas significativas y volatilidad en los precios de alimentos básicos. En este contexto, el GMML representa un segmento crucial para implementar modelos predictivos que permitan mejorar la planificación y reducir pérdidas.

### Impacto en la Seguridad Alimentaria

La Organización de las Naciones Unidas para la Alimentación y la Agricultura (FAO, 2023) reporta que a nivel global se desperdicia cerca del 14% de la producción alimentaria, mientras que en Perú las pérdidas poscosecha y en la cadena de distribución alcanzan niveles que afectan la disponibilidad y accesibilidad de alimentos. El GMML, al ser el principal mercado mayorista, concentra un volumen significativo de productos perecibles, cuya gestión eficiente impacta directamente en la reducción del desperdicio y en la estabilidad del suministro para millones de consumidores.

### Características Operativas y Desafíos

El GMML presenta una alta estacionalidad y variabilidad en la oferta y demanda, con picos de ingreso de productos que generan congestión logística y afectan la eficiencia operativa (EMMSA, 2025). Además, la concentración geográfica de proveedores en regiones vulnerables a fenómenos climáticos, como Piura para el limón y Junín para la papa, introduce incertidumbre adicional en la cadena de suministro (Tamasiga et al., 2023).

### Justificación para el Uso de Modelos Predictivos

Estudios previos en mercados mayoristas similares, como el de Gómez et al. (2020) en la Central de Abastos de Ciudad de México, han demostrado que la implementación de herramientas predictivas basadas en inteligencia artificial y análisis de series temporales contribuye a optimizar la gestión del inventario, reducir pérdidas y mejorar la satisfacción de la demanda. Además, investigaciones recientes (Abbasimehr et al., 2020; Neubauer & Filzmoser, 2025) han validado la eficacia de modelos híbridos que combinan técnicas estadísticas (SARIMA) con redes neuronales (LSTM) para capturar patrones complejos y estacionales en datos agrícolas, lo que es especialmente relevante para el contexto del GMML.

### Datos Relevantes del Segmento

- **Volumen diario de productos agrícolas:** Más de 6,000 toneladas (EMMSA, 2025).
- **Número de comerciantes mayoristas:** Aproximadamente 1,200.
- **Población abastecida:** 65% de Lima Metropolitana (~10 millones de habitantes).
- **Pérdidas alimentarias:** Estimadas en 14% a nivel global, con cifras similares en el contexto peruano (FAO, 2023).
- **Variabilidad en la oferta:** Fluctuaciones estacionales y climáticas que afectan la estabilidad del suministro (Tamasiga et al., 2023).
- **Falta de herramientas predictivas:** 78% de mercados mayoristas peruanos sin sistemas integrados de pronóstico (CEPES, 2024).

## Conclusión

El GMML, como segmento seleccionado, representa un entorno ideal para desarrollar e implementar un modelo predictivo híbrido que permita mejorar la gestión del abastecimiento agrícola en Lima. La relevancia del grupo radica en su impacto directo en la seguridad alimentaria de millones de personas, la magnitud de los volúmenes comerciales y la existencia de desafíos operativos y climáticos que requieren soluciones innovadoras basadas en inteligencia artificial y análisis avanzado de datos.

---

**Referencias clave:**  
- EMMSA (2025)  
- CEPES (2024)  
- FAO (2023)  
- Abbasimehr et al. (2020)  
- Gómez et al. (2020)  
- Tamasiga et al. (2023)  
- Neubauer & Filzmoser (2025)

# Referencias

1. Abbasimehr, H., Shabani, M. & Yousefi, M. (2020). An optimized model using LSTM network for demand forecasting. *Computers & Industrial Engineering, 143*, 106435.https://doi.org/10.1016/j.cie.2020.106435
2. Aljuneidi, T., Punia, S., Jebali, A., & Nikolopoulos, K. (2025). Forecasting and planning for a critical infrastructure sector during a pandemic: Empirical evidence from a food supply chain. *European Journal of Operational Research, 335*(2), 450–467. https://doi.org/10.1016/j.ejor.2024.04.009
3. Birkmaier, A., Imeri, A., Riester, M., & Reiner, G. (2023). Preventing waste in food supply networks: A platform architecture for AI-driven forecasting based on heterogeneous big data. In K. Mpofu, N. Sacks, & O. Damm (Eds.), *56th CIRP Conference on Manufacturing Systems, CIRP CMS ‘23, South Africa* (pp. 708-713). Elsevier BV. https://doi.org/10.1016/j.procir.2023.09.063
4. Box, G. E. P., Jenkins, G. M., Reinsel, G. C., & Ljung, G. M. (2016). *Time series analysis: Forecasting and control* (5th ed.). John Wiley & Sons, Inc.  https://doi.org/10.1111/jtsa.12194
5. Centro Peruano de Estudios Sociales (CEPES). (2024). Tendencias y perspectivas de la seguridad alimentaria en el Perú. *Debate Agrario, 50*, 34-71. https://cepes.org.pe/wp-content/uploads/2024/04/DebateAgrario50-1-34-71-Tendencias-y-perspectivas-de-la-seguridad-alimentaria-en-el-Peru.pdf
6. Chopra, S., & Meindl, P. (2006). *Supply chain management: Strategy, planning, and operation* (3rd ed.). Pearson College Div. https://doi.org/10.1007/978-3-8349-9320-5_22
7. Damari, Y., Avital, K., Tepper, S., Shahar, D. R. & Kissinger, M. (2024). Sustainable future food demand: Integrating social, health, and environmental considerations in forecasting. *Sustainable Production and Consumption, 49*, 354–361. https://doi.org/10.1016/j.spc.2024.07.003
8. Empresa Municipal de Mercados S.A. (EMMSA). (2025). *Boletín Trimestral de Estadísticas del GMML: 2020-2024*. https://www.emmsa.com.pe/index.php/boletines-trimestral/ .
9. FAO. 2023. The State of Food and Agriculture 2023 – Revealing the true cost of food to transform agrifood systems. Rome.
   https://doi.org/10.4060/cc7724en
10. Gómez, R., López, M. & Pérez, A. (2020). Predictive tools in wholesale markets: The case of Central de Abastos of Mexico City. *Journal of Food Distribution Research, 51*(1), 75-82.
11. Haberleitner, H., Meyr, H. & Taudes, A. (2010). Implementation of a demand planning system using advance order information. *International Journal of Production Economics, 128*(2), 518-526. [https://doi.org/10.1016/j.ijpe.2010.07.003](https://doi.org/10.1016/j.ijpe.2010.07.003)
12. Huang, L., Liu, H., Liu, B., Ma, S., Wang, N., Xie, H., & He, Z. (2025). Demand response with incomplete information: A systematic review. *Electric Power Systems Research, 246*, 111720. https://doi.org/10.1016/j.epsr.2025.111720
13. Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The elements of statistical learning: Data mining, inference, and prediction* (2nd ed.). Springer. [https://doi.org/10.1007/978-0-387-84858-7](https://doi.org/10.1007/978-0-387-84858-7)
14. Marwala Tshilidzi(2024). "Artificial Intelligence Can Transform Global Food Security and Climate Action," United Nations University, UNU Centre, 2024-07-01, https://unu.edu/article/artificial-intelligence-can-transform-global-food-security-and-climate-action.
15. Neubauer, L., & Filzmoser, P. (2025). Improving forecasts for heterogeneous time series by "averaging", with application to food demand forecasts. *International Journal of Forecasting*, *41*(3), 100789. https://doi.org/10.1016/j.ijforecast.2025.100789
16. OECD/FAO (2021), OCDE‑FAO Perspectivas Agrícolas 2021‑2030, OECD Publishing, Paris,
    https://doi.org/10.1787/47a9fa44-es.
17. ul Husna, ****A., Hassanzadeh Amin, S., & Ghasempoor, A. (2025). Machine learning techniques and multi-objective programming to select the best suppliers and determine the orders. *Machine Learning with Applications, 19*, 100623. https://doi.org/10.1016/j.mlwa.2025.100623
18. Tamasiga, P., Ouassou, E., Onyeaka, H., Bakwena, M., Happonen, A., & Molala, M. (2023). Forecasting disruptions in global food value chains to tackle food insecurity: The role of AI and big data analytics – A bibliometric and scientometric analysis. *Journal of Agriculture and Food Research, 14*, 100819. https://doi.org/10.1016/j.jafr.2023.100819


----
# Antecedentes de la Investigación



[1] https://www.periodicos.capes.gov.br/index.php/acervo/buscador.html?task=detalhes&id=W3014191625
[2] https://oaji.net/articles/2022/3603-1645865165.pdf
[3] https://research.uaeu.ac.ae/en/publications/forecasting-and-planning-for-a-critical-infrastructure-sector-dur
[4] https://www.scribd.com/document/738505281/Hossein-Abbasimehr-M-S-2020-An-optimized-model-using-LSTM-network-for-demand-forecasting-Tehran-Iran-Computer-Industrial-Engineering
[5] https://research.birmingham.ac.uk/en/publications/artificial-intelligence-in-food-system-innovative-approach-to-min
[6] https://www.youtube.com/watch?v=Q_OtdU734TI
[7] https://www.slideshare.net/slideshow/scm-chapter-1pptx/260901417
[8] https://go.gale.com/ps/i.do?aty=open-web-entry&id=GALE%7CA105786490&issn=00922102&it=r&linkaccess=abs&p=AONE&sid=googleScholar&sw=w&userGroupName=anon~d064f90&v=2.1
[9] https://arxiv.org/pdf/2306.07119.pdf
[10] https://www.matec-conferences.org/articles/matecconf/abs/2017/14/matecconf_gcmm2017_02048/matecconf_gcmm2017_02048.html
[11] https://www.emerald.com/insight/content/doi/10.1108/09600039310038161/full/html?skipTracking=true
[12] https://research.wu.ac.at/files/38635914/TaudesDemand_planning_Manuskript_final.pdf
[13] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/75551071/48c84d55-1711-494f-919d-1886471f0aaf/paste.txt
[14] https://doi.org/10.1016/j.cie.2020.106435
[15] https://www.semanticscholar.org/paper/An-optimized-model-using-LSTM-network-for-demand-Abbasimehr-Shabani/6b74918de044e2d1b53ca734cb741eb31fe85af6
[16] https://www.nal.usda.gov/research-tools/food-safety-research-projects/career-national-strategy-resilient-food-supply-chain
[17] https://thesai.org/Downloads/Volume13No5/Paper_81-Demand_Forecasting_Model_using_Deep_Learning_Methods.pdf
[18] https://inass.org/wp-content/uploads/2021/12/2022043042-3.pdf
[19] https://www.analyticsinsight.net/artificial-intelligence/smart-networks-against-hunger-how-ai-is-reshaping-food-redistribution
[20] https://pdfs.semanticscholar.org/c47b/35a83acec5cc522d8291033d11e741b59594.pdf
[21] https://pure-oai.bham.ac.uk/ws/portalfiles/portal/202688107/sustainability-15-10482.pdf
[22] https://arxiv.org/abs/2105.00333
[23] https://searchworks.stanford.edu/view/7868647
[24] https://pubs.rsc.org/en/content/articlepdf/2025/fb/d4fb00317a
[25] https://apps.fas.usda.gov/newgainapi/api/Report/DownloadReportByFileName?fileName=Grain+and+Feed+Annual_Lima_Peru_PE2024-0004.pdf
[26] https://archive.org/download/internationalagr00stan/internationalagr00stan.pdf
[27] https://annals-csis.org/Volume_5/pliks/83.pdf
[28] https://www.freshfruitportal.com/news/2024/02/29/perus-agricultural-sector-saw-its-lowest-performance-since-1992-in-2023/
[29] https://unu.edu/article/artificial-intelligence-can-transform-global-food-security-and-climate-action
[30] https://www.context.news/ai/opinion/ai-can-transform-global-food-security-and-climate-action
[31] https://www.linkedin.com/posts/tshilidzimarwala_knowledge-partnerships-and-impact-activity-7212133240134934530-meIz
[32] https://theafricanmirror.africa/thought-leadership/ai-can-transform-global-food-security-and-climate-action/
[33] https://www.academia.edu/118117451/Time_Series_Prediction_for_Food_sustainability
[34] https://www.sciencedirect.com/science/article/abs/pii/S0306261923012023
[35] https://www.ingentaconnect.com/content/asp/jctn/2020/00000017/f0020009/art00003;jsessionid=5lmn9o42pccco.x-ic-live-02
[36] https://www.sciencedirect.com/science/article/abs/pii/S0360835220301698
[37] https://www.sci-hub.se/10.1016/j.cie.2020.106435
[38] https://www.sciencedirect.com/science/article/pii/S2212827123007953
[39] https://research.wu.ac.at/en/publications/preventing-waste-in-food-supply-networks-a-platform-architecture-
[40] https://ouci.dntb.gov.ua/en/works/7XyPrkr4/
[41] https://ideas.repec.org/a/spr/jbecon/v94y2024i6d10.1007_s11573-024-01191-x.html
[42] https://gc.scalahed.com/recursos/files/r161r/w24567w/Sunil_Chopral.pdf
[43] https://mu.ac.in/wp-content/uploads/2021/02/Logistics-and-Supply-Chain-Management-Sunil-Chopra-1.pdf
[44] https://www.scirp.org/reference/referencespapers
[45] https://www.buscalibre.pe/libro-supply-chain-management-strategy-planning-and-operation-4ed/9780136080404/p/2690010
[46] https://www.sciencedirect.com/science/article/pii/S2666827025000064
[47] https://scholar.google.ca/citations?user=C1b3tpQAAAAJ
[48] https://scispace.com/papers/a-proposed-framework-for-supplier-selection-and-order-1a68rmnk9r
[49] https://ouci.dntb.gov.ua/en/works/lx81DN0l/
[50] https://www.linkedin.com/posts/ykhan_ai-can-transform-global-food-security-and-activity-7212191634434789376-cUvk