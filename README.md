# Proyecto 3 — Clustering y Reducción de Dimensionalidad sobre Comportamiento de Clientes

## Integrantes

| Nombre | Rol |
|--------|-----|
| Daniel Fernando Salgado Santamaria | Investigador |
| Jairo Wladimir Jhayya Perlaza | Investigador |
| Luis Gabriel Salgado Santamaria | Investigador |
| Oscar Paul Naranjo Castro | Investigador |

**Fecha:** Mayo 2026  
**Materia:** Aprendizaje Automático / Machine Learning  

---

## Descripción del Proyecto

Este proyecto aplica técnicas de **aprendizaje no supervisado** sobre un dataset de comportamiento de clientes de una plataforma de e-commerce. El objetivo es identificar perfiles de cliente mediante algoritmos de clustering (K-Means y DBSCAN), y visualizar la estructura de los datos en espacios reducidos utilizando t-SNE y PCA.

### Pregunta central

> ¿Es posible identificar perfiles de clientes diferenciados a partir de su comportamiento de navegación, compra y retroalimentación?

---

## Dataset

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Kaggle (repositorio público) |
| **Archivos** | 7 archivos CSV independientes |
| **Tamaño total** | ~10 millones de registros en todas las tablas |

### Archivos fuente (`data/raw/`)

| Archivo | Registros | Columnas | Descripción |
|---------|-----------|----------|-------------|
| `customers.csv` | 20,000 | 7 | Datos demográficos de clientes (edad, país, fecha de registro) |
| `sessions.csv` | 120,000 | 6 | Sesiones de navegación por cliente y dispositivo |
| `events.csv` | 760,958 | 10 | Eventos de interacción dentro de cada sesión |
| `orders.csv` | 33,580 | 10 | Órdenes de compra (método de pago, descuento, total) |
| `order_items.csv` | 59,163 | 5 | Detalle de productos por orden |
| `products.csv` | 1,197 | 6 | Catálogo de productos con categoría y precio |
| `reviews.csv` | 10,780 | 6 | Reseñas de clientes con rating y texto |

## Estructura del Repositorio

```text
proyecto3/
├── data/
│   ├── raw/                        # Archivos CSV originales (no modificar)
│   │   ├── customers.csv
│   │   ├── sessions.csv
│   │   ├── events.csv
│   │   ├── orders.csv
│   │   ├── order_items.csv
│   │   ├── products.csv
│   │   └── reviews.csv
│   ├── interim/                    # Datos intermedios del procesamiento
│   └── processed/                  # Datos listos para modelado
│       └── customer_features.csv
├── notebooks/
│   ├── 01-jj-entorno-y-carga.ipynb
│   ├── 02-jj-eda-clientes.ipynb
│   ├── 03-jj-clustering-clientes.ipynb
│   ├── 04-jj-dbscan-tsne-clientes.ipynb
│   └── 05-jj-pca-clientes.ipynb
├── reports/
│   ├── figures/
│   │   ├── eda_clientes/
│   │   ├── clustering_clientes/
│   │   ├── dbscan/
│   │   └── pca/
│   └── tables/
├── .venv/
├── requirements.txt
└── README.md
```

## Instalación del Entorno

```powershell
# 1. Clonar el repositorio
git clone <url-del-repositorio>
cd proyecto3

# 2. Crear entorno virtual
python -m venv .venv

# 3. Activar entorno virtual (Windows)
.venv\Scripts\activate

# 4. Instalar dependencias
pip install -r requirements.txt
```

### Dependencias principales

```txt
pandas>=2.0
numpy>=1.24
matplotlib>=3.7
seaborn>=0.12
scikit-learn>=1.3
jupyterlab>=4.0
```

---

## Pipeline de Ejecución

Los notebooks deben ejecutarse en orden:

| Notebook | Propósito | Outputs |
|----------|-----------|---------|
| `01` | Verificación del entorno, carga de CSVs | `tables/dataset_summary.csv` |
| `02` | EDA, feature engineering, `customer_features` | `processed/customer_features.csv`, figuras EDA |
| `03` | K-Means, selección de k óptimo | Elbow, silhouette, perfiles |
| `04` | DBSCAN + t-SNE | Grids de búsqueda, clusters DBSCAN, t-SNE 2D |
| `05` | PCA + comparación con t-SNE | Scree plot, biplot, loadings |

---

## Variables del Dataset Consolidado

| Variable | Descripción |
|----------|-------------|
| `customer_id` | Identificador único del cliente |
| `age` | Edad del cliente (18–75 años) |
| `n_sessions` | Número total de sesiones |
| `n_orders` | Número total de órdenes |
| `gross_revenue_usd` | Ingresos brutos generados (USD) |
| `avg_order_value_usd` | Ticket promedio por orden (USD) |
| `n_reviews` | Número de reseñas escritas |

---

## Modelos Implementados

### K-Means
- Selección de k con método del codo + Silhouette Score → **k=2 óptimo**
- Preprocesamiento: StandardScaler

### DBSCAN
- Parámetros óptimos: `eps=1.11`, `min_samples=5`
- Clasifica outliers como ruido (clase -1)

### PCA
- 2 componentes para visualización 2D
- Análisis de loadings e interpretación de ejes

### t-SNE
- `perplexity=40`, `max_iter=1000`, `init='pca'`
- Preserva vecindad local para visualización cualitativa

---

## Resultados Principales

### Perfiles identificados (K-Means, k=2)

| Cluster | Perfil | Características |
|---------|--------|-----------------|
| Cluster 0 | Cliente ocasional | Baja frecuencia, ticket bajo, pocas reseñas |
| Cluster 1 | Cliente activo | Alta frecuencia, mayores ingresos, más reseñas |

### K-Means vs DBSCAN

| Dimensión | K-Means | DBSCAN |
|-----------|---------|--------|
| Tipo | Partición (centroide) | Densidad |
| Detecta outliers | No | Sí (clase -1) |
| Forma de clusters | Esférica | Arbitraria |
| Requiere k | Sí | No |

---

## Exportación a PDF

```powershell
jupyter nbconvert --to pdf --no-prompt --output-dir reports notebooks/<nombre>.ipynb
```

---

## Licencia

Proyecto académico — uso educativo exclusivo.

