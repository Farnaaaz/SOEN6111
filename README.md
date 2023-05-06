## Project Definition

 The goal of the project is to get insight into correlation between fearfulness and various other physical and emotional characteristics.

## The Research Questions
First, the existence and nature of a significant correlation between fearfulness to physical strengths will be examined:

Question 1- Is there any correlation between physical strength and fearfulness? 

Question 2- Is the relationship between physical strength and fearfulness predictable?

Question 3- What are the important features in the prediction of fearfulness?

The outcome will set the basis for prediction:

Question 4- Can we predict a fearfulness score of a participant based on other features in the dataset? 

As a stretch goal, the following question will be posed:

Question 5- Is regression or classification more effective in the prediction of fearfulness?

## Dataset and Its Main Characteristics
Our dataset presents insight into gender differences in fear-related personality traits and their correlation with physical strength across five university samples. It contains 46 columns, including demographic information such as age (continuous), gender(binary), and ethnicity (categorical), as well as physical strength measures (continuous) – grip strength and chest strength, and 41 self-reported measures of HEXACO Emotionality (categorical ordinal). Taken from undergraduate students from multiple universities in the United States, this dataset explores the effects of physical strength on fear-related personality.
In order to clean the data, missing value interpolation will be applied. The self-reported measures of HEXACO Emotionality from each category (fearfulness, anxiety, depression, sentimentality) will be aggregated to obtain 5 emotional strength features, 2 physical strength features, and 2 features associated with the participant’s personal characteristics (age and gender).

## Machine Learning models
To answer questions 1 and 2, Spearman and Pearson correlations will be used.

Given that our dataset is labeled, we use supervised learning models. The main target in our research questions is the fearfulness score, which is scaled continuously from 1 to 7 (ordinal), therefore, we will be using a regression model.

## The Algorithms That Will Be Used
1-Random Forest can handle both continuous and categorical data, unbalanced data as well as data with missing values. It also overcomes the overfitting problem. This algorithm will fit our needs as our dataset is relatively small (chances of overfitting), and has missing values. 

2-Support Vector Machine (SVM) offers high-performance results in classification compared to other machine learning techniques and works best on small datasets, it is prone to be a proper algorithm to predict the fearfulness of a participant. SVM works well with a clear margin of separation and with high-dimensional space. We will compare the results with different kernels: Linear, Polynomial, RBF, and Sigmoid.

To find the best match of hyper-parameters in both algorithms, we will use Grid search Cross-Validation.


## Notes on feature importance calculation in PySpark for Random Forest and Linear Regression
The feature importance in PySpark for Random Forest and Linear Regression are calculated using two different algorithms for generating predictions, so they can yield to different results.

### Random Forest: 
By default, PySpark's implementation of Random Forest uses Gini importance to calculate feature importance. However, it also can be set to use Mean Decrease in Accuracy (MDA) as the method for calculating feature importance. 
To do so we need to set  featureSubsetStrategy="sqrt" and impurity="entropy" in RandomForestClassifier.

for the Gini importance (mean decrease impurity), the method measures the total reduction of the impurity of the model that results from splitting on a particular feature. The higher the reduction in impurity, the more important the feature is deemed to be.
in summary:
1) The model fits multiple decision trees on subsets of the data, using a random subset of the features for each tree.
2) For each feature, the Gini importance is calculated as the total reduction of the impurity of the model that results from splitting on that feature.
3) The Gini importance scores for all the features are then normalized to add up to 1.
https://spark.apache.org/docs/latest/ml-classification-regression.html#random-forests

### Linear Regression:
feature importance is measured by the magnitude of the coefficients in the (linear equation) model. 
The larger the coefficient for a particular feature, the more influential that feature is in determining the final prediction.
https://spark.apache.org/docs/latest/ml-classification-regression.html#linear-regression

