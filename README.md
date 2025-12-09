# **Austin Crash Risk Prediction — Advanced ML Project (UT MSBA)**

This repository contains the full implementation of our Advanced Machine Learning final project, focused on modeling the **probability and expected cost of traffic accidents across Austin, Texas**.  
Using spatiotemporal engineering, weather enrichment, LightGBM, Hurdle modeling, and XGBoost, we built a data pipeline and predictive system capable of identifying high-risk areas and times with strong interpretability and performance.

This project was completed as part of **MIS 382N — Advanced Machine Learning** in the MSBA program at The University of Texas at Austin.

---

## **Final Blog Report**

The final deliverable for this project was submitted as a blog-style report:

👉 **https://francosalinas.netlify.app/posts/2025-12-08-predicting-the-probability-and-cost-of-accidents-in-austin/**

This blog includes:  
- Full narrative explanation of methodology  
- Modeling insights  
- Visualizations  
- Discussion and policy implications  

---

## **Repository Structure**

data/raw/ – Contains the original Austin crash dataset (if file size permits uploading)
data/processed/ – Contains processed model-ready datasets stored via Git LFS

notebooks/preprocessing/ – Contains `01_preprocessing_data_pipeline.ipynb` for EDA, cleaning, feature engineering, H3 grid creation, and weather integration

notebooks/modeling/ – Contains:
    - `02_lightgbm_hurdle_modeling.ipynb` (Binary LightGBM + Hurdle model, SHAP, calibration, visualizations)
    - `03_xgboost_modeling.ipynb` (XGBoost modeling, evaluation, and visualization)

reports/ – Contains `final_report.md`, which links to the external blog-style final report

slides/ – Contains the project presentation deck `ADV_ML_Presentation.pdf`

README.md – Main project documentation

---

## **Project Motivation**

Austin’s rapid population growth and increasingly congested road network have created a pressing need for **data-driven accident risk forecasting**.

City data shows:

- An accident occurs every **57 seconds**
- Injury or fatal crashes place significant strain on emergency services
- Estimated **$35M+** annual taxpayer burden from motor-vehicle crashes

Identifying **when** and **where** crashes are most likely enables:  
- Smarter resource allocation  
- Infrastructure planning  
- Insurance and dynamic pricing applications  
- Safer route planning for rideshare and logistics  

---

## **Methodology Overview**

This project approaches crash prediction as a **spatiotemporal modeling problem**, integrating:

### **1️⃣ Data Engineering**
- Cleaning and standardizing Austin Open Data crash reports  
- Spatial binning using **H3 hexagonal indexes (resolution 8)**  
- Hourly temporal binning  
- Integrating **hourly weather data**  
- Lag features, weekend/holiday indicators, contextual variables  
- Generating **model-ready panels**  

### **2️⃣ Modeling Approach**
We model **crash probability** and **expected crash cost** using:

#### ✔ **Binary LightGBM**
Predicts whether a crash occurs in a given hex–time combination.

#### ✔ **Hurdle Model**
Two-stage approach:
- **Stage 1:** Probability of crash occurrence (binary LightGBM)  
- **Stage 2:** Expected cost conditional on a crash (regression)

#### ✔ **XGBoost (Tweedie / Regression)**
Used for comparison and capturing nonlinear patterns.

### **3️⃣ Evaluation**
- ROC-AUC, PR-AUC for occurrence modeling  
- Poisson deviance and RMSE for cost modeling  
- Calibration plots  
- SHAP feature importance  
- Out-of-time validation  

---

## **Key Features Engineered**

- **Spatial:** H3 hex cell, road type grouping  
- **Temporal:** hour-of-day, weekday, weekend, monthly seasonality  
- **Weather:** precipitation, temperature  
- **Lag features:** prior crash counts, recency indicators  
- **Context:** speed limits, location grouping  

Together, these form the basis of a **spatiotemporal risk surface** for Austin.

---

## **Notebooks Overview**

### **1. Preprocessing & Feature Engineering**  
\`01_preprocessing_data_pipeline.ipynb\`
- Raw crash dataset cleaning  
- H3 assignment  
- Time binning  
- Weather merge  
- Creation of processed datasets:
  - \`model_ready_hex1hr_leakfree.pkl.gz\`
  - \`accidents_weather.pkl.gz\`

### **2. LightGBM + Hurdle Modeling**  
\`02_lightgbm_hurdle_modeling.ipynb\`
- Binary LightGBM crash-occurrence model  
- Hurdle structure for cost modeling  
- SHAP analysis  
- Calibration and performance evaluation  

### **3. XGBoost Modeling**  
\`03_xgboost_modeling.ipynb\`
- Comparative modeling  
- Visualizations  
- Feature performance and classification behavior  

---

## **How to Run the Project**

### **1. Clone the repo**
\`\`\`bash
git clone https://github.com/francos1998/ADV-ML-MSBA.git
cd ADV-ML-MSBA
\`\`\`

### **2. Pull Git LFS data**
\`\`\`bash
git lfs install
git lfs pull
\`\`\`

### **3. Open notebooks**  
Use Jupyter, VSCode, or similar.

---

## **Presentation**

Slides summarizing the methodology and results:  
\`slides/ADV_ML_Presentation.pdf\`

---

## **Team**

UT Austin — MSBA, Advanced Machine Learning  
Fall 2024

- Franco Salinas  
- Shyam Patel  
- Ishrak Wasif Udoy  
- Sanchal Kalengada  
- Muzaffar Yezdan  

---

## **Summary**

This repository demonstrates a full end-to-end spatiotemporal ML pipeline:  
from raw crash logs to engineered risk surfaces and cost modeling.  
It showcases skills in:

- Data engineering  
- Feature design  
- Gradient boosting (LightGBM, XGBoost)  
- Model interpretability  
- Reproducible ML pipelines  

It serves both academic review and professional portfolio demonstration.

