# 🤖 AI Handover & Project Context

Este documento es el **punto de entrada principal** para cualquier IA (Gemini, Claude, GPT, etc.) que asuma una sesión de trabajo en este proyecto. Consolida el estado actual, las reglas críticas y los objetivos inmediatos para maximizar la eficiencia del contexto.

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

## 4. Reglas de Oro (Para la IA)
1. **Pragmatismo Proactivo:** Si una tarea es compleja, propón una simplificación inmediata. El progreso del usuario es lo más importante.
2. **SQL > Python:** Realiza transformaciones en DuckDB siempre que sea posible.
3. **Commit Metadata:** Incluye siempre la sección `[AI Context]` en los mensajes de commit.
4. **Log Actions:** Registra cada intervención en `metadata/logs/AI_ACTION_LOG.md`.

## 5. Próximo Paso Inmediato
- Configurar el entorno local de Python y crear el primer script para poblar `base_h3_grid` con los hexágonos H3 de las comarcas de Lleida.

---
*Leído por última vez por: Gemini el 2026-05-07.*
