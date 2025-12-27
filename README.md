
# House Price Prediction and Demand Analysis

## Introduction

This assignment examines different statistical and machine learning models and matrices to analyse and evaluate their application within the context of house price prediction. The study investigates how key variables such as **Income**, **Demand**, **Land Price**, **School Quality**, and others influence the target variable **Predicted House Price**.

In addition, the **House Demand Category** variable (High, Average, Low) is analysed through classification models to understand how demand differs from other explanatory features. Multiple models are applied and compared to evaluate their performance and prediction accuracy. The effectiveness of each model depends on the strength of relationships between the variables.

Data cleaning, preparation, and scaling are essential steps to ensure the reliability and accuracy of both statistical and machine learning models. **Principal Component Analysis (PCA)** and **Linear Discriminant Analysis (LDA)** are applied to reduce dimensionality, remove unnecessary information, and preserve the most relevant features.

The statistical analysis prepares the data for machine learning by:

* Removing outliers
* Visualising distributions
* Examining correlations
* Testing normality, means, and p-values

Finally, several machine learning models are trained and evaluated through regression and classification techniques using different train–test splits.

---

## Data Preparation

### Libraries and Initial Setup

The analysis begins by importing essential Python libraries:

* **Pandas** for data manipulation
* **NumPy** for numerical computations
* **Matplotlib** and **Seaborn** for data visualisation

Visualisation is a critical first step, offering a general overview of the dataset before applying any tests or models.

### Dataset Overview

* Approximately **2080 rows** and **13 columns**
* Mostly **numerical features**, with a small number of **categorical variables**

### Data Cleaning

Key steps included:

* Dropping missing values to prevent bias or distortion
* Renaming features for clarity (e.g., `avg_income_eur` → `Income`, `avg_land_price_eur_m2` → `Land Price`)
* Checking for duplicate rows (none were found)

### Outlier Detection

Boxplots were used to identify outliers and abnormal values. Outliers may arise from:

* Data entry errors
* Measurement issues
* Rare but extreme cases

Removing outliers significantly improved data reliability and model accuracy, as shown by noticeable differences in boxplots before and after removal.

### Distribution Analysis

Histograms combined with density plots revealed that variables such as:

* Land Price
* Transport
* School Quality
* Income

follow an approximately normal distribution. This is important because many statistical and machine learning methods assume normality. These plots helped identify skewness and determine whether transformations or scaling were needed.

### Correlation Analysis

A heatmap showed:

* **Positive correlations** between Predicted House Price and Income, Demand, Transport, and Land Price
* **Slight negative correlations** with School Quality, Crime Rates, Green Space, and Flood Risk

Scatter plots (e.g., Income vs. Demand, Land Price vs. Demand) provided further insight, though definitive conclusions required formal statistical testing.

### Encoding and Scaling

* Categorical variables (e.g., **County**, **House Type**) were encoded numerically
* Scaling was applied to handle differing ranges and units

  * **Min-Max Scaling** for values between 0 and 1
  * **Standard Scaling** to centre variables around zero with unit variance

---

## Dimensionality Reduction: PCA and LDA

### Principal Component Analysis (PCA)

* Applied to continuous variables for house price prediction
* Reduced features from **38 to 36** while retaining **99.5% variance**
* Improved computational efficiency, reduced redundancy, and removed noise

### Linear Discriminant Analysis (LDA)

* Applied to the categorical demand classification task
* Maximised separation between demand classes
* Achieved approximately **90% classification accuracy**

### Summary

* **PCA** improved stability and efficiency for regression tasks
* **LDA** enhanced class separability for classification
* Together, they improved model robustness and performance

---

## Statistical Techniques

### Normality Testing

* **Shapiro–Wilk Test** was applied to assess normality

  * Many selected variables did not follow a normal distribution
  * Selection based on high means and strong correlations likely biased results

* **Anderson–Darling Test**

  * More sensitive to tail deviations
  * Results varied across variables:

    * Income: 0.99
    * Demand: 0.66
    * Transport: 0.33
    * Flood Risk: 51.63

Q–Q plots visually illustrated deviations from normality.

---

## Confidence Intervals

The width of a 95% confidence interval depends on the standard error; higher uncertainty leads to wider intervals (Young & Lewis, 1997).

* **Income:** (-0.774, 0.466)
* **Land Price:** (-0.159, 1.081) – high uncertainty
* **Demand:** (0.384, 0.610) – moderately high and precise
* **Transport:** (0.410, 0.640)

---

## Chi-Square Test

Applied to categorical variables (**House Type** and **County**) using a contingency table.

* Chi-square statistic: **123.50**
* p-value: **0.395**

This high p-value suggests no significant difference between observed and expected distributions.

---

## ANOVA Test

* **House Type vs. Predicted House Price**

  * F-statistic: **490.493**
  * Significant differences across house types

* **County vs. Predicted House Price**

  * F-statistic: **3.990**
  * Very low p-value, indicating a significant county effect

---

## Pearson Correlation

* Income vs. Predicted House Price:

  * **r = 0.313**, **p < 0.001**
  * Moderately positive and statistically significant relationship

This suggests income influences house prices, but other factors also play important roles.

---

## Linear Regression Analysis

* **Land Price**

  * Coefficient ≈ 8,642
  * R² = 0.155

* **Income**

  * Coefficient ≈ 7,441
  * R² = 0.115

* **Demand**

  * Coefficient ≈ 37,738
  * R² = 0.098

Overall, these predictors explain a moderate to weak proportion of variance, indicating that additional factors influence house prices.

---

## Machine Learning Models

### Random Forest Regressor

* 10-fold cross-validation:

  * Mean R² = **0.99986**
  * Very low standard deviation (high stability)

* Hyperparameter tuning:

  * 300 trees
  * Max depth = 20
  * Square-root feature sampling

* Optimised model:

  * Cross-validated R² = **0.9653**
  * Test R² = **0.9619**

This model explains over **96%** of the variance in unseen data.

---

## Train–Test Split Analysis

### 10% Test Size

* R² ≈ 0.32–0.35
* MSE ≈ 0.03
* Weak predictive power, likely underfitting

### 20% Test Size

* R² ≈ 0.27–0.33
* MSE ≈ 0.02–0.03
* Stable but limited predictive ability

### 30% Test Size

* R² ≈ 0.30–0.35
* MSE ≈ 0.02
* Consistent but mildly underfitting

### Summary

Linear Regression performs consistently across all splits, providing a reliable baseline model. However, there remains room for improvement using more advanced techniques.

---

## References

* Shapiro, S.S. and Wilk, M.B. (1965). *An analysis of variance test for normality (complete samples)*. **Biometrika**, 52(3–4), 591–611.
* Anderson, T.W. and Darling, D.A. (1952). *Asymptotic theory of certain goodness-of-fit criteria based on stochastic processes*. **The Annals of Mathematical Statistics**, 193–212.
* Young, K.D. and Lewis, R.J. (1997). *What is confidence? Part 2: detailed definition and determination of confidence intervals*. **Annals of Emergency Medicine**, 30(3), 311–318.

