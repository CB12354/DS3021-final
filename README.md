# Predicting Shipping Disruptions
---
**DS 3021 | University of Virginia**

---

## Overview

NOTE: *This README is not the full response to the project requirements, it is a general description of our findings and a guide to navigating this repo. For the full writeup, go to project-writeup.ipynb.*

Can you predict whether a shipping disruption is likely to occur given features like distance, geopolitical risk, product type, and carrier reliability? This project aims to tackle that question using a dataset of shipments across the world, applying three classification approaches: k-Nearest Neighbors, Logistic Regression, and Decision Trees. These algorithms, together, helped build a practical disruption risk flagging model.

---

## Repository Structure

| Notebook | Description |
|---|---|
| `project-writeup.ipynb` | General process, best models, and overall conclusions |
| `KNN.ipynb` | Full k-Nearest Neighbors workflow |
| `LogRegression.ipynb` | Full Logistic Regression workflow |
| `decision-tree.ipynb` | Full Decision Tree workflow |
| `requirements.txt` | Full list of external libraries |
| `supply_chain.csv` | Full supply chain data used for all three algorithms and all models |

---

## Dataset

A record of shipments between various ports, including a diverse range of products (electronics, clothing, vehicles, and more). Features span both shipment context and global conditions:

- **Shipment features:** Origin/destination port, transport mode, product category, carrier reliability, lead time, distance, weight, date
- **Global features:** Fuel price index, geopolitical risk score, weather condition
- **Target:** `Disruption_Occurred` (binary: 0 = no disruption, 1 = disruption)

---

## Models & Results

| Model | AUC | Accuracy |
|---|---|---|
| Logistic Regression | 0.83 | 73% |
| Decision Tree (CCP-pruned) | 0.80 | 72% |
| k-Nearest Neighbors | 0.72 | 67% |

**Recommended model: Logistic Regression.** Its AUC of 0.83 was the strongest of the three approaches, and its interpretable coefficients and process make it actionable for logistics stakeholders. A manager can easily see which features are driving disruption risk and build policy around them, which was one of the primary reasons we recommend this algorithm.

---

## Key Findings

- **Geopolitical risk score** we believe is the most actionable feature for policy. It changes slowly enough to inform long-term structural decisions, unlike weather which is difficult to predict far enough in advance to act on.
- **KNN underperformed** due to a fundamental mismatch between Euclidean distance and mixed numeric/categorical data, compounded by weak univariate correlations across features, we found that kNN underperforms greatly.
- **High-dimensional OHE feature space** there is a signal for both KNN and logistic regression. Decision trees are naturally more robust to this since they evaluate one feature at a time.
- An AUC of 0.83 is a solid starting point but not strong enough to rely on the model blindly. More granular features like port congestion or carrier-level history would likely improve performance. 

---

## Practical Application

The model's probability scores can be used to flag high-risk shipments before departure. A logistics team could set a disruption probability threshold above which a shipment triggers human review, which would encourage decisions around backup carriers, adjusted timelines, or pre-positioned inventory.
