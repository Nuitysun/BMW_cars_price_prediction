<h1><center><span style="color:#C2571A"> Prediction of BMW used cars price </span></center></h1>

<h3>Table of Contents </h3>
    
1. [Project Motivation](#1)
2. [The Dataset](#2)
3. [Analysis Plan](#3)
4. [Performance Metrics](#4)
5. [Machine learning algorithms assumptions](#5)
6. Read the dataset and clean the data
7. Explore independent features relation to target, perform transformations and feature engineering
8. Model Development. Test regression algorithms
9. Tune model based on CatBoostRegression algorithm
10. Implement BMW used cars predictor using CatBoostRegressor algorithm
[11. Conclusion and Recommendations](#7)
12. References

## 1. Project Motivation <a name="1"></a>

What determines the price of used cars? The value of a car drops right from the moment it is bought and the depreciation increases with each passing year. In fact, only in the first year, the value of a car can decrease from 10 to 60 percent (Ref. 1). Different factors affect the value of a vehicle such as the mileage, model, fuel type, the condition, location, color of a car, etc.

The goals of this project are:
- explore what factors affect a sale price of used BMW cars and which characteristics are the most important to determine a car value,
- build a prototype of model which predicts price of used BMW cars.

The results of this project may be useful for businesses that work with reselling of used BWM cars and buyers who are looking to purchase a pre-owned BMW car. **Understanding the factors that determine the price and which of them have the biggest affect can help to improve the process of cars valuation.** On the one hand it can help to ensure the data with all important parameters is collected. On the other hand, it can help to save efforts on the initial steps of valuation, as only the most important car parameters can be collected to make a rough estimation of a car price or to assess how good is a particular deal of a car sale. 

**The developed sale price predictor can be of help during the process of cars search and valuation as it can be used as a tool that provides a quick rough estimation of a car price based on the given input parameters.**

## 2. The Dataset <a name="2"></a>

The dataset that was chosen for the analysis contains information about BMW Used Car Sales and was obtained from DataCamp GitHub repository for careerhub data (Ref. 2). There is no information about the source of this dataset, but a conclusion was made that most likely the data was collected in the United Kingdom. There was a reference about the `tax` column as information about the road tax, in the same time miles per gallon parameter (mpg) is commonly used only in three big countries: the United States, the United Kingdom and Canada. In the United States and Canada there is no road tax as such, but in the United Kingdom there is a road tax. The values of `tax` column in the data are also correspond to tax rates in UK.

### 2.1. Dataset characteristics

The dataset consists of 10781 observations and 9 columns:
- 3 categorical variables: `model`, `transmission`, `fuelType`,
- 5 numerical variables: `year`, `engineSize`, `mileage`, `tax`, `mpg`,
- continuous target vatable `price`.


### 2.2. Context of the dataset 

Below are the general statistics of car market in UK, it can be helpful during further analysis of factors that affect cars price.

According to the The Society of Motor Manufacturers and Traders (SMMT) in 2020 used car sales in UK decreased by 14.9% with the 6,753 thousands transactions made during the year. In each quarter of 2020 the most popular BMW car was 3 Series model, which took 6th place by the number of transactions among all models of used cars sales (Ref. 3).

According to Statista data platform the BMW share in new cars market sales in UK was fluctuating from 5% to 9% during 2015-2020 (Ref. 4). In 2020 there were 115.5K new BMW passenger cars sold in UK, which is a decline of about 32% year-on-year amid the outbreak of the coronavirus pandemic (Ref. 5) - this is a significantly bigger decline in sales in comparison to used cars market decline. Another interesting statistic is that as of 2016 the average age of cars on the road in the UK was 7.7 years old (Ref. 6).


## 3. Analysis Plan  <a name="3"></a>

The task to be solved in this project is supervised regression problem.
In this project we will follow the steps:
- Define performance metrics based on what is known about expected performance of the model,
- Define  machine learning algorithms that may be suitable based on what is known about the task,
- Read the dataset and clean the data,
- Explore independent features relation to target, perform necessary transformations/feature engineering,
- Test regression algorithms,
- Tune a model based on the best performing algorithm,
- Implement BMW used cars predictor,
- Summarize the results and next steps to improve the model.


## 4. Performance Metrics  <a name="4"></a> 

The choice of the best metric for regression task depends on specifics of the data and the requirements to the model performance.
For instance, what is more important: to predict price as accurate as possible on average or not to exceed certain threshold of acceptable error in predictions?

Based on what is known about the data at current stage and understanding of expectations from the model performance, it is suggested to use R-Squared/RMSE as the main metrics and MAE/RMSLE as the supporting metrics. This decision is based on the assumption that big errors in price predictions should be avoided, but in the same time accuracy of predictions is also should be measured. 

**R-Squared.** R-squared (R2) is a statistical measure, known as coefficient of determination, that represents the proportion of the variance for a dependent variable that is explained by an independent variable. R-squared metric determines goodness of fit and is scaled between 0 and 1. The advantage of this metric is ease of interpretation. 

**Root Mean Squared Error (RMSE).** RMSE is the most widely used metric for regression tasks and is the square root of the averaged squared difference between the target value and the value predicted by the model. It is preferred more in some cases because the errors are first squared before averaging which poses a high penalty on large errors. This implies that RMSE is useful when large errors are undesired. 

**Mean Absolute Error (MAE).** MAE is the absolute difference between the target value and the value predicted by the model. The MAE is more robust to outliers and does not penalize the errors as extremely as RMSE. MAE is a linear score which means all the individual differences are weighted equally.

**Root Mean squared logarithmic error (RMSLE).** Root mean squared logarithmic error can be interpreted as a measure of the ratio between the true and predicted values. In a simple words we can say that RMSLE only cares about the percentual difference and therefore is robust toward outliers as it scales down big errors nullifying their effect.

## 5. Machine learning algorithms assumptions <a name="5"></a>

Based on what is known about the data characteristics a linear regression and random forest/gradient boosting algorithms may be suitable for this task. During data preparation and exploration we will take into account assumptions about input data that these algorithms have.

Linear regression may be quite powerful algorithm given the input data complies with following assumptions:  
-	linearity: assumes that the relationship between predictors and target variable is linear,
-	no noise: eg. that there are no outliers in the data,
-	no collinearity: if you have highly correlated predictors, it’s most likely your model will overfit,
-	normal distribution: more reliable predictions are made if the predictors and the target variable are normally distributed,
-	scale: it’s a distance-based algorithm, so preditors should be scaled (Ref. 7).

Random Forest algorithm on the other hand is less demanding as for the data preprocessing:
- decision trees algorithm is insensitive to the absolute values of predictors, so the data does not need to be rescaled or transformed,
- algorithm is great with high dimensional data since it is working with subsets of data,
- algorithm is robust to outliers and non-linear data,
- problem of overfitting is frequently occur and can be solved with hyperparameters tuning.

## 11. Conclusion and Recommendations <a name="7"></a>

The aim of this project was to explore what factors affect used cars price the most and to implement a prototype of used BMW cars price predictor which can provide an assistance for the potential buyers and sellers to define a fair price of a car with minimal time efforts.

### Exploration of factors that affect price of used BMW cars
The results on the test set show that only 8 parameters  can explain almost 96% of variance in price:
-	Year when car was produced (importance_score – 29.7),
-	Number in model name (importance_score – 17.7),
-	Mileage (importance_score – 15.8),
-	Mileage per gallon parameter (importance_score – 13.2),
-	Boolean parameter `_big_engine_auto_semi_auto` which is True when a car has automatic or semi-automatic transmission and engine size above 2.9 liters (importance_score – 7.9),
-	Boolean parameter which is True when a car belongs to `X` model line (importance_score – 7.3),
-	Size of engine in liters (importance_score – 4.5),
-	Added feature `mpg_2` which is filled if ` fuelType` is ` Diesel` (importance_score – 3.9).

In other words we can conclude that all the features except `tax`, that were in the initial dataset proved are important for price prediction: `year`, `model`, `mileage`, `mpg`, `transmission`, `engineSize` and `fuelType`. 

### Prototype of price predictor for used BMW cars 

In this project several machine learning algorithms were tested and different data preprocessing approaches were explored. New features were extracted from the initial data. Data was spit into training (80%) and testing (20%) set.

Predictive model based on CatBoostRegressor algorithm had the best results on the test set:
 - explained_variance: 0.9631,
 - mean_absolute_error: 1435.5959, 
 - root_mean_squared_error: 2202.7952, 
 - mean_squared_log_error: 0.008453.

To check the model performance on the real data, 4 inputs of samples from [autotrader.co.uk](https://www.autotrader.co.uk) web-site were manually added and price were predicted for them. The results we got are: RMSE of £962 and MAE of £629 which is better than on training or testing set. The sample size for this test is not large enough to make any conclusions, so it's recommended to check model performance on the bigger sample and analyze the results.


**Limitations of the price prediction model:**
1.	Results of the best performing model on the test set are: mean absolute error of £1436  and mean squared error of £2203. There are about 20% of predictions that have error above 10% and almost 8% of predictions have error above 15%. It’s important to define what are minimal requirements for the model performance, because the current model's predictions might not be reliable enough.
2.	CatBoostRegressor algorithm provided the best results on the test set, but is more computationally expensive than other simpler algorithms with slightly bigger loss. Amount of data to be processed and the expected execution time should be taken into consideration when applying price prediction model.
3.	Cars sales data quickly gets irrelevant with time: demand on the market changes, new models are released and with each time period cars loose in value because their age increases, etc. The price predictor should be updated regularly to provide relevant predictions.

**Possible ways to improve performance of the model:**

1.	Explore in greater depth hyperparameter tuning for CatBoostRegressor. 
2.	Some values of price are not explained by the parameters that we have in the dataset. It’s possible that more information about cars can be retrieved that can explain unclear variance in price, for example: 
    -	assessment of car condition, 
    -	more information about important car characteristics (engine model, color, if navigation is installed, leather/textile interior, if car is convertible, number of doors, if a car was in accident and what was a severity of damage, if a car had more than one owner, etc),
    -	information about additional packages/additions installed in a car or assessment of value of additions/packages,
    -	location, etc. 
3. Collect more data (for example in the dataset there is not much data for the older cars).
4. Explore model performance on the real unseen data and tune it in accordance to received results.
