# 📋 Roadmap y Tareas Pendientes

## 📑 Índice
- [Fase 1: Infraestructura y Datos Base](#fase-1-infraestructura-y-datos-base)
- [Fase 2: Ingestión Dinámica](#fase-2-ingestión-dinámica)
- [Fase 3: Visualización Pro](#fase-3-visualización-pro)

---

## Fase 1: Infraestructura y Datos Base
- [x] Inicialización del repositorio y metadatos.
- [x] Propuesta de DDL inicial (DuckDB).
- [x] Catálogo de fuentes de datos Tier-1 y diseño de índices.
- [ ] Configuración del entorno de Python con Prefect.
- [ ] Ingesta Batch: Copernicus DEM -> `base_h3_grid`.
- [ ] Ingesta Batch: Red vial (IGN) -> Atributos de proximidad en H3.

## Fase 2: Ingestión Dinámica e Índices
- [ ] Conector para API de Meteocat (Lleida).
- [ ] Conector para API de AEMET.
- [ ] Implementación de `logistics_isolation_risk` (cruce nieve + pendiente + vial).
- [ ] Implementación de `construction_suitability_index` (pendiente + suelo + lluvia).

## Fase 3: Visualización Pro
- [ ] Setup de Deck.gl con MapLibre.
- [ ] Renderizado de la capa H3 según elevación/pendiente.
- [ ] Animación de eventos meteorológicos sobre la rejilla.
