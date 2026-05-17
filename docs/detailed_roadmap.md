# 🗺️ Roadmap Técnico Detallado (DevOps & Best Practices)

Este documento despliega el plan de ejecución del MVP, integrando en cada hito las mejores prácticas de ingeniería de software, testing (Data & Code) y CI/CD.

## 🏁 Milestone 0: Cimientos y Herramientas Base (Semana 1)
*Objetivo: Establecer el entorno de trabajo robusto, agnostic de la plataforma de CI.*

*   **Paso 0.1:** Configurar gestión de entornos virtuales en Python (`Poetry` o `uv`). Aislar dependencias es innegociable.
*   **Paso 0.2:** Configurar Linters y Formatters. `Ruff` para Python (rapidísimo, reemplaza a flake8, black, isort) y `ESLint` + `Prettier` para Frontend.
*   **Paso 0.3:** Configurar Hooks de Git (`pre-commit`). Ningún código sube roto. Si no pasa el linter o los tests rápidos, el commit se aborta.
*   **Paso 0.4:** Diseñar la estrategia CI/CD. Aunque sea agnostic (GitHub Actions, GitLab CI, o Jenkins), definir los tres pilares:
    *   *Build:* ¿Compila la app? ¿Se construyen las imágenes Docker?
    *   *Test:* Ejecutar suite.
    *   *Deploy:* Automático a Staging (`staging` branch), manual o condicionado a Producción (`main` branch).
*   **🧠 Concepto Clave:** "Fail Fast". Detectar errores en tu máquina antes de que lleguen al pipeline.

## 📐 Milestone 1: El Esqueleto Geoespacial (Semanas 1-2)
*Objetivo: Generar la malla H3 base con TDD (Test-Driven Development).*

*   **Paso 1.1:** Escribir el primer test (`pytest`). *Test: Dado un polígono cuadrado de 1x1 km, la función debe devolver X hexágonos de resolución 8.*
*   **Paso 1.2:** Implementar la lógica con `h3-py` hasta que el test pase.
*   **Paso 1.3:** Crear el DDL en DuckDB. Usar migraciones (ej: `Alembic` si usamos SQLAlchemy, o scripts versionados de SQL puros) para que la BD sea reproducible.
*   **Paso 1.4:** **Integridad Espacial:** Añadir tests que verifiquen que coordenadas extremas del Pirineo caen en los hexágonos correctos y que la proyección no sufre desviación transfronteriza (siempre EPSG:4326 a H3).
*   **🧠 Concepto Clave:** TDD Espacial. No asumas que la librería GIS hace la proyección bien; pruébala contra un Ground Truth.

## 🌍 Milestone 2: Enriquecimiento y Data Quality (Semana 3)
*Objetivo: Ingestar topografía (Copernicus DEM) y asegurar la calidad del dato.*

*   **Paso 2.1:** Pipeline de ingesta. (Python script aislado).
*   **Paso 2.2:** **Data Testing:** Almacenar datos en bruto en una capa `raw`. Aplicar tests de expectativas de datos (ej: `great_expectations` o validaciones Pydantic): *La elevación no puede ser negativa en el Pirineo. La pendiente debe estar entre 0 y 90 grados.*
*   **Paso 2.3:** Transformar (asignar elevación al hexágono) y guardar en la capa `curated`.
*   **Paso 2.4:** Configurar Docker para levantar DuckDB localmente de forma consistente en cualquier máquina.
*   **🧠 Concepto Clave:** Patrón Medallón (Raw, Bronze, Silver, Gold). Nunca sobrescribas los datos crudos originales.

## 🌩️ Milestone 3: Ingesta Dinámica y Orquestación (Semanas 4-5)
*Objetivo: Conectar APIs (Meteocat/AEMET) de forma resiliente.*

*   **Paso 3.1:** Implementar conectores API con manejo de errores (Retries, Circuit Breakers usando la librería `tenacity`). Si Meteocat cae, el pipeline no debe colapsar.
*   **Paso 3.2:** Tests de integración (Mocks). Usar librerías como `responses` o `vcrpy` para simular respuestas de la API de Meteocat y probar tu lógica de parseo sin depender de la red externa.
*   **Paso 3.3:** **Orquestación:** Configurar tareas periódicas. (Prefect local o un simple `APScheduler` dockerizado).
*   **🧠 Concepto Clave:** Observabilidad del Pipeline. Si la ingesta falla a las 3 AM, debes tener un log estructurado (JSON logging) que te diga exactamente por qué.

## 🧠 Milestone 4: Backend API Analítica (Semana 6)
*Objetivo: Exponer datos eficientemente (Parquet) con CI.*

*   **Paso 4.1:** FastAPI endpoints.
*   **Paso 4.2:** **Testing de Heurísticas:** Tests unitarios críticos. *Test: Si la nieve es > 50cm y la pendiente > 30 grados, el `logistics_isolation_risk` debe ser "HIGH".*
*   **Paso 4.3:** Optimización de transferencia. Asegurar soporte de Byte-Range Requests en el backend para servir archivos Parquet al frontend eficientemente.
*   **Paso 4.4:** Actualizar el pipeline CI/CD: Ahora los tests del backend corren contra una base de datos efímera (SQLite in-memory o un DuckDB temporal levantado por el pipeline).
*   **🧠 Concepto Clave:** Continuous Integration (CI). Fusionar código a la rama principal con confianza porque los tests automáticos te respaldan.

## 🎨 Milestone 5: Frontend y Gemelo Digital (Semanas 7-8)
*Objetivo: Visualización masiva con Deck.gl y estado robusto.*

*   **Paso 5.1:** React + Vite. Uso estricto de componentes funcionales puros.
*   **Paso 5.2:** Gestión de Estado con `Zustand`. Mantener el estado global de UI separado de la carga masiva de datos espaciales.
*   **Paso 5.3:** **Testing Frontend:** Tests de componentes con `React Testing Library`. Comprobar que los controles (sliders, toggles) renderizan correctamente y despachan las acciones adecuadas. No testear el renderizado 3D de Deck.gl (muy complejo), testear la UI que lo controla.
*   **Paso 5.4:** Despliegue de Frontend (CD). Generar el `build` estático. Si es Docker, empaquetarlo en un Nginx ligero (`nginx:alpine`).
*   **🧠 Concepto Clave:** Headless Components & Estado Derivado. Mantén la lógica de negocio (qué datos se muestran) separada de la capa de renderizado visual.

---
*Roadmap revisado por Arquitectura para incluir el ciclo de vida de desarrollo de software (SDLC) completo.*
