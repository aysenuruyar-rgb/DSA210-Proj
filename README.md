# Aysenur Uyar - DSA210 Project
## Data Sources

This project integrates two main datasets covering **2000s–present**, enriched and aligned temporally:

### 1. Dam Occupancy Data (Istanbul)

- **Source:** İstanbul Metropolitan Municipality Open Data Portal  
- **Frequency:** Daily  
- **Features:**
  - Dam occupancy rate (%)  
- **Collection Method:** Downloaded from official open data platform  

---

### 2. Weather Data (Istanbul Region)

- **Source:** Open-Meteo Historical Weather API  
- **Frequency:** Daily  
- **Features:**
  - Rainfall (mm)
  - Snowfall (cm)
  - Temperature (°C)  
- **Collection Method:** Python API requests  

---

**Data Organization:**

- Raw data: `data/raw/`  
- Processed data:
  - data/processed/final_dataset.csv
  - data/processed/featured_dataset.csv

---

## Data Analysis Pipeline

### 1. Data Preparation

- Merged dam and weather datasets based on date  
- Handled missing values  
- Created clean dataset (`final_dataset.csv`)  

Notebook: `notebook/01_data_preparation.ipynb`

---

### 2. Exploratory Data Analysis (EDA)

EDA focused on understanding patterns and relationships:

- Distribution analysis (histograms)  
- Time series plots  
- Scatter plots (rain vs dam, snow vs dam)  
- Seasonal comparisons  
- Correlation matrix  

Notebook: `notebook/02_eda.ipynb`  

All figures are stored in the `figures/` directory.

---

### 3. Hypothesis Testing

The following hypotheses were evaluated:

| Hypothesis | Description | Result |
|----------|------------|--------|
| **H1** | Rainfall affects dam occupancy | **Not significant** (p ≈ 0.415) |
| **H2** | Weather variables explain dam levels | **Very weak** (R² ≈ 0.02) |
| **H3** | Seasonality affects dam occupancy | **Confirmed** (p < 0.001) |

Notebook: `notebook/03_hypothesis_tests.ipynb`

---

### 4. Feature Engineering

To improve model performance, additional features were created:

- Lag variables (previous dam levels and weather conditions)
- Rolling averages (3-month trends)
- Combined precipitation features (rain + snow)
- Seasonal encoding using sine and cosine transformations
- Binary rain indicator (`is_rainy`)

The processed dataset is saved as:

- `featured_dataset.csv`

Notebook: `notebook/04_feature_engineering.ipynb`

---

### 5. Machine Learning Modeling

A regression-based machine learning approach was applied to predict dam occupancy.

- **Models used:**
  - Linear Regression
  - Random Forest Regressor

- **Features included:**
  - Weather variables
  - Lag features
  - Rolling averages
  - Seasonal features

- **Evaluation metrics:**
  - MAE (Mean Absolute Error)
  - R² (Coefficient of Determination)
  
**Results:**

- Linear regression achieved strong performance, largely driven by lagged dam variables  
- Random Forest captured non-linear relationships between variables  
- Temporal features (lags and seasonality) were the most important predictors  
- Models confirm that short-term weather variables alone are insufficient  

Notebook: `notebook/05_modeling.ipynb`

---

## Key Findings

- **Rainfall alone is not sufficient**  
  No statistically significant relationship was found  

- **Weather effects are weak**  
  Very low explanatory power  

- **Seasonality is strong**  
  Dam levels vary significantly across seasons  

- **Water systems are complex**  
  Dam levels depend on long-term accumulation, not daily rain

---

## Project Structure

```
DSA210-Proj/
│
├── data/
│ ├── raw/ # Original collected datasets
│ └── processed/ # Cleaned and merged dataset
│
├── figures/ # Generated plots and visualizations
│
├── notebook/ # Jupyter notebooks for analysis
│ ├── 01_data_preparation.ipynb
│ ├── 02_eda.ipynb
│ ├── 03_hypothesis_tests.ipynb
│ ├── 04_feature_engineering.ipynb
│ └── 05_modeling.ipynb
│
├── Project Proposal.pdf
└── README.md
```
