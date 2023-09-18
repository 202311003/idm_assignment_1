# Exploratory Data Analysis and Regression Modeling

## Overview
This project focuses on exploratory data analysis (EDA) and regression modeling using a weather dataset. The primary objectives include understanding the dataset, preparing it for modeling, and applying various regression techniques to predict a target variable and Hyperparamter Tuning implementation. Below is a summary of the key steps and findings.

## Dataset
- **Source**: https://www.kaggle.com/datasets/amirhoseinsedaghati/the-weather-of-187-countries-in-2020
- **Target Variable**: TMIN

## Exploratory Data Analysis (EDA)
- No. of entries: 1026119
- Data columns: 23
- dtypes: float64(12), int64(3), object(8)
- Number of missing data:
- STATION                  0
- Country/Region           0
- DATE                     0
- Year                     0
- Month                    0
- Day                      0
- PRCP                307737
- SNWD                811769
- TAVG                236346
- TMAX                373484
- TMIN                345959
- SNOW                922128
- LATITUDE            923812
- LONGITUDE           923812
- ELEVATION           923812
- PRCP_ATTRIBUTES    1020112
- TAVG_ATTRIBUTES    1022269
- TMAX_ATTRIBUTES    1020482
- TMIN_ATTRIBUTES    1020245
- DAPR               1024856
- MDPR               1026038
- WESD               1026117
- SNWD_ATTRIBUTES    1025765

## Data Preprocessing
- **Handling Missing Data**: Empty cells of TAVG, TMAX, TMIN, PRCP filled with the mode
- **Normalization**: We used LabelEncoder for STATION and Country/Region features. 

## Regression Models
### 1. Linear Regression
- **Model Performance**:
  - Mean Absolute Error (MAE): MAE: 2.5208005685605746
  - Root Mean Squared Error (RMSE): RMSE: 3.342600803775712
  - R-squared (R²): R-squared (R²): 0.8769824407994815

### 2. SGD Regression
- **Model Performance**:
  - Best Hyperparameters: {'alpha': 0.01, 'eta0': 1.0, 'learning_rate': 'optimal', 'max_iter': 2000, 'tol': 0.0001}
  - MAE: 2.5403256035426374
  - RMSE: 3.356887141360582
  - R-squared (R²): 0.8759336772392798

### 3. Polynomial Regression
- **Model Performance**:
  - Mean Squared Error (MSE): 9.680385014483944
  - R-squared (R²): 0.8934163202310743

## Conclusion
- From above observations we can say that SGDRegression and Linear Regression gives almost same results, Polynomial Regression gives very bad results
- The Linear and SGD models explain about 87% of the variance in target variable, so we can say that it is relatively good fit.
- MAE for polynomial regresion is the worst.
- MAE for other 2 models are far better than polynomial but still not giving precise results.



## Dependencies
- List of Python libraries and packages used in the project.

## How to Run
- Open in google collab 
- import archive.zip in data directory
- execute all the scripts

## Author
- Harsh Mistry
- 202311003@daiict.ac.in
