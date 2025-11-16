# Task 2: Exploratory Data Analysis (EDA) - Findings Report (Titanic Dataset)

### Objective
The goal was to perform Exploratory Data Analysis (EDA) on the preprocessed Titanic data to generate descriptive statistics, visualize feature distributions, and identify key patterns and relationships relevant to predicting survival.

### Tools Used
* **Python**
* **Pandas** (Descriptive statistics and data handling)
* **Seaborn & Matplotlib** (Visualization: Histograms, Boxplots, Correlation Matrix, Pairplot)

---

### Key Statistical and Distribution Findings

| Feature | Mean | Median | Skewness Observation | ML Implication |
| :--- | :--- | :--- | :--- | :--- |
| **Survived (Target)** | **0.384** | 0.0 | Highly concentrated at 0 (non-survivor). | **Imbalance:** Model evaluation must prioritize **F1-Score/Recall** over raw Accuracy. |
| **Fare** | $32.20 | $14.45 | **Highly Right-Skewed.** The mean is significantly higher than the median, pulled by high-value outliers. | **Transformation Needed:** A **logarithmic transformation** is strongly recommended to normalize the distribution before training. |
| **Age** | 29.7 years | 28.0 years | Visually symmetrical with a slight positive skew. | **Feature Engineering:** Creating **Age Bins** (e.g., Child, Adult, Senior) may capture non-linear survival patterns. |

---

### Relationship Analysis and Multicollinearity

#### 1. Correlation Matrix (Heatmap) Findings
The heatmap revealed critical structural issues and relationships:

* **Multicollinearity Identified:** The **SibSp** (Siblings/Spouses) and **Parch** (Parents/Children) features show a moderate to strong positive correlation ($\approx$ **0.41**).
    * **Inference:** This indicates **multicollinearity**. The optimal solution is to combine them into a single feature like `Family_Size` to eliminate redundancy and stabilize model coefficients.
* **Strongest Predictor Correlation:** **Pclass** (Ticket Class) shows the strongest **negative correlation** ($\approx$ **-0.34**) with the `Survived` target.
    * **Inference:** This confirms "class mattered." Lower Pclass numbers (1st class) are associated with a higher survival probability.

#### 2. General Data Quality Inferences
* **Categorical Status:** The numerical nature of `Pclass` (1, 2, 3) and `Survived` (0, 1) confirms they are **ordinal** and **binary categorical** variables, and should not be treated as continuous.

---

### Conclusion
EDA was successful in confirming the necessity of the cleaning steps performed in Task 1 and providing clear direction for subsequent **Feature Engineering** (combining family size features) and **Feature Transformation** (log-scaling the Fare column) prior to model selection.
