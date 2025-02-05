# Oldy-Car

Link to Notebook: https://github.com/saeedjazebi/Oldy-Car/blob/main/Oldy_Car.ipynb

Executive Summary/Business Objectives-----
In this application, i explored a dataset from Kaggle. The original dataset contained information on 3 million used cars. The used dataset contains information on 426K cars to ensure the speed of processing. The goal is to understand what factors make a car more or less expensive. 
The client is a used car dealership and they asked for the parameters that the consumer value most in used cars. As a result of my analysis, I am providing clear recommendations to my client as to what kind of cars they should bring in their inventory.
The target variable is price, we would like to advise our customer, the dealership of the used car, which attributes affect the prices more and give him some recommendation: for example, what kind of cars have more value, which ones are cheaper, and why each one of them might be appropriate for a specific customer. Following I started with data clean up and conversion of categorical data to numerical (encoding), and imputation.

Data Understanding -----
First, I imported appropriate packages, functions, and transformers from different libraries. Then pulled the data from a csv file with 426k records, and started exploring the data and understanding the different attributes of the data: How many columns have missing values, how many columns have zeros, what proportion of columns are zeros or missing values, what types of data exists? Categorical or numerical? How many unique value in each column? What method is best to convert categorical data to numerical data? How to impute the missing values? Should we completely delete any columns due missing information or because they do not change the price?

Data Preparation -----
I dropped the columns that are not affecting the prices (id, VIN), also dropped the 'model' column as it has 28266 unique names. Also, removed the size column as more than 50% of the values are null and it would negatively skew our model. I also dropped rows that the target variable (price) is zero. 
I converted all objects to strings.
After examination of unique values in drive column, it was observed that 4wd and fwd should be the same, so I converted fwd to 4wd in all rows. 
I filled the null values in categorical columns with the mode value of the column.
I filled the null values in numerical columns with the mode value of the column.
I converted the Cylinder and Drive columns to numbers, as number of cylinders and drive could be directly translated to numbers. 
I encoded the condition column, since it is ordinal data and could be ranked by numbers.
I used the target encoder to convert the remaining categorical columns to numbers. 

Modelling -----
I used trained and used two AI models to identify which parameters could better predict the price of a used car: 1) Sequential Selection Metod 2- Lasso Regularization Method
I used Sequential Feature Selection method, to select most important parameters that affect the price. Five most important features are selected: 
['year', 'condition', 'fuel', 'drive', 'paint_color']

A Pipline is created with A Lasso model of degree 1 polynomial, and a standard scaler. The model is then optimized with its alpha hyper parameter using GridSearchCV.  This was also trained to assess which parameters are more effective representing the price. It looks like that the Odometer parameter is the most effective variable 

Evaluation -----
The two models above are tested with the test data and mean squared errors are derived to assess the accuracy. 
Deployment
The following parameters will be recommended to the dealership:
'year'
'condition'
'fuel'
'drive'
'paint_color'
‘Odometer’
