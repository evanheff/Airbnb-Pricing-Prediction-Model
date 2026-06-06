**Airbnb Pricing Prediction Model**
A machine learning pipeline in R that predicts Airbnb listing prices in the Minneapolis–St. Paul market from listing-level features. The project compares six regression approaches under a unified cross-validation framework and produces a final set of price predictions for a held-out test set.

**Overview**

The goal is to predict nightly listing price from 16 predictors. Because the price distribution is heavily right-skewed, all models are fit on log(price) and back-transformed to the original scale for final predictions. Models are evaluated with 10-fold cross-validation, and the best performer is used to generate the submission file.

**Key findings from exploratory analysis**

No missing values in either dataset.
price is heavily right-skewed (skewness ≈ 9; max ≈ $5,556), motivating a log transformation of the target.
Multicollinearity among bathrooms, bedrooms, and accommodates.
A pronounced spike in minimum_nights at 30 days.
Several variables listed in the data dictionary (e.g., property_type, beds) are not present in the provided data.

**Feature Engineering**

Log-transform of host_total_listings_count to reduce skew.
minimum_nights capped at 30 to handle the long-stay spike.
A size interaction term combining capacity-related predictors.
Model-matrix construction with dummy encoding aligned between train and test so factor levels match.

**Models**

All six models are fit on log(price) and evaluated with 10-fold CV (via caret / glmnet):

OLS — baseline linear regression.
Regularized regression — Lasso, Ridge, and Elastic Net.
Regression tree — single CART tree.
Bagging — bootstrap-aggregated trees.
Random forest — decorrelated tree ensemble.
Gradient boosting — sequential boosted trees.

A model-comparison table reports cross-validated error for each, and predicted-vs-actual diagnostics are produced for the selected model.

**Results**

Cross-validated RMSE (back-transformed to the price scale)

**OLS:** 0.4432

**Ridge:** 0.4435

**LASSO:** 0.4425

**Elastic Net:** 0.4415

**Single Tree:** 0.4264

**Random Forest:** 0.3787

Fill in the final CV RMSE values from the model-comparison table once you've run the notebook.

Running the notebook reproduces the EDA, fits all six models, prints the comparison table, and writes submission.csv.
Tech Stack
R · R Markdown · caret · glmnet · tidyverse

**Context**

Built as a statistical learning course project (STAT1361) at the University of Pittsburgh.

**Author**

Evan Heffelfinger
