# weather_data_analytics

         ### Step-by-Step Explanation of the Weather Data Analytics Process

This notebook performs exploratory data analysis (EDA) on a weather dataset. Below is a step-by-step breakdown of the code, assuming the dataset is loaded from `C:\Users\MOHESWARAN.K\Downloads\Weather_Dataset.csv`. Each step corresponds to a cell or section in the notebook.

#### 1. **Import Libraries and Load Data**
   - **Code**: `import pandas as pd`, `import numpy as np`, `import matplotlib.pyplot as plt`, `import seaborn as sns`, `data=pd.read_csv(r"C:\Users\MOHESWARAN.K\Downloads\Weather_Dataset.csv")`, `data`
   - **Explanation**: Imports necessary libraries for data manipulation (pandas, numpy), plotting (matplotlib, seaborn). Loads the CSV file into a DataFrame called `data` and displays it. This initializes the dataset for analysis.

#### 2. **Basic Data Exploration**
   - **Code**: `data.head()`, `data.shape`, `data["Weather"].unique()`, `data.nunique()`, `data.dtypes`, `data.columns`, `data.count()`, `data.value_counts()`
   - **Explanation**: 
     - `head()`: Shows the first 5 rows.
     - `shape`: Prints the number of rows and columns (e.g., (8784, 8)).
     - `unique()`: Lists unique values in the "Weather" column.
     - `nunique()`: Counts unique values per column.
     - `dtypes`: Shows data types (e.g., object for strings, float for numbers).
     - `columns`: Lists column names.
     - `count()`: Counts non-null values per column.
     - `value_counts()`: Counts occurrences of each unique value in the entire DataFrame (may not be meaningful for mixed data).

#### 3. **Find Unique Wind Speed Values**
   - **Code**: `data.nunique()`, `data['Wind Speed_km/h'].nunique()`, `data['Wind Speed_km/h'].unique()`
   - **Explanation**: Confirms unique values in "Wind Speed_km/h" column. `nunique()` gives the count, `unique()` lists them.

#### 4. **Count Clear Weather Instances**
   - **Code**: `data["Weather"].value_counts()`, `data.head(2)`, `data[data['weather_condition'] == 'clear']`
   - **Explanation**: `value_counts()` shows frequency of each weather type. The filter `data[data['weather_condition'] == 'clear']` attempts to select rows where weather is 'clear', but the column is "Weather" (rename failed), so it may error. Use `data["Weather"] == 'Clear'` for exact match.

#### 5. **Filter Wind Speed = 4 km/h**
   - **Code**: `data.head(2)`, `data[data["Wind Speed_km/h"] == 4]`, `count_4 = data[data["Wind Speed_km/h"] == 4].shape[0]`, `print(count_4, "times the wind speed was 4 km/h")`
   - **Explanation**: Filters rows where wind speed is exactly 4. Counts and prints the number of such instances.

#### 6. **Check for Null Values**
   - **Code**: `data.isnull().sum()`
   - **Explanation**: Counts null/missing values per column. Useful for data cleaning.

#### 7. **Rename Column (Attempted)**
   - **Code**: `data.rename(columns={"weather": "weather_condition"}, inplace=True)`, `data`
   - **Explanation**: Tries to rename "weather" to "weather_condition". Since the column is "Weather" (capital W), it doesn't change anything. Use `{"Weather": "weather_condition"}` to fix.

#### 8. **Calculate Mean Visibility**
   - **Code**: `data.Visibility_km.mean()`
   - **Explanation**: Computes the average visibility in km.

#### 9. **Calculate Standard Deviation of Pressure**
   - **Code**: `data.Press_kPa.std()`
   - **Explanation**: Computes the standard deviation of pressure.

#### 10. **Calculate Variance of Relative Humidity**
    - **Code**: `data['Rel Hum_%'].var()`
    - **Explanation**: Computes the variance of relative humidity.

#### 11. **Find Snow Instances**
    - **Code**: `data[data['weather_condition'].str.contains('snow', case=False)]`
    - **Explanation**: Filters rows where "weather_condition" contains 'snow' (case-insensitive). May error if column name is wrong; use "Weather" instead.

#### 12. **Filter Wind Speed > 24 and Visibility = 25**
    - **Code**: `data[(data['Wind Speed_km/h'] > 24) & (data['Visibility_km'] == 25)]`
    - **Explanation**: Selects rows where wind speed > 24 km/h and visibility = 25 km.

#### 13. **Group by Weather and Date/Time for Mean**
    - **Code**: `data.groupby(['weather_condition', 'Date/Time']).mean()`
    - **Explanation**: Groups data by weather and date, computes mean for numeric columns. May error due to column name.

#### 14. **Group by Weather and Date/Time for Min/Max**
    - **Code**: `data.groupby(['weather_condition', 'Date/Time']).agg(['min','max'])`
    - **Explanation**: Groups and computes min/max for each group.

#### 15. **Filter Fog Records**
    - **Code**: `data[data['weather_condition'] == 'fog']`
    - **Explanation**: Selects rows where weather is 'fog'.

#### 16. **Filter Clear Weather or Visibility > 40**
    - **Code**: `data[(data['weather_condition']=='clear') | (data['Visibility_km'] > 40)]`
    - **Explanation**: Selects rows where weather is 'clear' or visibility > 40 km.

#### 17. **Complex Filter: Clear and Humidity > 50 or Visibility > 40**
    - **Code**: `data[((data['weather_condition'] == 'clear') & (data['Rel Hum_%'] > 50)) | (data['Visibility_km'] > 40)]`
    - **Explanation**: Applies OR condition with AND inside.

#### 18. **Line Chart: Temperature Over Time**
    - **Code**: Converts 'Date/Time' to datetime, plots Temp_C vs Date/Time.
    - **Explanation**: Visualizes temperature trend over time.

#### 19. **Line Chart: Humidity Over Time**
    - **Code**: Plots Rel Hum_% vs Date/Time.
    - **Explanation**: Shows humidity variation.

#### 20. **Bar Chart: Weather Distribution**
    - **Code**: `weather_counts = data['weather_condition'].value_counts()`, plots bar chart.
    - **Explanation**: Displays frequency of each weather type. Use "Weather" for correct column.

#### 21. **Box Plot: Temperature by Weather**
    - **Code**: `sns.boxplot(x='weather_condition', y='Temp_C', data=data)`
    - **Explanation**: Shows temperature distribution per weather condition.

#### 22. **Bar Plot: Average Pressure by Weather**
    - **Code**: Groups by weather, computes mean pressure, plots bar.
    - **Explanation**: Visualizes average pressure per weather.

#### 23. **Box Plot: Visibility by Weather**
    - **Code**: `sns.boxplot(x='weather_condition', y='Visibility_km', data=data)`
    - **Explanation**: Shows visibility distribution.

#### 24. **Pie Chart: Weather Value Counts**
    - **Code**: `plt.pie(weather_counts, ...)`
    - **Explanation**: Pie chart of weather frequencies.

#### 25. **Scatter Plot: Temperature vs Humidity**
    - **Code**: Scatter plot with color by weather.
    - **Explanation**: Shows relationship between temp and humidity, colored by weather.

#### 26. **Histogram: Wind Speed**
    - **Code**: `plt.hist(data['Wind Speed_km/h'], bins=20, ...)`
    - **Explanation**: Distribution of wind speeds.

**Notes**: 
- Many cells reference 'weather_condition', but the column is "Weather". Update to avoid errors.
- Ensure 'Date/Time' is datetime for time-based plots.
- This is a complete EDA workflow: load, explore, filter, aggregate, visualize. Run cells sequentially in Jupyter.M
    
