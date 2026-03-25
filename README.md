# WIDS_Datathon_2026
# 🔥 Wildfire Risk Prediction (WiDS Datathon 2026)

## 📌 Overview
When a wildfire ignites, emergency responders must make critical decisions with limited early information:
- Which fires will reach populated areas?
- How quickly will they spread?
- Which communities should prepare first?

This project develops a **survival analysis model** to predict the probability that a wildfire will threaten an evacuation zone within:

⏱️ **12, 24, 48, and 72 hours**  
using only the **first 5 hours after ignition**

---

## 🎯 Objectives
- Rank wildfires by **urgency**
- Generate **calibrated probability estimates**
- Support **evacuation planning and resource allocation**

---

## 🧠 Problem Formulation

We model wildfire spread as a **right-censored survival problem**:

- `event = 1` → fire reaches within 5 km of an evacuation zone  
- `event = 0` → fire does not reach within 72 hours (censored)  
- Target → `time_to_hit_hours`

We estimate:

P(T ≤ t),  where t ∈ {12, 24, 48, 72}

---

## ⚙️ Approach

### 🔹 Data Processing
- Used features from the **first 5-hour observation window**
- Handled missing values and normalized inputs
- Engineered temporal and spatial features

### 🔹 Feature Engineering
- Fire perimeter growth rate  
- Distance to nearest evacuation zone  
- Early spread dynamics  

### 🔹 Modeling
- Survival analysis models (Cox, tree-based methods)
- Gradient boosting for time-to-event prediction
- Probability calibration (isotonic regression, Platt scaling)

### 🔹 Evaluation
- **Ranking performance** → prioritization of high-risk fires  
- **Calibration quality** → reliability of predicted probabilities  

---

## 📊 Results (Work in Progress)
- Generated multi-horizon probability predictions  
- Identified high-risk fires early using limited data  
- Ongoing model tuning and evaluation  

---

## 🏗️ Tech Stack
- Python  
- Pandas, NumPy, Scikit-learn  
- Survival Analysis / Gradient Boosting  
- Matplotlib, Seaborn  

---

## 📂 Project Structure
├── data/ # Processed datasets
├── notebooks/ # EDA and experiments
├── src/
│ ├── preprocessing/
│ ├── features/
│ ├── models/
│ └── evaluation/
├── results/
├── requirements.txt
└── README.md
## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
pip install -r requirements.txt
jupyter notebook
