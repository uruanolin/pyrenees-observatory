# 📊 Datos y Estrategia de Índices

Este documento resume de dónde vienen nuestros datos y cómo los transformamos en conocimiento.

## 1. Fuentes de Datos Oficiales (Tier-1)
Solo usamos fuentes de alta fiabilidad para garantizar la precisión del modelo:
- **Topografía:** Copernicus DEM (30m de resolución).
- **Cartografía:** IGN (España y Francia) para carreteras e hidrografía.
- **Meteorología:** Meteocat, AEMET y Météo-France.
- **Suelo:** Copernicus Land Monitoring (CORINE).

## 2. Índices Heurísticos (Conocimiento Derivado)
Cruzamos variables estáticas y dinámicas sobre la rejilla H3 para generar métricas de valor:

### A. Riesgo de Aislamiento Logístico
Cruza la pendiente media y la proximidad a carreteras con el espesor de nieve y alertas de viento.

### B. Índice de Aptitud Constructiva
Cruza la pendiente y el tipo de suelo con alertas de lluvia extrema para predecir la estabilidad del terreno.

### C. Resiliencia de Cuenca
Analiza la salud de la vegetación (NDVI) y los niveles de embalses frente a la precipitación mensual.
