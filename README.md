# Practical Application Assignment 11.1 - What Drives the Price of a Car?


The goal of this project was to understand what factors make a car more or less expensive. Based on this understanding, clear recommendations as to what consumers value in a used car are to be provided. The dataset used in the analysis is available here:

[Link to Vehicles Dataset](/vehicles.csv)

The programming language used was Python, and the libraries used were: pandas, seaborn, matplotlib, numpy, sklearn and sweetviz.
The specifics of the analysis, including code, visualizations, comments, and observations are contained in the following Jupiter Notebook:

[Link to Jupyter Notebook](/PAA_11_1.jpynb)

## Business Understanding

The business task is to provide recommendations to a used car dealership on what factors influence car prices, helping them understand what consumers value in used cars. This will allow dealers to determine selling prices for their cars that the market will support. As a result of this understanding the key feature (aka. target) of concern for the analysis is price.

## Data Understanding

The python SweetViz and Panda profiling libraries were leveraged for initial data exploration. The complete reports are available here: 

[Link to SweetViz Report](/SWEETVIZ_Vehicles.html)
[Link to Pandas Report](/Pandas_Profiling_Report_Vehicles.html)

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
  
* Feature Statistics
  * Price: The average price is approximately $75199. There's a significant standard deviation, indicating wide price variations. The range is from $0 to over $3.7 billion, which suggests outliers or data entry errors.  
  * Year: The cars range from 1900 to 2022, with a median year of 2013. This indicates that most cars are relatively recent.  
  * Odometer: The average mileage is about 98,043 miles, with values ranging up to 10,000,000 miles, which might be an outlier.  
  * Condition: Most cars are listed as "good".  
  * Cylinders: "6 cylinders" is the most common specification.  
  * Fuel: The majority of cars use gas.  
  * Transmission: Automatic is the predominant transmission type.  
  * Drive: "4wd" (four-wheel drive) is common among specified entries.  
  * Type: Sedans are the most common type of car.  
  * Paint_color: White is the most frequent color.  

Other Observations
* The dataset is rich in categorical data, which provides a diverse view of the used car market across different regions and specifications.  
* The model column has a high number of unique values, indicating a wide variety of car models in the dataset.  
* The VIN column also has a high number of unique values, which could be useful for tracking individual cars but may not be as useful for general analysis due to its granularity.  

Data Quality Issues
* Price: Extremely high maximum value likely indicates outliers or errors.  
* Odometer: Extremely high maximum value suggests possible outliers.  
* Missing Values: Several columns like manufacturer, model, condition, cylinders, fuel, title_status, transmission, VIN, drive, size, type, paint_color have missing values. 

The dataset is expected to exhibit imbalance prior to entering the modeling phase. With the exception of "region," "price," and "state," all columns contain numerous "NaN" values. No duplicates were detected. To gain deeper insights into the dataset, a preliminary data preparation, specifically data cleaning, is deemed necessary.

## Data Preparation

The following initial data preparation steps were performed:
* Remove rows with missing values.
* Remove non-impactful or overly granular features i.e., id, VIN, model (21,555 unique values and somewhat correlated with manufacturer), and region (404 unique values and somewhat correlated with state).
* Remove unrealistic values (determined by visual inspection):
  *  Price (range preserved 100 - 600,000)
  *  Odometer (range preserved 0 - 500000)

Outliers - price, year, 
Outliers are removed from a dataset to enhance model performance, improve interpretability, meet assumptions of statistical techniques, increase model robustness, and ensure data quality. By eliminating outliers, models can better capture underlying patterns, make more accurate predictions, and draw clearer conclusions from the data. Outliers were removed using DBSCAN
<br>
<br>
Before removal:
![Image](/images/BoxPriceYearOdoBefore.png)
<br>
<br>
After removal:
![Image](/images/BoxPriceYearOdoAfter.png)




  
   
