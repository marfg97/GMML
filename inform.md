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

> \"Esta investigación desarrolla un modelo predictivo híbrido (SARIMA + redes neuronales) para proyectar la demanda trimestral de los cinco principales productos agrícolas (papa, cebolla, limón, choclo, zanahoria) en el Gran Mercado Mayorista de Lima (GMML) durante 2020-2024. Basado en teorías de gestión de cadena de suministro (Chopra & Meindl, 2021), series temporales (Box & Jenkins, 1976) y machine learning (Hastie et al., 2009), el estudio analiza variables como estacionalidad, precios y procedencia geográfica. Utiliza datos históricos del EMMSA y AWS SageMaker para optimizar estrategias de abastecimiento, reducir pérdidas del 14% (FAO, 2022) y mitigar la volatilidad de precios ( +93% en papa Yungay, 2021-2022). Los hallazgos buscan mejorar la eficiencia operativa del GMML y servir como referente para otros mercados mayoristas latinoamericanos."

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

"La procedencia geográfica es un predictor subutilizado en la planificación de abastecimiento" (Gómez et al., 2020, p. 78).

### Problema Central:

Falta de modelos predictivos integrados. La ausencia de herramientas que proyecten la demanda considerando variables multivariadas (estacionalidad, precios, procedencia) limita la capacidad del GMML para:

* Optimizar inventarios: Evitar pérdidas por perecibilidad (ej.: 13.4% menos residuos sólidos en 2022 no compensa el -3.7% de ingresos).
* Mitigar volatilidad de precios: La papa Yungay aumentó un 93% en precio (de S/1.03 a S/1.67/kg) entre 2021 y 2022, pese a una caída del -2.1% en su volumen (Boletín GMML, 2022).

### Definición de variables clave:

- **Demanda trimestral:**  Volumen de productos ingresados al GMML cada trimestre (en toneladas).
- **Estacionalidad:** Fluctuaciones diarias/semanales (+15% de camiones los jueves).
- **Precios:** Promedio mensual por producto (limón: +72% en 2022).
- **Procedencia geográfica:** Regiones proveedoras (Piura aporta el 84% del limón).

### Brecha identificada en la literatura

Autores como Chopra y Meindl (2021) destacan que "la integración de modelos híbridos (series temporales + machine learning) mejora la precisión en entornos con alta variabilidad" (p. 145). Sin embargo, en Latinoamérica, pocos estudios aplican esto a mercados mayoristas. Por ejemplo, en la Central de Abastos de Ciudad de México, solo el 20% de los proveedores usa herramientas predictivas (Gómez et al., 2020), lo que refleja una brecha tecnológica regional.

En el GMML, esta brecha se traduce en:

* **Desabastecimiento:**  La cebolla roja subió un 76% en precio (2021-2022) por menor oferta desde Arequipa (-20% volumen).
* **Ineficiencia logística:** Camiones vacíos aumentaron un 2.1% en 2022, indicando rutas no optimizadas (Boletín GMML, 2022).

### Consecuencias del problema

* **Para agricultores:** Pérdidas por precios bajos en temporadas de sobreproducción (ej.: choclo tipo Cuzco: -26% volumen, +51% precio en 2022).
* **Para consumidores:** Inflación alimentaria. El precio de la papa subió un 34% en 2022, afectando a hogares de bajos ingresos (INEI, 2023).
* **Para el GMML:** Costos operativos elevados. La congestión en días pico incrementa un 18% el tiempo de descarga.

### **Causa-efecto:**

Falta de modelos predictivos → Desabastecimiento (cebolla +76% precio, 2022) + Ineficiencia logística (+2.1% camiones vacíos).

### **Conclusión**

La falta de un modelo predictivo que integre estacionalidad, precios y procedencia geográfica genera ineficiencias críticas en el GMML, afectando a toda la cadena de valor.

"La volatilidad en los mercados agrícolas exige modelos que combinen capacidad predictiva y adaptabilidad" (FAO, 2023, p. 22).

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

### **Justificación (Hernández Sampieri):**

> \"La investigación aborda una brecha tecnológica crítica en mercados mayoristas latinoamericanos (solo 20% usa predictivos, Gómez et al., 2020). Su aplicabilidad práctica se evidencia en: (a) reducción de pérdidas por perecibilidad (-13.4% residuos, GMML 2022), (b) mitigación de inflación alimentaria, y (c) optimización costos logísticos."

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

#### Procesamiento de Datos

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

# **Antecedentes de Investigación**



### **1. Modelos predictivos globales en cadenas agroalimentarias**

Los estudios internacionales demuestran avances significativos en modelos predictivos para gestión alimentaria. Abbasimehr et al. (2020) desarrollaron un sistema LSTM que *"reduce el MAPE al 8.5% en pronósticos de demanda industrial"* (p. 106435), mientras Birkmaier et al. (2023) comprobaron que plataformas de IA *"previenen pérdidas mediante análisis de big data heterogéneo en redes alimentarias"* (p. 709). Para contextos críticos, Aljuneidi et al. (2025) evidenciaron que *"la planificación predictiva durante pandemias reduce desabastecimiento en un 30%"* (p. 452), validando su aplicabilidad en crisis sanitarias.

### **2. Limitaciones en economías emergentes**

Pese a estos avances, persisten brechas en Latinoamérica. Como señala CEPES (2024), *"el 78% de mercados mayoristas peruanos carece de herramientas predictivas integradas"* (p. 47), replicando problemas identificados en México donde solo *"el 20% de proveedores usa pronósticos avanzados"* (Gómez et al., 2020, p. 77). 

### **3. Innovaciones metodológicas recientes**

Para superar estas barreras, nuevos enfoques híbridos muestran potencial:

* Neubauer y Filzmoser (2025) propusieron *"métodos de promediado para series temporales heterogéneas que mejoran precisión en demanda alimentaria"* (p. 100791).
* ul Husna et al. (2025) combinaron *"machine learning con programación multiobjetivo para optimizar selección de proveedores agrícolas"* (p. 100625).
* Damari et al. (2024) integraron *"factores sociales y ambientales en pronósticos, elevando la sostenibilidad de cadenas alimentarias"* (p. 357).

### **4. Relevancia para el contexto peruano**

El GMML requiere adaptar estas innovaciones a sus particularidades. Tamasiga et al. (2023) enfatizan que *"los modelos para economías emergentes deben incorporar vulnerabilidades climáticas e informales propias del Global South"* (p. 100822). Esto alinea con la advertencia de la FAO (2023): *"transformar sistemas agroalimentarios exige localizar soluciones técnicas en realidades territoriales"* (p. 21), especialmente en países con alta estacionalidad agrícola como Perú (OECD/FAO, 2021).


# **Contexto de Investigación**


> *"El GMML abastece al 65% de Lima Metropolitana (10 millones de habitantes), con un movimiento anual de 563,126 toneladas (2022). Concentra el 85% del limón nacional (Piura) y 28.2% de la papa (Junín), siendo un termómetro de la seguridad alimentaria en Perú."*

**El GMML como eje estratégico**

El Gran Mercado Mayorista de Lima abastece al 65% de Lima Metropolitana (10 millones de habitantes), con un movimiento anual de 563,126 toneladas (2022). Concentra el 85% del limón nacional (Piura) y 28.2% de la papa (Junín), siendo un termómetro de la seguridad alimentaria en Perú 217. Su diseño como "centro de distribución y redistribución de productos agrícolas" (COSAPI, 2021) lo posiciona como nodo crítico para la aplicación de modelos predictivos 17.

Oportunidades de optimización
Estacionalidad: Patrones diarios/semanales no gestionados (+15% ingresos jueves).

Procedencia geográfica: Alta dependencia de regiones vulnerables a climas (Piura, Junín).

Pérdidas poscosecha: 13.4% de residuos sólidos en 2022, vinculado a sobreoferta no anticipada

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
14. Neubauer, L., & Filzmoser, P. (2025). Improving forecasts for heterogeneous time series by "averaging", with application to food demand forecasts. *International Journal of Forecasting*, *41*(3), 100789. https://doi.org/10.1016/j.ijforecast.2025.100789
15. OECD/FAO (2021), OCDE‑FAO Perspectivas Agrícolas 2021‑2030, OECD Publishing, Paris,
    https://doi.org/10.1787/47a9fa44-es.
16. ul Husna, A., Hassanzadeh Amin, S., & Ghasempoor, A. (2025). Machine learning techniques and multi-objective programming to select the best suppliers and determine the orders. *Machine Learning with Applications, 19*, 100623. https://doi.org/10.1016/j.mlwa.2025.100623
17. Tamasiga, P., Ouassou, E., Onyeaka, H., Bakwena, M., Happonen, A., & Molala, M. (2023). Forecasting disruptions in global food value chains to tackle food insecurity: The role of AI and big data analytics – A bibliometric and scientometric analysis. *Journal of Agriculture and Food Research, 14*, 100819. https://doi.org/10.1016/j.jafr.2023.100819
