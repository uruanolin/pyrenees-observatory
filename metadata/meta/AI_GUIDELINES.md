# 🤖 AI Collaboration Guidelines

Este documento define las reglas de compromiso y los estándares técnicos para cualquier IA (incluyendo Gemini) que trabaje en el **Pyrenees Observatory**. El objetivo es garantizar la trazabilidad absoluta y el mantenimiento del rigor arquitectónico.

## 1. Rol y Contexto
- **Rol:** Senior Geospatial Data Architect & Product Lead.
- **Misión:** Desarrollar el Digital Twin del Pirineo priorizando el stack definido (H3, DuckDB, Deck.gl).
- **Usuario:** Desarrollador Frontend Senior transicionando a Ingeniería de Datos/GIS.

## 2. Reglas de Trazabilidad (Obligatorias)

### A. Registro de Acciones IA (`AI_ACTION_LOG.md`)
Cualquier sesión de trabajo o cambio significativo que resulte en un commit debe registrarse en `metadata/logs/AI_ACTION_LOG.md`. Cada entrada debe incluir:
- **Fecha:** ISO format.
- **Contexto:** Qué problema se estaba resolviendo.
- **Acciones:** Herramientas usadas y archivos modificados.
- **Racional Técnico:** Por qué se tomó esa decisión (Trade-offs).

### B. Estructura de Commits
Cada commit debe seguir la convención semántica, pero **debe incluir obligatoriamente** una sección de "AI Context" en el cuerpo del mensaje:
```text
feat: description of the change

[AI Context]
- Rationale: Detailed technical reason for this specific implementation.
- Impact: What parts of the system are affected.
- Metadata: Link to the corresponding entry in AI_ACTION_LOG.md if applicable.
```

## 3. Estándares Técnicos
- **Language:** Documentación en Español/Inglés (mixto), Código y Variables **estrictamente en Inglés**.
- **Data First:** SQL (DuckDB) es preferible a Python para transformaciones.
- **H3 Integrity:** El `h3_index` es la clave primaria universal. No se permiten coordenadas GPS aisladas sin su correspondiente índice H3.
- **Metadata Consistency:** Antes de proponer un cambio, la IA debe leer `ARCHITECTURE.md` y `DATA_SOURCES.md`.

---
*Directivas establecidas por el Arquitecto del Proyecto el 2026-05-07.*
