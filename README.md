# Sound Clustering & HMMs – Formative 1

## Overview

This project explores unsupervised learning techniques to cluster an **unlabeled dataset of sound recordings**. By extracting **Mel Spectrogram** features, reducing dimensionality using **PCA** and **t-SNE**, and applying **K-Means** and **DBSCAN**, we aim to uncover hidden structures in the sound data and evaluate clustering performance using standard metrics.

## Objectives

- Extract meaningful features from sound data using **Librosa’s Mel Spectrogram**.
- Apply **dimensionality reduction** (PCA and t-SNE) to improve visualizations and clustering quality.
- Compare **K-Means vs DBSCAN** based on silhouette score, Davies-Bouldin index, and clustering visualization.
- Evaluate the impact of dimensionality reduction and justify its importance.
- Ensure modular, DRY-compliant code structure for readability and scalability.


## Project Structure
├── Kuir_clustering_assignment.ipynb # Main notebook

├── /audio_dataset/ # Directory with audio files (if applicable)

├── README.md # This file

└── /outputs/ # Visualizations, plots, and evaluation results

## Feature Extraction & Data Loading

- Mel Spectrograms were extracted using **Librosa** to capture the time-frequency characteristics of each audio sample.
- Features were loaded and preprocessed efficiently using `pandas` and `numpy`, ensuring scalability and reusability.
- Data normalization and reshaping steps ensured clean input for clustering and reduction methods.

## Why Dimensionality Reduction is Important

High-dimensional audio features (13 Mel coefficients) present the following challenges:

- **Visualization Limitations:** Can’t represent 13D in 2D/3D plots.
- **Curse of Dimensionality:** Sparse data and unreliable distances hinder clustering.
- **Computational Load:** Algorithms are slower and less accurate in high dimensions.
- **Feature Correlation:** Redundancy among features makes patterns harder to detect.

By applying **PCA** and **t-SNE**, we project the data into lower-dimensional spaces where clusters are easier to visualize and interpret. t-SNE, in particular, preserves **local structure**, crucial for identifying similar sound patterns.

## Comparison: PCA vs. t-SNE

| Method | Visual Output | Cluster Separability | Notes |
|--------|----------------|----------------------|-------|
| PCA    | Overlapping    | Weak                 | Linear method, retains global variance but loses non-linear detail. |
| t-SNE  | Distinct groups| Strong               | Preserves local relationships; better for this dataset. |

t-SNE clearly outperformed PCA by revealing **well-separated, compact clusters**, crucial for effective unsupervised classification. This aligns with the **non-linear nature of audio features** from Mel Spectrograms.


## Clustering Comparison: K-Means vs DBSCAN

| Metric                | K-Means (t-SNE Data) | DBSCAN (t-SNE Data) |
|-----------------------|----------------------|----------------------|
| Silhouette Score      | **0.56**              | 0.11                 |
| Davies-Bouldin Index  | **0.78**              | 1.89                 |
| Cluster Visual Quality| High                  | Low (many noise points) |

### Why K-Means Performed Best:
- Achieved **highest silhouette score** indicating compact, well-separated clusters.
- **Balanced DB Index** supports strong inter-cluster distinction.
- Performs well on data pre-processed with t-SNE, which enhances local patterns.

### Why DBSCAN Underperformed:
- Highly sensitive to `eps` and `min_samples`.
- Misclassified many points as noise.
- Assumes similar density across clusters — not suitable for this dataset.

## Code Structure & Modularity

- Code adheres to the **DRY principle**: reusable functions (≤ 4 arguments), no redundancy.
- Organized in sections: imports, loading, preprocessing, reduction, clustering, evaluation.
- Used classes and function encapsulation where appropriate.

## Conclusion

This notebook effectively demonstrates how dimensionality reduction and clustering can be used to explore unlabeled sound datasets. The combination of **t-SNE + K-Means** delivers the most meaningful insights, both visually and metrically, into the structure of the data. The approach follows best practices in unsupervised learning, and the analysis is rooted in real observations from code output.

## Key Libraries Used

- `librosa` – Audio feature extraction (Mel Spectrogram)
- `numpy`, `pandas` – Data handling
- `scikit-learn` – PCA, t-SNE, K-Means, DBSCAN, metrics
- `matplotlib`, `seaborn` – Visualizations

## Author

**Kuir Juach Kuir Thuch**  
African Leadership University  
May Term 2025 – Machine Learning Techniques II  
Email: k.thuch@alustudent.com

