# 🚢 Titanic Dataset — Exploratory Data Analysis Using Python





\

## 📌 Project Overview

This project performs **Exploratory Data Analysis (EDA)** on the famous **Titanic dataset** using Python.

The analysis explores passenger information and investigates how different factors such as **gender, passenger class, age, name titles, and number of siblings/spouses aboard** are related to passenger survival.

The complete analysis is implemented in a Jupyter Notebook using **Pandas, NumPy, Matplotlib, and Seaborn**.

---

## 🎯 Objectives

The main objectives of this project are:

* Understand the structure of the Titanic dataset.
* Load and inspect the training and testing datasets.
* Identify missing values.
* Analyze passenger survival.
* Explore the relationship between **gender and survival**.
* Analyze the relationship between **passenger class and survival**.
* Investigate **age and survival**.
* Extract passenger titles from names.
* Handle missing age values using passenger titles.
* Analyze the relationship between **SibSp (siblings/spouses aboard)** and survival.
* Visualize important patterns using different plots.

---

## 📂 Dataset

The project uses two CSV files:

* `train.csv` — Training dataset used for the main analysis.
* `test.csv` — Test dataset loaded and inspected in the notebook.

The main analysis is performed on `train.csv`.

### Important Features

| Feature    | Description                       |
| ---------- | --------------------------------- |
| `Survived` | Survival status                   |
| `Pclass`   | Passenger class                   |
| `Name`     | Passenger name                    |
| `Sex`      | Passenger gender                  |
| `Age`      | Passenger age                     |
| `SibSp`    | Number of siblings/spouses aboard |

---

## 🛠️ Technologies & Libraries

The following Python libraries are used:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sb
```

### Tools

* **Python**
* **Jupyter Notebook**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**

---

## 🔍 Exploratory Data Analysis

### 1. Loading the Dataset

The training and testing datasets are loaded using Pandas:

```python
train_data = pd.read_csv('train.csv')
test_data = pd.read_csv('test.csv')
```

The notebook also checks the current working directory and examines the shape and first few rows of the datasets.

---

### 2. Missing Value Analysis

Missing values are checked using:

```python
train_data.isnull().sum()
```

This helps identify columns containing missing or null values.

---

### 3. Survival Analysis

A count plot is used to visualize the number of passengers who survived and those who did not.

```python
sb.countplot(x='Survived', data=train_data)
plt.show()
```

This provides an initial overview of the survival distribution.

---

### 4. Gender vs Survival

The notebook investigates the relationship between passenger gender and survival.

```python
train_data.groupby(['Sex', 'Survived'])['Survived'].count()
```

It also uses visualizations to compare male and female survival:

```python
sb.countplot(x='Sex', hue='Survived', data=train_data)
plt.show()
```

This analysis helps identify differences in survival patterns between genders.

---

### 5. Passenger Class vs Survival

The relationship between passenger class and survival is explored using:

```python
sb.countplot(x='Pclass', hue='Survived', data=train_data)
plt.title('Pclass: Survived vs Dead')
plt.show()
```

The analysis considers:

* 1st Class
* 2nd Class
* 3rd Class

A cross-tabulation is also used to examine the interaction between gender, survival, and passenger class.

---

### 6. Passenger Class, Gender & Survival

A point plot is used to examine the relationship between passenger class, gender, and survival probability:

```python
sb.catplot(
    x='Pclass',
    y='Survived',
    hue='Sex',
    data=train_data,
    kind='point'
)
plt.show()
```

This provides a combined view of three important variables.

---

### 7. Age Analysis

The notebook examines the ages of passengers who survived.

It calculates:

* Maximum age among survivors
* Minimum age among survivors
* Average age among survivors

```python
survived_df = train_data[train_data['Survived'] == 1]

print('Oldest person Survived was of:', survived_df['Age'].max())
print('Youngest person Survived was of:', survived_df['Age'].min())
print('Average person Survived was of:', survived_df['Age'].mean())
```

---

### 8. Age, Passenger Class & Gender

Violin plots are used to visualize the relationship between age, passenger class, gender, and survival.

```python
sb.violinplot(
    x='Pclass',
    y='Age',
    hue='Survived',
    data=train_data,
    split=True
)
```

A similar visualization is created for:

```text
Sex vs Age vs Survived
```

These visualizations provide a more detailed understanding of the distribution of passenger ages.

---

## 👤 Passenger Title Analysis

One interesting part of the project is extracting titles from passenger names.

The notebook extracts titles such as:

* Mr
* Mrs
* Miss
* Master
* Dr
* Major
* Lady
* Countess
* Rev
* Sir
* Other

The title is extracted from the `Name` column using:

```python
train_data['Initial'] = train_data.Name.str.extract('([A-Za-z]+)\.')
```

Rare titles are then grouped into broader categories such as `Mr`, `Mrs`, `Miss`, and `Other`.

This creates a new feature:

```text
Initial
```

---

## 🧹 Handling Missing Age Values

The notebook uses passenger titles to estimate missing age values.

Different average ages are assigned to different title groups:

| Title  | Filled Age |
| ------ | ---------: |
| Mr     |         33 |
| Mrs    |         36 |
| Master |          5 |
| Miss   |         22 |
| Other  |         46 |

After filling the missing values, the notebook checks whether any missing age values remain:

```python
train_data.Age.isnull().any()
```

---

## 📊 Age Distribution by Survival

The project compares the age distribution of passengers who:

* Did not survive
* Survived

Histograms are used to visualize these distributions.

This helps understand how passenger age was distributed across the two survival groups.

---

## 👨‍👩‍👧 SibSp vs Survival

`SibSp` represents the number of siblings or spouses aboard the Titanic.

The notebook analyzes the relationship between `SibSp` and survival using:

* Cross-tabulation
* Bar plot
* Point plot

Example:

```python
sb.barplot(
    x='SibSp',
    y='Survived',
    data=train_data
)
```

The notebook also examines the relationship between `SibSp` and passenger class.

---

## 📈 Visualizations Used

The project uses several visualization techniques, including:

* 📊 Count Plot
* 📊 Bar Plot
* 📈 Point Plot
* 🎻 Violin Plot
* 📊 Histogram
* 📋 Cross-tabulation
* 📌 Categorical Point Plot

These visualizations make it easier to identify relationships and patterns in the dataset.

---

## 💡 Key Areas of Analysis

The notebook primarily focuses on these relationships:

```text
Gender ──────────────► Survival

Passenger Class ─────► Survival

Age ─────────────────► Survival

Gender + Class ──────► Survival

Age + Class ─────────► Survival

Age + Gender ────────► Survival

Passenger Title ─────► Age

SibSp ───────────────► Survival

SibSp ───────────────► Passenger Class
```

---

## 📁 Project Structure

```text
Titanic-EDA/
│
├── EDA_of_Titanic_Dataset.ipynb
├── train.csv
├── test.csv
├── README.md
└── requirements.txt
```

---

## ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/Titanic-EDA.git
```

Move into the project directory:

```bash
cd Titanic-EDA
```

Install the required libraries:

```bash
pip install numpy pandas matplotlib seaborn jupyter
```

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Then open:

```text
EDA_of_Titanic_Dataset.ipynb
```

---

## 📦 Requirements

Create a `requirements.txt` file containing:

```text
numpy
pandas
matplotlib
seaborn
jupyter
```

---

## 🧠 What I Learned

Through this project, I practiced:

* Loading datasets using Pandas
* Understanding dataset dimensions
* Inspecting DataFrames
* Detecting missing values
* Grouping and aggregating data
* Creating cross-tabulations
* Feature extraction from text
* Handling missing data
* Creating different data visualizations
* Exploring relationships between multiple variables
* Performing Exploratory Data Analysis using Python

---

## 🚀 Future Improvements

The current project focuses on **Exploratory Data Analysis**.

Possible future improvements include:

* Feature engineering
* Data preprocessing
* Encoding categorical variables
* Correlation analysis
* Building a machine learning model
* Predicting passenger survival
* Comparing different classification algorithms
* Evaluating model performance

---

## 👨‍💻 Author

**Mohd Arsalan**

BCA — Data Science & Artificial Intelligence

Babu Banarasi Das University, Lucknow

### Skills

`Python` • `SQL` • `Pandas` • `NumPy` • `Matplotlib` • `Seaborn` • `Power BI` • `Excel`

---

## ⭐ Project Status

**Status:** Completed — Exploratory Data Analysis

This repository represents my practical work in **Python-based Data Analysis and Visualization**.

If you found this project useful, consider giving the repository a ⭐.

---

## 📜 License

This project is intended for **educational and learning purposes**.
