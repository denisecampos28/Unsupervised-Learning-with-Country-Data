# Unsupervised-Learning-with-Country-Data

## Overview 
This project applies unsupervised machine learning to analyze socioeconomic and health indicators of countries around the world.
The goal is to group countries based on their level of development and identify those most in need of direct humanitarian or economic aid.
Using K-Means clustering and Principal Component Analysis (PCA), the project discovers hidden patterns in global data without predefined labels.

## Summary of Workdone 
Exploratory Data Analysis (EDA) – Examined statistical summaries, outliers, and distributions for each variable.

Feature Standardization – Scaled all numeric features so that large-valued features (like GDP) do not dominate distance calculations.

Model Selection – Determined the optimal number of clusters using the Elbow Method and Silhouette Score.

K-Means Clustering – Grouped 167 countries into five clusters representing distinct development levels.

Dimensionality Reduction (PCA) – Reduced data to two principal components for clear 2D visualization.

Interpretation – Analyzed socioeconomic meaning of each cluster to identify the least developed and most economically unstable nations.

Visualization – Created PCA scatterplots, boxplots, and bar charts to visualize development patterns and economic indicators.

## Data 
Dataset Name: Country Data – Kaggle
Total Records: 167 countries
Key Variables:
- child_mort: Deaths of children under 5 per 1,000 live births
- exports: Exports as % of GDP per capita
- health: Health spending as % of GDP per capita
- imports: Imports as % of GDP per capita
- income: Net income per person
- inflation: Annual growth rate of GDP (inflation rate)
- life_expec: Average life expectancy
- total_fer: Fertility rate (children per woman)
- gdpp: GDP per capita

## Preprocessing 
Removed no columns (all features relevant).
Dropped non-numeric field country before modeling.
Standardized numeric variables using StandardScaler() to ensure equal contribution of each feature.
Verified scaling (mean ≈ 0, std ≈ 1).
No missing values were found in the dataset.
Outliers were kept intentionally since they represent real-world extremes (e.g., poorest or richest nations), which are essential for clustering analysis.

## Training 
Model Used: K-Means clustering (scikit-learn)
Optimal K: Determined using:
Elbow Method → curve flattened after K = 5
Silhouette Scores → highest at K = 5 (0.301)
Final Model: KMeans(n_clusters=5, random_state=42)
Dimensionality Reduction: PCA with 2 components for visual clarity.

## Model Performance 
add silhoute and elbow outputs 

## Conclusion
add picute of fibal cluters and thier interperrtaionf 


## Overview of Files in this Repository 

## Software Setup 

## Data Download 
https://www.kaggle.com/datasets/rohan0301/unsupervised-learning-on-country-data/data?select=Country-data.csv
