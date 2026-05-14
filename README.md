# Segmentación de Clientes con Aprendizaje No Supervisado

Proyecto de clustering aplicado a datos de clientes de e-commerce con 7 fuentes de datos (customers, sessions, events, orders, order_items, products, reviews). Se aplican técnicas de aprendizaje no supervisado — K-Means, DBSCAN, t-SNE y PCA — para identificar perfiles de comportamiento de compra.

## Tecnologías

- Python 3.11
- Jupyter Notebook
- scikit-learn, pandas, numpy
- matplotlib, seaborn, plotly
- nbconvert (reportes HTML/PDF)
- LaTeX / xelatex (exportación PDF)

## Instalación

```bash
git clone https://github.com/jairowjp/proyecto-aprendizaje-automatico-no-supervisado.git
cd proyecto3

python -m venv .venv
.venv\Scripts\activate

pip install -r requirements.txt
```

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
│   ├── 01-jj-entorno-y-carga.html
│   ├── 01-jj-entorno-y-carga.pdf
│   ├── 02-jj-eda-clientes.html
│   ├── 02-jj-eda-clientes.pdf
│   ├── 03-jj-clustering-clientes.html
│   ├── 03-jj-clustering-clientes.pdf
│   ├── 04-jj-dbscan-tsne-clientes.html
│   ├── 04-jj-dbscan-tsne-clientes.pdf
│   ├── 05-jj-pca-clientes.html
│   ├── 05-jj-pca-clientes.pdf
│   ├── figures/
│   │   ├── eda_clientes/
│   │   ├── clustering_clientes/
│   │   │   ├── comparacion_distribucion_kmeans_dbscan.png
│   │   │   ├── comparacion_pca_tsne_kmeans.png
│   │   │   └── comparacion_silhouette_kmeans_dbscan.png
│   │   ├── dbscan/
│   │   │   ├── kdistance_graph_dbscan.png
│   │   │   ├── perfil_promedio_clusters_dbscan.png
│   │   │   └── tamano_clusters_dbscan.png
│   │   ├── pca/
│   │   │   ├── pca_biplot.png
│   │   │   ├── pca_clusters_dbscan.png
│   │   │   ├── pca_clusters_kmeans.png
│   │   │   └── pca_scree_plot.png
│   │   └── tsne/
│   │       └── tsne_clusters_dbscan.png
│   └── tables/
│       ├── comparacion_kmeans_dbscan.csv
│       ├── comparacion_silhouette_pca_tsne.csv
│       └── pca_loadings.csv
├── .venv/
├── requirements.txt
└── README.md
```

## Notebooks

| Notebook | Descripción |
|----------|-------------|
| 01-jj-entorno-y-carga | Configuración del entorno, carga y validación de los 7 datasets |
| 02-jj-eda-clientes | Análisis exploratorio: distribuciones, correlaciones y feature engineering |
| 03-jj-clustering-clientes | Segmentación con K-Means, método del codo y análisis Silhouette |
| 04-jj-dbscan-tsne-clientes | Clustering con DBSCAN, gráfico k-distancia y visualización t-SNE |
| 05-jj-pca-clientes | Reducción dimensional con PCA, biplot y proyección de clusters |

## Resultados

- **K-Means** identificó 4 segmentos diferenciados de clientes basados en comportamiento de compra y navegación
- **DBSCAN** detectó clientes atípicos (ruido) no capturados por K-Means, con clusters de densidad variable
- **t-SNE** confirmó visualmente la separación entre clusters en espacio bidimensional
- **PCA** redujo la dimensionalidad del dataset preservando la estructura principal de varianza
- Se generaron tablas comparativas de Silhouette entre K-Means y DBSCAN, y loadings de componentes principales

## Autores

| Nombre | GitHub |
|--------|--------|
| Daniel Fernando Salgado Santamaría | — |
| Jairo Wladimir Jhayya Perlaza | [@jairowjp](https://github.com/jairowjp) |
| Luis Gabriel Salgado Santamaría | — |
| Óscar Paul Naranjo Castro | — |
