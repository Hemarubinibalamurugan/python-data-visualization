# Python Data Analysis Assignment 2 - Data Visualization

## 📌 Project Overview

This project focuses on data cleaning, missing value handling, exploratory data analysis, and data visualization using Python.

The Seaborn `taxis` dataset is used for this assignment. The dataset contains information about taxi trips, including pickup time, dropoff time, passengers, distance, fare, tip, payment method, and borough information.

## 🎯 Objectives

The main objectives of this project are:

- Load and explore the dataset
- Identify missing values
- Handle missing values appropriately
- Convert the pickup column into datetime format
- Perform data analysis
- Create visualizations using Matplotlib
- Create visualizations using Seaborn
- Analyze relationships between numerical variables

## 📊 Dataset

The dataset used in this project is the built-in Seaborn `taxis` dataset.

### Dataset Size

- Rows: 6,433
- Columns: 14

### Important Columns

- `pickup` - Pickup date and time
- `dropoff` - Dropoff date and time
- `passengers` - Number of passengers
- `distance` - Trip distance
- `fare` - Trip fare
- `tip` - Tip amount
- `tolls` - Toll amount
- `total` - Total trip amount
- `color` - Taxi color
- `payment` - Payment method
- `pickup_zone` - Pickup zone
- `dropoff_zone` - Dropoff zone
- `pickup_borough` - Pickup borough
- `dropoff_borough` - Dropoff borough

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## 📥 Data Loading

The dataset was loaded using the Seaborn library.

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("taxis")

df.head()
```

## 🧹 Data Cleaning

### 🔍 Checking Missing Values

Missing values were checked using:

```python
df.isnull().sum()
```

### 🔧 Handling Missing Values

Numerical columns were filled using the median value.

Categorical columns were filled using the mode value.

```python
numerical_columns = df.select_dtypes(include=np.number).columns

for col in numerical_columns:
    df[col] = df[col].fillna(df[col].median())

categorical_columns = df.select_dtypes(include="object").columns

for col in categorical_columns:
    if df[col].isnull().sum() > 0:
        df[col] = df[col].fillna(df[col].mode()[0])

df.isnull().sum()
```

### 📅 Datetime Conversion

The `pickup` column was converted into datetime format.

```python
df["pickup"] = pd.to_datetime(df["pickup"])

df["pickup"].dtype
```

## 📈 Visualizations Using Matplotlib

### 1. Line Chart - Fare Over Time

A line chart was created to visualize fare over time.

- X-axis: Pickup Time
- Y-axis: Fare

```python
df = df.sort_values("pickup")

plt.figure(figsize=(12, 6))

plt.plot(df["pickup"], df["fare"])

plt.title("Fare Over Time")
plt.xlabel("Pickup Time")
plt.ylabel("Fare")

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### 2. Bar Chart - Total Fare by Pickup Borough

A bar chart was created to show the total fare for each pickup borough.

```python
borough_fare = df.groupby("pickup_borough")["fare"].sum()

plt.figure(figsize=(10, 6))

borough_fare.plot(kind="bar")

plt.title("Total Fare by Pickup Borough")
plt.xlabel("Pickup Borough")
plt.ylabel("Total Fare")

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### 3. Pie Chart - Payment Method

A pie chart was created to show the distribution of trips based on payment method.

```python
payment_counts = df["payment"].value_counts()

plt.figure(figsize=(8, 8))

plt.pie(
    payment_counts,
    labels=payment_counts.index,
    autopct="%1.1f%%",
    startangle=90
)

plt.title("Distribution of Trips by Payment Method")
plt.show()
```

### 4. Histogram - Trip Distance

A histogram was created to visualize the distribution of trip distance.

```python
plt.figure(figsize=(10, 6))

plt.hist(df["distance"], bins=30)

plt.title("Distribution of Trip Distance")
plt.xlabel("Distance")
plt.ylabel("Frequency")

plt.tight_layout()
plt.show()
```

### 5. Box Plot - Tips by Pickup Borough

A box plot was created to visualize the distribution of tip amounts for each pickup borough.

```python
plt.figure(figsize=(12, 6))

df.boxplot(
    column="tip",
    by="pickup_borough"
)

plt.title("Distribution of Tips by Pickup Borough")
plt.suptitle("")
plt.xlabel("Pickup Borough")
plt.ylabel("Tip")

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

## 📊 Visualizations Using Seaborn

### 6. Count Plot - Trips by Pickup Borough

A count plot was created to visualize the number of trips in each pickup borough.

```python
plt.figure(figsize=(10, 6))

sns.countplot(
    data=df,
    x="pickup_borough"
)

plt.title("Number of Trips by Pickup Borough")
plt.xlabel("Pickup Borough")
plt.ylabel("Number of Trips")

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### 7. Scatter Plot - Distance vs Fare

A scatter plot was created to visualize the relationship between distance and fare.

- X-axis: Distance
- Y-axis: Fare
- Color: Pickup Borough

```python
plt.figure(figsize=(10, 6))

sns.scatterplot(
    data=df,
    x="distance",
    y="fare",
    hue="pickup_borough"
)

plt.title("Relationship Between Distance and Fare")
plt.xlabel("Distance")
plt.ylabel("Fare")

plt.tight_layout()
plt.show()
```

### 8. Correlation Heatmap

A heatmap was created to visualize the correlation between numerical variables.

The following variables were used:

- Distance
- Fare
- Tip
- Tolls
- Total

```python
numeric_data = df[
    ["distance", "fare", "tip", "tolls", "total"]
]

correlation = numeric_data.corr()

plt.figure(figsize=(10, 7))

sns.heatmap(
    correlation,
    annot=True,
    cmap="coolwarm",
    fmt=".2f"
)

plt.title("Correlation Heatmap")
plt.tight_layout()
plt.show()
```

## 🔎 Final Dataset Check

The final dataset was checked for its shape and missing values.

```python
print("Dataset Shape:")
print(df.shape)

print("\nMissing Values:")
print(df.isnull().sum())

print("\nFirst 5 Rows:")
display(df.head())
```

## 📌 Final Result

- Dataset contains 6,433 rows
- Dataset contains 14 columns
- Missing values were handled
- `pickup` column was converted to datetime format
- Matplotlib visualizations were created
- Seaborn visualizations were created
- Correlation between numerical variables was analyzed

## 🎓 Learning Outcomes

Through this assignment, I learned:

- How to load datasets using Seaborn
- How to inspect datasets using Pandas
- How to identify missing values
- How to handle missing values using median and mode
- How to convert a column into datetime format
- How to perform basic data cleaning
- How to create line charts
- How to create bar charts
- How to create pie charts
- How to create histograms
- How to create box plots
- How to create count plots
- How to create scatter plots
- How to create correlation heatmaps
- How to use Matplotlib and Seaborn for data visualization
- How to perform basic exploratory data analysis

## 📁 Project Structure

```text
Python-DA-Assignment-2/
│
├── Python_DA_Assignment_2_Data_Visualization.ipynb
│
└── README.md
```

## 📝 Conclusion

This project demonstrates the basic process of data analysis and visualization using Python.

The Seaborn `taxis` dataset was cleaned, analyzed, and visualized using Pandas, NumPy, Matplotlib, and Seaborn.

## 👩‍💻 Author

### Hemarubini

Python Data Analytics Learner
