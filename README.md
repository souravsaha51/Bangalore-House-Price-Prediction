
# Bangalore House Prediction using Machine Learning Algorithm

## Project Objectives :
The objective of the project is to create a machine learning model. We are doing a supervised learning and our aim is to do predictive analysis to predict housing price.


## Introduction
* The project aim to predict rental house prices in Bangalore city, Karnataka. By combining Data Science techniques with web development skills, we’ve created a valuable resource for potential home buyers and real estate enthusiasts. 
* Linear Regression is the choosen Algorithm for the fundamental technique in predictive model. The project demonstrates a comprehensive approach to predicting housing prices.
* The purpose of deploying this project is to gain practical knowledge in the field of Data Science and to make the fundamental strongs. The project provide many new information about the Data Analysis, Outlier Detection and Removal and many more. 



## Implementation
  ### Data Collection
  * The dataset for model building is taken from the kaggle website. Kaggle is a data science competition platform and online community of data scientists and machine learning practitioners. Kaggle enables users to find and publish datasets, explore and build models in a web-based data science environment
  * The Bangalore Housing Dataset is a comprehensive collection of real estate listings within the bustling city of Bangalore, India. This dataset provides a very basic set of information about residential properties, facilitating in-depth analysis and insights into the city's housing market.
  Link: https://www.kaggle.com/datasets/sarthakniwate13/bangalore-house-price-dataset
  ### Data Cleaning
  * After collecting the dataset from the kaggle website, the data cleaning process set up. Identified and removed any missing null values from the dataset. Ensuring that the subsequent analysis are based on complete data.
  * Removed Unnecessary columns such as availability, society, balcony etc from the dataset and trim it down to dataset with columns such as location, bhk, total_sqft, bath and price.Trimming reduces noise and simplifies the dataset.
  * Converted some dataset columns values for easier access such as total_sqft columns values are converted into float values. A new column bhk is created for keeping the values of size column and the data type is int. 
  ### Feature Extraction
  * After completing the data cleaning process, we have begin with feature extraction process. Feature Engineering is the process of using domain knowledge to extract feature from raw data via machine learning techniques. These features can be used to improve the performance of machine learning algorithm.
  * Created a new column named price_per_sqft by calculating it. The price column is divided by total_sqft column. This column help in camparing the average price of 1bhk, 2bhk, 3bhk, 4bhk, 5bhk. This further help in later processes.
  * Extracted unique location values from the location columns which is helpful in making a drop-down list of our website. Explore statistical summaries for each location to identify trends and outliers. Eliminate locations where the houses available for rent is less than 10.
  ### Outlie Detection and Removal
  * Outlier is an observation that diverges from an overall pattern on a sample. There are many outlier detection techniques such as Extreme Value Analysis, Probabilistic and Statistical Modeling.Here we have used simple domain knowledge of real state market to detect the outliers of the dataset.
  * Firstly I remove houses which have less than 300 sqare feet area for 1 room, which is the average area of 1 bhk flat in Bangalore city. This step ensures that the dataset contains reasonable data points for analysis.
  * For outlier detection, I created a scatter plot for 2 bhk and 3 bhk houses which are in the same location. The discrepancy between 2 BHK and 3 BHK prices served as an indicator of outliers.
  * For outlier removal, group the houses for each location first. Then detected 2 BHK houses with unusually high prices compared to 3 BHK houses. Removing these outliers ensures a cleaner dataset for model training
  ### model Building
  * Categorical features (like location) were encoded into binary form (True/False) using one-hot encoding. For each house, compared its location with a dataset containing only location labels. If the location column matched a value, it turned True for that cell; otherwise, it was False.This process created a binary representation of location information.
  * The binary location representation was merged back into the original dataset. Now the dataset includes both numerical and binary features. We used train_test_split from sklearn.model_selection to split the dataset into training and testing sets. Importing LinearRegression from sklearn.linear_model,we trained a linear regression model.
  * Linear regression is a suitable choice for predicting continuous target variables like house prices. After fitting the model with the training and test datasets, we evaluated its performance. Achieving a model accuracy of 84.52% indicates that our linear regression model captures a significant portion of the variance in house prices.

## Web Development 
  ### prediction_model Directory
  * Under this directory, we have saved column.json file containing all the distinct location name in it. We are able to generate a dynamically populate location dropdowns on our website. 
  * Using the pickle library, we serialized our trained linear regression model. The model is saved as banglore_home_prices_model.pickle. Serialization ensures that we can easily load the model in our server code for predictions.
  ### backend_server Directory
  * Under this directory we have created a sub-directory name guide. It contain the copy of the column.json file and banglore_home_prices_model.pickle. These both were used in building our flask server. 
  * In server.py, integration includes invoking the fetch_loc_name function from util.py through a GET request API to retrieve location names and seamlessly deliver responses to the frontend UI. Additionally, it manages the forecast_home_price function, accessible via both GET and POST requests, which collects user inputs and initiates get_evaluated_price to deliver predicted responses effectively to the frontend UI.
  * The util.py file simply load the data from the column.json file when fetch_loc_name function request is generated from the server.py file. It load the banglore_home_prices_model.pickle for evalution of price when forecast_home_price function request is called from server.py file.
  ### frontend_ui Directory
  * The directory contains three distinct files namely app.html, app.css, and app.js, each utilizing a different language for developing the website's user interface. HTML defines the structure and content of the webpage, CSS dictates its presentation and styling, while JavaScript provides interactive functionality and dynamic behavior to enhance user experience.
  * The css file, app.css is basically use to inhance the UI of the website. This file help in selecting the background of the website. Font sizes for Website title, Different Labels. It is also useful for creating scale selection containg values from 1 to 5 which is use in the BHK configuration and Bath configuration.
  * The javascript file, app.js is used from proper functioning of the website. On clicking the button, it takes total_sqft area, location, no_bhk and no_bath as input and all prediction model from the server.py file and finally return the evatuated prince in Lakhs.

***Outcome:  Linear regression algorithm gave the best score and hence used for doing actual prediction***

| model |	Best_score|	Best_params|
| ---      | ---       | ----- |
linear_regression|	0.821906|	{'normalize': False}|
lasso|	0.703225|	{'alpha': 1, 'selection': 'cyclic'}|
decision_tree|	0.755886|	{'criterion': 'mse', 'splitter': 'best'}|
