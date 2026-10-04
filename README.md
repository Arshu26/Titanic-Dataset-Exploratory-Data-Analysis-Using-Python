# 🚢 Titanic Dataset — Exploratory Data Analysis Using Python

> **An exploratory data analysis project focused on understanding the factors associated with passenger survival on the Titanic.**

---

## 📌 About the Project

The **Titanic Dataset — Exploratory Data Analysis (EDA)** project analyzes passenger information from the Titanic dataset using **Python**.

The project explores how different passenger attributes such as **gender, passenger class, age, passenger titles, and number of siblings/spouses aboard** are associated with survival.

The complete analysis is performed using **Jupyter Notebook** with Python data-analysis and visualization libraries including **Pandas, NumPy, Matplotlib, and Seaborn**.

---

## 🎯 Project Objectives

The major objectives of this project are:

* Understand the structure and characteristics of the Titanic dataset.
* Load and inspect training and testing datasets.
* Identify and analyze missing values.
* Explore overall passenger survival.
* Analyze the relationship between **gender and survival**.
* Investigate the impact of **passenger class on survival**.
* Analyze **age distribution and survival**.
* Study the combined relationship between **gender, class, age, and survival**.
* Extract passenger titles from names.
* Use passenger titles to handle missing age values.
* Analyze the relationship between **SibSp and survival**.
* Create meaningful visualizations to identify patterns and relationships.

---

## 📂 Dataset

The project uses the following datasets:

| File        | Description                                  |
| ----------- | -------------------------------------------- |
| `train.csv` | Main dataset used for exploratory analysis   |
| `test.csv`  | Dataset loaded and inspected in the notebook |

### 🔑 Important Features

| Feature    | Description                       |
| ---------- | --------------------------------- |
| `Survived` | Survival status of the passenger  |
| `Pclass`   | Passenger class                   |
| `Name`     | Passenger name                    |
| `Sex`      | Passenger gender                  |
| `Age`      | Passenger age                     |
| `SibSp`    | Number of siblings/spouses aboard |

---

# 🔎 Exploratory Data Analysis

## 1️⃣ Dataset Loading & Inspection

The datasets are loaded using Pandas:

```python
import pandas as pd

train_data = pd.read_csv("train.csv")
test_data = pd.read_csv("test.csv")
```

The notebook also examines the dataset structure, dimensions, and initial records.

---

## 2️⃣ Missing Value Analysis

Missing values are identified using:

```python
train_data.isnull().sum()
```

This helps determine which columns contain missing data and require further analysis or treatment.

---

## 3️⃣ Survival Analysis

The overall survival distribution is analyzed using a count plot.

```python
sb.countplot(x="Survived", data=train_data)
plt.show()
```

This provides an initial understanding of the number of passengers who survived and those who did not.

---

## 4️⃣ Gender vs Survival

The project investigates the relationship between passenger gender and survival.

```python
train_data.groupby(
    ["Sex", "Survived"]
)["Survived"].count()
```

A visualization is also created:

```python
sb.countplot(
    x="Sex",
    hue="Survived",
    data=train_data
)
plt.show()
```

This allows survival patterns to be compared across male and female passengers.

---

## 5️⃣ Passenger Class vs Survival

Passenger class is analyzed to understand its relationship with survival.

The three passenger classes are:

* **1st Class**
* **2nd Class**
* **3rd Class**

Visualization:

```python
sb.countplot(
    x="Pclass",
    hue="Survived",
    data=train_data
)

plt.title("Pclass: Survived vs Dead")
plt.show()
```

The analysis also examines the interaction between **passenger class, gender, and survival**.

---

## 6️⃣ Passenger Class + Gender + Survival

A categorical point plot is used to analyze survival patterns across passenger class and gender.

```python
sb.catplot(
    x="Pclass",
    y="Survived",
    hue="Sex",
    data=train_data,
    kind="point"
)

plt.show()
```

This provides a combined view of three important variables.

---

# 🎂 Age Analysis

## 7️⃣ Age of Surviving Passengers

The project analyzes the age distribution of passengers who survived.

The following values are calculated:

* Oldest surviving passenger
* Youngest surviving passenger
* Average age of surviving passengers

```python
survived_df = train_data[
    train_data["Survived"] == 1
]

print(
    "Oldest person Survived was of:",
    survived_df["Age"].max()
)

print(
    "Youngest person Survived was of:",
    survived_df["Age"].min()
)

print(
    "Average person Survived was of:",
    survived_df["Age"].mean()
)
```

---

## 8️⃣ Age + Passenger Class + Survival

Violin plots are used to analyze the relationship between:

**Passenger Class + Age + Survival**

```python
sb.violinplot(
    x="Pclass",
    y="Age",
    hue="Survived",
    data=train_data,
    split=True
)
```

This visualization helps examine the distribution of passenger ages across different classes and survival groups.

---

# 👤 Passenger Title Analysis

## 9️⃣ Extracting Titles from Passenger Names

Passenger titles are extracted from the `Name` column.

Examples include:

* `Mr`
* `Mrs`
* `Miss`
* `Master`
* `Dr`
* `Major`
* `Lady`
* `Countess`
* `Rev`
* `Sir`
* `Other`

The title is extracted using:

```python
train_data["Initial"] = train_data.Name.str.extract(
    "([A-Za-z]+)\\."
)
```

Rare titles are grouped into broader categories such as:

* `Mr`
* `Mrs`
* `Miss`
* `Other`

This creates a new feature:

```text
Initial
```

---

# 🧹 Handling Missing Age Values

Passenger titles are used to help estimate missing age values.

The project uses the following filled ages:

| Title    | Filled Age |
| -------- | ---------: |
| `Mr`     |         33 |
| `Mrs`    |         36 |
| `Master` |          5 |
| `Miss`   |         22 |
| `Other`  |         46 |

After filling the missing values, the notebook checks whether any missing age values remain:

```python
train_data.Age.isnull().any()
```

---

# 📊 Age Distribution by Survival

The project compares the age distribution between:

* Passengers who **survived**
* Passengers who **did not survive**

Histograms are used to visualize the two groups and understand their age distributions.

---

# 👨‍👩‍👧 SibSp Analysis

`SibSp` represents the **number of siblings or spouses aboard the Titanic**.

The project examines the relationship between `SibSp` and survival using:

* Cross-tabulation
* Bar plots
* Point plots

Example:

```python
sb.barplot(
    x="SibSp",
    y="Survived",
    data=train_data
)
```

The relationship between **SibSp and passenger class** is also examined.

---

# 📈 Visualizations

The project uses multiple visualization techniques to understand the dataset.

| Visualization             | Analysis                                   |
| ------------------------- | ------------------------------------------ |
| 📊 Count Plot             | Survival and categorical comparisons       |
| 📊 Bar Plot               | SibSp and survival                         |
| 📍 Point Plot             | Survival relationships                     |
| 🎻 Violin Plot            | Age distribution                           |
| 📊 Histogram              | Age distribution by survival               |
| 📋 Cross-tabulation       | Relationship between categorical variables |
| 📍 Categorical Point Plot | Class, gender and survival                 |

---

# 🔗 Key Analysis Areas

The major relationships explored in this project are:

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

# 🛠️ Technologies & Tools

### Programming Language

* 🐍 **Python**

### Libraries

* **Pandas** — Data manipulation and analysis
* **NumPy** — Numerical operations
* **Matplotlib** — Data visualization
* **Seaborn** — Statistical visualization

### Development Environment

* **Jupyter Notebook**

---

# 📁 Project Structure

```text
Titanic-EDA/
│
├── 📓 EDA_of_Titanic_Dataset.ipynb
│
├── 📊 train.csv
│
├── 📊 test.csv
│
├── 📄 README.md
│
└── 📦 requirements.txt
```

---

# ⚙️ How to Run the Project

## 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/Titanic-EDA.git
```

## 2. Open the Project Directory

```bash
cd Titanic-EDA
```

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

## 5. Open the Notebook

Open:

```text
EDA_of_Titanic_Dataset.ipynb
```

Run the notebook cells sequentially to reproduce the analysis.

---

# 📦 Requirements

The project requires the following Python libraries:

```text
numpy
pandas
matplotlib
seaborn
jupyter
```

---

# 🧠 Skills Demonstrated

This project demonstrates practical skills in:

* Python Programming
* Data Cleaning
* Data Inspection
* Exploratory Data Analysis
* Missing Value Analysis
* Data Aggregation
* GroupBy Operations
* Cross-tabulation
* Feature Extraction
* Feature Transformation
* Data Visualization
* Statistical Exploration
* Analytical Thinking

---

# 📚 Key Learning Outcomes

Through this project, I gained practical experience in:

* Working with real-world datasets.
* Understanding dataset structure and variables.
* Identifying missing data.
* Performing exploratory analysis using Pandas.
* Extracting useful information from text data.
* Creating new features from existing columns.
* Handling missing values.
* Comparing categorical variables.
* Creating meaningful visualizations.
* Interpreting relationships between different variables.

---

# 🚀 Future Improvements

This project currently focuses on **Exploratory Data Analysis**.

Possible future improvements include:

* Advanced feature engineering
* Data preprocessing
* Encoding categorical variables
* Correlation analysis
* Feature selection
* Machine Learning model development
* Passenger survival prediction
* Classification algorithm comparison
* Model evaluation
* Hyperparameter tuning

---

# 👨‍💻 Author

### **Mohd Arsalan**

🎓 **BCA – Data Science & Artificial Intelligence**
🏫 **Babu Banarasi Das University, Lucknow**

### Technical Skills

`Python` • `SQL` • `Pandas` • `NumPy` • `Matplotlib` • `Seaborn` • `Power BI` • `Excel`

---

# 📌 Project Status

🟢 **Completed — Exploratory Data Analysis**

This project represents practical work in **Python-based Data Analysis and Data Visualization**.

---

# ⭐ Support

If you found this project useful or informative, consider giving the repository a ⭐ on GitHub.

---

## 📜 License

This project is created for **educational and learning purposes**.
