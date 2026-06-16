# Análisis de datos — Trabajo práctico integrador

**CEIA · FIUBA — Análisis de Datos (2B 2026)**

Análisis exploratorio (EDA) y preparación de datos para un problema de Machine Learning
supervisado sobre el dataset **Crímenes reportados en Chicago — 2025**. Siguiendo la
consigna, el trabajo **analiza y prepara los datos; no entrena ningún modelo**.

## Problema de ML planteado

- **Tipo:** clasificación binaria.
- **Target:** `Arrest` — ¿el delito reportado derivó en un arresto?
- **Desafío central:** la clase positiva es minoritaria (~16 %), por lo que el dataset es
  **desbalanceado**.

## Estructura del repositorio

```
.
├── datasets/
│   └── Crimes_-_2025_20260511.csv            # Dataset original (Chicago Data Portal)
├── notebooks/
│   └── TP_integrador_crimenes_chicago.ipynb  # Notebook integradora (ejecutada)
├── pyproject.toml
└── README.md
```

## Contenido de la notebook

1. **Exploración y comprensión** — dimensiones, tipos de variables, cardinalidad y diversidad
   (entropía de Shannon, moda).
2. **Patrones y distribuciones** — distribución del target, tipos de delito (y su jerarquía
   `Primary Type` → `Description`), patrones temporales, mapa geográfico y medidas de asociación
   (Cramér's V, punto-biserial).
3. **Outliers** — por qué no aplica la detección estadística de outliers sobre las coordenadas.
4. **Faltantes** — recuento, `missingno` y análisis del mecanismo (MCAR / MAR).
5. **Procesamiento y limpieza** — deduplicación, descarte de columnas redundantes, *feature
   engineering* temporal y split estratificado **sin *data leakage***. Tratamiento de faltantes
   ajustado en train: mediana por zona (`Beat`) en las coordenadas, categoría `"UNKNOWN"` para
   el lugar y eliminación de las pocas filas MCAR.
6. **Codificación, escalado y balance** — *target encoding*, codificación cíclica de la hora,
   estandarización y balanceo de clases con **SMOTE** (solo en train).
7. **Reducción de dimensionalidad** — selección de features por filtros (ANOVA F, chi²,
   información mutua) y **PCA** (documentado como alternativa).
8. **Conclusiones** — features finales y dataset listo para entrenar.

## Dataset

| | |
|---|---|
| Fuente | [Chicago Data Portal — Crimes 2025](https://data.cityofchicago.org/Public-Safety/Crimes-2025/t7ek-mgzi/about_data) |
| Observaciones | 237.193 |
| Variables | 22 |
| Período | Año 2025 |

## Cómo ejecutar

El proyecto usa [`uv`](https://docs.astral.sh/uv/) (ver `pyproject.toml`).

```bash
# Instalar dependencias
uv sync

# Abrir la notebook (ya viene ejecutada, con sus salidas)
uv run jupyter lab notebooks/TP_integrador_crimenes_chicago.ipynb
```
