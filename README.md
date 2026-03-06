# NBA Awards Prediction Model

Predicting **NBA Most Valuable Player (MVP), Rookie of the Year (ROY), and Defensive Player of the Year (DPOY)** using historical player performance data and machine learning models.

This project builds preseason forecasting models using over **20 seasons of NBA data** to estimate award vote share and identify likely winners before a season begins.

---

## Project Overview

Award prediction in professional sports presents a difficult modeling challenge. Each season has **only one winner**, making the dataset extremely imbalanced. Instead of predicting winners directly, this project models **vote share**, allowing the model to rank players by expected award performance.

The goal is to evaluate whether statistical indicators of player impact can meaningfully forecast award outcomes.

---

## Dataset

The dataset combines information from **21 NBA seasons (2004–2025)**.

Sources include:

- Basketball Reference player statistics
- Advanced metrics such as:
  - Box Plus/Minus (BPM)
  - Value Over Replacement Player (VORP)
  - Win Shares
  - Win Shares per 48 minutes

Dataset summary:

| Metric | Value |
|------|------|
| Seasons | 21 |
| Player Seasons | ~13,000 |
| Unique Players | ~2,200 |
| Awards Modeled | MVP, ROY, DPOY |

Because only one player wins each award each year, the base rate of MVP winners is approximately **0.16% of player seasons**, making this a highly imbalanced prediction problem.

---

## Methodology

### Modeling Strategy

Instead of predicting a binary winner variable, the models estimate **expected vote share**, allowing players to be ranked by predicted performance.

Two modeling approaches were tested:

- **Ridge Regression**
  - Linear baseline model
  - Interpretable feature relationships

- **Histogram Gradient Boosting Regressor**
  - Nonlinear ensemble model
  - Captures complex interactions between advanced metrics

All preprocessing was performed using **scikit-learn pipelines**, including:

- missing value imputation
- feature scaling
- categorical encoding

This ensures **reproducibility and prevents data leakage**.

---

### Train / Test Design

To simulate real forecasting conditions, the dataset was split chronologically:

- **Training Data:** First 16 seasons
- **Testing Data:** Most recent 5 seasons (2021–2025)

This prevents models from learning from future seasons and better reflects real-world prediction scenarios.

---

## Results

### MVP Model

The Gradient Boosting model outperformed the linear baseline.

Performance on the test dataset:

| Model | RMSE | Top-1 Accuracy |
|------|------|------|
| Ridge Regression | Higher error | Lower accuracy |
| Gradient Boosting | **0.0048 RMSE** | **1.00 Top-1 accuracy (5 seasons)** |

While perfect Top-1 accuracy should not be overinterpreted due to the small test window, the results indicate strong stability in identifying the top candidate.

Key predictive features included:

- Box Plus/Minus (BPM)
- Value Over Replacement Player (VORP)
- Win Shares

These metrics reflect the broader trend in modern MVP voting toward **overall impact rather than raw scoring totals**.

---

### Defensive Player of the Year

For DPOY prediction, the **Ridge Regression model produced more stable rankings**, likely because defensive voting often depends on team context and broader impact metrics.

Important predictors included:

- Defensive Win Shares
- Defensive BPM
- Team defensive rating rank

---

### Rookie of the Year

Rookie prediction requires a different approach because rookies have no NBA statistics.

A **draft-based dataset** was used to estimate ROY probability based on:

- draft position
- prospect profile
- historical rookie outcomes

---

## Key Takeaways

Several insights emerged from this analysis:

- Advanced impact metrics (BPM, VORP, Win Shares) strongly predict MVP outcomes.
- Defensive awards are influenced heavily by **team defensive performance**.
- Modeling vote share rather than binary winners improves predictive stability.
- Chronological validation is essential to avoid unrealistic evaluation.

---

## Tools & Technologies

Python  
pandas  
NumPy  
scikit-learn  
Gradient Boosting  
Ridge Regression  
Jupyter Notebook  

---

## Future Improvements

Possible extensions of this work include:

- Incorporating team performance projections
- Adding betting market information
- Expanding feature engineering for rookie prediction
- Applying probabilistic ranking models

---

## Author

Richard Wilders

M.S. Data Science (Expected 2026)  
Former U.S. Marine Corps Signals Intelligence Analyst

LinkedIn  
https://linkedin.com/in/richard-wilders-915395106
