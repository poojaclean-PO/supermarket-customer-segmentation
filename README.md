# Supermarket Customer Segmentation Using Machine Learning

## 1. Project Overview

This project applies unsupervised machine learning to identify customer segments based on supermarket purchasing behaviour. The objective is to understand differences in observed ordering frequency, basket size, product variety, and reorder behaviour.

The resulting segments can inform potential business strategies for customer retention, targeted promotions, and basket-building offers. These applications are recommendations for further testing, not proven business outcomes.

## 2. Dataset

- **Source:** `supermarket_data` table from `Clustering.db`
- **Product-order records analysed:** 1,000,000
- **Unique customers:** 101,335
- **Unique orders:** 188,452
- **Unique products:** 134

Each row represents a product associated with an order. The data was aggregated to create one customer-level record for segmentation.

## 3. Tools and Technologies

- Python
- Pandas and NumPy
- Scikit-learn
- Matplotlib and Seaborn
- SQLite
- Jupyter Notebook

## 4. Methodology

1. Inspected data types, missing values, duplicate records, and descriptive statistics.
2. Explored purchasing patterns and engineered customer-level features.
3. Calculated order frequency, total items, unique products, reorder ratio, average basket size, and average days between orders.
4. Corrected the average order-interval calculation by using distinct customer orders rather than individual product rows.
5. Preserved missing-interval information using an `interval_missing` indicator and imputed missing interval values during preprocessing.
6. Applied log transformations to selected skewed features and standardised the clustering inputs.
7. Evaluated K-Means models for cluster counts from 2 to 8 using inertia and sampled silhouette scores.
8. Examined cluster profiles and performed sensitivity analysis by comparing models with and without `interval_missing`.

## 5. Model Evaluation

The corrected feature pipeline was used to evaluate K-Means models with different cluster counts.

| Number of clusters (K) | Inertia | Sampled silhouette score |
|---:|---:|---:|
| 2 | 500,405.71 | 0.2623 |
| **3** | **389,655.78** | **0.3046** |
| 4 | 317,965.46 | 0.2637 |
| 5 | 278,330.26 | 0.2573 |
| 6 | 248,166.68 | 0.2586 |
| 7 | 227,095.39 | 0.2551 |
| 8 | 208,972.86 | 0.2446 |

Three clusters achieved the highest sampled silhouette score among the tested configurations. A score of approximately 0.3046 indicates moderate cluster separation; it is not a measure of predictive accuracy.

## 6. Customer Segmentation Results

The final three-cluster model produced the following customer profiles.

| Cluster | Customers | Share | Avg. orders | Avg. items | Avg. unique products | Avg. reorder ratio | Avg. basket size |
|---|---:|---:|---:|---:|---:|---:|---:|
| 0 | 6,136 | 6.06% | 1.00 | 5.19 | 4.31 | 0.00 | 5.19 |
| 1 | 47,617 | 46.99% | 2.58 | 16.70 | 10.68 | 0.59 | 7.45 |
| 2 | 47,582 | 46.96% | 1.25 | 3.63 | 3.08 | 0.55 | 3.09 |

### Cluster 0 — Customers with One Observed Order

This segment contains 6,136 customers. All have one observed order, a zero observed reorder ratio, and a missing average order interval.

These customers should be described as having one observed order in the available dataset, rather than as confirmed new or lifetime first-time customers.

### Cluster 1 — Higher Order Volume and Larger Baskets

This segment contains 47,617 customers. It has the highest average observed order count, total items, unique products, and basket size among the three segments.

Potential business application: test relevant complementary-product offers and repeat-purchase campaigns.

### Cluster 2 — Lower Order Volume and Smaller Baskets

This segment contains 47,582 customers. It has lower average observed order volume and smaller baskets than Cluster 1.

Potential business application: test relevant basket-building promotions and product recommendations, while evaluating whether these interventions improve purchasing outcomes.

Cluster numbers are model-generated identifiers; they do not imply a ranking or customer lifecycle stage.

## 7. Sensitivity Analysis

The effect of `interval_missing` was assessed by comparing three-cluster K-Means models with and without the indicator.

| Measure | With indicator | Without indicator |
|---|---:|---:|
| Sampled silhouette score | 0.3046 | 0.2424 |

The Adjusted Rand Index between the two sets of cluster assignments was **0.3788**, indicating meaningful changes in customer grouping when the indicator was removed.

The indicator was retained in the primary model because it improved cluster separation in the tested feature space. However, it also captures information about data availability. The resulting segments may therefore reflect missing order-history information as well as purchasing behaviour.

The sensitivity analysis does not establish that the model with the indicator is universally better for business use. Further evaluation of cluster stability and business relevance is warranted.

## 8. Data Coverage and Limitations

Order-history checks found that 89,830 customers had a minimum observed order number greater than 1. In addition, 94,811 customers had a distinct observed order count that differed from their maximum recorded order number.

These findings indicate that many customers' available records do not begin at order number 1. The checks alone do not establish why earlier records are absent or whether the source contains each customer's complete lifetime history.

Consequently:

- The segments describe purchasing patterns in the available records, not confirmed lifetime customer behaviour.
- Customers with one observed order must not automatically be classified as new customers or lifetime first-time buyers.
- Missing order intervals may influence cluster assignments.
- A silhouette score measures cluster separation, not predictive accuracy.
- Business recommendations are hypotheses that require validation before operational use.

## 9. Business Applications

The identified segments suggest several potential applications:

- Test targeted promotions for customers with smaller baskets.
- Explore complementary-product recommendations for customers purchasing more items.
- Evaluate repeat-purchase campaigns using subsequent order behaviour.
- Investigate whether the one-observed-order segment contains customers with incomplete histories before designing onboarding strategies.
- Assess the impact of any campaign using suitable business metrics and controlled testing where feasible.

These applications should be validated using additional data and measurable business outcomes before implementation.

## 10. Project Files

- `supermarket_segmentation.ipynb` — Data exploration, feature engineering, preprocessing, clustering, evaluation, and sensitivity analysis.
- `cluster_profile.csv` — Summary statistics for the final customer segments.
- `visualizations/` — Model evaluation, customer distribution, and cluster behaviour charts.

## 11. Conclusion

This project demonstrates a customer segmentation workflow using Python, feature engineering, data preprocessing, K-Means clustering, and sensitivity analysis.

After correcting the order-interval calculation, three clusters achieved the highest sampled silhouette score among the tested configurations. The sensitivity analysis also showed that missing-interval information materially influences customer assignments.

The results provide an exploratory view of customer purchasing patterns in the available data. Further stability testing, data-coverage validation, and business-outcome evaluation are recommended before using the segments for operational decisions.
