# Intelligent Smoke Detection System with AI Sensor Fusion

This repository presents the exploratory and advanced analytical work conducted for the development of an **AI-driven smoke detection system** using sensor fusion techniques. The goal is to build a reliable model capable of accurately identifying fire occurrences from environmental sensor data while minimizing false alarms.

The project combines data analytics, machine learning, and IoT technology to support intelligent fire detection in diverse indoor and outdoor environments.

---

## Project Overview

The Intelligent Smoke Detection System integrates multiple environmental sensors connected through an Arduino Pro Nicla Sense ME board and Sensirion SPS30 smoke sensor. These devices collect air quality, gas concentration, and particulate data to detect the presence of smoke or fire.  

The dataset used in this study contains approximately **60,000 sensor readings**, representing a range of conditions including indoor and outdoor environments, training fires, and background noise scenarios.

The analysis focuses on:
- Understanding sensor behavior and environmental patterns.
- Identifying correlations between features and fire occurrences.
- Developing and evaluating predictive models for accurate smoke detection.

---

## Objectives

- Perform exploratory data analysis (EDA) to understand sensor data distributions and relationships.
- Identify key features associated with fire detection.
- Apply dimensionality reduction (PCA) and clustering to uncover hidden patterns.
- Build and compare classification models including Logistic Regression, Regularization methods, and Random Forest.
- Select and interpret the best-performing model for deployment.

---

## Dataset Description

The dataset consists of time-series sensor readings with the following variables:

| Variable | Description |
|-----------|--------------|
| `Temperature` | Ambient air temperature (°C) |
| `Humidity` | Relative humidity (%) |
| `TVOC` | Total volatile organic compounds (ppb) |
| `eCO2` | Equivalent carbon dioxide concentration (ppm) |
| `Raw H2` | Raw molecular hydrogen |
| `Raw Ethanol` | Raw ethanol concentration |
| `Pressure` | Atmospheric pressure (hPa) |
| `PM1.0`, `PM2.5` | Particulate matter concentration (µm) |
| `CNT` | Sample counter |
| `UTC` | Timestamp (seconds) |
| `Fire Alarm` | Target variable (1 = Fire detected, 0 = No fire) |

---

## Exploratory Data Analysis (EDA)

### Descriptive Analysis
- Visualized distributions of environmental variables (humidity, pressure, hydrogen, ethanol).
- Observed that humidity, pressure, and hydrogen levels increase during fire presence.
- Identified correlations between air quality metrics (TVOC, eCO2, particulate matter) and fire alarms.

### Correlation Analysis
- Humidity showed the highest correlation (≈ 0.4) with the Fire Alarm variable.
- PM, eCO2, and gas readings displayed varying positive relationships with fire occurrences.

### PCA (Principal Component Analysis)
- PCA was performed to reduce dimensionality and address multicollinearity.
- The first **4 principal components** explained approximately **87%** of total variance.
- Variables such as `eCO2` and `TVOC` demonstrated similar patterns due to shared environmental influences.

### Cluster Analysis
- K-Means clustering identified **two distinct clusters**:
  - Cluster 0: Observations with no fire.
  - Cluster 1: Observations with fire presence.
- Scaling was applied before clustering to ensure comparability of variables.

---

## Advanced Analysis

### Logistic Regression
- A baseline logistic regression model achieved an accuracy of **0.89**.
- Some predictors were statistically insignificant and removed for refinement.
- While interpretable, the model’s performance was limited due to potential non-linear relationships.

### Regularization Techniques
- Applied **Ridge**, **Lasso**, and **Elastic Net** logistic regression.
- Each achieved approximately **0.88 accuracy**, reducing overfitting and managing correlated predictors.
- Ridge regression proved most stable among the linear models.

### Random Forest Classification
- Implemented a Random Forest classifier using all 12 predictors.
- Achieved **perfect classification (accuracy ≈ 1.00)** on the test data.
- Feature importance ranking identified:
  - **TVOC**, **Pressure**, **Raw Ethanol**, and **Humidity** as the most influential variables.
- A simplified model using only these four features maintained an accuracy of **0.9998**, enhancing interpretability without loss of performance.

### Model Interpretation
- **SHAP (SHapley Additive Explanations)** was used to interpret feature contributions.
- Low pressure and high humidity were strong indicators of fire presence.
- SHAP summary and waterfall plots provided interpretability at both global and instance levels.

---

## Model Comparison Summary

| Model | Accuracy | Key Characteristics |
|--------|-----------|--------------------|
| Logistic Regression | 0.89 | Simple, interpretable baseline |
| Ridge Regression | 0.88 | Manages correlated variables |
| Lasso Regression | 0.88 | Performs variable selection |
| Elastic Net | 0.88 | Combines Ridge and Lasso benefits |
| **Random Forest** | **0.9998** | Best performing, robust, interpretable |

---

## Key Insights

- Humidity, pressure, and VOC gases play critical roles in fire detection.  
- Random Forest significantly outperformed other models, providing both high accuracy and interpretability.  
- PCA and clustering revealed structure in the data useful for future model segmentation.  
- The proposed model can be integrated into IoT-based detection systems to enhance reliability and minimize false alarms.

---

## Tools and Technologies

- **Languages:** Python, R  
- **Libraries:**  
  - Python: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `shap`  
  - R: `factoextra`, `cluster`, `caret`  
- **Techniques:**  
  - Data Cleaning and Visualization  
  - PCA and K-Means Clustering  
  - Logistic Regression and Regularization  
  - Ensemble Learning (Random Forest)  
  - Model Interpretation (SHAP)

