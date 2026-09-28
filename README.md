# Runverve Wearable Fatigue Prediction
Wearable devices continuously generate signals related to physiological 
state, activity, sleep, and recovery.

The objective of this prototype is to investigate whether these signals 
can be combined into a supervised machine-learning pipeline to classify a 
user's fatigue state as:

- **Low**
- **Moderate**
- **High**

The prototype also proposes how the prediction model could become part of 
a personalized **Digital Twin** for continuous wellness monitoring.

---## 2. Dataset

A synthetic wearable dataset containing **1,500 observations** was 
generated for this prototype.

The input features are:

| Feature | Description |
|---|---|
| `age` | User age |
| `resting_hr_bpm` | Resting heart rate |
| `hrv_rmssd_ms` | HRV measured using RMSSD |
| `sleep_hours` | Sleep duration |
| `steps` | Daily step count |
| `activity_minutes` | Daily activity duration |
| `skin_temperature_c` | Skin temperature |
| `respiratory_rate_bpm` | Respiratory rate |
| `hydration_proxy` | Synthetic hydration-related proxy |
| `sleep_debt_hours` | Accumulated sleep debt |
| `previous_day_load` | Previous-day activity/load indicator |

Target:

```text
fatigue_level ∈ {Low, Moderate, High}

Machine Learning Pipeline:

Synthetic Wearable Data
          │
          ▼
 Missing-value analysis
          │
          ▼
 Median imputation
          │
          ▼

 Feature scaling
          │
          ▼
 Stratified train/test split
          │
          ▼
 Random Forest classifier
          │
          ▼
 Fatigue prediction
          │
          ├──────────────► Accuracy
          ├──────────────► Macro F1
          ├──────────────► Confusion Matrix
          └──────────────► Permutation Importance

The preprocessing and model are implemented together using a scikit-learn 
pipeline to avoid inconsistent transformations between training and 
inference.

Model

The prototype uses a Random Forest Classifier.

Configuration:

350 trees
Maximum depth: 9
Minimum samples per leaf: 4
Balanced class weighting
Fixed random seed for reproducibility

The train/test split is stratified to preserve the fatigue-class 
distribution.

On the held-out synthetic test set:

Metric	Result
Accuracy	0.777
Macro F1	0.781

Permutation importance is used to investigate which features most affect 
model predictions.

In this synthetic experiment, the strongest signals include sleep-related 
and workload-related variables.

Because the dataset is synthetic, these importance values should be 
interpreted as prototype-level model behaviour, not as evidence of 
physiological causality.

A future Runverve implementation could maintain a personalized digital 
representation of a user's physiological and recovery state.

Wearable Sensors
       │
       ▼
BLE / Mobile Data Ingestion
       │
       ▼
Feature Extraction
+ Sensor Quality Checks
       │
       ▼
Fatigue Model
+
Personal Baseline
       │
       ▼
Digital Twin State
       │
       ▼
Recovery / Training Recommendation

With real longitudinal wearable data, the prototype could be extended 
with:

Subject-aware train/test validation
Personalized baseline modelling
Temporal features
Time-series models such as LSTM/GRU
Gradient-boosted models such as XGBoost
Probability calibration
Sensor-quality and missing-data detection
Concept-drift monitoring
Personalized fatigue thresholds
Real-time inference
BLE/mobile data ingestion
Digital Twin state estimation
Prospective validation

A particularly important next step would be validating the model on real 
longitudinal data from multiple users, while preventing subject leakage 
between training and evaluation.

Reproducibility

Install dependencies:

pip install -r requirements.txt
Launch the notebook:

jupyter notebook Runverve_Fatigue_Prediction.ipynb
Then run the notebook from top to bottom.

The synthetic dataset is included as:

synthetic_wearable_fatigue.csv

Limitations

This is a technical ML prototype using synthetic data.

It does not establish:

clinical validity,
medical diagnostic capability,
physiological causality,
real-world wearable accuracy,
or performance on unseen real users.

Real deployment would require appropriately collected and consented 
wearable data, rigorous subject-independent validation, privacy controls, 
calibration, and prospective evaluation.
