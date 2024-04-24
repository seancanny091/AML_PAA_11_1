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

Outliers - price, year, odometer
Outliers are removed from a dataset to enhance model performance, improve interpretability, meet assumptions of statistical techniques, increase model robustness, and ensure data quality. By eliminating outliers, models can better capture underlying patterns, make more accurate predictions, and draw clearer conclusions from the data. In the case of this dataset we'll use DBSCAN to identify outliers as it is robust enough to handle different distributions.
<br>
<br>
Before removal:
<br>
![Image](/images/PreOutlierStats.png)
![Image](/images/BoxPriceYearOdoBefore.png)
<br>
<br>
After removal:
<br>
![Image](/images/PostOutlierStats.png)
![Image](/images/BoxPriceYearOdoAfter.png)

Visualizations of Features (independent variables) against Price (target/dependent variable):


![Image](/images/PriceCondition.png)
<br>
Observation: There is a direct correlation between condition and mean price with 'new' commanding the highest mean price, and 'fair' the lowest.


![Image](/images/PriceTransmission.png)
<br>
Observation: There is a direct correlation between condition and mean price with 'new' commanding the highest mean price, and 'fair' the lowest.


![Image](/images/PriceTransmission.png)
<br>
Observation: Other transmission commands the highest mean price. This may relate to some luxury/exotic cars having specialized transmission options.


![Image](/images/PriceSize.png)
<br>
Observation: There is a direct correlation between size and price with full-size commanding the highest mean price. Interestingly, sub-compacts appear to command a higher mean price than compacts which command the lowest mean price.


![Image](/images/PriceDrive.png)
<br>
Observation: 4-wheel drive commands the highest mean price. Front-wheel drive commands the lowest mean price.


![Image](/images/PriceFuel.png)
<br>
Observation: Diesel commands the highest mean price. Hybrid commands the lowest mean price.


![Image](/images/PriceColor.png)
<br>
Observation: White commands the highest mean price, followed by orange (strangely enough - again may be due to the presence of exotic cars in the dataset), and black. Green commands the lowest mean price.


![Image](/images/PriceTitle.png)
<br>
Observation: Vehicles with lien titles command the highest mean price, and vehicles with parts-only titles command the lowest mean price. This makes sense as a parts-only title basically means the vehicle is junk.


![Image](/images/PriceCyl.png)
<br>
Observation: 10 cylinders commands the highest mean price, and 5 cylinders commands the lowest mean price.


![Image](/images/PriceType.png)
<br>
Observation: Trucks command the highest mean price, and hatchbacks command the lowest mean price.


![Image](/images/PriceType.png)
<br>
Observation: Trucks command the highest mean price, and hatchbacks command the lowest mean price.


![Image](/images/PriceManuf.png)
<br>
Observation: Luxury brands such as Ferrari, Aston Martin, and Tesla command the highest mean price, and Saturn commands the lowest mean price.


![Image](/images/PriceOdo.png)
<br>
Observation: The mean price tends to decrease with increasing odometer.


![Image](/images/PriceYear.png)
<br>
Observation: For vehicles made in the last 20 years or so the mean price tends to increase with increasing year. There are interesting spikes for vehicles in the early 1900s and those made in the 1950s and 1960s. This is possibly due to these being collectible vehicles.


![Image](/images/PriceState.png)
<br>
Observation: Vehicles in Alaska command the highest mean price and those in Ohio command the lowest mean price.


![Image](/images/PriceState.png)
<br>
Observation: Vehicles in Alaska command the highest mean price and those in Ohio command the lowest mean price.


### Feature Engineering

Nominal Categorical Features (do not have a natural order or ranking) - treated using getDummies to translate variables to boolean values:
* manufacturer
* fuel
* title_status
* transmission
* drive
* type
* paint_color
* state

Ordinal Categorical Features (have a natural order or ranking) - treated by directly assigning integer values to the feature, e.g., size: full-size = 3, mid-size = 2, compact = 1, sub-compact = 0:
* condition
* cylinders
* size

Most of the features are binary valued, so it was decided to scale the values of the non-binary features "price", "odometer", "year" to reduce imbalance:
* Price/10000
* Odometer/100000
* Year/1000

The dataset was then split into independent and dependent variable datasets.

Permutation importance analysis was utilized in an attempt to identify the most impactful features: Odometer, fuel - gas, year, cylinders, drive - fwd were the top 5 most impactful feature identified. 




At this stage an attempt was made to build and run a linear regression model against the data but the K_Fold cross validation failed. It was suspected that this was due to the high dimensionality (127 features) of the dataset. It was decided to perform primary component analysis to reduce dimensionality while retaining most of the variance.

### Principal Component Analysis

Number of components to capture 80% variance: 20
Cumulative Variance explained by these components: 0.8019850326549288

![Image](/images/CumVarPCA.png)
<br>
<br>
![Image](/images/PCALoadings.png)

The top three features in the top five primary components were determined to be as follows:

![Image](/images/Top3FeatTop5PC.png)

## Modeling

A final dataset was generated after applying principal component analysis and this was used for modeling. The dataset was split 80:20 into training and testing datasets to allow for Hold-Out cross validation. Additionally, K-Fold cross validation was used.

### Simple Linear Regression Model

![Image](/images/SimLinReg.png)

#### Metrics:
* Cross Validation Negative Mean Squared Error (MSE): -0.886 ± 0.101
* Cross Validation R²: 0.492 ± 0.092
* Train MSE: 0.727
* Test MSE: 0.743
* Score: 0.531

PCA ranking:<br>
![Image](/images/SimLinRegPCA.png)


### Ridge Regression

![Image](/images/RidgeLinReg.png)

#### Metrics:
Cross Validation Negative MSE: -0.727 ± 0.025
Cross Validation R²: 0.492 ± 0.092
Train MSE: 0.727
Test MSE: 0.743
Score: 0.531

PCA ranking:<br>
![Image](/images/RidgeLinRegPCA.png)


### Lasso Regression:

![Image](/images/LassoLinReg.png)

#### Metrics:
Cross Validation Negative MSE: -1.614 ± 0.141
Cross Validation R²: -0.040 ± 0.021
Train MSE: 1.603
Test MSE: 1.645
Score: -0.037

PCA rankings:<br>
![Image](/images/LassoLinRegPCA.png)


## Evaluation

![Image](/images/eval.png)

Train and Test MSE: Ridge Regression has the lowest Mean Squared Error (MSE) for both training and testing, indicating it might be handling overfitting slightly better than Linear Regression, which has similar values. Lasso Regression, however, shows significantly higher MSE values, suggesting it might not be fitting the data well.  

Scores: Ridge and Linear Regression have similar scores, which are substantially higher than the negative score of Lasso Regression. This further supports that Lasso Regression is underperforming compared to the other two models in this dataset.  

These visualizations clearly show that Ridge Regression, while having similar performance metrics to Linear Regression, might be slightly more robust given its lower MSE values. Lasso Regression, on the other hand, appears to be the least effective model for this particular dataset.


### Conclusions and Next Steps:

Permutation Importance Findings: 
The odometer feature has the highest importance, suggesting mileage is a crucial factor in predicting vehicle price. Fuel-related features, year, and condition of the vehicle also show notable importance. Geographic location, manufacturer, and vehicle type also influence vehicle prices.  

Regression Model Findings: 
Ridge, Linear, and Lasso regression models all show a positive influence of features like 'cylinders', 'size', 'drive_fwd', and 'type_sedan' on vehicle price. The Ridge model appears to perform better than the other models based on the reported performance metrics. The Linear Regression model faced issues with the original dataset, requiring the use of Principal Component Analysis (PCA) to reduce dimensionality.  

Potential Next Steps: 
* Feature Engineering - Explore additional features that could further improve the predictive power of the models, such as detailed vehicle specifications, market trends, or economic factors.  
* Model Comparison and Tuning - Conduct a more comprehensive comparison of these and other regression models, including hyperparameter tuning and cross-validation to ensure robust performance.  
* Handling Dimensionality - Investigate alternative approaches to address the dimensionality issues encountered with the Linear Regression model, such as feature selection or other dimensionality reduction techniques.  
* Interpretability - Provide more detailed explanations of the feature importance and the relationships between the predictors and the target variable (vehicle price) to enhance the interpretability of the models.  
* Real-world Deployment - Consider deploying the best-performing model in a real-world application, such as a vehicle pricing tool or a decision support system for buyers and sellers.
   
