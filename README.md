## Structured Data Project: Predict the auction sale price for a piece of heavy equipment
# Overview
In this project, I am going to use machine learning with the goal of predicting the sale price of bulldozers. it is going to be a regression problem since i want to predict a number. 
I am going to use the evaluation metric ( root mean square log error or RMSLE) with the goal of minimizing the error

# Data
I got the data from Kaggle website: [Dataset Description](https://www.kaggle.com/c/bluebook-for-bulldozers/data)

The data is split into three parts 
* Train.csv : is the training set
* Valid.csv: is the validation set. This dataset is for the prediction throughout this project 
* Test.csv: is the final dataset I use to test the model. 

# Data Analysis and Manipulation

For the data analysis and manipulation i imported pandas, Numpy, matplotlib 

![Screen Shot 2023-09-26 at 6 31 58 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/4269226e-5334-4f1d-8020-1e414f1e5e0c)

* taking a look at the dataframe size and data types: 

![Screen Shot 2023-09-26 at 6 40 14 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/f3f48661-e2a5-4fe4-8657-0d0580ea2657)

* Next to explore more the dataset, I ploted one of the most important column saleDate after parsing it vs the target variable "SalePrice" by looking at the fisrt 1000 rows only

We can say that there are not many sells in 2008 and the highest sells were done in 2007
![Screen Shot 2023-09-26 at 7 29 44 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/3cad1fee-9cff-4226-aa5f-60905ca35606)


* I also did a distribution of the SalePrice (target variable)
  It shows that most of the machines are below $20000, and keeps going less and less. There are not many that cost over $100000

![Screen Shot 2023-09-26 at 6 52 52 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/842716da-eb27-4534-8de7-e51e4067cb9a)

* Since this is a time series data 
# Feature Engineering 

* Extract some of values from saleDate and create some more columns to enrish the dataframe
   
![Screen Shot 2023-09-26 at 7 44 45 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/034233cb-d0f8-4bf6-8dce-35c58914ee4a)

## Modeling 

* For creating a model, I am going to use RansomforestRegressor for the machine learing model

* But Before creating a model, I have a lot of missing values, and not all of the features are numeric so I have to do some model driven EDA

  ![Screen Shot 2023-09-26 at 8 07 56 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/96efc25d-13d0-4d74-aa5a-a2e13094c5f7)

* Convert Strings to categories
* I created a function that find columns which contain string values and **Convert** them to a category values
![Screen Shot 2023-09-26 at 8 28 01 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/0c511780-53ad-4d6b-a575-456401d5702e)

![Screen Shot 2023-09-26 at 8 26 44 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/59574047-2d46-4df1-ba54-29dfc441e2a0)

* Next i filled the numeric rows with the median ( median : just in case there are outliers)
* 
  **Turn categorical variable into numbers and fill missing values**
  
  For that I created a function that cheeck if a value is non-numeric. If it is not numeric, a new column is created with True and False to indicate weather the value is missing or not. To handle missing categorical value, I added 1 to them because missing values are represented by -1. Adding 1 makes them 0, which signifies a missing categorical value with codes of 

![Screen Shot 2023-09-26 at 9 44 56 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/0cf1d0db-97b5-4fe2-b851-6209f3935a66)


## Building a machine learning model now that all our features contains numeric value

   **Splitting data into train/validation sets**
   I want all of the rows up to 2011 to be a training set, and all of the rows from the 2012 can be a validation set

   ![Screen Shot 2023-09-26 at 10 07 49 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/0820044a-f726-4948-86d9-709fb4abbfcc)

   **Building an evaluation function RMSLE**
   
![Screen Shot 2023-09-26 at 10 35 44 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/9f99a889-d50b-4f5a-b810-0b4f982e9d02)

***for quiker result i change the max of samples to 10000***

![Screen Shot 2023-09-26 at 10 54 19 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/367e3755-c9f7-4733-9ca9-4c38d86ad4ad)

#### Call the show score function to see the scores of our model

I expect this metrics to be worse because I only trained the model on 10000 samples. 
Also the fact that the validation MAE is slightly higher than the training MAE suggest that it is not overfitting.

![Screen Shot 2023-09-26 at 11 11 12 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/d029c2f4-ff45-4047-bb67-bcaee71d35ef)

# Hyperparameter tuning with RandomizedSearchCV

I wanted to find the ideal hyperparameter than the defaults one, so i created a dictionary.
![Screen Shot 2023-09-27 at 11 13 01 AM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/177691f2-c171-444f-b5fc-4e560938bba7)

After finding the best parameters by running this code **rs_model.best_params_**, I trained a model with the best parameters as follow: 

![Screen Shot 2023-09-27 at 11 16 41 AM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/7ec63208-298d-4720-956e-1231a1a6ca85)

***Scores of the ideal model screen shot*** 

![Screen Shot 2023-09-27 at 11 45 45 AM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/769c99a3-afc5-4c73-9c81-07903ee96d87)

## Making prediction of test data

** test dataset have to look like the trained dataset so I create a function that takes a Dataframe as a parameter and performs transformation on the dataframe.

![Screen Shot 2023-09-27 at 11 55 54 AM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/1eefe347-eb3e-4830-85ce-5dbacf67cb88)













