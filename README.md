# SNCF Real-time Forecast of Platform Waiting Time Challenge

This repository contains the solution for the **SNCF Real-time Forecast of Platform Waiting Time Challenge**. The goal is to predict the waiting time difference for trains, helping to improve the accuracy of passenger information.

## Challenge Goal

The primary objective of this challenge is to predict the difference between the theoretical and actual waiting times for a train at a given station. This prediction is for a train located two stations upstream, aiming to provide more accurate real-time information to passengers. The metric for this challenge is the Mean Absolute Error (MAE).

## Data

The dataset is provided by SNCF-Transilien and consists of the following files:
- `x_train.csv`: Training data with 667,265 rows and 10 features.
- `y_train.csv`: Target variable for the training data.
- `x_test.csv`: Test data with 20,658 rows.
- `y_sample.csv`: An example submission file.

The data includes contextual features (train, station, date, stop number) and historical waiting time differences. The target variable, `p0q0`, is the difference between the theoretical and actual waiting time. A negative value indicates a longer wait than expected.

## Methodology

Our approach to solving this challenge is a comprehensive pipeline designed for robust feature engineering, model training, and evaluation.

### 1. Exploratory Data Analysis (EDA)
A thorough EDA was conducted to understand the underlying patterns in the data. This involved:
-   **Distribution Analysis:** Examining the distributions of individual features and the target variable.
-   **Correlation Analysis:** Identifying relationships between features and the target variable.
-   **Time Series Analysis:** Investigating temporal patterns and seasonality in the data.
-   **Outlier Detection:** Identifying and handling anomalous data points.

### 2. Feature Engineering
Based on the insights from EDA, a set of new features was engineered to enhance the predictive power of our models:
-   **Time-based Features:** Extracted features from the `date` column, such as day of the week, month, and year.
-   **Lag Features:** Created lag features for the target variable to capture temporal dependencies.
-   **Interaction Features:** Generated interaction features between key variables like `train` and `gare`.
-   **Rolling Statistics:** Calculated rolling means, medians, and standard deviations for historical waiting times.

### 3. Model Development
We experimented with several state-of-the-art regression models to find the best performer for this task:

-   **Baseline Model:** A simple Random Forest model was used as a benchmark, as suggested in the challenge description.
-   **Gradient Boosting Machines (GBMs):**
    -   **LightGBM:** A high-performance gradient boosting framework known for its speed and efficiency.
    -   **XGBoost:** Another popular and powerful GBM library.
-   **Ensemble Methods:** We combined the predictions of multiple models using techniques like stacking and blending to improve generalization and robustness.

### 4. Training and Evaluation
The models were trained and evaluated using a rigorous cross-validation strategy:
-   **Time-based Cross-Validation:** A time-series-aware cross-validation setup was used to prevent data leakage and ensure that the model generalizes well to future data.
-   **Hyperparameter Tuning:** We used Optuna for efficient hyperparameter optimization to find the best set of parameters for each model.
-   **Metric:** The models were evaluated using the Mean Absolute Error (MAE), as specified by the challenge.

### 5. Final Model and Prediction
The best-performing model, an ensemble of LightGBM models, was retrained on the entire training dataset. This final model was then used to make predictions on the test set, and the results were formatted for submission.

## Project Structure

The project follows a standard data science structure:
-   `data/`: Contains the raw and processed data.
-   `notebooks/`: Jupyter notebooks for EDA and experimentation.
-   `src/`: Source code for data processing, feature engineering, modeling, and visualization.
-   `models/`: Trained models and their outputs.
-   `submissions/`: Final submission files.
-   `requirements.txt`: Python dependencies.

