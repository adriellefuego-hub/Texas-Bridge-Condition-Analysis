# 🌉 Texas Bridge Condition — Regression Analysis
**Adrielle Fuego | Statistics for AI and Data Science**

A multiple linear regression analysis of **~34,000 Texas bridges**, predicting structural condition from age, material, design type, and traffic patterns. The project includes end-to-end data preparation, feature engineering, model comparison, and policy-oriented conclusions for infrastructure maintenance.

---

## Problem

The Texas Department of Transportation manages thousands of bridges across the state. This analysis investigates: **which factors most strongly predict a bridge's current structural condition**, and how well those factors can be modelled.

---

## Approach

### Target Variable
**Current Condition** — a composite score (0–27) derived from three sub-ratings:
- Deck rating + Superstructure rating + Substructure rating

Each component is mapped from categorical labels (*Failed → Excellent*) to a 0–9 numeric scale.

### Predictors
| Variable | Type | Notes |
|---|---|---|
| Age | Numeric | Derived as `2025 − Year built` |
| Average Daily Traffic | Numeric | Rescaled to thousands of vehicles/day |
| Truck Percentage | Numeric | Share of traffic that is heavy vehicles |
| Material | Categorical | Concrete / Steel / Other (small categories merged) |
| Design | Categorical | Beam / Slab / Other (small categories merged) |

### Data Cleaning Decisions
- **Excluded historic bridges** (classified as Registered/Possible Historic): preservation regulations make their condition unrepresentative of normal ageing
- **Excluded bridges over 100 years old**: extreme outliers distort regression coefficients
- **Merged rare categories**: design types with <200 bridges and materials with <500 bridges grouped into "Other" for statistical stability

---

## Results

Two models were compared:

| Model | Dataset | R² | RMSE |
|---|---|---|---|
| Model 1 | All bridges (<100 yrs) | 0.414 | 1.48 |
| Model 2 | Non-historic bridges (<100 yrs) | **0.456** | **1.30** |

### Key Coefficients (Model 2 — Non-historic)

| Predictor | Coefficient | Interpretation |
|---|---|---|
| Age | −0.077 | Each additional year reduces condition score by ~0.08 points |
| Material: Steel vs Concrete | −1.79 | Steel bridges score ~1.8 points lower |
| Material: Other vs Concrete | −2.72 | Non-standard materials score ~2.7 points lower |
| Design: Slab vs Beam | +0.075 | Marginal improvement |
| Traffic variables | ~0.001 | Negligible effect |

### Conclusions
- **Material** and **Age** are by far the strongest predictors of bridge condition
- **Concrete** bridges significantly outperform steel and other materials
- **Traffic volume and truck share** have minimal impact — deterioration is structural, not usage-driven
- The non-historic model explains **45.6% of variance** with predictions accurate to within ~1.3 condition points

### Policy Implication
> Maintenance funding should be prioritised for **ageing steel and non-concrete bridges**, where the risk of condition decline is greatest.

---

## Tech Stack

`Python` · `Pandas` · `NumPy` · `scikit-learn` · `Matplotlib`

---

## Run It

```bash
git clone https://github.com/YOUR_USERNAME/texas-bridge-condition.git
cd texas-bridge-condition
pip install -r requirements.txt
jupyter notebook Stats_Coursework_2.ipynb
```

**Data required:** `tx19_bridges_sample.csv` — not included in this repo.

---

## Project Structure

```
texas-bridge-condition/
├── Stats_Coursework_2.ipynb   # Full analysis notebook
├── tx19_bridges_sample.csv    # Dataset (not included)
├── requirements.txt
└── README.md
```
