# Required-Assignment-11.1-What-Drives-the-Price-of-a-Car-
Required Assignment 11.1

**Jupyter Notebook:** https://github.com/rarces82-rockyory/Required-Assignment-11.1-What-Drives-the-Price-of-a-Car-/blob/main/Roy_A_practical_application_ll_GIT.ipynb

**Model Design**

The first step was data cleaning. The dataset contained several missing values, a very large number of rows, and extremely large outliers in the price column.
I tested three different methods for handling outliers (Z-score, IQR, and manual filtering) and selected the approach that produced the lowest MSE.
Next, I built two forecasting models:
1. Model A – Simple Linear Regression (Numeric Features Only)
	•	Uses only year and odometer as predictors.
	•	A SimpleImputer with strategy "mean" was applied to handle missing values.
	•	This model provides a baseline to compare against the more complex model.

2. Model B – Multiple Regression with Mixed Features (Numeric + Categorical)
	•	Includes numeric features (year, odometer) and several categorical features (manufacturer, condition, cylinders, fuel, drive, type, state).
	Numeric data was processed with:
	•	SimpleImputer(strategy="mean")
	•	PolynomialFeatures(degree=2)
	•	StandardScaler()
	Categorical data was processed with:
	•	SimpleImputer(strategy="most_frequent")
	•	OneHotEncoder(handle_unknown="ignore")
Both pipelines were combined using a ColumnTransformer.
A Ridge regression model was applied to reduce overfitting.

Model Evaluation & Tuning

After fitting the model pipeline, I noticed that the MSE was too large to interpret due to the wide range of prices (0–300,000+).
For this reason, RMSE was used as the main performance metric.
	•	Best model RMSE: ≈ 7,448.9
	•	Performed cross-validation, which yielded RMSE values around 7,820.8 across folds.
	•	Conducted Grid Search to tune the Ridge parameter.
	•	Best alpha: 0.1
	•	This improved the overall error and stability of the model.

Feature Importance (Coefficients)

To understand what drives car prices, I extracted and analyzed the model coefficients.

I generated a table showing the Top 15 positive and Top 15 negative coefficients among the categorical variables.
To get accurate and interpretable results, I excluded certain highly granular fields such as model and year, since those features were included in other analysis
This allowed me to better understand which brands, fuel types, conditions, engine sizes, and states have the strongest upward or downward impact on vehicle price



**Executive Summary – Key Insights for Optimizing Used Car Inventory**

Dear Used Car Dealership Team,

Thank you for the opportunity to analyze your current inventory strategy. After an extensive review of more than 400,000 used-car listings across the United States, several important insights emerged that can help you fine-tune your inventory for profitability, turnover speed, and pricing accuracy.

Below is a consolidated summary of the most influential factors driving both vehicle price and sales behavior in the market.

1. Core Features That Drive Vehicle Price
These three variables consistently have the largest impact on how much a used vehicle sells for:
Year: Newer vehicles command a premium; each additional year of age typically decreases the average price.
Odometer: Mileage has a strong negative correlation with price. Lower mileage increases value substantially.
Condition: Vehicles listed as excellent or like new show significantly higher market prices, while fair or salvage conditions depress value.

2. Features That Increase Vehicle Price
Certain attributes significantly lift a vehicle’s market value: 

Larger Engines (10–12 cylinders):
These engines dramatically increase price and are often associated with:
	•	Performance vehicles
	•	Heavy-duty trucks
	•	Luxury brands

This aligns with premium models like Ferrari, McLaren, and high-end pickup trucks.

Sports & Luxury Body Types:
Convertibles, coupes, and high-performance variants tend to be priced higher because:
	•	They include premium engines
	•	Demand is strong among enthusiast buyers
	•	Production volumes are lower, increasing scarcity

Geography:
Certain states exhibit higher used-car prices due to:
	•	Strong local economies
	•	Higher demand for specific vehicle types
	•	Limited supply in rural markets

States showing above-average price lifts include:
Washington, Utah, Hawaii, Montana, and Oregon.

3. Features That Decrease Vehicle Price
On the opposite end of the spectrum, several features consistently reduce vehicle pricing:

Smaller Engines (3–4 cylinders):
These are common in compact sedans, wagons, and economy vehicles.
Price reductions typically range from $1,000 to $7,000 compared to larger engines.

Fuel Type (Gas & Hybrid):
Gasoline and hybrid vehicles tend to cost less on average compared to diesel vehicles

Traditional Body Styles:
Station wagons, compact sedans, and base-trim vehicles generally fall into lower price brackets.

4. Market Demand – What Sells the Most?
The Pareto analysis revealed that a small group of models accounts for the majority of all used-car listings and sales.

Top-Selling Vehicle: Ford F-150
The Ford F-150 remains the dominant leader in the U.S. market due to:
	•	High utility
	•	Broad consumer demand
	•	Strong resale value

Other highly demanded pickup trucks include:
	•	Chevrolet Silverado 1500
	•	Ram 1500

Pickup trucks represent a significant portion of market activity—no surprise given their popularity in both rural and urban regions.

Second-Tier Best Sellers: Sedans & SUV Models
The next most common and consistent sellers include:
	•	Toyota Camry
	•	Honda Accord
	•	Honda Civic
	•	Toyota Corolla
	•	Jeep Wrangler
	•	Nissan Altima

These vehicles combine reliability, affordability, and strong brand reputation, making them frequent and fast-moving inventory items.

5. Summary for Inventory Strategy

Based on the analysis, here are the key recommendations:

•	Stock more high-demand models
F-150, Silverado 1500, Camry, Accord, Civic, Wrangler.

•	Keep select high-margin luxury/performance vehicles
Ferrari, Porsche, Aston Martin, Tesla, McLaren, Rolls Royce.

•	Avoid excess inventory of low-demand, small-engine vehicles

Next Steps  

- Build an automated pricing dashboard  
- Integrate this model with your sales team and procurement  
- Continue monitoring new listings to update coefficients  
- Analyze seasonality to forecast peak buying periods  
- Use geographic demand insights
- Vehicles sourced from OR, UT, HI, MT, WA often carry higher resale value

