# Customer Churn Analysis for Telecommunications Company

## Stage 2 – Data Preparation and Clustering Analysis

### Team 3 – ACS WIL Data Analytics Project

This repository contains the Stage 2 deliverables for the **Customer Churn Analysis for Telecommunications Company** project.

Stage 2 focuses on preparing the customer dataset for analysis and predictive modelling and performing K-Means clustering to identify distinct customer segments.

The work completed in this stage includes data cleaning, categorical encoding, training and testing dataset preparation, feature scaling, identification of the optimal number of clusters using the Elbow Method, K-Means model training, cluster visualisation, customer segment labelling, and interpretation of the resulting clusters.

---

## Team Members

| Team Member | Project Role |
|---|---|
| Sangam B K | Project Manager |
| Ravi Nagpal | Data Engineer – Preprocessing & Feature Engineering |
| Ishan Bhattarai | Deputy Project Manager & Data Analyst – Predictive Modelling |
| Rupshana Pandit Chhetri | Data Analyst – Clustering Analysis |
| Geeta Arora | Business Analyst |

---

## Stage 2 Objectives

The main objectives of Stage 2 are to:

- Prepare and preprocess the customer dataset.
- Check and address data quality issues.
- Encode categorical variables into numerical format.
- Split the prepared dataset into separate training and testing sets.
- Apply appropriate feature scaling techniques.
- Prepare a clustering-ready dataset.
- Identify an appropriate number of clusters using the Elbow Method.
- Train a K-Means clustering model.
- Visualise and label the resulting customer segments.
- Interpret the clusters and develop actionable customer insights.

---

## Repository Structure

```text
Customer_Churn_Stage2/
│
├── README.md
│
├── Data_Preparation/
│   ├── ATS_clean_v1.csv
│   ├── ATS_cluster_ready_v1.csv
│   ├── ATS_test_features_v1.csv
│   ├── ATS_test_target_v1.csv
│   ├── ATS_train_features_v1.csv
│   ├── ATS_train_target_v1.csv
│   ├── Ravi_Data_Preparation_ATS_1 (1).ipynb
│   ├── Team 3-Training and Testing Sets Documentation.pdf
│   └── Team 3- Scaling Techniques Documentation.pdf
│
└── Clustering_Analysis/
    ├── cluster_profile_summary.csv
    ├── cluster_visualisation_tenure_charges.png
    ├── clustering_results.csv
    ├── elbow_method.png
    ├── Rupshana_KMeans_Clustering_ATS.ipynb
    ├── silhouette_scores.png
    ├── Team 3-Clustering Analysis Documentation.pdf
    └── trained_kmeans_model.pkl
```

---

# 1. Data Preparation

The data preparation stage was completed to ensure that the customer dataset was suitable for subsequent analysis and predictive modelling.

The original dataset contained **7,043 customer records**.

During data quality checking and preprocessing:

- Missing values were checked.
- Duplicate records were identified.
- 302 duplicate records were removed.
- 11 records with zero tenure were retained.
- Categorical variables were encoded into numerical representations.
- The target variable `Churn` was encoded into numerical format.

After duplicate removal, the prepared dataset contained:

**6,741 customer records**

The cleaned and encoded dataset is provided as:

`Data_Preparation/ATS_clean_v1.csv`

---

# 2. Feature Encoding

Binary categorical variables were converted into numerical representations.

The binary variables included:

- `gender`
- `Dependents`
- `PhoneService`
- `MultipleLines`

The target variable `Churn` was also converted into numerical format.

The multi-category variables:

- `InternetService`
- `Contract`

were encoded using dummy variables.

Following encoding, the prepared data contained numerical features suitable for subsequent machine learning and clustering analysis.

---

# 3. Training and Testing Sets

For predictive modelling, the prepared dataset was divided into separate training and testing sets using an **80/20 stratified split**.

The resulting datasets contained:

| Dataset | Number of Records |
|---|---:|
| Training Set | 5,392 |
| Testing Set | 1,349 |
| **Total** | **6,741** |

There are **10 predictive input features**, with `Churn` maintained separately as the target variable.

A `random_state` value of **42** was used for reproducibility.

The split also used `stratify=y` to maintain a similar Churn distribution between the training and testing datasets.

The approximate churn proportions were:

- Training set: **26.6%**
- Testing set: **26.5%**

The exported training and testing files are:

- `ATS_train_features_v1.csv`
- `ATS_test_features_v1.csv`
- `ATS_train_target_v1.csv`
- `ATS_test_target_v1.csv`

Further details about the size and composition of the training and testing sets are available in:

`Team 3-Training and Testing Sets Documentation.pdf`

---

# 4. Feature Scaling

Feature scaling was performed using **StandardScaler** from Scikit-learn.

The continuous numerical features scaled were:

- `tenure`
- `MonthlyCharges`

For predictive modelling, StandardScaler was fitted only on the training dataset and then applied to the testing dataset. This approach helps prevent information from the testing data from influencing preprocessing of the training data.

A separate StandardScaler was used to prepare the complete feature dataset for K-Means clustering.

The resulting clustering-ready dataset contained:

- **6,741 customer records**
- **10 features**
- **0 missing values**

The clustering-ready dataset is provided as:

`Data_Preparation/ATS_cluster_ready_v1.csv`

Detailed information about the scaling process and relevant code is provided in:

`Team 3- Scaling Techniques Documentation.pdf`

---

# 5. Clustering Analysis

K-Means clustering was used to identify customer segments based on the prepared customer characteristics.

The clustering analysis used:

- **6,741 customer records**
- **10 input features**
- Standardised `tenure`
- Standardised `MonthlyCharges`
- Encoded categorical and binary features

The `Churn` variable was **not used as an input feature** for K-Means clustering.

Churn information was examined after clustering to assist with interpretation and profiling of the resulting customer segments.

---

# 6. Optimal Number of Clusters

The **Elbow Method** was used to identify an appropriate number of clusters.

K-Means models were evaluated for values of K from **1 to 10**, and inertia was calculated for each solution.

The Elbow Method showed a noticeable reduction in the rate of improvement at approximately:

**K = 4**

Therefore, **four clusters** were selected for the final K-Means clustering model.

Silhouette analysis was also performed as a secondary evaluation.

The highest silhouette score occurred at K=2, while K=4 produced a silhouette score of approximately **0.1998**.

K=4 was selected primarily based on the Elbow Method and the usefulness of obtaining a more detailed four-segment customer interpretation.

Supporting visualisations are provided as:

- `Clustering_Analysis/elbow_method.png`
- `Clustering_Analysis/silhouette_scores.png`

---

# 7. K-Means Model

The final K-Means model was trained using:

- **Number of clusters:** 4
- **Random state:** 42
- **n_init:** 10

The resulting cluster distribution was:

| Cluster | Number of Customers |
|---|---:|
| Cluster 0 | 1,586 |
| Cluster 1 | 1,882 |
| Cluster 2 | 1,123 |
| Cluster 3 | 2,150 |
| **Total** | **6,741** |

The trained K-Means model is provided as:

`Clustering_Analysis/trained_kmeans_model.pkl`

The complete clustering analysis code is available in:

`Clustering_Analysis/Rupshana_KMeans_Clustering_ATS.ipynb`

---

# 8. Customer Segment Labels

The four resulting customer segments were interpreted and labelled based on their characteristics and post-clustering analysis.

## Cluster 0 – Newer, Lower-Spend Customers

- Customers: **1,586**
- Average tenure: **11.24 months**
- Average monthly charges: **$33.80**
- Observed churn rate: **24.91%**

This segment represents relatively newer customers with lower monthly charges.

## Cluster 1 – Long-Term, High-Value Customers

- Customers: **1,882**
- Average tenure: **58.73 months**
- Average monthly charges: **$93.17**
- Observed churn rate: **15.62%**

This segment represents longer-term customers with relatively high monthly charges.

## Cluster 2 – Long-Term, Low-Risk Customers

- Customers: **1,123**
- Average tenure: **54.35 months**
- Average monthly charges: **$34.90**
- Observed churn rate: **4.81%**

This segment represents longer-term customers with lower monthly charges and has the lowest observed churn rate among the four clusters.

## Cluster 3 – Newer, High-Risk Customers

- Customers: **2,150**
- Average tenure: **15.21 months**
- Average monthly charges: **$81.72**
- Observed churn rate: **48.74%**

This segment represents relatively newer customers with higher monthly charges and has the highest observed churn rate among the four clusters.

> **Important:** `Churn` was not used to create the clusters. The observed churn rates were examined after clustering to assist with interpretation and labelling of the customer segments.

---

# 9. Cluster Visualisation

The resulting customer segments were visualised using:

- `tenure`
- `MonthlyCharges`

The visualisation is available as:

`Clustering_Analysis/cluster_visualisation_tenure_charges.png`

The two-dimensional visualisation provides an interpretable view of differences between the resulting customer segments.

The final K-Means model itself was trained using all **10 clustering features**, rather than only tenure and MonthlyCharges.

---

# 10. Business Insights

The clustering analysis provides several potential business insights.

### Cluster 0 – Newer, Lower-Spend Customers

Early engagement, onboarding support and relevant targeted offers may help encourage longer customer relationships.

### Cluster 1 – Long-Term, High-Value Customers

Loyalty initiatives, personalised service, retention benefits and relevant value-added offers may help maintain engagement with these longer-term, higher-spending customers.

### Cluster 2 – Long-Term, Low-Risk Customers

This group has the lowest observed churn rate. Maintaining customer satisfaction while considering appropriate cross-selling or service upgrade opportunities may be suitable for this segment.

### Cluster 3 – Newer, High-Risk Customers

This segment has the highest observed churn rate at **48.74%**. Potential retention activities include early customer check-ins, service reviews, targeted offers and further investigation into customer value perception.

These insights are descriptive interpretations of the customer segments and observed churn outcomes and do not establish causal relationships.

---

# 11. Technologies and Libraries

The Stage 2 analysis uses:

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Joblib
- Jupyter Notebook
- Visual Studio Code

Key techniques used include:

- Data preprocessing
- Categorical encoding
- Train-test splitting
- StandardScaler
- K-Means clustering
- Elbow Method
- Silhouette analysis

---

# 12. Stage 2 Deliverables

## Data Preparation Deliverables

The `Data_Preparation` folder contains:

- Preprocessed customer dataset
- Clustering-ready dataset
- Training feature dataset
- Testing feature dataset
- Training target dataset
- Testing target dataset
- Data preparation source code
- Training and testing sets documentation
- Scaling techniques documentation

## Clustering Analysis Deliverables

The `Clustering_Analysis` folder contains:

- Clustering analysis source code
- Elbow Method analysis and visualisation
- Silhouette analysis
- Trained K-Means model
- Customer-level clustering results
- Cluster profile summary
- Cluster visualisation
- Cluster labels and interpretations
- Clustering analysis documentation

---

# 13. Limitations

K-Means clustering uses distance-based calculations and generally performs best when customer groups form relatively compact clusters.

The clustering dataset contains a combination of standardised continuous features and encoded binary features, which should be considered when interpreting the resulting segments.

The two-dimensional cluster visualisation displays only `tenure` and `MonthlyCharges`, while the actual K-Means model was trained using all 10 input features.

The cluster labels and business recommendations are descriptive interpretations of the resulting customer groups and should not be considered evidence of causal relationships.

---

# 14. Conclusion

Stage 2 successfully prepared the telecommunications customer dataset for subsequent analysis and predictive modelling.

Following data cleaning and preprocessing, **6,741 customer records** were prepared. Separate training and testing datasets were generated, appropriate feature scaling was applied, and a clustering-ready dataset was produced.

K-Means clustering was then applied to identify distinct customer segments. Based on the Elbow Method, **four clusters** were selected and subsequently profiled, labelled and visualised.

The resulting customer segments provide a structured basis for understanding different customer groups and support the next stages of the project, including predictive churn modelling and development of customer retention recommendations.