# Unsupervised-Learning-with-Country-Data

## Overview 
This project applies unsupervised machine learning, specifically the K-Means Model, to analyze socioeconomic and health indicators of countries around the world.
The goal is to group countries based on their level of development and identify those most in need of direct humanitarian or economic aid.
The project discovers hidden patterns in global data without predefined labels.

## Summary of Workdone 
Exploratory Data Analysis (EDA) – Examined statistical summaries, outliers, and distributions for each variable.

Feature Standardization – Scaled all numeric features so that large-valued features (like GDP) do not dominate distance calculations.

Model Selection – Determined the optimal number of clusters using the Elbow Method and Silhouette Score.

K-Means Clustering – Grouped 167 countries into five clusters representing distinct development levels.

Dimensionality Reduction (PCA) – Reduced data to two principal components for clear 2D visualization.

Interpretation – Analyzed socioeconomic meaning of each cluster to identify the least developed and most economically unstable nations.

Visualization – Created PCA scatterplots, boxplots, and bar charts to visualize development patterns and economic indicators.

## Data 

Dataset Name: Country-data.csv 

Total Records: 167 countries

**Key Variables:**
- child_mort: Deaths of children under 5 per 1,000 live births
- exports: Exports as % of GDP per capita
- health: Health spending as % of GDP per capita
- imports: Imports as % of GDP per capita
- income: Net income per person
- inflation: Annual growth rate of GDP (inflation rate)
- life_expec: Average life expectancy
- total_fer: Fertility rate (children per woman)
- gdpp: GDP per capita calculated as the tota; GDP divided by the total population

## Domain Knowledge

Most of the variable in my dataset are pretty self explanatory, but some require some more understanding. This is because when it comes down to it ands countrties are being compreae, we need to know what high ir low values in a ceratin v ariable means, and if that is an indicator of a more or less developed country. 

**child_mort**
The global child mortality rate is 37 per 1000 deaths. Some countries are a lot higher/lower than that. The lower, the more highly developed the country most likly is. 

**exports**
Exports show how much of the country’s economy comes from selling goods and services abroad. Low exports means country doesn’t trade much internationally and might rely heavily on local production. High exports means he country is very trade-oriented and often developed. 

**health**
This metric shows how much is invested in keeping people healthy compared to how much they earn. Low health spending: usually happens in developing countries. High health spending usually happens developed countries. 

**imports**
Imports show how much of the economy comes from bringing in foreign goods/services. Low import means the country may produce most goods locally, or it may be poor and unable to afford imports. High imports means the country is globally connected and buys a lot from other nations. 

**income**
This is the net income per person. Obviously the higher the better. This should be double checked though when a high net income also comes with high inflation. 

**inflation**
This metric is the measurement of the annual growth rate of the Total GDP
How much more expensive life gets each year. Infaltion rates have a sweet spot, given by the table below: 

| **Value** | **What It Means** | **Interpretation** |
|------------|-------------------|--------------------|
| **0–2%** | Very low inflation | Stable, but maybe too low. It could signal weak economic demand. |
| **2–5%** | Normal / Healthy inflation | Indicates a growing, stable economy. Ideal for development. |
| **5–10%** | Moderate inflation | Prices rising faster. This is manageable for developing nations. |
| **10–30%** | High inflation | Economy starting to overheat. Purchasing power is dropping. |
| **>30%** | Hyperinflation or crisis | Prices spiral out of control. Money is losing value rapidly |


**life_expec**
Globally, the average life expentancy is 73 years, with significant regioal differences. The higher the number, the better. 

**total_fer**
The average fertility rate is 2.3 children per woman. Developing countries will have a lot higher ratio. Developed countries will have a lower ratio. 

**gdpp**
This metric is the total market value of all finished goods and services produced within a country. A high GDP signifies a developed nation, but if it increases too fast, that is sign of inflation, which is not good. 


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
