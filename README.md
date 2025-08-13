# 🏭 Garment Factory Productivity – EDA & ANN Regression

This project analyzes a real-world garment production dataset and builds **Artificial Neural Network (ANN)** models to predict each team’s **productivity score**. It walks through the full pipeline: data loading, EDA, feature engineering, scaling, modeling (Sequential & Functional ANN), and evaluation with regression metrics.

---

## 🎯 Objectives

* Explore how operational factors relate to productivity
* Engineer features from dates and categories
* Train and compare **Sequential vs Functional** ANN architectures
* Evaluate models with **MSE, RMSE, and R²**
* Select the best-performing model for reporting

---

## 🗂️ Dataset

Each row is a team–day observation.

* `date` — Date of assessment
* `day` — Day of week
* `quarter` — Quarter of year (`Quarter1–Quarter4`)
* `Team Code` — Team identifier
* `smv` — Standard Minute Value (allocated time per task)
* `wip` — Work-in-progress units
* `over_time` — Overtime minutes
* `incentive` — Incentive (USD)
* `idle_time` — Idle minutes
* `idle_men` — Number of idle workers
* `no_of_style_change` — Style change count
* `no_of_workers` — Team size
* `productivity_score` — **Target** (percentage, typically 0–1)

---

## 🧹 Data Preparation

### Outliers

* Inspected via histograms and boxplots.
* **Kept** (considered operationally reasonable).

### Feature Engineering

* **Date split** (derived components as needed).
* **Manual encoding for `day`** (ordinal).
* **One-hot encoding for `Team Code`** (and relevant categoricals).

### Train/Test Split & Scaling

* **Split before scaling** to avoid leakage.
* **RobustScaler** applied to features (robust to heavy tails).

---

## 📊 Exploratory Data Analysis (EDA)

* **Distributions** for numeric variables (e.g., `over_time`, `idle_time`, `wip`, `smv`, `incentive`).
* **Boxplots of `productivity_score`** against all variables.
* **Correlation heatmap** among numeric features and `productivity_score`.

---

## 🧠 Modeling

### Models

* **ANN – Sequential API**
* **ANN – Functional API**
* Both base versions were **modified** (architecture/regularization tweaks).
* **Best model:** **Modified Sequential ANN** (selected by test-set metrics).

### Training Setup

* Loss: **MSE**
* Optimizer: (e.g., **Adam**, per notebook)
* Early stopping / callbacks as configured in the notebook
* Reproducible splits with fixed random state

---

## 📈 Evaluation

**Metrics:** **MSE**, **RMSE**, **R²**.
**Comparison:** Sequential (base) vs Functional (base) vs **Modified Sequential** vs Modified Functional.
The **Modified Sequential ANN** achieved the **lowest MSE/RMSE** and **highest R²** on the test set.
(See notebook outputs for exact values.)

---

## 📌 Conclusion

* Outliers **kept**; **RobustScaler** mitigated heavy-tailed features.
* EDA focused on **distributions**, **boxplots vs productivity**, and **correlation heatmap**.
* Features: **date split**, **manual `day` encoding**, **one-hot `Team Code`**.
* **Train/test split before scaling** to prevent leakage.
* Compared **Sequential vs Functional** ANN (base + modified).
* **Modified Sequential ANN** delivered the **best MSE/RMSE/R²** on the test set.
