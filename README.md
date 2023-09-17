"# idm_assignment_1" 
Dataset:

The dataset used in this assignment is 'The Weather of 187 Countries in 2020' which is freely availabe on Kaggle.The link for the same is: https://www.kaggle.com/datasets/amirhoseinsedaghati/the-weather-of-187-countries-in-2020.

EDA: 

In EDA we had visualize data by using various functions.We have observerd that data consisted 23 columns and a total of 1392575 entries.The problem arised when we check for the null values in dataset and found out many rows were having mnearly all entries null.

Data pre-processing: 

We started data processsing by droping the columns which had more than half of the values null.In total we dropped 14 columns.Now we needed to fill the null values which we left.To do that firstly we have grouped our data by 'Country/Region','STATION' and 'Month'.Then after grouping found out median of the groups.The median was calculated for 'TMIN','TMAX','TAVG','PRCP'.Later this median was used to fill the null values of those respective columns.After this all the rows containing null values were droped.The columns having value types as string were converted to numerical lebelling using label encoder.

Regression:

For regression we have used 4 models namely Linear Regression,Lasso Regression,Ridge regression and Polynomial regression. Except Linear regression all other models are implemented in two ways that is by random values and also by fine tuning.For getting the best parameters values of hyper parameters GridSearchCV is used.

Evaluation:

The evaluation of the models is done by two metrics namely Mean Squared Error(MSE) and Mean Absolute Error(MAE).

Results:

1] Linear regression:
   MSE=1.2719,
   MAE=0.7188
   
2] Lasso regression: 
   MSE=2.3060,
   MAE=1.1487
   
3] Lasso regression after tunning:
   MSE=1.2719,
   MAE=0.7188,
   params {'alpha': 0.001, 'fit_intercept': True, 'max_iter': 100, 'positive': False}
   
4] Ridge regression:
   MSE=1.2719,
   MAE=0.7188
   
5] Ridge regression after tunning:
   MSE 1.2719,
   MAE 0.7188,
   params {'alpha': 1, 'fit_intercept': True, 'max_iter': 100, 'positive': False, 'tol': 0.0001}
   
6] Polynomial regression:
    MSE 1.2038,
    MAE 0.6866
    
7] Polynomial regression after tunning:
   MSE 1.1046,
   MAE 0.6512,
   params {'polynomialfeatures__degree': 4}

   
