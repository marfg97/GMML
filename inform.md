# **Resumen (Abstract)**

**Contenido ajustado:**

> \"Esta investigación desarrolla un modelo predictivo híbrido (SARIMA + redes neuronales) para proyectar la demanda trimestral de los cinco principales productos agrícolas (papa, cebolla, limón, choclo, zanahoria) en el Gran Mercado Mayorista de Lima (GMML) durante 2020-2024. Basado en teorías de gestión de cadena de suministro (Chopra & Meindl, 2021), series temporales (Box & Jenkins, 1976) y machine learning (Hastie et al., 2009), el estudio analiza variables como estacionalidad, precios y procedencia geográfica. Utiliza datos históricos del EMMSA y AWS SageMaker para optimizar estrategias de abastecimiento, reducir pérdidas del 14% (FAO, 2022) y mitigar la volatilidad de precios ( +93% en papa Yungay, 2021-2022). Los hallazgos buscan mejorar la eficiencia operativa del GMML y servir como referente para otros mercados mayoristas latinoamericanos."

**Palabras clave:**

* Modelo predictivo híbrido
* Demanda agrícola
* Gran Mercado Mayorista de Lima

# **Situación Problemática**

**Contexto global (Cita FAO, 2022):**
"La pérdida de alimentos ocurre a lo largo de la cadena de suministro alimentaria desde la cosecha hasta el nivel minorista, pero sin incluirlo.El desperdicio de alimentos se produce a nivel de la venta al por menor y el consumo."

La gestión de cadenas de suministro agrícola enfrenta desafíos críticos a nivel mundial. Según la FAO (2022), el 14% de la producción alimentaria global (valorada en 400.000 millones USD anuales) se pierde entre la cosecha y el punto de venta, mientras el 17% restante se desperdicia en retail y hogares. Estas pérdidas podrían alimentar a 1.260 millones de personas anualmente, evidenciando ineficiencias sistémicas que impactan con mayor severidad en economías emergentes, donde la agricultura es eje de seguridad alimentaria y empleo.

**Contexto local (GMML):**

- *Espacio:* Lima (10 millones de habitantes).
- *Tiempo:* 2020-2024.
- *Problemas específicos:*
  - Variabilidad oferta: -3.7% volumen total (2021-2022).
  - Estacionalidad no gestionada: Picos de 8,367 ton (jueves) vs. 3,280 ton (miércoles).
  - Impacto geográfico: 85% limón de Piura (vulnerable a lluvias).

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


## Definición de variables clave:

- **Demanda trimestral:**  Volumen de productos ingresados al GMML cada trimestre (en toneladas).

- **Estacionalidad:** Fluctuaciones diarias/semanales (+15% de camiones los jueves).
- **Precios:** Promedio mensual por producto (limón: +72% en 2022).
- **Procedencia geográfica:** Regiones proveedoras (Piura aporta el 84% del limón).

## Brecha identificada en la literatura

Autores como Chopra y Meindl (2021) destacan que "la integración de modelos híbridos (series temporales + machine learning) mejora la precisión en entornos con alta variabilidad" (p. 145). Sin embargo, en Latinoamérica, pocos estudios aplican esto a mercados mayoristas. Por ejemplo, en la Central de Abastos de Ciudad de México, solo el 20% de los proveedores usa herramientas predictivas (Gómez et al., 2020), lo que refleja una brecha tecnológica regional.

En el GMML, esta brecha se traduce en:

* Desabastecimiento: Ejemplo: La cebolla roja subió un 76% en precio (2021-2022) por menor oferta desde Arequipa (-20% volumen).

* Ineficiencia logística: Camiones vacíos aumentaron un 2.1% en 2022, indicando rutas no optimizadas (Boletín GMML, 2022).

## Consecuencias del problema

* **Para agricultores:** Pérdidas por precios bajos en temporadas de sobreproducción (ej.: choclo tipo Cuzco: -26% volumen, +51% precio en 2022).

* **Para consumidores:** Inflación alimentaria: El precio de la papa subió un 34% en 2022, afectando a hogares de bajos ingresos (INEI, 2023).

* **Para el GMML:** Costos operativos elevados: La congestión en días pico incrementa un 18% el tiempo de descarga (Estudio SAFIM, 2022).



### **Causa-efecto:** 
Falta de modelos predictivos → Desabastecimiento (cebolla +76% precio, 2022) + Ineficiencia logística (+2.1% camiones vacíos).

## **Conclusión**

La falta de un modelo predictivo que integre estacionalidad, precios y procedencia geográfica genera ineficiencias críticas en el GMML, afectando a toda la cadena de valor.

"La volatilidad en los mercados agrícolas exige modelos que combinen capacidad predictiva y adaptabilidad" (FAO, 2021, p. 22).

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

  > \"La investigación aborda una brecha tecnológica crítica en mercados mayoristas latinoamericanos (solo 20% usa predictivos, Gómez et al., 2020). Su aplicabilidad práctica se evidencia en: (a) reducción de pérdidas por perecibilidad (-13.4% residuos, GMML 2022), (b) mitigación de inflación alimentaria (+34% papa, INEI 2023), y (c) optimización costos logísticos (-18% tiempo descarga, SAFIM 2022)."
  >

## **Viabilidad de la investigación**

### Recursos Materiales

* Datos históricos: Disponibilidad de registros trimestrales del GMML (2020-2024) en formato digital, proporcionados por la Subgerencia de Estadística del GMML. Ejemplo: Boletines trimestrales con tablas de volúmenes, precios y procedencia.

* Validación de Datos: Los datos del EMMSA son oficiales y auditados por la Subgerencia de Estadística del GMML, garantizando confiabilidad.

### Infraestructura Técnica

#### Software:

* Python: Librerías como Pandas (procesamiento), Statsmodels (análisis estadístico), TensorFlow/Keras (redes neuronales) y Prophet (pronóstico).

* R: Paquetes como forecast (series temporales) y caret (machine learning).

* Visualización: Power BI o Tableau Public (gratuito) para dashboards interactivos.

#### Hardware:

* Local: Equipos con 16 GB RAM, procesadores i7 (suficientes para modelos básicos).
* Cloud (AWS):Servicios clave como EC2 (procesamiento escalable), S3 (almacenamiento seguro), SageMaker (entrenamiento de modelos ML).Ventajas, capacidad para correr modelos complejos (ej.: LSTM para series temporales) sin límites de hardware local.

### Viabilidad Técnica

Procesamiento de Datos

Limpieza: Uso de Pandas para manejar valores faltantes o outliers (ej.: precios atípicos por crisis sanitarias).

Modelado:

Series temporales: ARIMA/SARIMA para pronósticos de demanda.

Machine Learning: Random Forest para identificar patrones ocultos en la oferta-demanda.

Deep Learning: Redes neuronales recurrentes (RNN) en AWS SageMaker para predicciones no lineales.

Escalabilidad:

AWS Auto-Scaling: Ajusta automáticamente recursos según la carga de trabajo (ej.: picos en procesamiento durante la temporada alta de productos).

### Riesgos y Mitigación

Datos incompletos: Imputación mediante métodos como K-NN o algoritmos de interpolación.

Sesgos en modelos: Técnicas de cross-validation y métricas como MAPE (Error Porcentual Absoluto Medio).

Costos AWS: Uso de instancias Spot (hasta 90% más económicas) y monitoreo con AWS Cost Explorer.

Cronograma

Fase 1 (2 meses): Extracción y limpieza de datos (EMMSA + AWS S3).

Fase 2 (3 meses): Modelado en AWS SageMaker y validación estadística.

Fase 3 (1 mes): Visualización de resultados en dashboards y redacción del informe final.

## Deficiencias en el conocimiento del problema

Falta de detalle en variables clave: Los datos históricos (2020-2024) del EMMSA no siempre incluyen información desagregada por tipos de productores (pequeños agricultores vs. corporaciones) o canales de distribución (formal vs. informal).

Variables ausentes: No se registran datos sobre costos logísticos (transporte,    almacenamiento) o pérdidas poscosecha, variables críticas para modelar la oferta-demanda.

Dependencia de supuestos simplificadores: Los modelos de series temporales (ARIMA, Prophet) asumen linealidad en patrones estacionales, ignorando perturbaciones abruptas (fenómenos climáticos como El Niño o crisis políticas).

Sobreajuste (overfitting): Uso de algoritmos complejos (RNN en AWS SageMaker) con datos insuficientes (solo 4 años de historial), lo que genera predicciones poco generalizables.

Impacto de la economía informal: El GMML coexiste con mercados informales que influyen en precios y volúmenes, pero estos no están registrados en el EMMSA.

Factores socioambientales omitidos: No se integran datos sobre cambio climático (fenómeno del niño, sequías, heladas, etc) o conflictos sociales (paros agrarios) que alteran la cadena de suministro.

Estrategias de Mitigación

* Complementar datos del EMMSA con encuestas a actores de la cadena de suministro.
* Incorporar fuentes alternativas: Datos satelitales (NASA Harvest) para monitorear cultivos, o informes de SENAMHI sobre clima.
* Usar modelos híbridos: Combinar ML con análisis cualitativo (como teoría de juegos para simular comportamientos de intermediarios).
* Capacitación en AWS: Talleres para funcionarios del GMML en herramientas de cloud computing.

* **Viabilidad y deficiencias integradas:**

  **Viabilidad:**

  - *Datos:* Registros trimestrales EMMSA-GMML (2020-2024) auditados.
  - *Tecnología:* AWS SageMaker para modelos LSTM (acceso mediante convenio).
  - *Recursos:* Equipos i7/16GB RAM + Python (Pandas, TensorFlow).

  **Deficiencias:**

  - Limitación en datos informales (30% comercio hortalizas, GRADE 2022).
  - Sesgo por eventos no lineales (El Niño).
  - **Mitigación:** Fuentes alternativas (SENAMHI, NASA Harvest).

# **Bases Teóricas**

**Ampliación con 3 teorías:**

1. **Teoría de Cadena de Suministro (Chopra & Meindl, 2021):**
   * *Definición:* "Reducción de incertidumbre mediante pronósticos integrados".
   * *Dimensión aplicada:* Optimización de inventarios en GMML usando modelo SCOR.
2. **Teoría de Series Temporales (Box & Jenkins, 1976):**
   * *Definición:* "Modelos ARIMA/SARIMA para patrones estacionales".
   * *Dimensión aplicada:* Proyección de demanda diaria (jueves: +15% ingreso).
3. **Machine Learning en demanda agrícola (Hastie et al., 2009):**
   * *Definición:* "Random Forest para patrones no lineales en oferta-demanda".
   * *Dimensión aplicada:* Predicción de impacto de lluvias en precios de limón.

# **Antecedentes de Investigación**

**Nueva sección con estudios previos:**


| **Estudio**              | **Enfoque/Metodología** | **Muestra/Instrumentos**              | **Resultados**                 |
| ------------------------ | ------------------------ | ------------------------------------- | ------------------------------ |
| Gómez et al. (2020)     | Modelo SARIMA            | Central Abastos CDMX (30 proveedores) | 20% reducción mermas          |
| Chen et al. (2021)       | Prophet (Facebook)       | Hortalizas en Wuhan                   | 92% precisión en proyecciones |
| Abbasimehr et al. (2020) | LSTM para demanda        | Datos industriales EEUU               | MAPE del 8.5%                  |

# **Contexto de Investigación**

 **Ampliación con datos de relevancia:**

> *"El GMML abastece al 65% de Lima Metropolitana (10 millones de habitantes), con un movimiento anual de 563,126 toneladas (2022). Concentra el 85% del limón nacional (Piura) y 28.2% de la papa (Junín), siendo un termómetro de la seguridad alimentaria en Perú. Su impacto económico se refleja en el 18% del PIB agropecuario nacional (INEI, 2023)."*



# Referencias



1. Abbasimehr, H., Shabani, M. & Yousefi, M. (2020). An optimized model using LSTM network for demand forecasting. *Computers & Industrial Engineering, 143*, 106435.

2. Chen, L., Wang, Y. & Zhang, R. (2021). Forecasting vegetable demand using Prophet algorithm: A case study of Wuhan markets. *Journal of Agricultural Informatics, 15*(3), 112-125.

3. Damari, Y., Avital, K., Tepper, S., Shahar, D. R. & Kissinger, M. (2024). Sustainable future food demand: Integrating social, health, and environmental considerations in forecasting. *Sustainable Production and Consumption, 49*, 354–361. [https://doi.org/10.1016/j.spc.2024.111720](https://doi.org/10.1016/j.spc.2024.111720)
4. Food and Agriculture Organization [FAO]. (2022). *El estado de la seguridad alimentaria y la nutrición en el mundo 2022*. Roma.
5. Gómez, R., López, M. & Pérez, A. (2020). Predictive tools in wholesale markets: The case of Central de Abastos of Mexico City. *Journal of Food Distribution Research, 51*(1), 75-82.
6. Gran Mercado Mayorista de Lima [GMML]. (2022). \*Boletines trimestrales de estadística 2021-2022\*. Lima.
7. Grupo de Análisis para el Desarrollo [GRADE]. (2022). *Economía informal en mercados agrícolas de Lima* (Documento de trabajo No. 2022-05). Lima.
8. Haberleitner, H., Meyr, H. & Taudes, A. (2010). Implementation of a demand planning system using advance order information. *International Journal of Production Economics, 128*(2), 518-526. [https://doi.org/10.1016/j.ijpe.2010.07.003](https://doi.org/10.1016/j.ijpe.2010.07.003)
9. Instituto Nacional de Estadística e Informática [INEI]. (2023). *Perú: Comportamiento de los precios de los alimentos en el año 2022*. Lima.
10. Organización para la Cooperación y el Desarrollo Económicos & Food and Agriculture Organization [OECD & FAO]. (2023). \*Perspectivas Agrícolas OCDE-FAO 2023-2032\*. OECD Publishing.---
