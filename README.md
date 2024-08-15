# Flight Fare Prediction

## Problem Statement

As a Machine Learning Engineer or Data Scientist at MakeMyTrip (or a similar startup), our task is to develop a model that predicts flight fares across various routes. The core objective is to leverage this model to help the platform increase revenue by identifying customers who are less likely to book tickets. By recognizing these customers, the platform can strategically offer discounts, coupon codes, or special deals to encourage bookings. This approach can enhance customer engagement, improve conversion rates, and ensure that potential revenue is not lost.

## Methodology

### 1. **Loading and Understanding the Dataset**
   - **Objective:** Predict flight prices using various features.
   - **Actions:** 
     - Loaded the dataset and examined its structure.
     - Checked for null values, data types, and unique values in each column to ensure the data is suitable for modeling.

### 2. **Handling Missing Values**
   - **Objective:** Ensure data completeness to avoid any bias in the model.
   - **Actions:** 
     - Filled missing values in relevant columns like `Total_Stops` using the forward fill method.
     - Dropped rows with missing values in certain columns where data imputation was not feasible.

### 3. **Feature Engineering**
   - **Objective:** Extract meaningful information and create new features that contribute to model accuracy.
   - **Actions:**
     - Extracted day, month, and year from the `Date_of_Journey` column.
     - Extracted hours and minutes from the `Dep_Time` and `Arrival_Time` columns.
     - Converted `Duration` into hours and minutes, and created a `Duration_total_mins` feature representing the total duration in minutes.

### 4. **Data Transformation and Encoding**
   - **Objective:** Prepare categorical data for modeling and reduce the complexity of the dataset.
   - **Actions:**
     - Performed label encoding for categorical features like `Destination` and `Total_Stops`.
     - Dropped redundant or unnecessary columns like `Date_of_Journey`, `Additional_Info`, and others that were no longer needed after feature extraction.

### 5. **Outlier Detection and Handling**
   - **Objective:** Handle extreme values that could skew the model and lead to inaccurate predictions.
   - **Actions:**
     - Identified outliers in the `Price` column using the Interquartile Range (IQR) method.
     - Replaced extreme values above 35,000 with the median price to reduce their influence. We used the median instead of the mean because the mean is affected by outliers, whereas the median provides a more robust measure of central tendency.

### 6. **Feature Selection**
   - **Objective:** Identify the most important features that contribute to the model's predictive power.
   - **Actions:**
     - Used `mutual_info_regression` to calculate feature importance.
     - Sorted features by importance to focus on those most relevant for prediction.

### 7. **Building Initial ML Model**
   - **Objective:** Establish a baseline predictive model to assess initial performance.
   - **Actions:**
     - Split the data into training and test sets.
     - Built a `RandomForestRegressor` model and evaluated its performance using the `R²` score.

### 8. **Model Persistence with Pickle**
   - **Objective:** Save the trained model for future use without the need to retrain it.
   - **Actions:**
     - Serialized the trained model using `pickle`.
     - Provided examples of how to load the model and make predictions on new data.

### 9. **Automating ML Pipeline & Defining Evaluation Metric**
   - **Objective:** Streamline the model-building process and introduce custom evaluation metrics.
   - **Actions:**
     - Created a custom `mape` (Mean Absolute Percentage Error) function to evaluate the model.
     - Built a function to automate model training, prediction, and evaluation, providing key metrics like `MAE`, `MSE`, `RMSE`, and `MAPE`.

### 10. **Hyperparameter Tuning**
   - **Objective:** Optimize the model's performance by fine-tuning its parameters.
   - **Actions:**
     - Used `RandomizedSearchCV` to tune hyperparameters for the `RandomForestRegressor`.
     - Expanded the hyperparameter space to include a wider range of values for a more thorough search.
     - Achieved improved performance with the optimal hyperparameters, leading to better model accuracy.

### 11. **Final Evaluation**
   - **Objective:** Compare the improvements in model performance after hyperparameter tuning.
   - **Actions:**
     - Compared the `R²` score and model structure between the initial and optimized models.
     - Observed that the expanded hyperparameter space and tuning led to better performance, capturing more data patterns and improving generalization.

## Conclusion

This project followed a structured approach to data preprocessing, feature engineering, model building, and optimization. By expanding the hyperparameter space and performing thorough tuning, the predictive accuracy of the model was significantly enhanced. The final model can now be used to predict flight fares reliably, helping the platform make informed decisions to improve customer engagement and maximize revenue.
