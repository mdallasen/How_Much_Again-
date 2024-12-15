# **Airbnb LA Pricing**

## **Overview**  
This project predicts nightly prices for Airbnb listings in Los Angeles using machine learning techniques. The analysis identifies key features influencing price predictions and provides actionable insights for hosts to optimize their pricing strategies.

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
  - Imputed numerical values with the median.  
  - Filled categorical missing values with the mode.  
- **Feature Scaling**:  
  - Applied standard scaling to continuous features.  
  - One-hot encoded categorical features for compatibility with machine learning models.  
- **Outlier Handling**:  
  - Excluded listings with extreme `price` values (e.g., >$1,000) for better model performance.

### 2. **Data Splitting**:  
- **Train/Test Split**:  
  - Used **GroupShuffleSplit** to ensure integrity of neighborhood-based groupings (`neighbourhood_cleansed`) across splits.  
  - Split ratio: 80% train, 20% test.  

### 3. **Modeling**:  
- **Algorithms Evaluated**:  
  - XGBoost, Random Forest, Ridge Regression, and Decision Trees.  
- **Hyperparameter Tuning**:  
  - Conducted grid search with cross-validation for optimal hyperparameters.  
- **Evaluation Metric**:  
  - Used **R² Score** and **Root Mean Squared Error (RMSE)** for model evaluation.  

### 4. **Feature Importance**:  
- Analyzed feature contributions using:  
  - **Permutation Importance**: Quantifies the effect of shuffling a feature on model performance.  
  - **SHAP Values**: Provides detailed interpretability by explaining individual predictions.

---

## **Results**  

### Key Findings:  
1. **Best Model**:  
   - XGBoost achieved the highest R² score of **0.85** on the test set.  
2. **Top Predictive Features**:  
   - Reviews (`number_of_reviews`, `review_scores_rating`).  
   - Amenities (e.g., `amenity_count`).  
   - Property types (`property_type`).  
   - Availability metrics (`availability_30`, `availability_365`).  

### Visuals:  
Generated figures are available in the `/figures` directory, including feature importance plots, model performance comparisons, and SHAP value visualizations.

---

## **Repository Structure**  
```plaintext
.
├── data/                  # Raw and preprocessed data
├── figures/               # Generated plots and visualizations
├── results/               # Model predictions and evaluation results
├── report/                # Final project report (PDF and LaTeX files)
├── src/                   # Source code and Jupyter notebooks
├── .gitignore             # Files and directories to ignore in version control
├── LICENSE                # License for the repository
└── README.md              # Project overview and instructions