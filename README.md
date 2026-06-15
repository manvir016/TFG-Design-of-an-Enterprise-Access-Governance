# SAP Access Governance Framework — Role Mining Pipeline

**Final Degree Project (TFG)**
Mathematical Engineering in Data Science — Universitat Pompeu Fabra, 2025–2026
**Author:** Manvir Kaur Singh

---

## Overview

This repository contains the implementation of a data-driven role mining pipeline for SAP ERP environments. The pipeline derives a business role model from real SAP transaction usage data, clusters job titles by behaviour, and maps them to SAP standard roles using semantic matching and a greedy set cover algorithm with SoD constraints.

The selected clustering method is **HDBSCAN-Guided** (K=51, Silhouette=0.525, ARI=0.926, BP Coherence=61.2%), chosen for its balance between geometric quality and business alignment.

---

## Repository Structure

```
.
├── PrimeraParteDataProc.ipynb             # Phase 1: Data extraction and preprocessing
├── SegundaParteClustering_JobTitle.ipynb  # Phase 2: Dimensionality reduction and clustering
└── TerceraParteRoleMapping.ipynb          # Phase 3: SAP role matching and set cover
```

> Input and output datasets are not included in this repository, it is only for visualisation purpose. Every cell is already run where the results can be seen

---

## Pipeline

The pipeline is divided into three phases:

1. **Data Preprocessing** (`PrimeraParteDataProc.ipynb`)
   - Loads raw SAP transaction usage logs
   - Aggregates data at job-title level
   - Applies TF-IDF weighting and L2 normalisation

2. **Clustering** (`SegundaParteClustering_JobTitle.ipynb`)
   - Evaluates three dimensionality reduction strategies: SVD, UMAP, SVD+UMAP
   - Compares nine clustering methods: K-Means, Bisecting K-Means, GMM, HDBSCAN, FCM, LFM, COP-KMeans, HDBSCAN-Guided, FCMCL
   - Selects HDBSCAN-Guided as the final method based on internal and business metrics

3. **Role Mapping** (`TerceraParteRoleMapping.ipynb`)
   - Builds cluster profiles from transaction usage
   - Filters SAP Business Catalogues by semantic similarity (Word2Vec)
   - Applies greedy set cover with SoD-aware stopping criterion

---

