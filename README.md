### Project Readme : Used Car Price Analysis

**Prepared by:** `Sylvester Prasanna`

**Project Summary:**

The `vehicles.csv dataset was analyzed using numpy, pandas and seaborn.

This analysis explores a dataset of 426,000 used cars to identify and quantify the factors that determine a vehicle's market price. The objective is to provide actionable recommendations to a used car dealership client, informing their inventory acquisition, pricing strategy, and marketing efforts. The project was executed using the CRISP-DM (Cross-Industry Standard Process for Data Mining) methodology to ensure a structured and robust approach.
1. Link to Jupyter Notebook:
2. Link to data folder:
3. Link to images folder:
4. ### CRISP:DM - Phase 1 : Business Understanding

### Problem Statement:
The primary business question is: **"What factors make a car more or less expensive?"**

The goal is to develop a predictable model that explains the variance in car prices, with a focus on core variables like age, mileage,  features like color, and intrinsic attributes (luxury class, fuel type, drivetrain). The output is required for car showroom managers for planning their future sales proposal.
### CRISP:DM - Phase 2 : Data Understanding
#### Data Understanding

**Goal:** Inspect dataset (vehicle.csv) shape, columns, distributions, NaN and identify cleaning needs.
**Steps followed:**
1. Loaded /data/vehicles.csv.
2. Showed head(), .info() and basic describe() for price.
3. Located price as the target column and counted missing values.

**Observation**

1. Dataset contains  rows × columns: 426,880 × 18.
2. price found as target (non-null for all rows).
3. Numeric columns detected: id, price, year, odometer.
4. Many categorical columns present: region, manufacturer, model, condition, cylinders, fuel, transmission, VIN, drive, size, type, paint_color, state, etc.
5. After dropping rows with missing price the dataset remained 426,880 rows.

**Next steps & Plan of action**
1. For initial model estimation, the following features are considered for dropping due to potential lack of sufficient data or insignificant influence on the target variable ("price"):
2. Region: Dropped due to having no significant influence on "price."
3. Model: Dropped.
4. #%% md
#### Data Understanding

**Goal:** Inspect dataset (vehicle.csv) shape, columns, distributions, NaN and identify cleaning needs.
**Steps followed:**
1. Loaded /data/vehicles.csv.
2. Showed head(), .info() and basic describe() for price.
3. Located price as the target column and counted missing values.

**Observation**

1. Dataset contains  rows × columns: 426,880 × 18.
2. price found as target (non-null for all rows).
3. Numeric columns detected: id, price, year, odometer.
4. Many categorical columns present: region, manufacturer, model, condition, cylinders, fuel, transmission, VIN, drive, size, type, paint_color, state, etc.
5. After dropping rows with missing price the dataset remained 426,880 rows.

**Next steps & Plan of action**
1. For initial model estimation, the following features are considered for dropping due to potential lack of sufficient data or insignificant influence on the target variable ("price"):
2. Region: Dropped due to having no significant influence on "price."
3. Model: Dropped.
4. Highly Sparse/Irrelevant Features: "Cylinders," "Title_status," "transmission," "VIN," "drive," and "size" can also be dropped for the preliminary model.
5. Potentially Insufficient Data: "condition," "paint_color," and "lat" are also flagged as having insufficient data, similar to some features above, and may be selectively dropped.
6. Further analysis on these dropped and sparse features will be considered after an initial, preliminary model has been successfully fitted.

### CRISP:DM - Phase 3 : Data Preparation
#%% md
#### Goal of Data Preparation Phase:

1. Cleaning data
2. Handling missing values
3. Encoding variables
4. Scaling features
5. Selecting relevant attributes
6. Feature engineering

#### Summary of Data Understanding Phase:
1. Columns with Int and Float will be used for all estimations.
2. Non numeric features will be used to estimate other factors inpacting the car price.

### CRISP:DM - Phase 4 :  MODELING &
#%% md
The core task was to fit a regression model to predict price. A pipeline approach was used, combining preprocessing steps with linear models.

1. LINEAR REGRESSION
2. RIDGE
3. LASSO
4. POLYNOMIAL REGRESSION

**Approach and purpose**

1. Regularization: Regularization (Ridge/Lasso) was required due to the instability of Ordinary Least Squares (OLS) coefficients in the presence of numerous One-Hot Encoded features.
2. Best $\alpha$: A sweep of the Ridge $\alpha$ (regularization strength parameter) was performed to find the optimal trade-off between bias and variance.
3. Polynomial Degree: Analysis of polynomial features suggested that non-linear terms are beneficial, with Degree 4 exhibiting the highest variance in prediction errors, highlighting the complex non-linear nature of price depreciation.

### CRISP:DM - Phase 5 : EVALUATION

**Results and Findings**
1. L2 Loss (MSE) = 145,461,667.79  ==> The average squared difference between the predicted price and the actual price.
2. RMSE = $12,060.75  ==> The root mean squared error, representing the average dollar magnitude of prediction error.
3.  R-Squared ($R^2$) = ~0.245 ==> The proportion of the variance in the price dependent variable that is predictable from the independent variables (indicating that only about 24.5% of the total price variance is explained by the simple linear model).

### CRISP:DM - Phase 6 : DEPLOYMENT
### Conclusion
#%% md
**Primary Finding:**
1. `Car Age` (year of mfg) and `Odometer` are the primary  numerical predictors. Scatter plots visualize a clear relationship. These 2 factors impact the vehicles base value.
2. `Evaluation Metrics (L2 Loss)` : The primary loss functions used for model training and evaluation were `L1 Loss (MAE) and L2 Loss (MSE)`. The simple linear model had an L2 Loss (MSE) of 145,461,667.79 and an RMSE of $12,060.75.
3. `Model Generalization`: Ridge (L2 regularization) and Lasso (L1 regularization) regression pipelines were employed to prevent overfitting, with a multi-feature model achieving an R-Squared of approximately 0.245.
4. `LASSO`: The Lasso regression penalized less influential features, setting 3 coefficients to exactly zero, thus performing intrinsic feature selection.
5. `K Means Clustering`: The K-Means clustering based on year and odometer successfully identified natural correlations (like  low-mileage/new vs. high-mileage/old), even before full feature processing.

**Additional Finding:**

6. Popular `colors` showed negative coefficients, notably paint_color_silver (-2,142.13) and paint_color_blue (-1,677.00).
7. Some common colors  'black' as the baseline, paint_color_white had a positive coefficient (523.18).
8. The `fuel_diesel` feature showed a high positive linear coefficient (14,131.50) compared to the baseline (gasoline), indicating a significant value-add.
9. The largest positive linear coefficients belong to `luxury manufacturers`, such as manufacturer_ferrari (74,098.18) and manufacturer_aston-martin (49,301.88).



5. Highly Sparse/Irrelevant Features: "Cylinders," "Title_status," "transmission," "VIN," "drive," and "size" can also be dropped for the preliminary model.
6. Potentially Insufficient Data: "condition," "paint_color," and "lat" are also flagged as having insufficient data, similar to some features above, and may be selectively dropped.
7. Further analysis on these dropped and sparse features will be considered after an initial, preliminary model has been successfully fitted.
