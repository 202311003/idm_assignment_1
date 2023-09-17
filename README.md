# Temperature Prediction Project

## Dataset: The Weather of 155 Countries in 2020

### Project Overview

In this machine learning project, we embarked on the journey of developing a robust temperature prediction model. Our methodology encompassed several pivotal stages:

#### Data Preprocessing

1. **Identification of Missing Values**: We meticulously examined the dataset and discovered significant gaps in data. Most columns exhibited more than 50% missing values, including crucial attributes other than TAVG, TMIN, TMAX, DATE, Month, Day, and PRCP. Addressing this issue was imperative.

2. **Filling Missing Values**: To rectify the gaps in TAVG, TMIN, and TMAX data, we employed a data-driven approach. We computed the mean values by grouping the data based on countries. A noteworthy observation was that the resulting distributions closely resembled normal distributions, bolstering our data imputation strategy.

3. **Correlation Analysis**: Our exploration revealed strong correlations between TAVG, TMIN, TMAX, Latitude, and Longitude. As a substantial portion of Latitude and Longitude values were missing, we opted to omit these columns from further analysis.

#### Model Training

4. **Linear Regression Model**: Our temperature prediction model of choice was the Linear Regression model. This model was trained rigorously using the processed dataset.

#### Evaluation and Metrics

5. **Model Evaluation**: We assessed our model's performance using key regression metrics, including Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and R-squared (R²). These metrics provided a comprehensive evaluation of our model's predictive accuracy.

#### Visualization

6. **Visualizing Predictions**: The final step involved visualizing the results. We created a scatter plot to depict the relationship between actual and predicted values. This visualization aids in comprehending the model's performance on the test data.

Through these meticulously executed steps, we successfully developed a robust temperature prediction model. Our commitment to excellence at every stage of development ensures the reliability and accuracy of our predictions.
