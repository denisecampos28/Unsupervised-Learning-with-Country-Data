# Unsupervised-Learning-with-Country-Data

## Overview 
This project applies unsupervised machine learning, specifically the K-Means Model, to analyze socioeconomic and health indicators of countries around the world.
The goal is to group countries based on their level of development and identify the country most in need of direct humanitarian or economic aid.
The project discovers hidden patterns in global data without predefined labels.


## Data 

**Dataset Name:** Country-data.csv 

**Rows:** 167 countries

**Columns:** 10

**There were no missing or duplicated values in the dataset.**

**Key Variables:**

- country: gives the name of the country 
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

### **child_mort**

The global child mortality rate is 37 per 1000 deaths. Some countries are a lot higher/lower than that. The lower, the more highly developed the country most likly is. 

### **exports**

Exports show how much of the country’s economy comes from selling goods and services abroad. Low exports means country doesn’t trade much internationally and might rely heavily on local production. High exports means he country is very trade-oriented and often developed. 

### **health**

This metric shows how much is invested in keeping people healthy compared to how much they earn. Low health spending: usually happens in developing countries. High health spending usually happens developed countries. 

### **imports**

Imports show how much of the economy comes from bringing in foreign goods/services. Low import means the country may produce most goods locally, or it may be poor and unable to afford imports. High imports means the country is globally connected and buys a lot from other nations. 

### **income**

This is the net income per person. Obviously the higher the better. This should be double checked though when a high net income also comes with high inflation. 

### **inflation**

This metric is the measurement of the annual growth rate of the Total GDP, which measures how much more expensive life gets each year. Inflation rates have a sweet spot, given by the table below: 

| **Value** | **What It Means** | **Interpretation** |
|------------|-------------------|--------------------|
| **0–2%** | Very low inflation | Stable, but maybe too low. It could signal weak economic demand. |
| **2–5%** | Normal / Healthy inflation | Indicates a growing, stable economy. Ideal for development. |
| **5–10%** | Moderate inflation | Prices rising faster. This is manageable for developing nations. |
| **10–30%** | High inflation | Economy starting to overheat. Purchasing power is dropping. |
| **>30%** | Hyperinflation or crisis | Prices spiral out of control. Money is losing value rapidly |


### **life_expec**

Globally, the average life expentancy is 73 years, with significant regioal differences. The higher the number, the better. 

### **total_fer**

The average fertility rate is 2.3 children per woman. Developing countries will have a lot higher ratio. Developed countries will have a lower ratio. 

### **gdpp**

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

Choosing the right number of clusters is crucial in unsupervised learning, as it directly affects how well the model separates similar countries. Two methods were used to determine the optimal value of **K**:

1. **Elbow Method:**  
   - The Elbow Method involves plotting the **Within-Cluster Sum of Squares (WCSS)** against different values of *K*.  
   - As *K* increases, WCSS naturally decreases because points are assigned to smaller, tighter clusters.  
   - The "elbow" point of the curve represents a balance between compact clusters and minimal overfitting.  

   
  <img width="622" height="461" alt="Screenshot 2025-10-10 102932" src="https://github.com/user-attachments/assets/9dac3483-6c9e-484c-a0f1-830b53fa79aa" />

  
2. **Silhouette Score:**  
   - The Silhouette Score measures how well each data point fits within its cluster compared to other clusters.  
   - Scores range from **-1 to 1**, where values close to 1 indicate that samples are well matched to their own cluster and poorly matched to others.  
   - A higher average silhouette score means more distinct and meaningful clusters.  
   - The highest score observed was **0.301 at K = 5**, confirming that five clusters provided the best separation and cohesion among the countries.


  
<img width="225" height="100" alt="Screenshot 2025-10-10 102946" src="https://github.com/user-attachments/assets/96c0ab91-f5fc-42a7-9d9c-152704312371" />


  
Initially, K = 5 appeared to be the best choice based on the silhouette score. However, when we examined the resulting cluster sizes, we discovered that one cluster contained only a single country. This is a sign of over-segmentation. To address this, we created K diagnostics tables that compared silhouette scores and cluster size distributions across different K values. This allowed us to evaluate both cluster quality and cluster stability before selecting the most appropriate number of clusters.



<img width="669" height="325" alt="Screenshot 2025-11-14 014347" src="https://github.com/user-attachments/assets/397d380c-f614-4d07-847a-38365b42d34d" />



The table makes it clear that once K exceeds 3, the model consistently produces a cluster with only one observation. This confirms that the data is being over-partitioned, which means K = 3 is the only reasonable choice that avoids singleton clusters while still producing a strong silhouette score. However, rather than immediately finalizing K = 3, it is standard practice to test whether transforming the data improves cluster structure. This is especially important because most real world datasets are skewed or unbalanced, and transformations can significantly affect clustering performance.


### Log Transformation 

We applied a log transformation to all variables except inflation, since inflation contains negative values and taking the log of a negative number is mathematically undefined, which would have produced NaN values. The log transformation helps by shrinking very large values more than small ones, reducing skewness and improving distance-based calculations in K-Means. After re-evaluating the K diagnostics table with the transformed data, we confirmed that K = 3 remained the optimal choice. The transformation improved the distribution of several variables but did not change the overall clustering structure in a meaningful way.

The following K diagnostics table is post-log transformation: 



<img width="664" height="332" alt="Screenshot 2025-11-14 014824" src="https://github.com/user-attachments/assets/36a855e7-51d5-4ad5-a8a8-d5f7618ac008" />




## Model Performance 

The final K-Means model (K = 5) successfully grouped countries into five distinct clusters based on their socio-economic and health indicators. The table below represents the mean values of each variable within each cluster.


<img width="771" height="233" alt="Screenshot 2025-10-10 103618" src="https://github.com/user-attachments/assets/78c6c6f2-7244-4eb4-9ac3-f9a080d5dd41" />




| Cluster | General Profile | Summary |
|--------|-----------------|---------|
| **0** | Developing / middle-income nations | Moderate child mortality (~29.7), modest income (~$7,534), and mid-range GDP per capita (~$3,409). Life expectancy (~69.5) and fertility (~2.75) indicate improving but still developing socio-economic conditions. Inflation (~9.89%) is elevated, suggesting economic instability. |
| **1** | Developed / high-income nations | Low child mortality (~6.75), high income (~$28,707), and strong GDP per capita (~$20,920). High life expectancy (~77.9) and low fertility (~1.77) reflect advanced healthcare and stable living conditions. Inflation (~4.01%) remains within a healthy, stable range. |
| **2** | Least-developed / high-need nations | Extremely high child mortality (~90.8), very low income (~$1,694), and extremely low GDP per capita (~$722). Life expectancy (~58.6) is significantly below global standards. Very high fertility (~4.95) and high inflation (~10.97%) reflect severe economic hardship and limited access to essential healthcare resources. |



<img width="989" height="590" alt="download" src="https://github.com/user-attachments/assets/8a5a7587-231b-4de3-835d-aa25091ef360" />



- **Cluster 0** includes developing, middle-income countries that show moderate progress but still face notable health and economic challenges.
- **Cluster 1** represents high-income, developed nations with excellent health, strong GDP, and stable economic conditions.
- **Cluster 2** represents the least-developed, highest-need nations, characterized by extremely poor health indicators, very low economic output, and high fertility and inflation—making them the group most urgently in need of aid.



## Choosing One Country 

Now that we identified which cluster was the most in need, the next step is to determine one single country within that cluster that requires aid the most.


To do this, we created a **Neediness Index**, which produces one score per country.  
**A higher score = worse conditions and greater need.**


### How the Neediness Index works:
- We **add** the values of:
  - child mortality  
  - total fertility  
  - inflation  
  These are variables where **higher values mean worse conditions**, so adding them directly makes sense.

- For variables where **lower values indicate worse conditions**, we flip them using the formula:  
  \[
  \frac{1}{\text{value} + 1}
  \]
  This gives:
  - **lower income → higher score**  
  - **lower GDP → higher score**  
  - **lower life expectancy → higher score**

- This formula ensures that **every variable contributes in the correct direction**:  
  higher need → higher score.


### Final Result:
- After calculating the index for every country in the most vulnerable cluster,  
  **Nigeria** received the highest neediness score.




<img width="790" height="490" alt="download" src="https://github.com/user-attachments/assets/6c432ef6-926b-4901-ac49-30644fcce565" />





  
<img width="309" height="351" alt="Screenshot 2025-11-14 020657" src="https://github.com/user-attachments/assets/11f0664b-c0c8-411f-bafc-c1d24ca9ee5f" />







## Conclusion




## Data Download 
https://www.kaggle.com/datasets/rohan0301/unsupervised-learning-on-country-data/data?select=Country-data.csv
