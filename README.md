# 🎬 Netflix Movies & TV Shows – Exploratory Data Analysis

## 📌 Project Overview

This project focuses on performing **Exploratory Data Analysis (EDA)** on a Netflix Movies and TV Shows dataset using Python.

The primary goal is to understand the structure and quality of the dataset, identify missing and inconsistent data, perform data cleaning and transformation, and prepare the dataset for further analysis.

The project covers the initial stage of an EDA workflow, with a major focus on **Data Understanding and Data Cleaning**.

---

## 🎯 Project Objectives

The main objectives of this project are:

* Understand the structure of the Netflix dataset.
* Identify the number of rows and columns.
* Examine column names and data types.
* Identify missing values.
* Check for duplicate records.
* Convert columns into appropriate data types.
* Identify inconsistent values.
* Clean categorical data.
* Transform multiple-value columns for analysis.
* Prepare a clean dataset for further EDA and visualization.

---

## 📂 Dataset Description

The dataset contains information about Netflix Movies and TV Shows.

### Main Columns

| Column         | Description                                      |
| -------------- | ------------------------------------------------ |
| `show_id`      | Unique identifier of the content                 |
| `type`         | Type of content – Movie or TV Show               |
| `title`        | Title of the content                             |
| `director`     | Director of the content                          |
| `cast`         | Cast members                                     |
| `country`      | Country or countries associated with the content |
| `date_added`   | Date when the content was added to Netflix       |
| `release_year` | Original release year                            |
| `rating`       | Content rating                                   |
| `duration`     | Duration of the content                          |
| `listed_in`    | Genre/category of the content                    |
| `description`  | Description of the content                       |

---

# 🔍 Project Workflow

## 1. Import Libraries

The project begins by importing the required Python libraries:

```python
import pandas as pd
import numpy as np
```

**Pandas** is used for data manipulation and analysis, while **NumPy** is used for numerical operations.

---

## 2. Load the Dataset

The Netflix dataset is loaded using Pandas:

```python
df = pd.read_csv("netflix_movies.csv")
```

The first few records are displayed using:

```python
df.head()
```

This helps to understand the structure and contents of the dataset.

---

## 3. Identify Rows and Columns

The shape of the dataset is checked using:

```python
df.shape
```

This provides the number of rows and columns present in the dataset.

---

## 4. Check Column Names

The column names are displayed using:

```python
for col in df.columns:
    print(col)
```

This helps identify the variables available for analysis.

---

## 5. Check Data Types

The data types of all columns are checked using:

```python
df.dtypes
```

This helps identify columns that may require data-type conversion.

---

## 6. Convert `date_added` to Datetime

The `date_added` column is converted into datetime format:

```python
df["date_added"] = pd.to_datetime(
    df["date_added"],
    errors="coerce"
)
```

This conversion makes it possible to perform date-based analysis later.

The year, month, and day can then be extracted using:

```python
df["date_added"].dt.year
df["date_added"].dt.month
df["date_added"].dt.day
```

---

# 🧹 Data Cleaning

## 7. Identify Missing Values

Missing values are checked using:

```python
df.isnull().sum()
```

The project also calculates the percentage of missing values:

```python
(df.isnull().sum() / len(df) * 100).round(2)
```

In the initial dataset check, the `date_added` column contains missing values.

---

## 8. Check Duplicate Records

Duplicate records are identified using:

```python
print(df.duplicated().sum())
```

If duplicates are present, they can be removed using:

```python
df = df.drop_duplicates()
```

The dataset can then be checked again:

```python
df.duplicated().sum()
```

---

## 9. Handle Missing Categorical Values

The project handles missing values in categorical columns using `"Unknown"` where required.

Examples:

```python
df["director"] = df["director"].fillna("Unknown")
df["cast"] = df["cast"].fillna("Unknown")
df["country"] = df["country"].fillna("Unknown")
df["rating"] = df["rating"].fillna("Unknown")
df["duration"] = df["duration"].fillna("Unknown")
```

---

## 10. Convert `release_year`

The `release_year` column is converted into numeric format:

```python
df["release_year"] = pd.to_numeric(
    df["release_year"],
    errors="coerce"
)
```

The minimum and maximum release years are also checked.

---

# ⚠️ Identifying Inconsistent Data

## 11. Check Content Types

Unique values in the `type` column are checked:

```python
df["type"].unique()
```

This helps identify whether the column contains expected content categories.

---

## 12. Check Ratings

Unique rating values are examined using:

```python
print(df["rating"].unique())
```

The project identifies records containing:

```text
74 min
84 min
66 min
```

These values are investigated because they appear to represent duration values rather than content ratings.

---

# 🌍 Country Data Cleaning

The country column contains records where multiple countries are stored in a single cell.

For example:

```text
United States, India, France
```

To analyze individual countries, the values are split and expanded:

```python
countries = df["country"].str.split(", ").explode()

countries.value_counts().head(10)
```

This transforms multiple country values into individual records that can be counted separately.

The project also removes unnecessary spaces and commas from country values.

---

# 🎭 Genre Data Transformation

The `listed_in` column contains multiple genres in some records.

The values are separated using:

```python
genre_df = df["listed_in"].str.split(",").explode()
genre_df = genre_df.str.strip()
```

Then genre frequencies can be calculated using:

```python
genre_df.value_counts()
```

This prepares the genre information for further analysis.

---

# 🛠️ Technologies Used

* **Python**
* **Pandas**
* **NumPy**
* **Jupyter Notebook**
* **Google Colab**

---

# 📚 Skills Demonstrated

Through this project, I practiced:

* Data Loading
* Data Inspection
* Data Cleaning
* Missing Value Analysis
* Duplicate Detection
* Data Type Conversion
* String Manipulation
* Data Transformation
* `split()`
* `explode()`
* Basic Exploratory Data Analysis

---

# 🚀 Future Scope

The cleaned dataset can be used for further analysis and visualization, including:

* Movie vs TV Show distribution
* Netflix content trends by year
* Country-wise content analysis
* Genre analysis
* Rating analysis
* Duration analysis
* Interactive dashboard development

---

## 📁 Project Files

```text
Netflix-EDA-Data-Analysis/
│
├── Netflix_EDA.ipynb
├── netflix_movies.csv
├── README.md
└── images/
```

---

## 👩‍💻 Author

**Archana Meegada**

B.Tech – Artificial Intelligence & Data Science

Aspiring Data Analyst

---

⭐ If you find this project useful, feel free to explore the notebook and share your feedback.
