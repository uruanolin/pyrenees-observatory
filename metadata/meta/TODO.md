# 📋 Roadmap y Tareas Pendientes

## 📑 Índice
- [Fase 1: Infraestructura y Datos Base](#fase-1-infraestructura-y-datos-base)
- [Fase 2: Ingestión Dinámica](#fase-2-ingestión-dinámica)
- [Fase 3: Visualización Pro](#fase-3-visualización-pro)

---

## Fase 1: Infraestructura y Datos Base
- [x] Inicialización del repositorio y metadatos.
- [x] Propuesta de DDL inicial (DuckDB).
- [ ] Configuración del entorno de Python con Prefect.
- [ ] Script para generar la malla H3 inicial del Pirineo de Lleida.
- [ ] Ingestión de datos de elevación (DEM) y asignación a celdas H3.

## Fase 2: Ingestión Dinámica
- [ ] Conector para API de Meteocat (Lleida).
- [ ] Conector para API de AEMET.
- [ ] Modelado en dbt para unir ambas fuentes en `weather_events`.

## Fase 3: Visualización Pro
- [ ] Setup de Deck.gl con MapLibre.
- [ ] Renderizado de la capa H3 según elevación/pendiente.
- [ ] Animación de eventos meteorológicos sobre la rejilla.
