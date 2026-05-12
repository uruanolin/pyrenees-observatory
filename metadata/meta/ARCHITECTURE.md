# 🏛️ Architecture Analysis: Pyrenees Observatory

## 📑 Índice
- [1. Análisis del Proyecto](#1-análisis-del-proyecto)
- [2. El Rol de H3](#2-el-rol-de-h3)
- [3. Estrategia de Datos](#3-estrategia-de-datos)
- [4. Catálogo de Fuentes e Índices](./DATA_SOURCES.md)
- [5. Propuesta Inicial de DDL (DuckDB)](#5-propuesta-inicial-de-ddl-duckdb)

---

## 1. Análisis del Proyecto
El **Pyrenees Observatory** resuelve el problema de la fragmentación de datos en zonas transfronterizas. España y Francia usan diferentes proyecciones y formatos. Al proyectar todo a una rejilla hexagonal **H3**, convertimos un problema geométrico complejo en un problema de "Join" de tablas SQL masivo y eficiente.

## 2. El Rol de H3
H3 es el "pegamento". Cada celda hexagonal tiene un ID único. 
- **Resolución sugerida:** Nivel 8 (~0.7 km²) para visión regional, Nivel 9-10 para análisis de detalle.
- **Ventaja:** Permite sumarización rápida (buckets) y análisis de vecindad sin cálculos trigonométricos costosos.

## 3. Estrategia de Datos
Usamos **DuckDB** por su capacidad de leer archivos Parquet y GeoParquet de forma nativa a velocidad extrema. **MotherDuck** nos da la persistencia en la nube sin configurar servidores pesados. Consulta el [Catálogo de Fuentes](./DATA_SOURCES.md) para más detalle.

## 4. Propuesta Inicial de DDL (DuckDB)

Para el MVP centrado en el **Pirineo de Lleida**, propongo estas tablas base:

```sql
-- Central table for H3 Cells with static attributes
CREATE TABLE base_h3_grid (
    h3_index_8 VARCHAR PRIMARY KEY, -- Resolution 8
    elevation_meters DOUBLE,
    slope_degrees DOUBLE,
    aspect_degrees DOUBLE,
    land_cover_code INTEGER,
    country_code VARCHAR(2), -- 'ES' or 'FR'
    admin_region_1 VARCHAR, -- Province/Department
    admin_region_2 VARCHAR, -- Municipality
    centroid_lat DOUBLE,
    centroid_lon DOUBLE
);

-- Table for dynamic meteorological events
CREATE TABLE weather_events (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    h3_index_8 VARCHAR,
    timestamp TIMESTAMP,
    temperature_celsius DOUBLE,
    precipitation_mm DOUBLE,
    snow_depth_cm DOUBLE,
    wind_speed_ms DOUBLE,
    source_api VARCHAR -- 'AEMET', 'METEOCAT', 'METEOFRANCE'
);

-- Indices for performance
CREATE INDEX idx_weather_h3 ON weather_events (h3_index_8);
CREATE INDEX idx_weather_time ON weather_events (timestamp);
```

### Racional de Diseño:
- **`base_h3_grid`**: Almacena lo que no cambia (o cambia poco). Es el "esqueleto".
- **`weather_events`**: Almacena el "latido" del territorio. La relación es 1 a N.
- **UUID**: Para los eventos, permitiendo ingestas distribuidas sin colisiones.
