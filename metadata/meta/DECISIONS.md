# 📝 Decision Log (ADR)

## 📑 Índice
- [2026-05-07: Inicialización y Elección de H3](#2026-05-07-inicialización-y-elección-de-h3)

---

## 2026-05-07: Inicialización y Elección de H3

### Contexto
Necesitamos normalizar datos de múltiples fuentes transfronterizas (España/Francia) con diferentes sistemas de coordenadas.

### Decisión
Uso de **H3** como sistema de indexación espacial primario.

### Consecuencias
- **Positivas:** Análisis espacial basado en joins de tablas, fácil agregación jerárquica, independencia de la proyección original.
- **Riesgos:** Pérdida de precisión milimétrica (aceptable para este caso), curva de aprendizaje para el usuario en funciones de H3.
