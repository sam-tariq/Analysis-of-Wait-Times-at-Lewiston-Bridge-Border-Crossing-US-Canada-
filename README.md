# Analysis of Wait Times at Lewiston Bridge Border Crossing US-Canada 
### Advance Data Management and Regression Analysis


### Introduction

Although the term Big Data has been in use since the early 1990s. It's fairly recently that the volume and speed with which data has been growing has truly done justice to the term. The total amount of data in the world was 4.4 zettabytes in 2013. That has risen steeply to 44 zettabytes by 2020. To put that in perspective, 44 zettabytes is equivalent to 44 trillion gigabytes. With this exponential increase in data, the need for better data management capabilities has also increased.

**Data Management** is the process of ingesting, storing, organizing, and maintaining data. It includes a complex set of operations that make accurate data in corporate systems easily available and accessible. This proves to be crucial to help drive operational decision-making and effective strategic planning by the various end-users in the business setting.

### Project Overview

In this project, we aim to demonstrate effectively **Advance Data Management** and **Regression Analysis** skills to analyze wait times at the Lewiston Bridge border crossing between the US and Canada. Using the dataset provided we perform preliminary data analysis to prepare it for our regression analysis. We have used two types of regression models, namely the **Ordinary Least Squares** regression and **Logistic regression** models, to analyze wait times for travelers. The purpose of developing two models is to identify the relevant relationships between the dependent variables and the independent variable and compare our results.

### Methodology

In this project, we show proficiency in **Data Cleaning** to extract the relevant data from the provided dataset. **Feature Engineering** to tailor our variables for our Regression models. **Exploratory Data Analysis** to determine how our variables are affecting our independent variable and determining trends between them and lastly developing the **Regression Models** to model the relationships between our target variable and dependent variables.

### Project Data

The Dataset for this project was taken from the **Open Government Canada website**. The Dataset provides periodic information regarding the delays experienced by both commercial and travelers flow for all border crossings between the US and Canada, for the years of **2010-2014**.

### Data Management and Analysis

Before developing the Regression models we need to prepare the dataset to the appropriate format. This involves the following steps:
1. Analysis Setup
2. Data Reading, Cleaning, and Filtering
3. Feature Engineering 
4. Exploratory Data Analysis

### Analysis Setup

The first step of our preliminary analysis was to incorporate all the relevant Python libraries which will allow us to fulfill our requirements. These include:
1. **Pandas** for data managenent
2. **Numpy** for mathematical operations
3. **Datetime** and **time** to manipulate datetime data
4. **Matplotlib** and **Seaborn** for visualizations 
5. **Holidays** to find the holidays of a specific country
6. **Statsmodels.formula.api** to run regression analysis 

### Data Reading, Cleaning and Filtering

Once we have imported all relevant packages we need to import the dataset as a dataframe to run some preliminary analysis on it and based on the results we filter and clean it. This involves the following steps:
1. The Dataset contains the data for all border crossings between the US and Canada, however for this project we are only focussing on the Lewiston bridge crossing. As such we filter out only the relevant rows from the dataset.
2. We drop the columns which are irrelevant to our requirements.
3. We observe that in the Travellers Flow column we have **"No Delay"** and **"Closed"** which are strings. As we can not use string values for our regression analysis, we replace all instances of "No Delay" with 0 and remove all instances of "Closed".
4. We rename the **"Travellers Flow"** column to **"Wait_Time"** and plot a distribution graph to visualize the delay time entries. We also use the **value_counts()** function to compliment the graph and see the number of times of a data entry in the dataset.
5. Through our visualization we observed that our dataset has some outliers. We remove these outliers to further clean our dataset.

### Feature Engineering

Feature engineering in machine learning is a process of transforming the given data into a form that is easier to interpret. We extract features from our dataset to use them on our regression models. The process includes the following steps:

1. Deciding what features to create
2. Creating features
3. Testing the impact of the identified features on the task
4. Improving the features if needed

Typically we perform numerical transformations, Category encoding, clustering, group aggregating, and principal component analysis. All of this is done to provide our machine learning models with high-quality data that in turn helps our models to explain the maximum amount of the data and improve their predictive capability.

In the case of our dataset, we use the **"Updated"** column, which contains the EDT date time as a string, to get datetime dependent variables. We first convert it from string to datetime format in a new column labeled **"Date"**. Using this new column we extract different components of the date to be used as our dependent variables. Namely, the **"hour"** variable containing the hour component of the datetime variable in 24-hour format, **"day"** variable containing the weekdays, and **"Months"** variable containing the 12 months. Using these three variables we further extract two more variables,  one being **"Weekday_or_Weekend"** which tells if a day is a business day or weekend day, second being **"Holidays"** which tells us if the day is a Canadian or US holiday.

To make these variables fit for our models we convert them into binary categorical variables. Using the hour variable we determine if a particular hour is in the first 12 hours of the day (represented by 0) or the last 12 hours of the day (represented by 1). Similarly using the day variable we determine if a day is a weekday or weekend, represented by 0 and 1 respectively. A similar approach is also used to determine if a day is a holiday or not, where 0 represents no holiday and 3 represents US & Canadian holidays.

This categorical conversion allows us to study the impact of these variables at a deeper subdivided level instead of just using them as their original versions.

### Exploratory Data Analysis

Exploratory Data Analysis is a tool that complements the results of the Feature Engineering process. In EDA we use visualization to view the patterns and trends of our dependent variables with our independent variable. This allows us to refine our variables and determine any hidden relationships and attributes of our variables.

With our refined dataset we plot our new variables against wait time. Using the subplot function of matplotlib we plot the scatter plots of each variable. From the resulting graphs, we can observe that for the **"hours"** variable the wait time is higher for the second part of the day. Also for the **"Months"** variable, we see that certain months have higher wait times as compared to others. As for **"Holidays"** variable, we observe that the wait time is slightly less when there is a holiday while for the **"Weekday_or_Weekend"** variable we observe no distinguishable pattern.

Based on our EDA we can categorize our **"Months"** variable into high wait time months and low wait time months, represented by 1 and 0 respectively.

Once we are done with refining our dataset and regression variables we can now remove some of the now redundant columns to make the dataset cleaner.

Lastly, we perform correlation analysis to measure the strength of the linear relationship between two variables and compute their association. This is done to determine which of the variables are highly correlated with our target variable and among themselves. High correlation with the target variable is desirable, however high correlation among the dependent variables leads to multicollinearity which distorts the results of our regression models.

We observe that all dependent variables are positively correlated with the target variable. With the **"hours"** variable being the highest correlated variable. As such we can use all of the variables in our models.

### Regression Analysis
Regression analysis is a powerful statistical tool that allows you to examine the relationship between two or more variables. While there are many types of regression analysis, the core concept of all of them is to examine the influence of one or more independent variables on a dependent variable. This analysis allows us to estimate a value for the dependent variable when the independent variables are given a specific set of values.

For our project, we are running two types of regression analysis. The first is the Ordinary Least Square analysis and the second is the Logistic regression analysis. 

#### Ordinary Least Squares (OLS) Regression 
In Ordinary Least Squares (OLS) we estimate the target parameters in a linear regression model. OLS minimizes the sum of the squares of the differences between the observed dependent variable in the given dataset and those predicted by the linear function of the independent variable. Smaller the differences, the better the model fits the data. In simple linear regression, there is a single regressor on the right side of the regression equation.

For our dataset, we run the OLS regression analysis using the **Statsmodels.formula.api** package. It has a convenient ols function that just requires a simple equation of the variables.

#### Results
To interpret the results of our regression analysis we look at the P-values and Adjusted R-Squared value in the regression table. The P-value tells us which of the dependent variables are significant to our model and affect the target variable. While the Adjusted R-Squared value tells us about how much of our target variable's variability is explained by the dependent variables. We can observe that the P-value of all variables is less than alpha, which in our case is 0.05, as such all of them are significant and affect the wait time. The Adjusted R-Squared is 0.148, which means that approximately 14.8% of the variability in wait time can be explained by our dependent variables.

#### Logistic Regression
Logistic regression is a classification model used when the target variable is a categorical variable having discrete values. The basic form of the model caters to binary target variables. The primary difference between linear regression and logistic regression is that logistic regression's range is bounded between 0 and 1. In addition, as opposed to linear regression, logistic regression does not require a linear relationship between inputs and output variables. This is due to applying a nonlinear log transformation to the odds ratio.

Before running our logistic regression analysis we need to convert our wait time variable into a binary categorical variable. To achieve this we take the Average of the wait time column and compare it with all the data entries. All instances where the average wait time was greater than the data value, are denoted by 0 while all other instances are represented by 1. 

Just like in the case of OLS, Statsmodels.formula.api package also has a convenient logit function that just requires a simple equation of the variables.

#### Results
To interpret the results of our regression analysis we look at the P-values and Pseudo Adjusted R-Squared value in the regression table. The P-value tells us which of the dependent variables are significant to our model and affect the target variable. While the Pseudo Adjusted R-Squared value tells us about how much of our target variable's variability is explained by the dependent variables. We can observe that the P-value of all variables is less than alpha, which in our case is 0.05, as such all of them are significant and affect the wait time categorical variable. The Adjusted R-Squared is 0.1778, which means that approximately 17.78% of the variability in wait time can be explained by our dependent variables.

### Model Comparison
In both of our regression models, we observe that all the dependent variables were significant. However, when we compare the Adjusted R-Squared value of the OLS model and Pseudo Adjusted R-Squared value of the Logistic model we see that the Logistic model explains a greater percentage of variability in the target variable. As such we can conclude that for this dataset the Logistic Regression model was a better fit.

### Conclusion:
By looking at the results we can conclude that despite the Logistic model being a better fit, both models don't explain a significant percentage of variability in the test variable. This can be explained by the influence of other external factors that may be affecting the wait time. Some of them may be:

1. Number of lanes 
2. Amount of traffic
3. Time taken by the Immigration officers to process a vehicle
4. Security checking time

By having data on such factors we may be able to not only better explain the variability of our target variable but also enhance the predictive capabilities of our models. 
