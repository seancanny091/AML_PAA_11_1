# Practical Application Assignment 11.1 - What Drives the Price of a Car?


The goal of this project was to understand what factors make a car more or less expensive. Based on this understanding, clear recommendations as to what consumers value in a used car are to be provided. The dataset used in the analysis is available here:

[Link to Vehicles Dataset](/vehicles.csv)

The programming language used was Python, and the libraries used were: pandas, seaborn, matplotlib, numpy, sklearn and sweetviz.
The specifics of the analysis, including code, visualizations, comments, and observations are contained in the following Jupiter Notebook:

[Link to Jupyter Notebook](/PAA_11_1.jpynb)

## Business Understanding

The business task is to provide recommendations to a used car dealership on what factors influence car prices, helping them understand what consumers value in used cars. This will allow dealers to determine selling prices for their cars that the market will support. As a result of this understanding the key feature (aka. target) of concern for the analysis is price.

## Data Understanding

Dataset Overview:
* Total Rows: 362,867  
* Total Columns: 18  

Data Types and Features:
* Numerical Features: price, year, odometer. Note: price is the target value.  

* Categorical Features: region, manufacturer, model, condition, cylinders, fuel, title_status, transmission, VIN, drive, size, type, paint_color, state  
  * Nominal Categorical Features - categories do not have a natural order or ranking: region, manufacturer, model, fuel, title_status, transmission, VIN, drive, type, paint_color, state  
  * Ordinal Categorical Features - categories have a natural order or ranking: condition, cylinders, size  
  * Unique Values in Categorical Features  
* Region: 404 unique values  
* Manufacturer: 41 unique manufacturers  
* Model: 21,555 unique models  
* Condition: 6 categories  
* Cylinders: 8 categories  
* Fuel: 5 types  
* Title Status: 6 categories  
* Transmission: 3 types  
* Drive: 3 types  
* Size: 4 categories  
* Type: 13 categories  
* Paint Color: 12 colors  
* State: 51 states (including Washington D.C.)  

The dataset, named vehicles.csv, is in .csv format and comprises 18 columns and 426,880 rows, as illustrated below (refer to Figure 2). The target column, "price," is numerical, while only two other columns, "odometer" and "year," are also numerical. The remaining columns are categorical, encompassing both ordinal and nominal data. Consequently, the dataset is expected to exhibit imbalance prior to entering the modeling phase. With the exception of "region," "price," and "state," all columns contain numerous "NaN" values. No duplicates were detected. To gain deeper insights into the dataset, a preliminary data preparation, specifically data cleaning, is deemed necessary.

## Exploratory Data Analysis:

The python SweetViz and Panda profiling libraries were leveraged for initial data exploration. The complete reports are available here: 

[Link to SweetViz Report](/SWEETVIZ_Vehicles.html)
[Link to Pandas Report](/Pandas_Profiling_Report_Vehicles.html)


The following potential data quality issues were identified:
