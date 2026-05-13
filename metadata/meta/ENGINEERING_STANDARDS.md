# 🛠️ Engineering Standards & DevOps Strategy

Este documento define los estándares técnicos, el enfoque de testing y la infraestructura de despliegue para el **Pyrenees Observatory**.

## 1. Separación Frontend / Backend (Headless Architecture)
Aunque el proyecto es un monorepo por simplicidad de desarrollo, mantenemos una separación clara de responsabilidades:

- **Backend (FastAPI):** Actúa como un motor puramente analítico. No sirve HTML. Expone endpoints que devuelven:
    - **JSON:** Para metadatos y configuraciones.
    - **Apache Parquet / Arrow:** (Optimización) Para transferencia masiva de datos H3 hacia el frontend, permitiendo que Deck.gl los procese eficientemente.
- **Frontend (React + Deck.gl):** Es el "consumidor pesado". Realiza todo el renderizado espacial en el cliente mediante WebGL/WebGPU.

## 2. Enfoque de Testing (Data-Centric Testing)
El testing en un proyecto GIS/Data difiere del software tradicional. Implementaremos:

### A. Testing de Heurísticas (Unit Tests)
- **Objetivo:** Validar que las fórmulas de los índices (aislamiento, resiliencia) se comporten como esperamos.
- **Herramienta:** `pytest`.
- **Caso de uso:** Probar que si `snow_depth = 0`, el `logistics_isolation_risk` no puede ser máximo.

### B. Testing de Integridad Espacial (Geometric Tests)
- **Objetivo:** Asegurar que la "hexagonalización" es correcta.
- **Caso de uso:** Verificar que un punto GPS conocido en Vielha (Val d'Aran) cae exactamente en el `h3_index` esperado de resolución 8.

### C. Data Quality (dbt Tests)
- **Objetivo:** Detectar anomalías en la ingesta de APIs.
- **Herramienta:** `dbt expectations`.
- **Caso de uso:** Alertar si una estación de Meteocat devuelve temperaturas de +60°C o -100°C.

## 3. Entornos y CI/CD

### Entornos (Lifecycle)
1.  **Local (Development):** DuckDB in-memory o archivo local `.db`. Ingesta manual o Prefect local.
2.  **Staging (MotherDuck):** Base de datos compartida en la nube para pruebas de visualización.
3.  **Production (MotherDuck + Vercel/CloudRun):** Despliegue final con datos reales y triggers automáticos.

### Pipeline de GitHub Actions
- **Linting & Style:** `Ruff` para Python, `ESLint` para React.
- **Automation:** Ejecución de `pytest` en cada PR.
- **Data CI:** (Fase avanzada) Validación de modelos dbt antes de mergear a `main`.

## 4. Aspectos No Obvios (Pitfalls a evitar)
- **CORS & Data Volumes:** Servir archivos Parquet grandes requiere una configuración correcta de cabeceras HTTP para que el navegador los descargue por fragmentos (Range requests).
- **H3 Precision:** No mezclar resoluciones en la misma tabla sin una columna que indique el nivel. Por defecto, el MVP operará en **Resolución 8**.
- **Cross-Border Coordinate Shifting:** Siempre proyectar a `EPSG:4326` (WGS84) antes de convertir a H3 para evitar errores de 1-2 metros en la frontera.

---
*Directivas de ingeniería establecidas el 2026-05-07.*
