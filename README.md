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

**Dataset Name:** Country-data.csv 
**Rows:** 167 countries
**Columns:** 10

**There were no missing or duplicated values in the dataset.**

**Key Variables:**

- country: give the name of the country 
- child_mort: Deaths of children under 5 per 1,000 live births
- exports: Exports as % of GDP per capita
- health: Health spending as % of GDP per capita
- imports: Imports as % of GDP per capita
- income: Net income per person
- inflation: Annual growth rate of GDP (inflation rate)
- life_expec: Average life expectancy
- total_fer: Fertility rate (children per woman) per 1000 live births


## Domain Knowledge

Most variables in my dataset are fairly self-explanatory, but a few require deeper interpretation. This is important because when comparing countries, we need to understand what high or low values in certain variables represent and whether they indicate a more or less developed nation.

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

Before applying the K-means algorithm, the dataset was cleaned and prepared to ensure accurate results. The preprocessing steps included:  

- **Inspecting for missing values:** Verified that the dataset contained no null entries. No null entries were found.

- **Standardizing country names:** Removed leading and trailing spaces to ensure uniform formatting. This was a cautionary step because everything was already well-formatted. 

- **Outlier detection and handling:** Reviewed boxplots for each numeric variable to identify extreme values that could distort cluster formation.

Although unsupervised learning models like K-Means are sensitive to outliers, these data points in this project represent meaningful variation, such as countries with exceptionally low GDP or high child mortality rates. Removing them would undermine the purpose of the analysis, which is to capture the full spectrum of development levels. Instead, all numerical variables were standardized to ensure that no single feature or extreme value dominated the clustering process. Outliers were intentionally retained, as they provide important insights for identifying less-developed nations within the dataset.

- **Feature scaling:** Applied standardization using scikit-learn’s StandardScaler, transforming all numerical variables to have a mean of 0 and a standard deviation of 1. This ensured that features with larger ranges did not dominate the clustering process.
  
These preprocessing steps ensured that the dataset was clean, comparable, and ready for unsupervised modelling. 


## Training 

**Model Used:** K-Means clustering (scikit-learn)
**Model Parameters:** KMeans(n_clusters=5, random_state=42)
Dimensionality Reduction: PCA with 2 components for visual clarity.

Choosing the right number of clusters is crucial in unsupervised learning, as it directly affects how well the model separates similar countries. Two methods were used to determine the optimal value of **K**:

1. **Elbow Method:**  
   - The Elbow Method involves plotting the **Within-Cluster Sum of Squares (WCSS)** against different values of *K*.  
   - As *K* increases, WCSS naturally decreases because points are assigned to smaller, tighter clusters.  
   - The "elbow" point of the curve represents a balance between compact clusters and minimal overfitting.  
   - In this project, the curve began to flatten at **K = 5**, suggesting that adding more clusters provided diminishing returns in reducing WCSS.

     
  <img width="622" height="461" alt="Screenshot 2025-10-10 102932" src="https://github.com/user-attachments/assets/9dac3483-6c9e-484c-a0f1-830b53fa79aa" />

  
2. **Silhouette Score:**  
   - The Silhouette Score measures how well each data point fits within its cluster compared to other clusters.  
   - Scores range from **-1 to 1**, where values close to 1 indicate that samples are well matched to their own cluster and poorly matched to others.  
   - A higher average silhouette score means more distinct and meaningful clusters.  
   - The highest score observed was **0.301 at K = 5**, confirming that five clusters provided the best separation and cohesion among the countries.

  
<img width="225" height="100" alt="Screenshot 2025-10-10 102946" src="https://github.com/user-attachments/assets/96c0ab91-f5fc-42a7-9d9c-152704312371" />

  
Together, these steps ensured that the clustering results were both statistically sound and visually interpretable, revealing meaningful groupings among countries based on their economic and health indicators.


## Model Performance 

The final K-Means model (K = 5) successfully grouped countries into five distinct clusters based on their socio-economic and health indicators.  
The table below represents the mean values of each variable within each cluster.

| Cluster | General Profile | Summary |
|----------|-----------------|----------|
| **0** | Lower-middle income nations | Moderate child mortality (22.22) and average life expectancy (72.63). Income (~12,679) and GDP per capita (~6,494) suggest developing economies with room for growth. |
| **1** | Developed / high-income nations | Low child mortality (5.18), high income (~44,022), and strong life expectancy (80.08). Stable inflation (2.51) indicates a healthy, developed economy. |
| **2** | Poorly developed nations | Very high child mortality (94.31), low income (~3,503), and low life expectancy (59.02). Reflects underdeveloped economies with limited access to healthcare and resources. |
| **3** | Economically unstable nations | Highest child mortality (130.00) and extremely high inflation (104), suggesting crisis-level economic instability. Low GDP and life expectancy (60.50) further highlight struggling conditions. |
| **4** | Advanced, export-driven economies | Lowest child mortality (4.13) and highest income (~64,033) with strong exports (176.00). Very high GDP (~57,566) and life expectancy (81.43) identify these as highly developed nations. |

- **Clusters 1 and 4** represent **developed nations**, characterized by high income, strong health outcomes, and low inflation.  
- **Cluster 0** includes **developing nations** with improving but moderate metrics.  
- **Clusters 2 and 3** represent **underdeveloped or economically unstable countries**, with high child mortality, low income, and weak health infrastructure.


<img width="894" height="505" alt="Screenshot 2025-10-10 111451" src="https://github.com/user-attachments/assets/2258d7b9-917e-4583-968c-4849e33890d7" />



## Conclusion

Although Cluster 2 countries display extremely low GDP and income, further analysis revealed that **Cluster 3** countries are in even more critical condition. They exhibit the highest child mortality rate (130 deaths per 1,000 live births), the highest fertility rate, and hyperinflation exceeding 100%, indicating severe economic instability. These conditions reflect countries facing both economic and humanitarian crises. Therefore, Cluster 3 was identified as the group most urgently in need of direct aid, as their populations are likely experiencing simultaneous health, economic, and structural challenges.

After reviewing which countries belonged to each cluster, I felt further assured in selecting **Cluster 3** as the one most in need of aid. This cluster stood out because it contained **only one country, Nigeria**, while all other clusters included at least three or more countries. This isolation suggests that Nigeria’s socio-economic indicators are uniquely severe compared to others, highlighting its urgent need for focused support and development initiatives.


<img width="430" height="411" alt="Screenshot 2025-10-10 112058" src="https://github.com/user-attachments/assets/1d28c52d-a0f8-4dfb-99e0-c73fe66cf506" />


<img width="491" height="378" alt="Screenshot 2025-10-10 112116" src="https://github.com/user-attachments/assets/08037a85-818d-486a-9f23-71447e480e55" />


<img width="506" height="439" alt="Screenshot 2025-10-10 112126" src="https://github.com/user-attachments/assets/42434568-9c87-492b-908c-a62421ebc73d" />


<img width="431" height="103" alt="Screenshot 2025-10-10 112138" src="https://github.com/user-attachments/assets/f7fcc7a0-9a8d-4b57-a71c-e1aafc1ea816" />


<img width="457" height="153" alt="Screenshot 2025-10-10 112146" src="https://github.com/user-attachments/assets/9da893db-034d-4ffd-95c9-ea00e32a8710" />



## Data Download 
https://www.kaggle.com/datasets/rohan0301/unsupervised-learning-on-country-data/data?select=Country-data.csv
