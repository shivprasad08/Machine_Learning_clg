# Machine_Learning_clg

**Assignment - 1:**
**COVID-19 Data Cleaning and Exploratory Data Analysis (EDA)**

Project Overview
  This repository hosts a Python-based mini-project focused on Data Cleaning and Exploratory Data Analysis (EDA) of a real-world COVID-19 dataset. The objective is to transform raw, inconsistent data into a clean, usable format and to extract valuable insights    through visual and statistical analysis. This project demonstrates essential data preprocessing techniques crucial for any data science workflow.

Dataset
The dataset used for this analysis is covid_19_data.csv, likely sourced from platforms like UCI or Kaggle. It contains daily COVID-19 statistics including case counts, deaths, and recoveries across various regions.

Requirements
To run this notebook, you will need:
-Python 3 
-Jupyter Notebook 
-Libraries: 
  pandas, numpy, scikit-learn (for SimpleImputer, zscore, LabelEncoder, VarianceThreshold, SelectKBest, SelectPercentile, PCA, StandardScaler), matplotlib.pyplot, seaborn.

Methodology & Key Steps
  The project follows a standard data cleaning and EDA pipeline to ensure data quality and derive insights:

1. Data Loading and Initial Inspection:
  The covid_19_data.csv file is loaded into a pandas DataFrame.
  Initial checks (.head(), .info(), .describe(), .isna().sum()) are performed to understand the data's structure, types, and identify missing values and anomalies.

2. Handling Missing Values:
- The dataset was found to have 78,103 missing values specifically in the 'Province/State' column.
- Two strategies were explored:
    1. Row Removal: Dropping rows with missing values, which resulted in a significant 25% data loss (78,103 rows removed), reducing the dataset size from (306429, 8) to (228326, 8).
    2. Imputation: Numerical missing values were filled with the mean, and categorical missing values with the most frequent value. This method successfully retained all original rows while addressing missing data.

3. Handling Anomalous Negative Values:
  - Initial inspection revealed illogical negative minimum values in 'Confirmed', 'Deaths', and 'Recovered' columns (e.g., -302844.0 for 'Confirmed', -178.0 for 'Deaths', -854405.0 for 'Recovered').
  - As a crucial data cleaning step, all these negative values were explicitly replaced with 0 to ensure logical consistency of count data.

4. Outlier Detection and Treatment:
  - Outliers were identified in numerical columns ('Confirmed', 'Deaths', 'Recovered') using both the IQR and Z-score methods.
  - IQR detected a substantial number of outliers: 43,978 in 'Confirmed', 42,102 in 'Deaths', and 46,463 in 'Recovered'.
  - The Z-score method (with a threshold of 3) identified 8,297 outliers, which was more data-conservative, preserving more rows (298,132 rows) compared to IQR.
  - Boxplots provided visual confirmation of outlier presence.

5. Plotting Distributions (EDA):
  - Histograms revealed that 'Confirmed', 'Deaths', and 'Recovered' distributions remained highly right-skewed even after outlier treatment, indicating a concentration of lower values.
  - A countplot visualized the distribution of records across the top 10 countries.
  - A scatter plot of 'Confirmed' vs. 'Deaths' (sampled) with 'Recovered' cases as hue visually suggested a positive correlation between 'Confirmed' and 'Deaths'.

6. Correlation Analysis (EDA):
  - Correlation analysis showed strong positive relationships: 'Confirmed' with 'Deaths' (0.824703) and 'Recovered' (0.716452), suggesting an increase in deaths and recoveries with confirmed cases.
  - 'ObservationDate' (-0.106272) and 'Province/State' (-0.007339) showed very weak inverse correlations with 'Confirmed'.
  - A correlation heatmap provided a visual summary of these relationships.

7. Converting Categorical Data to Numerical:
  - Categorical columns were converted using both Label Encoding and One-Hot Encoding.
  - One-Hot Encoding notably increased the dataset's dimensionality, expanding the column count from 8 to 3363.

8. Feature Selection:
  - Variance Threshold: All original columns were retained after applying a variance threshold of 0.01, indicating sufficient variability.
  - SelectKBest: This method identified 'SNo', 'ObservationDate', 'Province/State', 'Country/Region', 'Last Update', 'Deaths', and 'Recovered' as the most informative features.
  = SelectPercentile: Selecting the top 20% of features consistently highlighted 'Deaths' and 'Recovered' as highly relevant, reinforcing correlation findings.
  = PCA (Principal Component Analysis): PCA reduced dimensionality to 5 components, with the first component explaining approximately 26.5% (0.26566359) of the total variance, effectively capturing a significant portion of the dataset's variability.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
