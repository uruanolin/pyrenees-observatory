# 🚀 MVP Plan: Pyrenees Observatory (Lleida Focus)

Este plan define una ruta realista y práctica para construir un prototipo funcional del "Modelo Vivo Computable del Pirineo". El objetivo es priorizar el aprendizaje del stack de datos y la visualización masiva sobre la perfección académica.

## 1. El Alcance del MVP (Scope)
- **Geografía:** Pirineo de Lleida (Val d'Aran, Pallars Sobirà, Alta Ribagorça). Es un área manejable pero con gran complejidad topográfica y meteorológica.
- **Caso de Uso:** **Monitoreo de Riesgo de Aislamiento Invernal.** 
- **Visualización:** Malla H3 coloreada por el índice de riesgo dinámico.

## 2. Fases de Ejecución

### Fase 1: El Esqueleto Estático (Semana 1-2)
*Objetivo: Tener la rejilla H3 poblada con datos que no cambian.*
1. **Grid Generation:** Script Python para generar todos los IDs de celdas H3 (Resolución 8) que cubren los polígonos de las comarcas de Lleida.
2. **Topography Ingestion:** Descargar el DEM de Copernicus, proyectarlo a H3 y guardar `elevation` y `slope` en DuckDB.
3. **Infrastructure Mapping:** Extraer carreteras principales de OpenStreetMap/IGN y asignar a cada celda una columna `is_road` o `dist_to_road`.

### Fase 2: El Latido Dinámico (Semana 3-4)
*Objetivo: Conectar con el "mundo real" mediante APIs.*
1. **Meteocat Connector:** Un flujo Prefect que consulte cada hora el estado de las estaciones XEMA en Lleida.
2. **Spatial Interpolation (Simple):** Asignar los datos de la estación más cercana a cada celda H3 (K-Nearest Neighbors simplificado). 
3. **Heuristic Engine:** Calcular el `logistics_isolation_risk` cada vez que entran datos de nieve.

### Fase 3: La Ventana Visual (Semana 5-6)
*Objetivo: Demostrar tu seniority frontend aplicada a datos masivos.*
1. **DuckDB API:** Una API mínima (FastAPI) que sirva las celdas H3 y sus métricas en formato GeoJSON o Parquet.
2. **Deck.gl Layer:** Usar `H3HexagonLayer` para renderizar miles de hexágonos coloreados dinámicamente según el riesgo.
3. **Time Slider:** Línea de tiempo para navegar por los eventos de las últimas 24h.

## 3. Lo que "Sacrificamos" (Imperfecciones Aceptables)
- **Precisión Física:** No usaremos modelos de interpolación atmosférica complejos (Kriging); un simple "punto más cercano" es suficiente para el MVP.
- **Backend Robusto:** DuckDB local será nuestro motor. No nos liaremos con escalado de servidores todavía.
- **Frontend Pixel-Perfect:** Usaremos componentes base de Deck.gl. El valor está en el dato, no en el padding del botón.

---
*Plan diseñado para la transición de Frontend a Data/GIS Engineer.*

