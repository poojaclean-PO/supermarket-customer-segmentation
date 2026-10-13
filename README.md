# Supermarket Customer Segmentation Using Machine Learning

## 1. Project Overview

This project uses unsupervised machine learning to identify customer segments based on supermarket purchasing behavior. The objective is to support targeted marketing, customer retention, and inventory planning.

## 2. Dataset

- Source: `supermarket_data` table from `Clustering.db`
- Product-order records analyzed: 1,000,000
- Unique customers: 101,335
- Unique orders: 188,452
- Unique products: 134

Each row represents a product associated with an order.

## 3. Tools and Technologies

- Python
- Pandas and NumPy
- Scikit-learn
- Matplotlib and Seaborn
- SQLite
- Jupyter Notebook

## 4. Methodology

1. Inspected data types, missing values, duplicates, and descriptive statistics.
2. Aggregated product-order records into customer-level behavioral features.
3. Engineered features such as order frequency, basket size, product variety, reorder ratio, and order intervals.
4. Preprocessed and standardized features.
5. Applied K-Means clustering and compared candidate cluster counts using inertia and silhouette scores.
6. Examined customer segment profiles and translated the results into business recommendations.

## 5. Preliminary Results

Three customer segments were identified in the initial model:

- Cluster 0: Lower-frequency, smaller-basket customers.
- Cluster 1: Larger-basket, repeat-active customers.
- Cluster 2: First-order customers represented in the dataset.

The initial three-cluster model achieved a silhouette score of approximately 0.306.

These findings are preliminary and should be interpreted alongside validation of the missing-order-interval feature.

## 6. Business Applications

- Design targeted promotions for different customer segments.
- Encourage second purchases through onboarding campaigns.
- Support repeat-purchase and customer-retention initiatives.
- Inform complementary-product recommendations and basket-building offers.

## 7. Project Files

- `supermarket_segmentation.ipynb`: Data analysis, feature engineering, clustering, and evaluation.
- `cluster_profile.csv`: Summary statistics for customer segments.
- `visualizations/`: Charts showing model evaluation and cluster profiles.

## 8. Limitations

The results depend on the coverage and quality of the available order history. The missingness indicator may influence cluster separation. Further validation is needed before deploying these segments in business operations.