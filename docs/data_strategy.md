# 📊 Datos y Estrategia de Índices

Este documento detalla el origen de la información y la lógica de transformación para generar conocimiento sobre el territorio.

## 1. Catálogo de Fuentes Oficiales (Tier-1)

Garantizamos la fiabilidad del modelo utilizando únicamente fuentes de agencias nacionales y europeas.

| Dominio | Fuente | Tipo de Datos | Uso en el Proyecto |
| :--- | :--- | :--- | :--- |
| **Topografía** | [Copernicus DEM](https://spacedata.copernicus.eu/) | Elevación y Pendiente | Esqueleto estático de las celdas H3. |
| **Cartografía** | [IGN Spain](https://centrodedescargas.cnig.es/) / [IGN France](https://geoservices.ign.fr/) | Red vial e Hidrografía | Capas de infraestructura y logística. |
| **Meteorología** | [AEMET](https://opendata.aemet.es/) / [Météo-France](https://meteo.data.gouv.fr/) | Tiempo real y avisos | Datos dinámicos para los índices de riesgo. |
| **Meteo Local** | [Meteocat](https://apidocs.meteocat.gencat.cat/) | Estaciones XEMA | Alta resolución para el Pirineo de Lleida. |
| **Usos del Suelo** | [Copernicus Land (CORINE)](https://land.copernicus.eu/) | Cobertura vegetal | Clasificación de estabilidad y aptitud. |
| **Hidrología** | [ACA (CAT)](https://aca.gencat.cat/) / [CHE (Ebro)](https://www.chebro.es/) | Embalses y caudales | Cálculo de resiliencia hídrica. |

---

## 2. Validación Visual (Red de Webcams)

Utilizamos sensores visuales como "Ground Truth" para validar los datos numéricos de las estaciones.

- **Francia:** [Meteo Pyrénées](https://www.meteopyrenees.fr/webcams/) (Alta Resolución), [N-PY](https://www.n-py.com/fr/webcams).
- **España:** [Infonieve](https://www.infonieve.es/webcams/pirineos/), [Albergues y Refugios](https://www.alberguesyrefugios.com/webcams/) (Puntos de alta cota).
- **Tráfico:** [DGT](https://infocar.dgt.es/infocar/), [Mobilitat.ad](https://www.mobilitat.ad/), [Bison Futé](https://www.bison-fute.gouv.fr/).

---

## 3. Índices Heurísticos (Conocimiento Derivado)

Cruzamos las variables anteriores sobre la rejilla H3 para generar métricas de valor:

### A. Riesgo de Aislamiento Logístico (`logistics_isolation_risk`)
Identifica zonas con alta probabilidad de quedar incomunicadas.
- **Cruce:** Pendiente + Distancia a carretera + Espesor de nieve acumulada.

### B. Índice de Aptitud Constructiva (`construction_suitability_index`)
Evalúa la viabilidad de mantenimiento o nuevas obras.
- **Cruce:** Pendiente + Tipo de suelo + Alertas de lluvia extrema.

### C. Resiliencia de Cuenca (`watershed_resilience_index`)
Predice la disponibilidad de recursos hídricos.
- **Cruce:** Superficie de cuenca H3 + Vegetación (NDVI) + Niveles de embalses.
