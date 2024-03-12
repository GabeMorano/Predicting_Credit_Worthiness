## Overview of Analysis

### Purpose

The purpose of this analysis is to train and evaluate a machine learning model to correctly identify and categorize healthy and risky credit loans. The models were trained on historical financial data gathered from a CSV file containing 77,536 rows of user credit data. The data contained 7 columns of relevant credit history for each user and a final column called "loan_status" which represents the final decision for each case of whether or not to issue the loan.

### Variables

The 7 columns of credit history for each user represent our features for this analysis. They make up our X variable and are used to predict the "loan_status" for each case. The "loan_status" is our target variable, or our y.

### Balancing Data

Our data in this analysis is imbalanced, as is common in credit fraud cases, since healthy loans are much more common than risky loans. The first portion of this analysis is a linear regression model conducted without rebalancing the data. This result will act as a reference point for part two, when we rebalance the data by oversampling the number of risky loans in our data set to match the number of healthy loans and rerun our linear regression. We will then be able to see what impact oversampling the data had on our model's accuracy.

### Modeling

#### Imbalanced Model

To conduct our analysis of our original, imbalanced data, Our X and y variables are first seperated into sets of training data and testing data for our model. We then fit our X and y training data into a linear regression model and use that model to predict the value of our X test data. 

#### Balanced Model

Conducting our balanced analysis follows the same steps as above with one key difference; we utilize the RandomOverSampler module to artificially raise the number of risky loans issued to match the number of healthy loans. In this instance, the categorized are balanced at 56271 each. We then fit our linear regression model with the new resampled values for X and y and print the reports to measure and compare our models' accuracies.

### Results

#### Model 1, Imbalanced

Accuracy - 99%
Healthy Loan Precision(0) - 100%
Risky Loan Precision(1) - 86%
Healthy Loan Recall(0) - 100%
Risky Loan Recall(1) - 90%

Considering the nature of our data, these scores are quite good. Our original data contained 75036 healthy loans, and 2500 risky loans. Despite being so heavily imbalanced, our model's precision and recall for healthy loans was perfect at 100%. 86% precision in risky loans means our model was correct 86% of the time in identifying a risky loan, the remaining 14% were identified as risky but were in fact healthy (false positives). 90% recall on risky loans means that the model correctly identified 90% of risky loans as risky, the remaining 10% were not identified by the model (false negatives). 

#### Model 2, Balanced

Accuracy - 99%
Healthy Loan Precision(0) - 100%
Risky Loan Precision(1) - 84%
Healthy Loan Recall(0) - 99%
Risky Loan Recall(1) - 99%

The data was balanced in this section using RandomOverSampling to yield 56271 samples of both healthy and risky applicants. The main difference between this model and our original, imbalanced model, is our new score for Risky Loan Recall. This term represents the number of false negatives in our model which rose from 90% to 99% with balanced data. This improvement means the loaning agent only has to worry about 1% of loans issued being false negatives (unidentified risky loans issued to applicants). We did see a small decrease in the number of false positives identified by our balanced model, with the risky loan precision falling from 86% to 84%. This means that the loaning agent will incorrectly identify an extra 2% of healthy credit applicants as risky.

### Summary

It is difficult to say which is preferrable in this scenario, false positives means the loaning agent misses the opportunity for quality business, but false negatives means the loaning agent issues loans to unidentified risky applicants. However, since our balanced linear regression model erradicated all but 1% of false negatives while only losing 2% of false positives, it is safe to say balancing our data had a meaningful impact on the model's ability to predict healthy or risky loans and if we were to deploy one of these two models into regular use, the balanced model would be the better choice.
