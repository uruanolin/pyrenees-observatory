# 🛠️ Estándares de Ingeniería y Testing

Guía de buenas prácticas y protocolos de calidad para asegurar que el proyecto sea robusto y profesional.

## 1. Separación Frontend / Backend
Mantenemos una arquitectura **Headless**:
- **Backend (FastAPI):** Un motor analítico puro. Expone datos en JSON y Parquet.
- **Frontend (React + Deck.gl):** Encargado de la visualización pesada mediante renderizado por GPU.

## 2. Estrategia de Testing (Data-Centric)
Implementamos tres niveles de pruebas específicos para este dominio:

### A. Unit Testing (Heurísticas)
Validación de las fórmulas matemáticas de nuestros índices.
- *Ejemplo:* Asegurar que el riesgo de aislamiento se calcula correctamente bajo condiciones extremas.

### B. Geometric Testing (Integridad H3)
Garantizar que la "hexagonalización" de las coordenadas GPS es precisa y consistente.

### C. Data Quality (dbt Tests)
Detección de anomalías en los datos crudos provenientes de APIs externas antes de que lleguen al modelo final.

## 3. Gestión de Entornos
1.  **Local (Dev):** Base de datos DuckDB local y hot-reload.
2.  **Staging:** Pruebas de visualización con MotherDuck (Cloud).
3.  **Production:** Datos reales y despliegue final optimizado.

## 4. Pipeline de CI/CD
Usamos **GitHub Actions** para:
- Ejecutar linters (`Ruff`, `ESLint`).
- Correr la suite de tests automáticos en cada commit/PR.
