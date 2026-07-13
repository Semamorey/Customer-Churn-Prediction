# Customer Churn Model Improvement Plan

## Objective

Improve the predictive performance (AUC) of the customer churn model
while maintaining compatibility with Google Colab and producing a
deployable model.

## Goals

-   Keep the current Google Colab data-loading workflow unchanged.
-   Reduce predictors to approximately 25--30 features.
-   Engineer three new churn-focused variables.
-   Compare multiple machine learning models.
-   Tune the prediction threshold.
-   Save a deployment-ready model.

------------------------------------------------------------------------

## Chunk 1 -- Data Preparation

Run after the existing data-loading code.

Tasks: - Import libraries. - Clean column names. - Use `CHURN` as the
target. - Split using `CALIBRAT`. - Engineer:

1.  **value_efficiency**
    -   log(MOU + 1) − log(REVENUE + 1)
2.  **service_failure_intensity**
    -   (DROPVCE + BLCKVCE + UNANSVCE) / (MOU + 1)
3.  **customer_stress_score**
    -   (CUSTCARE + OVERAGE + ROAM + CALLWAIT + 10 ×
        service_failure_intensity) / (MONTHS + 1)

------------------------------------------------------------------------

## Chunk 2 -- Feature Reduction

Recommended predictors:

-   REVENUE
-   MOU
-   RECCHRGE
-   DIRECTAS
-   OVERAGE
-   ROAM
-   CHANGEM
-   CHANGER
-   DROPVCE
-   BLCKVCE
-   UNANSVCE
-   CUSTCARE
-   CALLWAIT
-   OUTCALLS
-   INCALLS
-   PEAKVCE
-   MONTHS
-   PHONES
-   MODELS
-   EQPDAYS
-   SETPRC
-   RETCALLS
-   RETACCPT
-   RETCALL
-   CREDIT_RATING
-   value_efficiency
-   service_failure_intensity
-   customer_stress_score

------------------------------------------------------------------------

## Chunk 3 -- Preprocessing

Use:

-   Median imputation
-   Standard scaling
-   ColumnTransformer
-   Pipeline

Evaluate: - AUC - Accuracy - Precision - Recall - F1

------------------------------------------------------------------------

## Chunk 4 -- Model Comparison

Train:

-   Logistic Regression (L2)
-   Logistic Regression (L1)
-   Random Forest
-   Extra Trees
-   Histogram Gradient Boosting

Select the model with the highest validation AUC.

------------------------------------------------------------------------

## Chunk 5 -- Deployment

-   Tune thresholds from 0.20 to 0.70.

-   Select the best F1 threshold.

-   Display confusion matrix.

-   Export feature importance.

-   Save:

-   deployable_churn_model.joblib

-   model_comparison_results.csv

-   threshold_tuning_results.csv

-   best_model_feature_importance.csv

------------------------------------------------------------------------

## Expected Outcome

This workflow balances feature reduction with predictive performance,
emphasizes behavioral churn signals, compares multiple models, and
produces a reproducible deployment-ready pipeline suitable for academic
submission and GitHub.
