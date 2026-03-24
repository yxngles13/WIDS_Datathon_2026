# WIDS_Datathon_2026
🔥 Wildfire Risk Prediction (WiDS Datathon 2026)

📌 Overview

Emergency responders must make high-stakes decisions with limited early data when a wildfire ignites.

This project builds a survival analysis model to predict the probability that a wildfire will threaten an evacuation zone within:

⏱️ 12, 24, 48, and 72 hours
using only the first 5 hours after ignition

🎯 Objectives
Rank wildfires by urgency (which fires need attention first)
Generate calibrated probability estimates for decision-making
Support evacuation planning and resource allocation
🧠 Problem Formulation

We model wildfire spread as a right-censored survival problem:

event = 1 → fire reaches within 5 km of evacuation zone
event = 0 → no impact within 72h (censored)
Target → time_to_hit_hours

We predict:

𝑃
(
𝑇
≤
𝑡
)
,
𝑡
∈
{
12
,
24
,
48
,
72
}
P(T≤t),t∈{12,24,48,72}
⚙️ Approach
🔹 Data Processing
Used only first 5-hour window features
Handled missing values + normalization
Engineered time + spatial features
🔹 Feature Engineering
Fire growth rate
Distance to evacuation zones
Temporal progression signals
🔹 Modeling
Survival models (Cox, tree-based methods)
Gradient boosting for time-to-event prediction
Probability calibration (isotonic / Platt scaling)
🔹 Evaluation
Ranking performance (prioritization)
Calibration quality (probability reliability)
📊 Results (WIP)
✅ Generated multi-horizon probability predictions
✅ Identified high-risk fires early
🚧 Final model tuning and evaluation in progress
🏗️ Tech Stack
Python
Pandas, NumPy, Scikit-learn
Survival Analysis / Gradient Boosting
Matplotlib, Seaborn
📂 Project Structure
├── data/                # Processed datasets
├── notebooks/           # EDA + experiments
├── src/
│   ├── preprocessing/
│   ├── features/
│   ├── models/
│   └── evaluation/
├── results/
├── requirements.txt
└── README.md
🚀 Getting Started
1. Clone repo
git clone https://github.com/your-username/your-repo.git
cd your-repo
2. Install dependencies
pip install -r requirements.txt
3. Run notebooks
jupyter notebook
💡 Why This Project Matters
Applies ML to real-world disaster response
Focuses on decision-making under uncertainty
Balances prediction accuracy + interpretability
🔮 Future Work
Integrate weather + satellite data
Apply GNNs for spatial modeling
Deploy real-time prediction system
🤝 Acknowledgments

WiDS Global Datathon 2026
