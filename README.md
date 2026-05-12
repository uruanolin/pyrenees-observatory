# 🏔️ Pyrenees Observatory (Modelo Vivo Computable del Pirineo)

Bienvenido al **Pyrenees Observatory**, un sistema de observabilidad territorial diseñado para modelar el "estado vivo" del Pirineo (España/Francia). Este proyecto utiliza índices espaciales jerárquicos (**H3**) para normalizar datos fragmentados y derivar conocimiento mediante índices heurísticos de alta resolución.

---

## 📂 Índice
- [1. Visión y Misión](#1-visión-y-misión)
- [2. Arquitectura Técnica](#2-arquitectura-técnica)
- [3. Principios de Diseño](#3-principios-de-diseño)
- [4. Estructura de Metadatos](#4-estructura-de-metadatos)
- [5. Primeros Pasos](#5-primeros-pasos)

---

## 1. Visión y Misión
Transformar el Pirineo de un mapa de capas estáticas a un **Modelo Vivo Computable**. No solo visualizamos donde están las cosas; computamos el estado del territorio cruzando datos meteorológicos, topográficos y de movilidad para predecir riesgos y optimizar la toma de decisiones.

## 2. Arquitectura Técnica
El stack está elegido para maximizar la velocidad analítica y la visualización masiva:

- **Spatial Indexing:** [H3 (Uber)](https://h3geo.org/) como malla de normalización universal.
- **Data Stack:**
    - **Ingestion:** Python ([Prefect](https://www.prefect.io/)) para APIs transfronterizas.
    - **Storage/Compute:** [DuckDB](https://duckdb.org/) + [MotherDuck](https://motherduck.com/) (Analítica) y [PostGIS](https://postgis.net/) (Geometría compleja).
    - **Transformation:** [dbt](https://www.getdbt.com/) para modelado y estandarización.
- **Visualization:** [Deck.gl](https://deck.gl/) (GPU rendering), [MapLibre](https://maplibre.org/) / [Cesium](https://cesium.com/) (3D).

## 3. Principios de Diseño
- **Estado vs Capas:** Modelamos el estado $T$ del territorio.
- **Índices Compuestos:** Creación de heurísticas como *Resilience Index* o *Isolation Risk*.
- **Normalización Transfronteriza:** Resolución de heterogeneidad de fuentes mediante H3.

## 4. Estructura de Metadatos
Siguiendo las buenas prácticas de organización, este repositorio mantiene una memoria activa en `/metadata`:
- **[MVP_PLAN.md](./metadata/meta/MVP_PLAN.md):** Hoja de ruta simplificada y realista para el prototipo.
- **[AI_GUIDELINES.md](./metadata/meta/AI_GUIDELINES.md):** 🤖 Reglas y estándares para la colaboración con IAs.
- **[ARCHITECTURE.md](./metadata/meta/ARCHITECTURE.md):** Análisis profundo y diseño del sistema.
- **[DATA_SOURCES.md](./metadata/meta/DATA_SOURCES.md):** Catálogo de fuentes e índices heurísticos.
- **[DECISIONS.md](./metadata/meta/DECISIONS.md):** Log de decisiones técnicas (ADR).
- **[TODO.md](./metadata/meta/TODO.md):** Roadmap y backlog técnico.
- **[AI_ACTION_LOG.md](./metadata/logs/AI_ACTION_LOG.md):** 📜 Historial de acciones y razonamiento de la IA.

## 5. Primeros Pasos
Para iniciar el entorno de desarrollo local (DuckDB):
*(Instrucciones de instalación próximamente)*

---
*Proyecto liderado por un Arquitecto de Datos Geospatiales Senior.*
