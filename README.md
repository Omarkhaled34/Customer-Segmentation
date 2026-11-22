# Customer Segmentation with K-Means

Segmenting customers into 5 groups using K-Means clustering on demographics, spending, and purchase behavior, with PCA for visualization.

## Overview

This project analyzes a customer marketing dataset (2,240 customers, 29 columns) to discover distinct customer segments. The goal is to help a business understand who its customers are and tailor marketing, offers, and retention strategies for each group.

## Workflow

1. **Data cleaning**
   - Dropped 24 rows with missing `Income`
   - Converted `Dt_Customer` to a datetime
2. **Feature engineering**
   - `Age` (from `Year_Birth`)
   - `Total_childern` (`Kidhome` + `Teenhome`)
   - `Total_spending` (sum of all `Mnt*` product columns)
   - `Customer_since` (days since the customer joined)
3. **Exploratory data analysis**
   - Age and spending distributions
   - Income by education, spending by marital status
   - Pivot table of income by education and marital status
   - Average spending by education level
4. **Preprocessing**
   - Selected features: `Age`, `Income`, `Total_spending`, `NumWebPurchases`, `NumStorePurchases`, `NumWebVisitsMonth`, `Recency`
   - Standardized with `StandardScaler`
   - Removed outliers (|z-score| >= 3 on any feature), leaving 2,188 customers
5. **Clustering**
   - Elbow method for k = 2 to 10
   - Final model: K-Means with **k = 5**
6. **Visualization and evaluation**
   - 2D PCA scatter plot colored by cluster (`tab10` palette)
   - Cluster profiles using the mean of each feature per cluster


The clusters overlap in the 2D PCA view, which is common for customer data where behavior changes gradually rather than falling into isolated groups. The segments are best judged by how different their average profiles are (spending, income, purchase channel, recency), not by visual separation alone. Removing outliers improved the scores compared to the first run .

## Tech Stack

- Python
- pandas, NumPy
- scikit-learn (KMeans, PCA, StandardScaler, clustering metrics)
- SciPy (z-score outlier removal)
- Matplotlib, Seaborn
- Jupyter Notebook


## Possible Improvements

- Compare K-Means with Gaussian Mixture Models and Agglomerative Clustering
- Test additional features (e.g. campaign responses, product category mix)
- Try t-SNE or UMAP for a clearer 2D view of the clusters
- Name each segment (e.g. high-value loyal, low-spend online) and attach a recommended action
- Check cluster stability across different random seeds

