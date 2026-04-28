All the .csv files were ignored due to the data privacy

# Predicting Case Reoccurrence in Adult Protective Services 🛡️📊

**A Machine Learning and Survival Analysis Approach**

## 📖 Overview
Adult Protective Services (APS) agencies investigate allegations of abuse, severe neglect, and financial exploitation among vulnerable adults. A critical challenge in resource management is identifying individuals at high risk for case reoccurrence after an initial investigation closes. 

This project develops a predictive classification framework to identify APS cases likely to reoccur within a 6-month window. By prioritizing the recall of the minority class (returning clients) and weaponizing missing administrative data, this model allows agencies to preemptively allocate post-investigation resources and monitor high-risk environments.

## 🛠️ Data Strategy & Feature Engineering
The dataset originated from highly unstructured, real-world APS logs containing over 191,000 records. After defining an active cohort and rigorously stripping post-investigation features to prevent data leakage, the feature space was refined to 78,559 cases.

**Key Preprocessing Techniques:**
* **Survival Analysis Framework:** Restructured the static dataset chronologically, calculating observation windows (`stop_time`) from the date of case closure ($t_0$) to properly evaluate continuous risk without overlapping timelines.
* **Weaponizing Missingness (MNAR):** Rather than dropping incomplete records or imputing global averages, structural voids in demographic data (e.g., missing marital status) were preserved. Recognizing the "Crisis Triage" effect—where caseworkers abandon paperwork in hostile or acute medical emergencies—these gaps were engineered into a distinct `Unknown` class, allowing the algorithms to leverage missing data as a behavioral risk signal.
* **Vulnerability-Adjusted Imputation:** Missing continuous variables (like age) were imputed using grouped medians based on specific cognitive and physical impairment flags.

## 🚀 Modeling Pipeline
The project transitioned from a linear baseline to an advanced ensemble method, focusing heavily on maximizing Class 1 Recall over pure accuracy to minimize False Negatives.

1.  **Baseline Model (Logistic Regression):** Achieved an initial accuracy of 69.6% but struggled with the highly imbalanced, sparse categorical data matrix, capturing only 30% of actual reoccurrences (Recall: 0.30).
2.  **Novel Model (Extreme Gradient Boosting - XGBoost):** * Transitioned to XGBoost to bypass the Gini impurity bias found in standard Random Forests. 
    * Utilized sequential boosting and hyperparameter tuning (`scale_pos_weight`, `max_depth`) to penalize minority class errors.
    * **Result:** Maintained overall accuracy while surging Class 1 Recall to **0.63**, successfully identifying over 3,250 returning vulnerable adults—more than doubling the baseline's effectiveness.

## 🔍 Key Insights
* **The "Smoke Means Fire" Theory:** Feature importance (Gain) revealed that the initial hotline allegation of *Self-Neglect* is the dominant predictor of future case reoccurrence, mathematically outweighing demographic profiles. Even if an investigation is legally "Unsubstantiated" at the time of closure, the mere presence of an investigator evaluating a home for self-neglect indicates a fundamentally unstable environment highly likely to require future intervention.
* **Administrative Friction:** The duration an investigation remains open serves as a strong proxy for legal and environmental complexity, correlating with higher reoccurrence risk.

## 📂 Repository Structure
```text
├── data/                   # (Note: Raw APS data not uploaded due to privacy constraints)
├── notebooks/
│   ├── 01_IDA.ipynb
│   ├── 02_missingness.ipynb
│   ├── 03_missingness_pt2.ipynb
│   └── 04_preprocessing_modeling.ipynb
├── presentations/
│   └── Predicting Case Reoccurence in Adult Protective Services.pdf
├── requirements.txt        # Project dependencies
└── README.md




⚙️ How to Run
Clone the repository: git clone https://github.com/yourusername/aps-reoccurrence-prediction.git

Install dependencies: pip install -r requirements.txt

Navigate to the notebooks/ directory and run the Jupyter notebooks in chronological order.

👤 Author
Yernar Bakatay

Master of Science in Data Science | Michigan State University

LinkedIn Profile: https://www.linkedin.com/in/yernar-bakatay/  | GitHub: https://github.com/yernarbakatay