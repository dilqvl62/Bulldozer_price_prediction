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

![Screen Shot 2023-09-26 at 7 29 44 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/3cad1fee-9cff-4226-aa5f-60905ca35606)


* I also did a distribution of the SalePrice (target variable)
  It shows that most of the machines are below $20000, and keeps going less and less. There are not many that cost over $100000

![Screen Shot 2023-09-26 at 6 52 52 PM](https://github.com/dilqvl62/Bulldozer_price_prediction/assets/107519883/842716da-eb27-4534-8de7-e51e4067cb9a)

* Since this is a time series data 





















