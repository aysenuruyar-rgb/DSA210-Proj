# Aysenur Uyar - DSA210 Project
## Project Goal

Water sustainability and resource management are becoming some of the most critical global challenges of both today and the near future. Increasing population growth, climate change, and irregular precipitation patterns make understanding water systems more important than ever.

This project investigates whether weather conditions, particularly rainfall and snowfall, are sufficient to explain Istanbul dam occupancy levels. Using historical reservoir and weather datasets, the project applies exploratory data analysis, statistical hypothesis testing, feature engineering, and machine learning methods to better understand the complex factors affecting water availability and reservoir behavior.

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

**Data Enrichment:**

- After merging the datasets by date, additional temporal and seasonal features were created to better capture long-term reservoir behavior. These include lag variables, rolling averages, seasonal encodings, and combined precipitation indicators.
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
| **H4** | Rainy seasons have higher occupancy levels | **Confirmed** (p < 0.001) |

The hypothesis testing results suggest that short-term daily rainfall alone is not sufficient to explain dam occupancy levels. However, seasonal and long-term patterns appear to play a much stronger role.

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

- `data/processed/featured_dataset.csv`

Notebook: `notebook/04_feature_engineering.ipynb`

---

### 5. Machine Learning Modeling

A regression-based machine learning approach was applied to predict Istanbul dam occupancy levels using engineered temporal and weather-related features.
Since the dataset is time-series based, chronological train-test splitting was used to avoid data leakage.

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

### Model Performance Summary

| Model | Features | Metric | R² |
|---|---|---|---|
| Linear Regression | Weather + lag + rolling + seasonal features | MAE = 2.99 | 0.955 |
| Random Forest Regressor | All engineered features | MSE = 25.18 | 0.937 |

The machine learning results demonstrate that engineered temporal features such as lagged occupancy levels and rolling averages significantly improve prediction performance.

Both models achieved high R² values, indicating that historical occupancy patterns and seasonal dynamics are strong predictors of reservoir levels. The findings further support the earlier hypothesis testing results, which showed that short-term rainfall alone is insufficient to fully explain dam occupancy behavior.

The results show that engineered temporal features significantly improve prediction performance. Lagged occupancy levels and seasonal patterns were among the strongest predictors, while short-term daily weather variables had relatively weak predictive power.

Notebook: `notebook/05_modeling.ipynb`

---

## Key Findings

- **Rainfall alone is not sufficient**  
  No statistically significant relationship was found  

- **Weather effects are weak**  
  Very low explanatory power  

- **Seasonality is strong**  
  Dam levels vary significantly across seasons
  Rainy seasons generally have significantly higher occupancy levels than non-rainy seasons

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
│ ├── 03_hypothesis_testing_cleaned_version.ipynb
│ ├── 03_hypothesis_tests_old_version.ipynb
│ ├── 04_feature_engineering.ipynb
│ └── 05_ML_methods.ipynb
│
├── Final_Report.docx
├── Project Proposal.pdf
├── Project Proposal (extended version).pdf
├── README.md
└── requierements.txt
```
## AI Disclosure

Large Language Models (LLMs) (specifically ChatGPT) were used during parts of the project for:
- improving documentation
- refining report writing
- debugging and code explanations

All analysis, implementation, interpretation, and final decisions were completed and verified by the author.
