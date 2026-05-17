# 🏛️ Arquitectura del Sistema

Esta guía detalla la arquitectura técnica del **Pyrenees Observatory**, justificando las decisiones clave para el procesamiento de datos geoespaciales a gran escala.

## 1. El Rol de H3 (Uber Hexagonal Grid)
H3 es el "pegamento" de este proyecto. Su función es normalizar datos de múltiples fuentes transfronterizas (España/Francia) que originalmente usan diferentes proyecciones.

### Beneficios Clave:
- **Normalización Universal:** Convierte polígonos complejos y puntos GPS en identificadores de celdas SQL.
- **Relaciones Espaciales Rápidas:** Permite realizar análisis de vecindad y agregaciones jerárquicas mediante operaciones de tablas SQL, sin cálculos trigonométricos costosos.
- **Eficiencia:** Reduce la carga computacional en el frontend al tratar con mallas regulares.

## 2. Motor de Datos: DuckDB + Parquet
Hemos elegido **DuckDB** como el motor analítico principal por su velocidad extrema en consultas locales y su integración nativa con el formato **Parquet**.

### Flujo de Datos:
1.  **Ingesta (Python/Prefect):** Descarga datos de APIs y DEMs.
2.  **Procesamiento (SQL/DuckDB):** Proyecta los datos a índices H3 y realiza cruces.
3.  **Transferencia:** Los datos se sirven al frontend en formato Parquet/Arrow para minimizar el tamaño de red y maximizar el rendimiento de Deck.gl.

## 3. Sensores Visuales (Webcams)
El sistema incluye una red de webcams para la validación visual de los índices dinámicos (Ground Truth).
- **Backend Proxy:** FastAPI actúa como un proxy para servir snapshots de cámaras externas, evitando problemas de CORS y preparando el camino para futuro análisis de imagen con Python.
