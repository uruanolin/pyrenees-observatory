# 🛰️ Catálogo de Fuentes de Datos y Estrategia de Índices

Este documento detalla las fuentes de datos oficiales (Tier-1) y la lógica de cruce para derivar conocimiento mediante índices heurísticos aplicados al Pirineo.

## 1. Fuentes de Datos de Alta Fiabilidad (Official Sources)

Se priorizan agencias nacionales y europeas que garantizan continuidad y precisión.

| Dominio | Fuente | Tipo de Datos | Fiabilidad | Uso en el Modelo |
| :--- | :--- | :--- | :--- | :--- |
| **Topografía** | [Copernicus DEM (GLO-30)](https://spacedata.copernicus.eu/) | Elevación, Pendiente, Orientación | 99% | Esqueleto estático de las celdas H3. |
| **Topografía** | [IGN Spain](https://centrodedescargas.cnig.es/) / [IGN France](https://geoservices.ign.fr/) | Redes de transporte, Hidrografía | 100% | Capas de infraestructura y logística vial. |
| **Meteo** | [AEMET](https://opendata.aemet.es/) / [Météo-France](https://meteo.data.gouv.fr/) | Tiempo real, histórico y avisos | 100% | Latido dinámico del territorio. |
| **Meteo** | [Meteocat](https://apidocs.meteocat.gencat.cat/) | Estaciones automáticas (XEMA) | 100% | Granularidad extrema para Lleida/Girona. |
| **Land Cover** | [Copernicus Land (CORINE)](https://land.copernicus.eu/) | Usos del suelo, vegetación | 95% | Clasificación de aptitud para construcción/logística. |
| **Hidrología** | [ACA (CAT)](https://aca.gencat.cat/) / [CHE (Ebro)](https://www.chebro.es/) | Caudales, niveles de embalses | 100% | Modelado de cuencas y estrés hídrico. |

---

## 2. Estrategia de Cruce de Datos (Indices Design)

El valor del proyecto no reside en los datos individuales, sino en cómo se cruzan sobre la rejilla H3.

### A. Índice de Riesgo de Aislamiento Logístico (`logistics_isolation_risk`)
**Objetivo:** Identificar núcleos o infraestructuras que pueden quedar aisladas en invierno.
- **Variables Cruzadas:**
    - Estática: Pendiente media de la celda + Distancia a la red vial principal (IGN).
    - Dinámica: Espesor de nieve acumulada (Meteo) + Avisos de viento (AEMET/Météo-France).
- **Fórmula Heurística:** $Risk = (Slope \cdot 0.4) + (SnowDepth \cdot 0.4) + (RoadDist \cdot 0.2)$.

### B. Índice de Aptitud Constructiva y Estabilidad (`construction_suitability_index`)
**Objetivo:** Analizar la viabilidad técnica de nuevas obras o mantenimiento de infraestructuras críticas.
- **Variables Cruzadas:**
    - Estática: Grado de pendiente + Tipo de suelo (Land Cover) + Orientación (Aspect).
    - Dinámica: Precipitación acumulada en 24h (Riesgo de deslizamiento).
- **Caso de uso:** Celdas con pendiente > 30% y lluvia extrema = Alerta de mantenimiento preventivo en carreteras.

### C. Índice de Resiliencia de Cuenca (`watershed_resilience_index`)
**Objetivo:** Predecir disponibilidad de agua para logística hidroeléctrica o consumo.
- **Variables Cruzadas:**
    - Estática: Superficie de la cuenca (H3 Aggregation) + Densidad de vegetación (NDVI/Copernicus).
    - Dinámica: Precipitación media mensual + Nivel de embalses (ACA).

---

## 3. Implementación Técnica de los Datos

1.  **Normalización:** Todos los datos (GeoTIFF de elevación, GeoJSON de carreteras, JSON de APIs meteo) se proyectan a la resolución H3 seleccionada.
2.  **Granularidad:** 
    - **Resolution 8:** Para visualización regional y tendencias de cuenca.
    - **Resolution 10:** Para análisis de carreteras y zonas de construcción.
3.  **Storage:** Uso de archivos Parquet particionados por `country_code` y `h3_index_prefix` para consultas DuckDB ultra-eficientes.

---
*Documentación técnica de fuentes de datos. Última actualización: 2026-05-07.*
