---
layout: single
title: "Techniques to handle imbalanced dataset"
description: "Class imbalance "
category: banking
tags: [r, banking]
comments: false
header:
  image: assets/images/banner/ihh330-half.jpg
  caption: "Data science ©ihh300"
toc: true
toc_sticky: true
---

## Data science to prevent financial fraud

### The role of the data scientist in financial fraud prevention
In financial fraud prevention, here credit card fraud, the aim of the data scientist is to develop a scalable classification model so the company can accurately classify transactions as either legitimate or fraudulent. To do so, the data scientist uses a pre-labelled dataset, comprising fraudulent and legitimate transactions, so to train, validate and test its models.

### Dealing with imbalanced financial fraud data
Fraudulent transactions are the target class to be detected by the model but it is also the minority class, far outnumbered by the legitimate transactions class. An in depth exploratory data analysis, of the dataset used for this project, is provided in a previous article showing the imbalance and other variables characteristics. The target class (frauds) accounts for 0.172% of all transactions

## Classification on imbalanced data

### Challenges of assessing classifier performance
The following usual metrics or visualizations are proven not to be significant for performance assessment of classification models on imbalanced dataset:

> Accuracy = (TP+TN) / (TP+FN+FP+TP)

- **Accuracy**. As the model goal is to achieve a high rate of correct detection in the minority class, allowing a small error rate in the majority class, Accuracy is not appropriate in the case of fraud detection. **Kappa**. Kappa or Cohen’s Kappa is a normalized measure of Accuracy.

>  ROC curve is a 2d plot:
- the X-axis represents FPR = FP/(TN + FP) = 1 - Specificity where Specificity = TN / (TN + FP))
- the Y-axis represents TPR = TP/(TP + FN) aka Recall

- **ROC curve**. ROC (Receiver Operating Characteristics) curve displays the TPR (True Positive Rate also called Recall) against the FPR (False Positive Rate) through various probability thresholds. The ROC curve gives insights on the model ability to distinguish between the classes so it is most suitable when, as data scientist, we want to design a model that predicts equally both positive and negative classes.


### Metrics - Precision

> Precision = TP/(TP+FP)

Precision measures the probability of a sample classified as positive to actually be positive. In financial fraud, the fraud is classified as the positive class and the model is designed so to detect correctly positive samples, therefore Precision is one of the suitable metrics.

### Metrics - Recall

> Recall = TPR = TP/(TP+FN)

TPR (True Positive Rate also called Recall or Sensitivity) measures the actual positive observations which are predicted correctly.  

### Metrics - F1 score

> F1 = 2 * (precision * recall) / (precision + recall)

F1 score is a compounded metrics (from Precision and Recall) measuring the effectiveness of classification. The  F1-measure, the harmonic mean of precision and recall and so is a good indicator of the performance of our model as a higher F1 will help us choosing between two models.

### Metrics - AUROC
Area Under the Receiver-Operating Characteristic (AUROC) is equal to the probability that a classifier will rank a randomly chosen positive instance higher than a randomly chosen negative one (assuming 'positive' ranks higher than 'negative').

### Metrics - AUPRC
The Area Under the Precision-Recall Curve (AUPRC) is computed by plotting the Precision against Recall and measuring the area under this curve.

### Metrics - Matthews correlation coefficients

 > MCC =  (TP x TN - FP x FN) / sqrt( (TP + FP) x (TP + FN) x (TN + FP) x (TN + FN))

The MCC metric has been first introduced by B.W. Matthews to assess the performance of protein secondary structure prediction. Matthews Correlation Coefficient (MCC) is defined in terms of True Positive (TP), True Negative (TN), False Positive (FP) and False Negative (FN).

### Visualization - Confusion matrix
The confusion matrix is described in the table below:

|   |   |  Actual|  class |
|:-------:|:-------:|:-------:|:-------:|
|   |   | Actual Positive  |  Actual Negative |
| **Predicted**  |Predicted Positive   |True Positive   |  False Positive (Type I error) |
| **class**  |Predicted Negative   |  False Negative (Type II error) |  True Negative |

The interpretation of the confusion matrix is done as follow for a binary classification problem. Reviewing the models results to effectively predict if one transaction was positive (fraud) or negative (legitimate), the confusion matrix summarizes the results:
- True Positive (TP) – When a transaction is fraudulent and is classified correctly as fraudulent.
- False Positive (FP) – When a transaction is legitimate and was predicted and classified incorrectly as fraudulent.
- True Negative (TN) – When a transaction is legitimate and is classified correctly as legitimate.
- False Negative (FN) – When a transaction is fraudulent but was classified incorrectly as legitimate.

### Visualization - Precision-Recall curve

> Precision-Recall curve is a 2d plot:
- the X-axis represents Recall = TPR = TP/(TP + FN)
- the Y-axis represents the Precision = TP / (TP + FP)

The Precision-Recall Curve (AUPRC) displays the relationship between
* the true positive rate (TPR) = Recall = Sensitivity
* and the Precision = TP / (TP + FP)

## Data preparation approaches to deal with imbalanced data

### Oversampling
Oversampling randomly replicates a number of observations from the minority class so to match the user-defined number of observations in the majority class. This replication may lead to overfitting from the duplicated minority class data then presents in the resulting training dataset.

### Under sampling
Under sampling reduces the number of observations in the majority class (non-fraudulent transactions) to match the number of observations in the minority class (fraudulent transactions). Under sampling is done by randomly selecting observations from the predominant class so to matches the n observations of the minority class initially present in the dataset. Under sampling means information loss as only a portion of the data are kept to match the minority class so this technique may lead to classification models underperformance.

### Both sampling
In this two-ways sampling method, the majority class is under sampled while the minority class is oversampled, at the same time, so to obtain a user defined even number of observations from each class.

### Synthetic data generation - ROSE
[ROSE][1] (Random Over-Sampling Examples) aids the task of binary classification in the presence of rare classes. It produces a synthetic, possibly balanced, sample of data simulated according to a
smoothed-bootstrap approach.

### Synthetic data generation - SMOTE
[SMOTE][2] over-samples the minority fraudulent class by generating synthetic fraudulent data in the neighborhood of observed ones, interpolating to create those synthetic data between real observation of the same minority class. SMOTE first finds the k-nearest-neighbors for minority class observations and then randomly choose one of the k-nearest-neighbors to create this synthetic data belonging to the minority Class. One of the downsize of SMOTE is noise generation from interpolation between outliers and inliers.

### Cost Sensitive Learning (CSL)

> Total Cost = C(FN)xFN + C(FP)xFP
> where C(FN) and C(FP) are the costs associated with False Negative and False Positive respectively (C(FN) > C(FP))

This approach is a cost-based approach where the model parameters are set-up such as misclassification of the minority class is weighted differently so a high misclassification cost is attributed when predicting False Positives or False Negatives instead of, usually, weighting them equally.

## Modeling - Supervised learning - Decision tree

### Using a decision tree classifier
Our model uses a Decision Tree classifier in order to predict fraudulent transactions. The module used is [r, Rpart][3].Decision tree builds classification or regression models in the form of a tree structure. It breaks down a data set into smaller and smaller subsets while at the same time an associated decision tree is incrementally developed. The final result is a tree with decision nodes and leaf nodes.

### Modeling with the decision tree classifier
To build and develop this model, I have followed the steps:
1. Train/Test split with a 70/30 ratio
2. Separate scaling (to avoid leaking information of each subsequent dataset)
3. Hold out of the test dataset
4. Creation of 5 different datasets from the training dataset: training, training under sampled, training oversampled, training both sampled, training post-ROSE, training post ROSE.
5. Application of the decision tree classifier on each 6 datasets (original + the 5 created by the resampling)
6. Prediction of the class on the test dataset

## Performance of the decision tree classifier on imbalance data
Using *Rpart*, a decision tree model is built whose Visualization is provided below.
![Visualization of the decision tree model on an imbalanced dataset](/assets/images/credit_card/imbalance/imb_ccf_orig_tree.jpeg)

### ROC curve and AUC
When it comes to model evaluation, a decision tree on the imbalance dataset, gives poor performance in term of fraud detection with an AUC of 0.89 - The ROC curve is not recommended to assess model performance on imbalanced dataset and is just given as reference.
![Visualization of ROC curve - Decision tree model on an imbalanced dataset](/assets/images/credit_card/imbalance/imb_ccf_orig_curve_roc.jpeg)

### Confusion matrix

The following confusion matrix provided shows a high number of false negative ie fraud which were not detected.
- as 4 fold plot
![Visualization of the confusion matrix - imbalanced dataset - 4fold](/assets/images/credit_card/imbalance/imb_ccf_orig_cm.jpeg)
- and also with its metrics summary
![Visualization of the confusion matrix - imbalanced dataset - summary](/assets/images/credit_card/imbalance/imb_ccf_orig_cm2.jpeg)

### F1 score
F1 Score, the weighted average of Precision and Recall, is 0.82 and this baseline value will be compared to other classifier in our next models comparison article as the aim of this project is to pick a model that has the best F1 score on the fraudulent class.

### Precision - Recall curve
The Precision - Recall curve shows precision values for corresponding sensitivity (recall) values and its AUPRC is 0.68 which gives a baseline for the performance of classification models.
![Visualization of Precision_recall curve - Decision tree model on an imbalanced dataset](/assets/images/credit_card/imbalance/imb_ccf_orig_curve_pr.jpeg)

### Matthews correlation coefficient
The Matthews correlation coefficient is fairly robust to data imbalance and therefore is an interesting baseline metrics here, at 0.82.

## Performance of the decision tree classifier on balanced data

### Dataset class ratio
Five training datasets were created so to be compared once the same classifier was applied. The 5 datasets were balanced.
![Training datasets generated - Balanced Class ](/assets/images/credit_card/imbalance/imb_ccf_compa_balance.jpg)

### Overview of metrics comparison
The metrics were then compared as per figure below.
![Metrics comparison ](/assets/images/credit_card/imbalance/imb_ccf_compa_metrics.png)

This plot helps understand how the different sampling techniques impact the model performance. Here, comparison with under sampled dataset model shows lower performance in term of F1.

![Metrics visualisation ](/assets/images/credit_card/imbalance/imb_ccf_compa_plot.jpg)

### AUC comparison
As AUC is higher with all 5 models than the original one, it will be safe to do a dual comparison between different classification models other than decision trees and to use as input the original and both sampled datasets to have a safe final approach.
![ROC curve ](/assets/images/credit_card/imbalance/imb_ccf_compa_ROC_curve.jpeg)

![AUC comparison ](/assets/images/credit_card/imbalance/imb_ccf_compa_AUC_plot.jpeg)

### Matthews correlation coefficient comparison
For each model, the Matthews correlation coefficient were computed and compared. With a lower performance with the original dataset tough.

![Matthews correlation coefficient ](/assets/images/credit_card/imbalance/imb_ccf_compa_MCC_Coeff.jpeg)

## Conclusion
Regarding re-sampling the training dataset, a subsequent article will focus on how to improve those results using other classifiers than decision tree and how to build different models and by ensembling those algorithms to create a scalable final model.

[1]:https://cran.r-project.org/web/packages/ROSE/index.html "CRAN | ROSE: Random Over-Sampling Examples"
[2]:https://cran.r-project.org/web/packages/DMwR/DMwR.pdf "CRAN | DwR: Data Mining with R' incl. SMOTE"
[3]:https://cran.r-project.org/web/packages/rpart/index.html "CRAN | rpart: Recursive Partitioning and Regression Trees"
