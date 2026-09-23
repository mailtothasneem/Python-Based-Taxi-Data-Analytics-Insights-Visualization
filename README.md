# Python-Based-Taxi-Data-Analytics-Insights-Visualization
This project focuses on exploring, analyzing, and visualizing taxi trip data using Python. The Seaborn Taxis dataset is used to perform data cleaning, missing-value handling, exploratory data analysis, and statistical visualization.

## 📌 Project Overview

This project focuses on **Taxi Data Analysis and Visualization** using Python. The Seaborn **Taxis dataset** is loaded, cleaned, analyzed, and visualized using **NumPy, Pandas, Matplotlib, and Seaborn**.

The main objective of this project is to understand taxi trip patterns and relationships between variables such as:

* Distance
* Fare
* Tip
* Total amount
* Tolls
* Payment method
* Pickup borough
* Pickup zone
* Pickup time

The project demonstrates important **Data Analytics and Data Visualization** techniques using Python.

---

## 🎯 Objectives

The main objectives of this project are:

* Load the Seaborn Taxis dataset.
* Understand the structure and characteristics of the dataset.
* Check and handle missing values.
* Analyze numerical and categorical data.
* Convert date/time columns into the appropriate format.
* Create different types of visualizations.
* Understand relationships between taxi trip variables.
* Identify patterns, distributions, and possible correlations.
* Practice Python libraries commonly used in Data Analytics.

---

## 🛠️ Technologies & Libraries Used

### Programming Language

* Python

### Libraries

* **NumPy** – Numerical operations
* **Pandas** – Data manipulation and analysis
* **Matplotlib** – Data visualization
* **Seaborn** – Statistical data visualization

---

## 📂 Dataset

The project uses the built-in **Taxis dataset** available through Seaborn.

The dataset is loaded using:

```python
import seaborn as sns

df = sns.load_dataset("taxis")
```

The dataset contains information about taxi trips, including pickup and drop-off details, distance, fare, tip, tolls, total amount, payment method, and location information.

---

# 🔍 Project Workflow

The project follows these major steps:

```text
Load Dataset
      ↓
Understand Dataset
      ↓
Check Dataset Information
      ↓
Handle Missing Values
      ↓
Convert Date/Time Data
      ↓
Create Visualizations
      ↓
Analyze Relationships
      ↓
Draw Data Insights
```

---

# 1️⃣ Loading the Dataset

The Seaborn Taxis dataset is loaded using Pandas and Seaborn.

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("taxis")

df
```

The dataset is then explored to understand its rows, columns, data types, and values.

---

# 2️⃣ Dataset Exploration

## Dataset Shape

The `shape` function is used to identify the number of rows and columns.

```python
df.shape
```

This helps understand the overall size of the dataset.

---

## Dataset Information

The `df.info()` function provides information about:

* Number of rows
* Column names
* Data types
* Non-null values
* Missing values

```python
df.info()
```

This is useful for understanding the structure of the dataset before performing analysis.

---

## Statistical Summary

The project uses `describe()` to understand the statistical characteristics of the dataset.

### Categorical Columns

```python
df.describe(include='object')
```

### Numerical Columns

```python
df.describe(include='number')
```

The numerical summary provides:

* Count
* Mean
* Standard deviation
* Minimum
* 25th percentile
* Median
* 75th percentile
* Maximum

---

# 3️⃣ Handling Missing Values

Missing values are checked using Pandas.

### Percentage of Missing Values

```python
round(df.isnull().mean() * 100, 1)
```

### Number of Missing Values

```python
df.isnull().sum()
```

Different strategies can be used depending on the type and importance of the column.

### General approach

* **Numerical columns** → Mean or Median
* **Categorical columns** → Mode
* **Critical columns** → Remove rows if missing information cannot be reasonably imputed

---

## Handling Categorical Missing Values

The project identifies the mode of categorical columns such as:

* `payment`
* `pickup_zone`
* `dropoff_zone`
* `pickup_borough`
* `dropoff_borough`

Example:

```python
df['payment'].mode()
```

Missing values in categorical columns are filled using the mode.

Example:

```python
df['payment'] = df['payment'].fillna(df['payment'].mode()[0])
```

Similarly:

```python
df['pickup_zone'] = df['pickup_zone'].fillna(
    df['pickup_zone'].mode()[0]
)

df['dropoff_zone'] = df['dropoff_zone'].fillna(
    df['dropoff_zone'].mode()[0]
)

df['pickup_borough'] = df['pickup_borough'].fillna(
    df['pickup_borough'].mode()[0]
)

df['dropoff_borough'] = df['dropoff_borough'].fillna(
    df['dropoff_borough'].mode()[0]
)
```

After handling missing values, the dataset is checked again:

```python
df.isnull().sum()
```

---

# 4️⃣ Converting Pickup Time to Datetime

The `pickup` column is converted into datetime format so that it can be used for time-based analysis.

```python
df['pickup'] = pd.to_datetime(df['pickup'])
```

The dataset is then sorted according to pickup time:

```python
df = df.sort_values('pickup')
```

---

# 📊 Data Visualizations

The project includes several visualization techniques using **Matplotlib, Pandas Plot, and Seaborn**.

---

# 5️⃣ Line Chart – Fare Over Time

A line chart is created to visualize how taxi fares vary over pickup time.

```python
plt.figure(figsize=(12, 5))

plt.plot(df['pickup'], df['fare'])

plt.xlabel('Pickup Time')
plt.ylabel('Fare')
plt.title('Fare Over Time')

plt.xticks(rotation=45)
plt.tight_layout()

plt.show()
```

### Purpose

The line chart helps visualize:

* Fare variation over time
* Changes in fare values
* Possible time-based patterns

---

# 6️⃣ Bar Chart – Total Fare by Pickup Borough

The total fare is calculated for each pickup borough.

```python
total_fare = df.groupby('pickup_borough')['fare'].sum()
```

The result is displayed using a bar chart.

```python
total_fare.plot(
    kind='bar',
    figsize=(8, 5)
)

plt.xlabel('Pickup Borough')
plt.ylabel('Total Fare')
plt.title('Total Fare by Pickup Borough')

plt.xticks(rotation=45)
plt.tight_layout()

plt.show()
```

### Purpose

The bar chart is used to compare the total fare across different pickup boroughs.

### Key Concept

```python
groupby('pickup_borough')
```

Groups taxi trips according to pickup borough.

```python
['fare']
```

Selects the fare column.

```python
.sum()
```

Calculates the total fare for each group.

---

# 7️⃣ Pie Chart – Trips by Payment Method

The number of trips for each payment method is calculated using:

```python
payment_counts = df['payment'].value_counts()
```

A pie chart is then created:

```python
plt.figure(figsize=(7, 7))

plt.pie(
    payment_counts,
    labels=payment_counts.index,
    autopct='%1.1f%%'
)

plt.title('Distribution of Trips by Payment Method')

plt.show()
```

### Purpose

The pie chart shows the proportion of taxi trips according to payment method.

It helps understand how frequently different payment methods are used.

---

# 8️⃣ Histogram – Distribution of Trip Distance

A histogram is used to understand the distribution of taxi trip distances.

```python
plt.figure(figsize=(8, 5))

plt.hist(
    df["distance"],
    bins=20,
    edgecolor="black"
)

plt.xlabel("Distance")
plt.ylabel("Number of Trips")
plt.title("Distribution of Trip Distance")

plt.show()
```

### Purpose

The histogram helps identify:

* Common trip distances
* Short trips
* Long trips
* Distribution of trip distances

### Important Concept

```python
bins=20
```

divides the distance values into 20 groups or intervals.

---

# 9️⃣ Box Plot – Tip Amount by Pickup Borough

A box plot is created using Seaborn to analyze tip amounts across pickup boroughs.

```python
plt.figure(figsize=(8, 5))

sns.boxplot(
    x="pickup_borough",
    y="tip",
    data=df
)

plt.title("Distribution of Tip Amount by Pickup Borough")
plt.xlabel("Pickup Borough")
plt.ylabel("Tip Amount")

plt.show()
```

### Purpose

The box plot helps understand:

* Median tip
* Spread of tip values
* Variation in tips
* Outliers
* Differences between pickup boroughs

---

# 🔟 Count Plot – Number of Trips by Pickup Borough

A Seaborn count plot is used to visualize the number of trips in each pickup borough.

```python
plt.figure(figsize=(8, 5))

sns.countplot(
    x="pickup_borough",
    data=df,
    palette="Set2"
)

plt.title("Number of Trips by Pickup Borough")
plt.xlabel("Pickup Borough")
plt.ylabel("Number of Trips")

plt.show()
```

### Purpose

The count plot provides a simple frequency comparison between pickup boroughs.

It shows how many taxi trips belong to each pickup borough.

---

# 1️⃣1️⃣ Scatter Plot – Distance vs Fare

A scatter plot is used to visualize the relationship between distance and fare.

```python
plt.figure(figsize=(8, 6))

sns.scatterplot(
    x="distance",
    y="fare",
    data=df,
    hue="pickup_borough"
)

plt.title("Relationship Between Distance and Fare")
plt.xlabel("Distance (km)")
plt.ylabel("Fare Amount")

plt.show()
```

### Purpose

The scatter plot helps visualize:

* Relationship between distance and fare
* How fare changes with distance
* Differences between pickup boroughs

The `hue` parameter uses pickup borough to differentiate the data points.

---

# 1️⃣2️⃣ Heatmap – Correlation Matrix

A correlation matrix is created using numerical variables:

```python
corr_matrix = df[
    ["distance", "fare", "tip", "tolls", "total"]
].corr()
```

The correlation matrix is visualized using a Seaborn heatmap.

```python
plt.figure(figsize=(8, 5))

sns.heatmap(
    corr_matrix,
    annot=True,
    cmap="coolwarm",
    fmt=".2f"
)

plt.title("Correlation Heatmap of Trip Variables")

plt.show()
```

## 📌 Understanding Correlation

Correlation describes the relationship between two numerical variables.

### Positive Correlation

A value close to **+1** indicates a strong positive relationship.

This means the variables tend to increase together.

### Negative Correlation

A value close to **-1** indicates a strong negative relationship.

This means when one variable increases, the other tends to decrease.

### Weak or No Correlation

A value close to **0** indicates a weak or limited linear relationship.

---

# 1️⃣3️⃣ Pair Plot – Pairwise Relationships

A pair plot is used to compare multiple numerical variables simultaneously.

The selected variables are:

* Distance
* Fare
* Tip
* Total

```python
selected_vars = [
    "distance",
    "fare",
    "tip",
    "total"
]
```

The pair plot is created using:

```python
g = sns.pairplot(
    df[selected_vars + ["pickup_zone"]],
    vars=selected_vars,
    hue="pickup_zone",
    palette="Set2",
    diag_kind="kde",
    height=2
)
```

The layout is adjusted to improve the appearance:

```python
g.fig.subplots_adjust(
    top=0.95,
    bottom=0.08,
    left=0.05,
    right=0.85
)
```

A title is added:

```python
g.fig.suptitle(
    "Pairwise Relationships of Trip Variables by Pickup Zone",
    y=0.96
)
```

### Purpose

The pair plot helps compare multiple variables at the same time.

It can help identify:

* Relationships between numerical variables
* Distribution of individual variables
* Different patterns across pickup zones

The `hue="pickup_zone"` parameter differentiates observations based on pickup zone.

---

# 1️⃣4️⃣ Violin Plot – Fare by Payment Method

A violin plot is used to visualize the distribution of fare values for each payment method.

```python
plt.figure(figsize=(8, 6))

sns.violinplot(
    x="payment",
    y="fare",
    data=df,
    palette="Set2"
)

plt.title(
    "Distribution of Fare by Payment Method",
    fontsize=14
)

plt.xlabel("Payment Method", fontsize=12)
plt.ylabel("Fare Amount", fontsize=12)

plt.show()
```

### Purpose

The violin plot helps understand:

* Distribution of fare
* Spread of fare values
* Differences between payment methods
* Density of observations

---

# 📈 Visualizations Included

| Visualization | Variables Used                          | Purpose                                |
| ------------- | --------------------------------------- | -------------------------------------- |
| Line Chart    | Pickup, Fare                            | Fare variation over time               |
| Bar Chart     | Pickup Borough, Fare                    | Compare total fare                     |
| Pie Chart     | Payment                                 | Payment method distribution            |
| Histogram     | Distance                                | Distribution of trip distance          |
| Box Plot      | Pickup Borough, Tip                     | Tip distribution and outliers          |
| Count Plot    | Pickup Borough                          | Number of trips                        |
| Scatter Plot  | Distance, Fare                          | Relationship between distance and fare |
| Heatmap       | Distance, Fare, Tip, Tolls, Total       | Correlation analysis                   |
| Pair Plot     | Distance, Fare, Tip, Total, Pickup Zone | Multiple variable relationships        |
| Violin Plot   | Payment, Fare                           | Fare distribution by payment method    |

---

# 🔎 Key Data Analysis Concepts Practiced

This project provides practical experience with:

* Data loading
* Data inspection
* Data cleaning
* Missing value detection
* Missing value treatment
* Mean and median concepts
* Mode imputation
* Data type conversion
* Datetime conversion
* GroupBy operations
* Aggregation using `sum()`
* Frequency analysis using `value_counts()`
* Correlation analysis
* Data distribution
* Outlier identification
* Data visualization
* Exploratory Data Analysis (EDA)

---

# 📌 Project Insights

The visualizations help explore several aspects of taxi trip data:

### Fare Over Time

The line chart allows fare values to be examined across pickup timestamps.

### Total Fare by Borough

The bar chart provides a comparison of total fare across pickup boroughs.

### Payment Methods

The pie chart shows the distribution of trips across different payment methods.

### Trip Distance

The histogram provides an overview of common and less common trip distances.

### Tip Distribution

The box plot allows comparison of tip amounts between pickup boroughs and helps identify possible outliers.

### Pickup Borough Frequency

The count plot shows the number of taxi trips associated with each pickup borough.

### Distance and Fare Relationship

The scatter plot helps examine how fare values vary with trip distance.

### Correlation

The heatmap provides a numerical view of relationships between distance, fare, tip, tolls, and total.

### Multiple Variable Relationships

The pair plot provides a broader view of relationships among distance, fare, tip, and total while differentiating observations by pickup zone.

### Fare Distribution by Payment

The violin plot provides a distribution-based comparison of fare values across payment methods.

---

# 📁 Project Structure

```text
Data-Visualization-Using-NP-PD-SNS/
│
├── Data_Visualization_Using_NP_PD_SNS.ipynb
│
└── README.md
```

---

# ▶️ How to Run the Project

## Step 1: Clone the Repository

```bash
git clone <your-github-repository-url>
```

## Step 2: Open the Project Folder

```bash
cd Data-Visualization-Using-NP-PD-SNS
```

## Step 3: Install Required Libraries

```bash
pip install numpy pandas matplotlib seaborn
```

## Step 4: Open the Jupyter Notebook

```bash
jupyter notebook
```

Then open:

```text
Data_Visualization_Using_NP_PD_SNS.ipynb
```

Run the notebook cells from top to bottom.

---

# 💡 Skills Demonstrated

Through this project, I practiced:

**Python | NumPy | Pandas | Matplotlib | Seaborn | Data Cleaning | EDA | Data Visualization | Missing Value Handling | Correlation Analysis | Statistical Analysis**

---

# 👩‍💻 Author

**Thasneem L**

Aspiring AI Driven Data Analytics


---

# ⭐ Project Purpose

This project was completed as part of my **Data Analytics learning journey** to strengthen my practical understanding of Python-based data analysis and visualization.

It demonstrates how raw data can be explored, cleaned, analyzed, and transformed into meaningful visual representations using Python.

---

## 📌 Conclusion

The **Taxi Data Analysis & Visualization** project demonstrates a complete exploratory data analysis workflow using Python.

Starting from dataset loading and missing-value handling, the project progresses through data transformation, statistical exploration, and multiple visualization techniques. These visualizations provide different perspectives of taxi trip characteristics such as **fare, distance, tips, payment methods, pickup boroughs, and relationships between numerical variables**.

This project helped build practical knowledge of **Pandas, NumPy, Matplotlib, Seaborn, Exploratory Data Analysis (EDA), and data visualization**, which are important foundations for a career in Data Analytics.
