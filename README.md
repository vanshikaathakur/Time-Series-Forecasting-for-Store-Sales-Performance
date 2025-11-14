# Time Series Forecasting for Store Sales Performance

## Project Overview
This project focuses on predicting store sales performance using historical sales data from a retail dataset (specifically focused on the "Furniture" category). The goal is to build machine learning models to forecast sales based on various features such as shipping details, customer segments, location, product sub-categories, quantity, discount, profit, and shipping days.

The analysis involves data cleaning, feature engineering, encoding categorical variables, and training regression models to predict the `Sales` target variable. Two models were evaluated: **Random Forest Regressor** and **XGBoost Regressor**. The Random Forest model outperformed XGBoost based on evaluation metrics.

Key steps include:
- Data loading and exploration.
- Data preprocessing (dropping irrelevant columns, handling dates, adding new features like shipping days).
- Encoding categorical features using OneHotEncoder.
- Splitting data into training and validation sets.
- Training and evaluating models.
- Comparing model performance using metrics like MAE, MSE, RMSE, and R².

Although titled as "Time Series Forecasting," the approach is more of a regression task on static features (with dates converted to shipping days but dropped otherwise). No explicit time-series components (e.g., ARIMA, Prophet, or lagged features) were used, and the train-test split is random rather than time-based. For true time-series forecasting, consider adding temporal features (e.g., year, month, seasonality) and using chronological splits.

## Dataset
- **File**: `stores_sales_forecasting.csv` (not included in the repository; download or provide your own).
- **Source**: Assumed to be a retail sales dataset (e.g., similar to Superstore sales data).
- **Key Columns**:
  - `Order Date`, `Ship Date`: Converted to datetime and used to calculate `Shipping_Days`.
  - `Ship Mode`, `Segment`, `Country`, `City`, `State`, `Region`, `Category`, `Sub-Category`: Categorical features (encoded).
  - `Sales`: Target variable (continuous).
  - `Quantity`, `Discount`, `Profit`: Numerical features.
  - `Product Name`: Dropped as it's high-cardinality and not used in modeling.
- **Size**: 2121 rows, focused on Furniture category (Bookcases, Chairs, Tables, Furnishings).
- **Encoding**: Loaded with `latin-1` encoding due to special characters.
- **Statistics** (from `df.describe()`):
  - Sales: Mean ~349.83, Min 1.89, Max 4416.17.
  - Quantity: Mean ~3.79, Min 1, Max 14.
  - Discount: Mean ~0.17, Min 0, Max 0.7.
  - Profit: Mean ~8.70, Min -1862.31, Max 1013.13.
  - Shipping_Days: Mean ~3.92, Min 0, Max 7.

## Requirements
To run the notebook, install the following Python libraries:
```
pandas==2.2.2
numpy==1.26.4
matplotlib==3.9.2
seaborn==0.13.2
scikit-learn==1.5.1
xgboost==2.1.1
```
Install via pip:
```
pip install pandas numpy matplotlib seaborn scikit-learn xgboost
```

## Installation and Setup
1. Clone the repository:
   ```
   git clone https://github.com/your-username/time-series-forecasting-store-sales.git
   cd time-series-forecasting-store-sales
   ```
2. Download the dataset (`stores_sales_forecasting.csv`) and place it in the appropriate path (update the path in the notebook if needed: `r"C:\Users\nt397\Downloads\stores_sales_forecasting.csv"`).
3. Run the Jupyter Notebook:
   ```
   jupyter notebook "Time Series Forecasting for Store Sales Performance.ipynb"
   ```

## Usage
- Open the notebook in Jupyter.
- Execute cells sequentially.
- Key sections:
  - **Data Loading and Cleaning**: Loads CSV, drops unnecessary columns (`Row ID`, `Order ID`, `Customer ID`, `Product ID`, `Customer Name`, `Postal Code`), converts dates, adds `Shipping_Days`.
  - **Exploratory Data Analysis (EDA)**: Uses `df.info()`, `df.describe()`, and `df.head()` to inspect data.
  - **Feature Engineering**: Prepares features (X) and target (y = Sales). Encodes categorical columns using `OneHotEncoder`.
  - **Model Training**:
    - Train-Test Split: 80/20 split with `random_state=42`.
    - Random Forest: Trained with default parameters.
    - XGBoost: Trained with default parameters.
  - **Evaluation**: Computes MAE, MSE, RMSE, R² on the test set.
  - **Predictions**: Generates predictions for the test set.

To customize:
- Update the dataset path.
- Experiment with hyperparameters (e.g., via GridSearchCV).
- Add time-series elements like extracting month/year from `Order Date` and including them in features.

## Models Used
1. **Random Forest Regressor** (from `sklearn.ensemble`):
   - Ensemble method using decision trees.
   - Handles non-linear relationships well.
   - Trained on encoded features.

2. **XGBoost Regressor** (from `xgboost`):
   - Gradient boosting framework.
   - Efficient and handles missing values/sparse data.
   - Trained similarly on the same features.

## Results
- **Random Forest**:
  - Mean Absolute Error (MAE): 117.0866
  - Mean Squared Error (MSE): 51611.5458
  - Root Mean Squared Error (RMSE): 227.1817
  - R² Score: 0.7399 (73.99% variance explained)

- **XGBoost**:
  - Mean Absolute Error (MAE): 126.2862
  - Mean Squared Error (MSE): 57627.0090
  - Root Mean Squared Error (RMSE): 240.0563
  - R² Score: 0.7096 (70.96% variance explained)

The Random Forest model shows better performance across all metrics, indicating it captures the relationships in the data more effectively.

## Conclusion
The Random Forest Regressor is recommended for sales prediction in this dataset, achieving an R² of ~74%. Future improvements could include:
- Incorporating true time-series techniques (e.g., ARIMA, LSTM for sequential forecasting).
- Time-based splitting to avoid data leakage.
- Feature importance analysis (e.g., from Random Forest) to identify key drivers of sales.
- Hyperparameter tuning for better accuracy.
- Handling potential multicollinearity (e.g., Profit is highly correlated with Sales).

## Acknowledgments
- Dataset inspired by retail sales benchmarks (e.g., Superstore dataset).
- Built using open-source libraries: pandas, scikit-learn, XGBoost.
