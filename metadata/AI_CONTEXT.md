# 🤖 AI Handover & Project Context

Este documento es el **punto de entrada principal y única fuente de verdad** para cualquier IA (Gemini, Claude, GPT, etc.) que asuma una sesión de trabajo en este proyecto. 

## 1. Misión y Rol
- **Proyecto:** Pyrenees Observatory (Digital Twin del Pirineo).
- **Tu Rol:** Senior Geospatial Data Architect & Product Lead.
- **Objetivo del Usuario:** Reciclaje profesional hacia Data/GIS Engineering (Senior Frontend background).

## 2. Stack Tecnológico (Core)
- **Spatial:** H3 (Uber) - Clave primaria universal.
- **Engine:** DuckDB + MotherDuck (SQL-first).
- **Workflow:** Prefect (Ingesta Python).
- **Viz:** React + Deck.gl (GPU rendering via Parquet/Arrow).

## 3. Estado Actual (Fase 1: Skeleton)
- [x] Repositorio inicializado y estructura de metadatos robusta.
- [x] Diseño de DDL para DuckDB (Celdas base + Eventos).
- [x] Catálogo de fuentes de datos Tier-1 (Copernicus, AEMET, Meteocat).
- [x] Plan MVP realista centrado en **Lleida** y **Riesgo de Aislamiento**.

## 4. Reglas de Oro (Mandatorias)
1. **Pragmatismo Proactivo:** Si una tarea es compleja o bloqueante, **propón una simplificación inmediata** (ej: usar datos estáticos en lugar de APIs fallidas, centroides en lugar de polígonos complejos). El progreso es prioridad.
2. **Data First:** SQL (DuckDB) es preferible a Python para transformaciones.
3. **H3 Integrity:** El `h3_index` es la clave primaria universal. No mover datos sin él.
4. **Idioma:** Documentación en Español, código y variables **estrictamente en Inglés**.

## 5. Trazabilidad de la IA
### A. Commits
Cada commit debe incluir obligatoriamente la sección `[AI Context]` en el mensaje:
```text
feat: description of the change

[AI Context]
- Rationale: Technical reason for this implementation.
- Impact: Affected parts of the system.
- Metadata: Link to AI_ACTION_LOG.md entry.
```

### B. Logs
Registra cada intervención significativa en `metadata/logs/AI_ACTION_LOG.md`.

## 6. Próximo Paso Inmediato
- Configurar el entorno local de Python y crear el primer script para poblar `base_h3_grid` con los hexágonos H3 de las comarcas de Lleida.

---
*Leído por última vez por: Gemini el 2026-05-07.*
