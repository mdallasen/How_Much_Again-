# **Airbnb LA Pricing**

## **Overview**  
Airbnb hosts continually face the challenge of accurately pricing their listings in line with property and location characteristics. Achieving a representative price remains a difficult task, yet doing so will prevent lost earnings from mispricing and improve the customer experience. To determine what an “appropriate” price is for an Airbnb listing, this report will aim to provide a price per night prediction based on several property, review, and market characteristics.

An LA Airbnb Pricing dataset was web scraped from the Airbnb website for property listings, providing ~44,000 property listings with over 70+ pricing, market, property, and review features. The target variable selected from this dataset was price per night, which ranged from 6 to 99999 with an average price of 317.20. Due to the nature of how the data was acquired, there were several issues that needed to be solved prior to model development. Namely, over 45% of property listings contained missing values with various imbalanced and skewed features. 

---

## **Dataset**  
- **Source**: [Inside Airbnb / Kaggle](https://www.kaggle.com/datasets/achal2703/airbnb-listings-in-la-california-inside-airbnb/data)  
- **Size**: ~44,000 listings with 70+ features.  
- **Target Variable**: `price` (nightly rate).  
- **Data Download Instructions**:  
  1. Download the dataset from the [link above](https://www.kaggle.com/datasets/achal2703/airbnb-listings-in-la-california-inside-airbnb/data).
  2. Place the `listings.csv` file in the `/src` folder.

---

## **Methodology**  

### 1. **Data Preprocessing**:  
- **Missing Values**:  
  - Imputed numerical values with BaysianRidge Iterative Imputer.  
  - Filled categorical missing values with a new category called "Missing"
- **Feature Scaling**:  
  - Applied standard and min max scaling to continuous features.  
  - One-hot encoded categorical features.  

### 2. **Data Splitting**:  
- **Train/Test Split**:  
  - Non IID dataset
  - Used **GroupShuffleSplit** and **GroupKfold** to ensure integrity of geographical groupings across splits.
  - Used KNN clustering to define geographical groupings  
  - Split ratio: 80% train, 20% test.  

### 3. **Modeling**:  
- **Algorithms Evaluated**:  
  - XGBoost, Random Forest, Ridge Regression, and Decision Trees.  
- **Hyperparameter Tuning**:  
  - Conducted grid search with cross-validation for optimal hyperparameters.  
- **Evaluation Metric**:  
  - Used **R² Score** for model evaluation.  

### 4. **Feature Importance**:  
- Analyzed feature contributions using:  
  - **Permutation Importance**: Quantifies the effect of shuffling a feature on model performance.  
  - **SHAP Values**: Provides detailed interpretability by explaining individual predictions.

---

## **Results**  

### Key Findings:  
1. **Best Model**:  
   - XGBoost achieved the highest R² score of **~0.75** on the test set.  
2. **Top Predictive Features**:  
   - Reviews (`number_of_reviews`, `review_scores_rating`).  
   - Amenities (e.g., `amenity_count`).  
   - Property types (`property_type`).  
   - Availability metrics (`availability_30`, `availability_365`).  

---

### Visuals:  
Generated figures are available in the `/figures` directory, including feature importance plots, model performance comparisons, and SHAP value visualizations.

## Dependencies

The following Python libraries are required to run this project:

- **Core Libraries**:
  - `pandas`: Data manipulation and analysis
  - `numpy`: Numerical computing
  - `matplotlib`: Visualization
  - `seaborn`: Statistical data visualization
  - `warnings`: Warning control

- **Scikit-learn**:
  - `Pipeline`, `ColumnTransformer`: Building machine learning pipelines
  - `SimpleImputer`, `IterativeImputer`: Handling missing values
  - `StandardScaler`, `MinMaxScaler`, `OneHotEncoder`, `MultiLabelBinarizer`: Data preprocessing
  - `train_test_split`, `GroupKFold`, `GroupShuffleSplit`, `GridSearchCV`: Data splitting and hyperparameter tuning
  - `shuffle`: Random shuffling
  - `KMeans`: Clustering
  - `r2_score`, `mean_squared_error`: Metrics for regression
  - `Ridge`, `RandomForestRegressor`, `DecisionTreeRegressor`: Machine learning models
  - `permutation_importance`: Feature importance analysis

- **XGBoost**:
  - `XGBRegressor`: Gradient boosting model

- **Geospatial Analysis**:
  - `folium`: Geospatial visualization

- **Model Interpretability**:
  - `shap`: Model explainability

### Installation

Install the dependencies using `pip`:

pip install pandas numpy matplotlib seaborn scikit-learn xgboost folium shap

---

## **Repository Structure**  
```plaintext
.
├── figures/               # Generated plots and visualizations
├── report/                # Final project report (PDF and LaTeX files)
├── src/                   # Source code and Jupyter notebooks
├── LICENSE                # License for the repository
└── README.md              # Project overview and instructions

