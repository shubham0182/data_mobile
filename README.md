# 📱 Mobile Data Cleaning & Analysis Project

## 📌 Overview

This project focuses on **data cleaning, preprocessing, and visualization** of a noisy mobile dataset.
The dataset contains information like **brand, price, battery, storage, and ratings**, but includes missing and inconsistent values.

The goal is to transform raw data into a clean and usable format for analysis.

---

## 📂 Dataset

File used:

* `noisy_mobile_dataset.csv`

---

## 🛠️ Technologies Used

* Python 🐍
* Pandas 📊
* NumPy 🔢
* Matplotlib 📈

---

## 🔄 Step-by-Step Code Explanation

### 1️⃣ Import Libraries

```python
import pandas as pd
import numpy as np
import word2number as w2n
```

* `pandas` → Data handling
* `numpy` → Numerical operations
* `word2number` → Convert text numbers to numeric

---

### 2️⃣ Load Dataset

```python
data_mobile = pd.read_csv('noisy_mobile_dataset.csv')
```

* Reads CSV file into DataFrame

---

### 3️⃣ Initial Data Exploration

```python
data_mobile.head()
data_mobile.info()
data_mobile.describe()
```

* `head()` → View first 5 rows
* `info()` → Check data types & null values
* `describe()` → Statistical summary

---

### 4️⃣ Convert Columns to Numeric

```python
data_mobile['battery'] = pd.to_numeric(data_mobile['battery'], errors='coerce')
data_mobile['price'] = pd.to_numeric(data_mobile['price'], errors='coerce')
data_mobile['storage'] = pd.to_numeric(data_mobile['storage'], errors='coerce')
data_mobile['rating'] = pd.to_numeric(data_mobile['rating'], errors='coerce')
```

* Converts text values into numbers
* `errors='coerce'` → invalid values become `NaN`

---

### 5️⃣ Handle Missing Values

#### 🔹 Rating Column

```python
data_mobile['rating'] = data_mobile['rating'].fillna(data_mobile['rating'].mean())
```

* Missing ratings replaced with **mean value**

#### 🔹 Price Column

```python
data_mobile['price'] = data_mobile['price'].fillna(data_mobile['price'].median())
```

* Missing prices replaced with **median value**

---

### 6️⃣ Format Data

```python
data_mobile['rating'] = data_mobile['rating'].round(2)
```

* Limits rating to **2 decimal places**

---

### 7️⃣ Feature Engineering

#### 🔹 Storage Based on Price

```python
data_mobile["storage"] = data_mobile["price"].apply(lambda x: 512 if x > 50000 else 256)
```

* Expensive phones → 512GB
* Budget phones → 256GB

#### 🔹 Battery Based on Price

```python
data_mobile["battery"] = data_mobile["price"].apply(lambda x: 6500 if x > 50000 else 5000)
```

* High price → bigger battery

---

### 8️⃣ Remove Unnecessary Column

```python
data_mobile.drop("id", axis=1, inplace=True)
```

* Removes `id` column

---

## 📊 Data Visualization

### 🔹 Pie Chart (Brand Distribution)

```python
plt.figure(figsize=(10, 10))
plt.pie(data_mobile['brand'].value_counts(), autopct='%1.1f%%')
plt.legend(data_mobile['brand'].unique(), loc='upper right')
plt.show()
```

* Shows percentage distribution of brands

---

### 🔹 Bar Chart (Price by Brand)

```python
plt.bar(data_mobile['brand'], data_mobile['price'])
plt.xlabel('Brand')
plt.ylabel('Price')
plt.title('Price of Mobile Phones by Brand')
plt.xticks(rotation=45)
plt.grid(axis='y', color='black')
plt.show()
```

* Compares price across brands

---

### 🔹 Scatter Plot

```python
plt.scatter(data_mobile['brand'], data_mobile['price'])
plt.show()
```

* Visualizes relationship between brand and price

---

## ⚠️ Important Notes

* Avoid using `inplace=True` with assignment:

```python
data_mobile['rating'] = data_mobile['rating'].fillna(..., inplace=True) ❌
```

✔️ Correct:

```python
data_mobile['rating'] = data_mobile['rating'].fillna(...)
```

---

## 🚀 Conclusion

This project demonstrates:

* Data cleaning
* Handling missing values
* Feature engineering
* Data visualization

It transforms a messy dataset into meaningful insights 📊

---

## 🔗 Future Improvements

* Add machine learning model 🤖
* Predict mobile price or rating
* Build dashboard using Power BI

---

## 👨‍💻 Author

**Shubham Thakor**
