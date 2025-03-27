# Sales Analysis & Forecast

## Project Overview
This project analyzes sales data from 2020 to 2025, providing insights into trends, seasonality, and future sales predictions. The dataset includes:
- **Daily sales data** with seasonal variations and anomalies
- **Regional sales** (North, South, East, West)
- **Product categories** (Electronics, Clothing, Furniture, Groceries)

The project utilizes **Python, Pandas, Matplotlib, Plotly, Statsmodels, and ARIMA forecasting** for comprehensive data analysis.

## Features
- **Data Cleaning**: Handles missing values and ensures proper sorting
- **Moving Average Calculation**: Smooths out trends
- **Seasonal Decomposition**: Identifies seasonal and trend components
- **ARIMA Forecasting**: Predicts sales for the next 30 days
- **Interactive Visualization**: Uses Plotly for better data exploration

## Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/sales-analysis.git
   cd sales-analysis
   ```
2. Install dependencies:
   ```bash
   pip install pandas matplotlib plotly statsmodels
   ```
3. Run the Jupyter Notebook or Python script to analyze the data:
   ```bash
   jupyter notebook
   ```

## Usage
1. Ensure `sales_data_large.csv` is in the project directory.
2. Run the script to generate sales insights and forecasts.
3. Explore interactive visualizations in your browser.


## How the code works?
---

### **1. Load and Prepare the Data**
```python
df = pd.read_csv('sales_data.csv', parse_dates=['Date'])
df.dropna(inplace=True)
df.sort_values(by='Date', inplace=True)
```
- Reads `sales_data.csv` and converts the `Date` column into a **datetime format**.  
- Removes any **missing values** to avoid errors in analysis.  
- Sorts the data by date for proper trend analysis.  

---

### **2. Display the First Few Rows**
```python
print("Dataset:")
print(df.head())
```
- Prints the first few rows to check the data structure.  

---

### **3. Moving Average Calculation**
```python
df['Moving_Avg'] = df['Sales'].rolling(window=7, min_periods=1).mean()
```
- Calculates a **7-day moving average** to smooth out short-term fluctuations and show trends.  

---

### **4. Seasonal Decomposition**
```python
result = seasonal_decompose(df['Sales'], model='additive', period=30)
result.plot()
plt.show()
```
- Decomposes sales data into **trend, seasonality, and residual (random noise) components**.  
- The `period=30` assumes a **monthly pattern** in sales data.  
- Plots the decomposition using `matplotlib`.  

---

### **5. ARIMA Forecasting (Time Series Prediction)**
```python
model = ARIMA(df['Sales'], order=(5,1,0))
model_fit = model.fit()
predictions = model_fit.forecast(steps=30)
```
- Uses **ARIMA (AutoRegressive Integrated Moving Average)** to forecast future sales.  
- `(5,1,0)` means:
  - **5** previous values (lags) are used.
  - **1** difference applied to make the data stationary.
  - **0** moving average terms.
- Predicts the next **30 days** of sales.  

---

### **6. Interactive Visualization with Plotly**
```python
fig = px.line(df, x='Date', y=['Sales', 'Moving_Avg'], labels={'value': 'Sales', 'variable': 'Legend'}, title='Sales Analysis & Forecast')
fig.show()
```
- Creates an **interactive line chart** using **Plotly**.
- Displays **both actual sales and moving average** trends.  

---

### **7. Print Forecasted Sales**
```python
print("Forecasted Sales for Next 30 Days:")
print(predictions)
```
- Outputs the **forecasted values** for the next month.  

---

