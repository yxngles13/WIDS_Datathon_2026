# WIDS_Datathon_2026
# 🔥 Wildfire Risk Prediction (WiDS Datathon 2026)

This notebook demonstrates a survival analysis approach to predict the time until a wildfire event ('time_to_hit_hours') and the probability of an event occurring within specific time horizons.

## Project Overview

The goal is to analyze wildfire incident data, identify factors influencing their spread, and build a predictive model using survival analysis techniques. The project utilizes data from the WiDSWorldWide_GlobalDathon26 Kaggle competition.

## Dataset

The dataset consists of `train.csv` and `test.csv` files, containing various features related to wildfire events, including geographical, temporal, and physical characteristics. Key target variables are `time_to_hit_hours` (the time duration until an event) and `event` (a binary indicator for whether an event occurred or was censored).

## Exploratory Data Analysis (EDA)

The EDA phase involved:

*   **Distribution Analysis**: Histograms of `time_to_hit_hours` for both 'hit' (event=1) and 'censored' (event=0) observations to understand their distributions.
*   **Class Imbalance Check**: Verified the distribution of the `event` variable to identify potential imbalance (`event=0` (censored) vs `event=1` (hit)).
*   **Feature Correlation**: Generated a correlation matrix for numeric features to understand relationships between variables.
*   **Feature Selection**: Identified and selected a subset of relevant features (`features_to_keep`) to reduce redundancy and improve model performance.

## Model Training

### Survival Analysis with Random Survival Forest

*   **Motivation**: Traditional classification or regression models are not ideal for 'time-to-event' data due to censoring (where the event has not yet occurred by the end of observation). Survival analysis, specifically the Random Survival Forest (RSF), is used to handle censored data appropriately.
*   **Library**: The `scikit-survival` library was used for implementing the survival model.
*   **Model**: A `RandomSurvivalForest` model was initialized with specific parameters (`n_estimators=300`, `min_samples_leaf=20`, `max_features=0.5`, `max_depth=4`, `random_state=42`).
*   **Training**: The model was trained on the `X_train` features and `y_train` (structured as `Surv` objects from `event` and `time_to_hit_hours`).

## Model Evaluation

### Concordance Index (C-index)

*   **Metric**: The Concordance Index (C-index) is used to evaluate the ranking ability of the survival model, indicating how well the model predicts the order of event times. A higher C-index (closer to 1) indicates better performance.
*   **Training Data C-index**: The model achieved a C-index of `0.9466` on the training data.
*   **Cross-Validation**: A 5-fold stratified cross-validation was performed to get a more robust estimate of the model's performance. The mean C-index was `0.9342` with a standard deviation of `0.0163`, indicating good generalization capability.

## Prediction and Submission

*   **Survival Probabilities**: The trained `RandomSurvivalForest` model was used to predict survival functions for the `X_test` dataset.
*   **Horizon Probabilities**: From the survival functions, the probability of a 'hit' (event=1) occurring within specific time horizons (12, 24, 48, 72 hours) was calculated (1 - survival probability).
*   **Submission File**: These probabilities were compiled into a `submission.csv` file, formatted with `event_id` and corresponding probability columns (`prob_12h`, `prob_24h`, `prob_48h`, `prob_72h`).

## Visualizations of Predicted Probabilities

To understand the model's output, several visualizations were generated:

*   **Probability Distributions per Horizon**: Histograms showing the distribution of predicted 'hit' probabilities for each horizon (12h, 24h, 48h).
*   **Mean Predicted Probability per Horizon**: A line plot illustrating how the average predicted probability of a hit increases with longer time horizons, along with standard deviation to show variability.
*   **Heatmap: Probability per Fire per Horizon**: A heatmap visualizing the predicted probabilities for each fire (sorted by 48h risk) across the different horizons, providing a quick overview of high-risk incidents.
*   **Number of High-Risk Fires**: A bar chart showing the count of fires predicted to have a probability greater than 0.5 for each time horizon, highlighting the increasing number of critical events over time.

