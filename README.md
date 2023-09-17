# Assignment1
#Weather Prediction

We have conducted a data analysis on weather data. Here's a brief discussion of what we did:

Data Splitting: We started by splitting our dataset into training and testing sets using the train_test_split function from scikit-learn. This is a common step in machine learning to evaluate the performance of models.

Data Scaling: We used the StandardScaler from scikit-learn to standardize our features. Standardization is important for many machine learning algorithms as it helps ensure that features are on the same scale.

Model Selection: We created a dictionary called model_dict that contains several regression models, including Linear Regression and RandomForestRegressor. Each model is associated with a set of hyperparameters to be tuned.

Model Evaluation: We defined a function eval_models to evaluate each model. Inside this function, We used GridSearchCV to perform hyperparameter tuning for each model. This technique tries different combinations of hyperparameters to find the best-performing model.

Model Metrics: We calculated and recorded various regression metrics for each model, such as Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE). These metrics are used to assess how well your models are performing on both the training and testing datasets.

Best Model Selection:We selected the best model based on the test RMSE (Root Mean Squared Error). The model with the lowest test RMSE was considered the best.

Visualization: We plotted the prediction errors using the best model to visualize how well it performed on the test data.

Data Preprocessing: Before starting with model evaluation, We performed some data preprocessing steps. We computed the average temperature (TAVG), minimum temperature (TMIN), and maximum temperature (TMAX) for each country/region and month combination. This likely helped in filling missing values in our dataset, ensuring that temperature data was more complete and consistent.

Data Cleanup: We dropped unnecessary columns from our dataset, which can help reduce noise and improve model performance.

Data Analysis: We provided information about the columns in our original dataset, including the features and attributes.

Missing Data Handling: We addressed missing data in the TMIN and TMAX columns by filling them with the average values calculated for each country/region and month combination. This approach helps retain as much data as possible while handling missing values appropriately.

Data Quality Check:We checked for missing values in our dataset after the filling operation to ensure that there are no remaining NaN values.

Overall, our project involved data preprocessing, feature engineering, model selection, hyperparameter tuning, and model evaluation. The goal is to develop a regression model to predict maximum temperatures (TMAX) based on the given weather data features. The RandomForestRegressor model with specific hyperparameters (max_depth: 9, n_estimators: 15) performed the best according to the test RMSE metric
