# Segmentación de Clientes con Aprendizaje No Supervisado

Proyecto de clustering aplicado a datos de clientes de e-commerce con 7 fuentes de datos (customers, sessions, events, orders, order_items, products, reviews). Se aplican técnicas de aprendizaje no supervisado — K-Means, DBSCAN, t-SNE y PCA — para identificar perfiles de comportamiento de compra sobre una base de **20,000 clientes**.

## Justificación

La segmentación de clientes es una necesidad estratégica en negocios de e-commerce: permite identificar grupos con comportamientos de compra similares y diseñar estrategias diferenciadas de marketing, retención y activación. Los métodos supervisados requieren etiquetas previas que en este contexto no existen, por lo que el aprendizaje no supervisado es la alternativa natural. Se aplican K-Means y DBSCAN como algoritmos de clustering complementarios — el primero para segmentación compacta y el segundo para detección de outliers — y se complementan con PCA y t-SNE para reducción dimensional y validación visual de los resultados.

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

## Análisis de Resultados

### K-Means

El método del codo y el Silhouette Score indican que **k=2** es el número óptimo de clusters (Silhouette: **0.30**). Los dos segmentos identificados son:

- **Cluster 0 — Clientes de alto valor** (35% de la base): mayor número de sesiones (media: 7.65), más órdenes (media: 2.86), ingreso total elevado (media: USD 476.67), ticket promedio alto (media: USD 193.40) y mayor número de reseñas (media: 1.21).
- **Cluster 1 — Clientes de menor valor** (65% de la base): menor frecuencia de sesiones (media: 5.10), pocas órdenes (media: 1.04), ingreso total reducido (media: USD 87.74), ticket promedio bajo (media: USD 63.35) y reseñas casi inexistentes (media: 0.18).

### DBSCAN

DBSCAN detectó clientes atípicos (ruido) no capturados por K-Means y generó clusters de densidad variable. La separación entre grupos es coherente con la estructura observada en K-Means, confirmando la robustez de la segmentación.

### PCA

Los dos primeros componentes principales explican el **60.76%** de la varianza total (PC1: 43.22%, PC2: 17.53%). Las variables de mayor contribución en PC1 son `gross_revenue_usd` (0.56), `n_orders` (0.51) y `avg_order_value_usd` (0.42), interpretándose como una **dimensión de valor económico y volumen de compras**. PC2 contrasta `avg_order_value_usd` (0.65) con `n_sessions` (−0.52), capturando el **contraste entre ticket alto y frecuencia de visitas**. La proyección de clusters en el plano PCA confirma la separación visual entre perfiles de cliente.

### t-SNE

La visualización t-SNE confirmó la separación entre clusters en espacio bidimensional, validando que las diferencias entre segmentos son estructurales y no un artefacto del algoritmo.

## Autores

| Nombre | GitHub |
|--------|--------|
| Daniel Fernando Salgado Santamaría | — |
| Jairo Wladimir Jhayya Perlaza | [@jairowjp](https://github.com/jairowjp) |
| Luis Gabriel Salgado Santamaría | — |
| Óscar Paul Naranjo Castro | — |
