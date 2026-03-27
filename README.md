# Q4
(a) Explain the problem and why AI is suitable.
The Problem:
CompanyA, a charity organization, faces the challenge of accurately predicting the daily demand for lunchboxes over a 30-day period, coinciding with the Hari Raya festive season. They have a fixed target of providing lunchboxes to 40 families. The core problem is to determine how many lunchboxes will be needed each day to meet the needs of these families without excessive waste or shortages. Factors influencing this demand can include:
The specific needs or availability of the 40 families on any given day.
The impact of the Hari Raya period on family routines and needs.
Potential external factors like weather, local events, or logistical challenges.
An incorrect prediction can lead to either:
Food Waste: Preparing too many lunchboxes, leading to financial and resource inefficiency for the charity.
** unmet Needs:** Preparing too few lunchboxes, failing to serve all the intended families and potentially causing disappointment.
Why AI is Suitable:
AI, particularly machine learning, is well-suited for this problem due to its ability to:
Identify Complex Patterns: Food demand is rarely static. It can be influenced by subtle, interconnected factors (e.g., day of the week, proximity to Hari Raya, weather). AI algorithms can analyze historical data to uncover these non-linear relationships and patterns that might be missed by traditional forecasting methods or human intuition.
Handle Time-Series Data: The problem involves predicting demand over a sequence of days, making it a time-series forecasting task. AI models are adept at learning from sequential data and identifying trends, seasonality, and holiday effects.
Optimize Resource Allocation: By providing more accurate demand predictions, AI enables CompanyA to optimize the number of lunchboxes prepared. This directly translates to efficient use of their budget and resources, minimizing waste and ensuring that aid reaches those who need it most.
Adaptability: AI models can be retrained with new data as it becomes available. This allows the prediction system to adapt to changing circumstances or evolving demand patterns, maintaining its accuracy over time.
Quantifiable Forecasting: AI provides quantitative predictions (e.g., "predicting 35 lunchboxes for Tuesday"), which are actionable for planning procurement and preparation.
Q4 (b) Propose a complete AI solution.
Here's a proposed AI solution for CompanyA's food demand prediction:
Data Collection and Understanding:
Historical Data: Gather past data on lunchbox distribution. This should ideally include:
Date and time of distribution.
Number of lunchboxes distributed each day.
Information about specific periods (e.g., if it was during a holiday, school break, or Hari Raya season).
Potentially, any recorded external factors like weather for those days.
Contextual Data: Information specific to the 30-day period, such as the official Hari Raya dates, any planned community events, or known changes in family availability.
Data Preprocessing and Feature Engineering:
Cleaning: Handle any missing values in the historical data (e.g., impute with the average demand for that day of the week). Ensure all data is in a consistent format.
Feature Creation: Engineer relevant features that can help the model learn demand patterns:
Time-Based Features: Day of the week, week of the year, day of the month, is_weekend.
Holiday/Event Features: A binary feature is_hari_raya_period (1 if within the 30 days, 0 otherwise), days_until_hari_raya, days_since_hari_raya.
Lagged Features: Demand from the previous day (demand_lag_1), demand from the same day last week (demand_lag_7).
External Factors: If available, incorporate weather data (e.g., temperature, precipitation).
Model Selection:
Problem Type: This is a time-series forecasting problem aiming to predict a numerical value (number of lunchboxes).
Recommended Model: Facebook Prophet (now Meta Prophet) is an excellent choice for this scenario.
Why Prophet? It's specifically designed for business time series that have strong seasonal effects and holiday impacts. It can automatically handle:
Daily, weekly, and yearly seasonality.
Customizable holiday effects (perfect for Hari Raya).
Robustness to missing data and outliers.
It's relatively easy to use and interpret.
Alternative: Gradient Boosting models like XGBoost or LightGBM could also be used if more complex feature interactions need to be modeled, but Prophet is likely more direct for this specific problem.
Model Training and Tuning:
Training: Train the Prophet model using the prepared historical data, including the engineered features.
Holidays DataFrame: Create a separate DataFrame for Prophet that explicitly lists Hari Raya dates and any other relevant local holidays.
Hyperparameter Tuning: Adjust parameters like seasonality_mode, changepoint_prior_scale, and seasonality strengths if needed, possibly using cross-validation on historical data.
Prediction and Evaluation:
Forecasting: Create a future dataframe for the 30-day period (including the engineered features for those future dates) and use the trained Prophet model to forecast the number of lunchboxes needed each day.
Evaluation Metrics:
Mean Absolute Error (MAE): This is highly suitable as it directly represents the average number of lunchboxes that the prediction is off by. For example, an MAE of 3 means, on average, the prediction is 3 lunchboxes away from the actual number.
Root Mean Squared Error (RMSE): Also useful, as it penalizes larger errors more significantly.
Validation: Assess the model's performance on a held-out test set from the historical data.
Deployment and Usage:
The trained model can be saved and loaded into a script or application.
When the 30-day period approaches, the system can generate daily predictions.
CompanyA can then use these predictions to inform their procurement of food items and preparation of lunchboxes, aiming to match the predicted demand as closely as possible.
Monitoring and Retraining:
After the 30-day period, compare the actual distributed lunchboxes against the predictions to evaluate performance.
Periodically retrain the model with the newly collected data to keep the predictions up-to-date for future campaigns.

