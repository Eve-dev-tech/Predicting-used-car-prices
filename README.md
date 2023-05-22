# Predicting-used-car-prices
This is a project that expected me to come up with a pricing model that could effectively predict the price of used cars and help the business in devising profitable strategies using differential pricing.

This project is part of my project assignments for my MIT IDSS data science and Machine learning Certification program.


## Objective
Explore and visualize the dataset.
Build a model to predict the prices of used cars.
Generate a set of insights and recommendations that will help the business.

## The key question
Which factors would affect the price of used cars?

## Problem Formulation:
I have a regression problem at hand where I will try to predict the price of used cars based on several factors such as - Year of manufacturing, Number of seats, Mileage of the car, etc.

## Data Dictionary
S.No.: Serial Number

Name: Name of the car which includes Brand name and Model name

Location: The location in which the car is being sold or is available for purchase (Cities)

Year: Manufacturing year of the car

Kilometers_driven: The total kilometers driven in the car by the previous owner(s) in KM.

Fuel_Type: The type of fuel used by the car. (Petrol, Diesel, Electric, CNG, LPG)

Transmission: The type of transmission used by the car. (Automatic / Manual)

Owner: Type of ownership

Mileage: The standard mileage offered by the car company in kmpl or km/kg

Engine: The displacement volume of the engine in CC.

Power: The maximum power of the engine in bhp.

Seats: The number of seats in the car.

New_Price: The price of a new car of the same model is INR 100,000 (INR = Indian Rupee)

Price: The price of the used car is INR 100,000 (Target Variable)


## Proposed approach
## Potential techniques :
Since it is a regression problem I will first start with the parametric model - linear regression and Ridge Regression.

## Overall solution design :
The potential solution design would look like this:

Checking the data description to get the idea of basic statistics or summary of data.
Univariate analysis to see how data is spread out, getting to know about the outliers.
Bivariate analysis to see how different attributes vary with the dependent variable.
Outlier treatment if needed - In this case, outlier treatment is not necessary as outliers are the luxurious cars and in real-world scenarios, such cars would appear in data and we would want our predictive model to capture the underlying pattern for them.
Missing value treatment using appropriate techniques.
Feature engineering - transforming features, creating new features if possible.
Choosing the model evaluation technique - 1) R Squared 2) RMSE can be any other metrics related to regression analysis.
Splitting the data and proceeding with modeling.
Model tuning to see if the performance of the model can be improved further.

## Measures of success :
R-squared and RMSE can be used as a measure of success.

R-squared: This will tell me how much variation our predictive model can explain in data.

RMSE: This will give me a measure of how far off the model is predicting the original values on average.

## Model Building
What I want to predict is the "Price". I will use the normalized version 'price_log' for modeling.
Before I proceed to the model, I'll have to encode categorical features. I will drop categorical features like Name.
I'll split the data into train and test, to be able to evaluate the model that I build on the train data.
Build Regression models using train data.
Evaluate the model performance.

## Observations from the model
With my linear regression model I have been able to capture ~90 variations in omy data.

The model indicates that the most significant predictors of the price of used cars are -

The year of manufacturing

Number of seats in the car

Power of the engine

Mileage

Kilometers Driven

Location

Fuel_Type

Transmission - Automatic/Manual

Car Category - budget brand to ultra-luxury

The p-values for these predictors are <0.05 in our final model.

Newer cars sell for higher prices. 1 unit increase in the year of manufacture leads to [exp(0.1170) = 1.12 Lakh] increase in the price of the vehicle when everything else is constant. It is important to note here that the predicted values are log(price) and therefore coefficients have to be converted accordingly to understand that influence in Price.
As the number of seats increases, the price of the car increases - exp(0.0343) = 1.03 Lakhs.
Mileage is inversely correlated with Price. Generally, high Mileage cars are the lower budget cars. It is important to note here that correlation is not equal to causation. That is to say, an increase in Mileage does not lead to a drop in prices. It can be understood in such a way that the cars with high mileage do not have a high power engine and therefore have low prices.
Kilometers Driven have a negative relationship with the price which is intuitive. A car that has been driven more will have more wear and tear and hence sell at a lower price, everything else being constant.
The categorical variables are a little hard to interpret. But it can be seen that all the car_category variables in the dataset have a positive relationship with the Price and the magnitude of this positive relationship increases as the brand category moves to the luxury brands. Here the dropped car_category variable for budget-friendly cars serves as a reference variable to other car_category variables when everything else is constant. 1 unit increase in car_category_Luxury_Cars leads to [exp(0.4850) = 1.62 Lakh] increase in the price of the vehicle than the car_category_budget_friendly_Cars that serves as a reference variable when everything else is constant.


# Refined insights:
## Name:
The Name column has 2041 unique values and this column would not be very useful in our analysis. But the name contains both the brand name and the model name of the vehicle and we can process this column to extract Brand and Model names to reduce the number of levels.
Extracting the car brands:

After extracting the car brands from the name column I find that the most frequent brand in our data is Maruti and Hyundai.
## Extracting car model name:

After extracting the car name it gets clear that our dataset contains used cars from luxury as well as budget-friendly brands.
The mean price of a used Lamborghini is 120 Lakhs and that of cars from other luxury brands follow in descending order and this output is very close to our expectation (domain knowledge), in terms of brand order. Towards the bottom end, we have more budget-friendly brands.
## Important variable with Random Forest:
According to the Random Forest model the most significant predictors of the price of used cars are
Power of the engine
The year of manufacturing
Engine
New_Price
# Business Insights and Recommendations
Some southern markets tend to have higher prices. It might be a good strategy to plan growth in southern cities using this information. Markets like Kolkata (coeff = -0.2) are very risky and I need to be careful about investments in this area.
I will have to analyze the cost side of things before we can talk about profitability in the business. We should gather data regarding that.
The next step would be to cluster different sets of data and see if we should make multiple models for different locations/car types.
Proposal for the final solution design:
My final tuned Decision model has an R-squared of ~0.89 on the test data, which means that my model can explain 89% variation in my data also the RMSE on test data is ~3.75 which means i can predict very closely to the original values. This is a very good model and I can use this model in production.

