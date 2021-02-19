# Data Processing

I use the data profiling tool before and after processing to try and get rid of all the warnings. These were the warnings:


1) Overdue buckets have a high correlation, I made a simple composite to remove multicollinearity.
2) I imputed missing fields with means or medians based on skewing warnings.
3) I bumped the entire row if any field in that row had a value >3 standard deviations above or below the mean.
4) I applied the StandardScaler from sklearn to scale the features to unit variance. Note: I may try to improve the distribution of certain features using different scaling techniques but performance is reasonable now.


# Model Training

I selected these models to test:

Logistic Regression, KNN, Gradient Boosting Tree, Random Forrest, Decision Tree

It is an unbalanced dataset 3:1 negative:positive, I used SMOTE to balance 1:1 (could try other ratios as well)

I used recursive feature elimination to select features, most got selected except for decision trees which only found 2 features optimal.

I calculated the mean AUC using cross validation with 10 split kfolds.

Post-training I've generated a few metrics for evaluation: Confusion matrix, Classification Report, and AUC chart

Random Forrest had the most balanced performance across models with the highest F1 at 87% and the highest AUC at 94%. 

# Business Value

This model is perfect for deployment in a credit application system to either deny potential borrowers based on risk or at least escalate them to the next level of vetting. The calculations and data processing steps are simple enough to function at low latency and serialized model size is also reasonable.  