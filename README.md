# Electricity and Weather data Visualization and Demand and Trend Prediction Project

This project aims to predict electricity demand using time series analysis and linear regression modeling. It encompasses data integration from disparate sources (JSON and CSV), comprehensive exploratory data analysis (EDA), model building, evaluation, and interactive visualization using Gradio.

## Project Objectives

* Accurately predict electricity demand based on historical usage and weather data.
* Develop a robust data processing pipeline for handling large datasets.
* Perform thorough EDA to understand data patterns and relationships.
* Build and evaluate a linear regression model for demand prediction.
* Create an interactive web application for easy visualization and sharing of results.

## Detailed Functionality

1.  **Data Loading and Integration:**
    * `load_and_integrate_json_data(data_folder)`:
        * Recursively searches for JSON files in the specified directory.
        * Parses each JSON file, extracts electricity usage data, and normalizes it into a pandas DataFrame.
        * Handles potential errors during file reading and JSON parsing.
        * Concatenates all DataFrames into a single DataFrame.
        * Converts the timestamp column to datetime objects.
    * `load_and_integrate_csv_data(data_folder)`:
        * Searches for CSV files in the specified directory.
        * Reads each CSV file into a pandas DataFrame, handling potential encoding issues and bad lines.
        * Extracts weather data, specifically temperature, and converts the date column to datetime objects.
        * Concatenates all DataFrames into a single DataFrame.

2.  **Data Preprocessing:**
    * `detect_outliers_iqr(df, col)` and `detect_outliers_zscore(df, col)`:
        * Implement outlier detection using the Interquartile Range (IQR) and Z-score methods.
        * Return DataFrames containing detected outliers.
    * `preprocess_data(combined_data)`:
        * Merges electricity and weather data based on the timestamp.
        * Performs feature engineering:
            * Extracts hour, month, and day of week from the timestamp.
            * Creates a binary feature indicating weekends.
        * Applies outlier detection and removal using both IQR and Z-score methods.
        * Handles missing values.
        * Returns the cleaned and preprocessed DataFrame.

3.  **Exploratory Data Analysis (EDA):**
    * `perform_eda(data)`:
        * Generates various plots to visualize data patterns and relationships:
            * Time series plot of electricity usage with trendline and peak annotations.
            * Histograms and boxplots for univariate analysis.
            * Correlation matrix heatmap.
            * Seasonal decomposition plot.
        * Performs statistical tests:
            * Calculates descriptive statistics (mean, std, skewness, kurtosis).
            * Performs Augmented Dickey-Fuller (ADF) test for stationarity.
        * Saves all graphs into the `eda_plots/` directory.

4.  **Regression Modeling:**
    * `build_regression_model(data)`:
        * Splits the data into training and testing sets.
        * Builds a linear regression model using scikit-learn.
        * Evaluates the model using MAE, MSE, RMSE, and R².
        * Performs residual analysis to assess model fit.
        * Saves the Actual vs. Predicted graph, residual distribution graph, and residual vs predicted graph into the `regression_plots/` directory.

5.  **Interactive Visualization with Gradio:**
    * `process_data_and_visualize(electricity_folder, weather_folder)`:
        * Orchestrates the entire data processing and visualization pipeline.
        * Calls the data loading, preprocessing, EDA, and regression functions.
        * Returns the file paths of generated plots.
    * Gradio Interface:
        * Creates a web interface using Gradio to allow users to input data folder paths.
        * Displays the generated plots using the `gr.Image` component.
        * Provides an interactive and user-friendly way to explore the results.

## Dependencies

* Python 3.x
* pandas
* numpy
* scipy
* matplotlib
* seaborn
* statsmodels
* scikit-learn
* gradio

Install dependencies using:

```bash
pip install pandas numpy scipy matplotlib seaborn statsmodels scikit-learn gradio
