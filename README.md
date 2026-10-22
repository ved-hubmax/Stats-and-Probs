# Statistics & Probability Practical Analysis

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A hands-on, repository-ready exploratory data analysis and statistical modeling project demonstrating foundational principles of **Descriptive Statistics**, **Outlier Detection**, **Correlation Analysis**, **Feature Encoding**, and **Probability Theory** in Python.

---

## 📌 Project Overview

This repository provides an end-to-end practical implementation of core statistical and probabilistic concepts essential for Data Science and Machine Learning. Using two diverse datasets—the global **UN Country Profile Variables** dataset and Seaborn's classic **Restaurant Tips** dataset—this project bridges theoretical concepts with programmatic execution.

### Key Highlights
- **Descriptive Statistics**: Evaluation of measures of central tendency (Mean, Median, Mode) and dispersion (Range, Quartiles, Interquartile Range).
- **Outlier Detection**: Implementation of John Tukey's IQR rule (Fences) to identify and filter population outliers, alongside a generalized multi-column outlier filtering function.
- **Correlation Analysis**: Extraction of numerical sub-matrices and visualization of multi-variable interactions using Pearson correlation heatmaps.
- **Categorical Feature Preprocessing**: Application of `scikit-learn`'s `LabelEncoder` with class mapping (`.classes_`) and automated batch categorical encoding.
- **Probability Theory**: Calculation of marginal probabilities, single-condition conditional probabilities, and compound union conditional probabilities using real transaction data.

---

## 📂 Repository Structure

```text
STATS & PROBS/
│
├── data/
│   └── country_profile_variables.csv        # Primary UN country statistics dataset (229 records, 50 features)
│
├── Statistics_and_Probability_Analysis.ipynb # Clean, fully executed, structured analysis notebook
├── 5_B_Stats&ProbHandsOn_(ved)(18_04).ipynb   # Cleaned project notebook
├── country_profile_variables.csv            # Root-level dataset fallback
├── requirements.txt                         # Python package dependencies
├── .gitignore                               # Git ignore configuration
└── README.md                                # Project documentation and methodology summary
```

---

## 📊 Datasets

### 1. UN Country Profile Variables (`country_profile_variables.csv`)
- **Source**: United Nations Data Division / World Bank Statistics.
- **Dimensions**: 229 countries/territories $\times$ 50 socioeconomic indicators.
- **Key Features Analyzed**:
  - `country`: Country name.
  - `Region`: Geographic region/classification (e.g., Caribbean, Southern Europe, Polynesia).
  - `Population in thousands (2017)`: Total national population count.
  - `Surface area (km2)`: Total geographical area.
  - `GDP: Gross domestic product`: Total economic output.
  - `Population density`: Density per square kilometer.

### 2. Restaurant Tips Dataset (`tips` via Seaborn)
- **Source**: Built-in Seaborn benchmark dataset.
- **Dimensions**: 244 dining transactions $\times$ 7 features.
- **Key Features Analyzed**:
  - `total_bill`: Bill amount in USD.
  - `tip`: Gratuity amount in USD.
  - `day`: Day of transaction (`Thur`, `Fri`, `Sat`, `Sun`).
  - `time`: Meal service time (`Lunch`, `Dinner`).
  - `size`: Party size.

---

## 🔬 Methodology & Statistical Concepts

### 1. Measures of Central Tendency
Measures of central tendency locate the focal center of a distribution:
- **Arithmetic Mean**:
  $$\mu = \frac{1}{N} \sum_{i=1}^N x_i$$
  *Population Mean:* $32,756.79$ thousand. Highly sensitive to extreme population centers (e.g., China, India).
- **Median ($50^{\text{th}}$ Percentile)**:
  $$\text{Median} = \text{Middle value of sorted array}$$
  *Population Median:* $5,448.00$ thousand. Resilient against extreme skewness.
- **Mode**:
  $$\text{Mode} = \arg\max_k (\text{Frequency}(x_k))$$
  *Region Mode:* `Caribbean` (most frequent category with 25 member states).

> **Statistical Insight**: Because $\text{Mean} \gg \text{Median}$ ($32,756.79 > 5,448.00$), the global population distribution exhibits significant **positive (right) skewness**.

---

### 2. Measures of Dispersion & Outlier Filtering (Tukey's Fences)

- **Range**: $\text{Max} - \text{Min} = 1,409,517 - 1 = 1,409,516$ thousand.
- **Quartiles & IQR**:
  - $Q_1$ ($25^{\text{th}}$ percentile): $431.00$ thousand
  - $Q_2$ ($50^{\text{th}}$ percentile / Median): $5,448.00$ thousand
  - $Q_3$ ($75^{\text{th}}$ percentile): $19,193.00$ thousand
  - $\text{IQR} = Q_3 - Q_1 = 18,762.00$ thousand

- **Tukey's IQR Fences**:
  $$\text{Lower Bound (LB)} = Q_1 - 1.5 \times \text{IQR} = 431 - 1.5 \times 18762 = -27,712.00$$
  $$\text{Upper Bound (UB)} = Q_3 + 1.5 \times \text{IQR} = 19193 + 1.5 \times 18762 = 47,336.00$$

- **Outlier Elimination**:
  - Total records before filtering: 229
  - Outliers identified beyond Upper Bound: 29 countries (e.g., mega-nations exceeding 47.3M population)
  - Records retained within normal distribution bounds: 200

---

### 3. Correlation Analysis & Visual Heatmap
Pearson correlation measures linear association between paired continuous features:
$$r_{xy} = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum (x_i - \bar{x})^2 \sum (y_i - \bar{y})^2}}$$

A $16 \times 16$ correlation matrix of all numeric variables was computed and rendered via a custom Seaborn heatmap, highlighting multi-collinearity and relationships across economic output, demographics, and energy production.

---

### 4. Categorical Feature Preprocessing (Label Encoding)
Machine learning algorithms mandate numerical input arrays:
- `Region` was mapped from 22 geographical string labels into ordinal discrete integers $[0, 21]$ using `sklearn.preprocessing.LabelEncoder`.
- The mapping between categories and integers is inspected using `le.classes_`.
- An automated reusable pipeline `encode_categorical_columns()` was developed to systematically encode all object-type features and preserve the encoder objects for inverse transformations.

---

### 5. Probability Analysis (Restaurant Dining Patterns)

Using the `tips` dataset, we evaluate both unconditional and conditional event probabilities:

| Event | Mathematical Formulation | Favorable Count | Sample Space | Probability | Percentage |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Marginal Probability of Sunday** | $P(\text{Day} = \text{Sun}) = \frac{n(\text{Sun})}{N}$ | 76 | 244 | **0.3115** | **31.15%** |
| **Conditional: Sunday given Dinner** | $P(\text{Day} = \text{Sun} \mid \text{Dinner}) = \frac{n(\text{Sun} \cap \text{Dinner})}{n(\text{Dinner})}$ | 76 | 176 | **0.4318** | **43.18%** |
| **Compound: Fri or Sat given Dinner** | $P(\text{Day} \in \{\text{Fri}, \text{Sat}\} \mid \text{Dinner}) = \frac{n(\{\text{Fri}, \text{Sat}\} \cap \text{Dinner})}{n(\text{Dinner})}$ | 99 | 176 | **0.5625** | **56.25%** |

#### Probability Theory Deductions:
1. All Sunday meal transactions occur during dinner hours ($n(\text{Sun} \cap \text{Dinner}) = 76 = n(\text{Sun})$), which increases Sunday's likelihood from $31.15\%$ globally to $43.18\%$ when conditioned on dinner service.
2. Friday and Saturday dinners represent the majority of dinner patronage ($56.25\%$).

---

## 🛠️ Setup & Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/stats-and-probability-analysis.git
cd stats-and-probability-analysis
```

### 2. Create and Activate a Virtual Environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

---

## 🚀 How to Run the Notebook

Launch JupyterLab or Jupyter Notebook:
```bash
jupyter notebook Statistics_and_Probability_Analysis.ipynb
```
Or open directly in **VS Code** with the Python and Jupyter extensions enabled.

All cell outputs, charts, and mathematical summaries are pre-executed and ready for viewing.

---

## 📈 Summary of Key Results

| Metric / Analysis | Variable / Query | Result |
| :--- | :--- | :--- |
| **Mean** | Population in thousands (2017) | **32,756.79** |
| **Median** | Population in thousands (2017) | **5,448.00** |
| **Mode** | Region | **Caribbean** (25 countries) |
| **IQR Spread** | Population in thousands (2017) | **18,762.00** ($Q_1=431.0, Q_3=19,193.0$) |
| **Tukey Upper Fence** | Population in thousands (2017) | **47,336.00** (29 outliers detected) |
| **$P(\text{Sun})$** | Day = Sunday | **31.15%** (76 / 244) |
| **$P(\text{Sun} \mid \text{Dinner})$** | Day = Sunday given Dinner | **43.18%** (76 / 176) |
| **$P(\text{Fri} \cup \text{Sat} \mid \text{Dinner})$** | Day in [Fri, Sat] given Dinner | **56.25%** (99 / 176) |

---

## 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

