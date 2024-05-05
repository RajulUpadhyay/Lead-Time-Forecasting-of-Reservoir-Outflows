# Lead-Time-Forecasting-of-Reservoir-Outflows

This repository contains the code and analysis related to predicting the outflow of the Panchet reservoir in Dhanbad, Jharkhand, India, up to 3 days in advance.

**Objective:**

Develop machine learning models to predict the reservoir outflow (amount of water discharged) for lead times of 1, 2, and 3 days.

**Data:**

Reservoir data (daily inflow, level, and outflow) from 2000 to 2019 obtained from the Panchet reservoir operations team.
Daily gridded rainfall data at 0.25-degree resolution from the India Meteorological Department for the same period.

**Data Preprocessing:**

Handled missing values: Rainfall data filled using forward fill (ffill), reservoir data using mean imputation (suitable for time series).
Identified and removed outliers based on distribution (skewed & normal) and percentiles (99th percentile).
Analyzed relationships between variables using:
Cross-Correlation Function (CCF): Identified significant correlations between reservoir inflow and outflow (up to 3-day lag) and reservoir level and outflow (up to 2-day lag).
Partial Autocorrelation Function (PACF) and Autocorrelation Function (ACF): Confirmed the significant correlation of reservoir outflow with its own past values (up to 4-day lag).

**Feature Engineering:**

Selected features based on the identified relationships:
Lags of reservoir inflow (3-day), level (2-day), and rainfall (1-day).
Past reservoir outflow values (up to 4-day lag).
Applied min-max scaling to features.

**Model Development:**

Employed and evaluated three machine learning models:
Support Vector Regression (SVR) with grid search for hyperparameter tuning.
Random Forest (RF) with default hyperparameters.
Long Short-Term Memory (LSTM) neural network with dropout regularization.
Implemented an ensemble method where past predictions were fed as additional features for 2-day and 3-day lead predictions, leading to improved performance.

**Model Evaluation:**

Visualized training and testing loss plots to monitor model convergence.
Performed inverse transformation on predictions to obtain real-world units.
Generated predicted vs. observed plots and scatter plots with a 1:1 line for visual assessment.

Employed performance metrics:

**Nash-Sutcliffe Efficiency (NSE):** Measures agreement between predicted and observed values (1 indicates perfect match).

**Root Mean Squared Error (RMSE):** Measures the magnitude of the error between predictions and observations.

**R-squared:** Coefficient of determination, indicates the proportion of variance explained by the model.

**Results and Conclusion:**

LSTM achieved the best performance for 1-day and 2-day lead predictions (highest R-squared and NSE, lowest RMSE).
All models exhibited a decrease in performance with increasing lead time, which is a common challenge in time series forecasting.
