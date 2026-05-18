# DSA210-Project

**DSA 210 – Introduction to Data Science (Spring 2026)** ---

## Motivation 
Istanbul is a very large city where earthquake safety is a major topic because of the history of earthquakes and the high number of old buildings. This project explores how earthquake risk and building characteristics affect property prices. By analyzing prices along with variables like building age, district risk levels, and apartment sizes, the study aims to see if the real estate market actually prices in these safety risks. 

---

## Data Sources
The project uses a structured dataset covering housing listings across various districts in Istanbul:
* **Source:** Real estate listings and regional risk assessments.
* **Features:** `price` (TL), `sq_meters`, `building_age`, `district`, and `earthquake_risk`.
* **Calculated Feature:** `price_per_m2` (Price divided by square meters) to normalize property sizes for fair comparisons.
* **Risk Classification:** Properties are grouped into **Low**, **Medium**, and **High** risk categories based on municipality hazard maps.

---

## Data Analysis Pipeline

### 1. Data Preparation
* Loaded the raw data using `pandas`.
* Created the `price_per_m2` metric to ensure fair comparisons regardless of apartment size.
* Grouped the earthquake risk zones to prepare the data for statistical testing.

### 2. Exploratory Data Analysis (EDA)
Generated comparative charts using `matplotlib` to understand the data:
* **Bar Chart**: Shows the average price per square meter for Low, Medium, and High earthquake risk zones.
* **Histogram**: Shows the overall distribution of housing prices to spot any unusual trends or outliers.

---

## Hypothesis Testing

The following hypotheses were evaluated using ANOVA and Independent T-Tests via `scipy.stats` to check if housing prices differ based on risk levels:

| Hypothesis | Description | Statistical Test | Result / P-value | Conclusion |
| :--- | :--- | :--- | :--- | :--- |
| **H1** | Prices per $m^2$ are different across all three risk groups. | One-Way ANOVA | $p \approx 0.0124$ | **Confirmed** ($p < 0.05$) |
| **H2** | There is a significant price gap specifically between Low and High-risk zones. | Two-Sample T-Test | $p \approx 0.0233$ | **Confirmed** ($p < 0.05$) |

> **Statistical Interpretation:** Since both $p$-values are less than 0.05, we reject the null hypothesis. The data shows that earthquake risk level is a statistically significant factor in housing prices, and safer zones command a higher price.

---

## Machine Learning Models (Unsupervised Learning)

We used **K-Means Clustering** and **Hierarchical Clustering** via `scikit-learn` and `scipy.cluster.hierarchy` to find natural groups in the data.

### Model Setup
* **Features Used:** `price_per_m2` and `building_age`.
* **Preprocessing:** Features were scaled using `StandardScaler` to handle the large differences between pricing numbers and building ages.
* **Hyperparameters:** $K=3$ clusters for K-Means; Ward's linkage method for the Dendrogram.

### Model Performance and Evaluation

| Model Type | Key Metric / Visualization | Primary Evaluation Strategy | Result / Insight |
| :--- | :--- | :--- | :--- |
| **K-Means ($K=3$)** | Cluster Scatter Plot | Cross-referenced clusters with real risk tiers using `.value_counts()` | Separated premium new builds from older, lower-priced properties. |
| **Agglomerative** | Hierarchical Dendrogram Tree | Inspected tree branches and split distances | Confirmed a natural 3-cluster split matching the market data. |

> **Key Machine Learning Insight:** Even though the machine learning models did not see the `earthquake_risk` column during training, the final clusters lined up closely with the real-world risk zones. This shows that building age and price automatically group properties along safety lines.

---

## Key Findings
* **Risk Premiums Exist:** Properties in low earthquake risk zones show a statistically higher average price per square meter compared to high-risk zones.
* **Age and Price Grouping:** Unsupervised clustering successfully isolated older, lower-priced properties from newer, premium developments, showing high alignment with regional risk divisions.

---

## Limitations and Future Work
* **Sample Size:** The analysis is based on a clean sample of 50 listings; expanding to a larger web-scraped dataset from local real estate portals would increase robustness.
* **Confounding Variables:** Factors like proximity to the metro, coastal views, or luxury finishes were not modeled but highly influence price.
* **Future Models:** Implementing supervised classification (e.g., Random Forest) to predict a property's risk tier using only its market listing features.

---

### Installation
git clone [https://github.com/Murad-Mammadov/DSA210-Project.git](https://github.com/Murad-Mammadov/DSA210-Project.git)
cd DSA210-Project

## Project Structure

DSA210-Project/
├── istanbul_housing.csv              # Cleaned property dataset
├── DSA210_Istanbul_Housing_EDA.ipynb # Full pipeline (EDA, Testing, Clustering)
└── README.md                         # Project documentation

## Ai Assistance Disclosure

* Ai tools were used to help with troubleshooting the data analysis setup, formatting some codes, and organizing the project structure.