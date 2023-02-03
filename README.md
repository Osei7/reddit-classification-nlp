# PROBLEM STATEMENT:

In this project, the challenge is illustrating the ability to collect unstructured data, pre-process that data, then build a predictive classification model. Utlizing Pushshift's API on the subreddit's "Personal Finance" and "Financial Independence" the data was collected and pre-processed to then build a model to accurately predict which category a subreddit post would fall into.  

## Overview of Notebook:

Notebook 1: Data Extraction

Using Pushshit's API to extract subreddit posts from "Personal Finance" and "Financial Independence." The data was extracted then compiled into individual csv files for further cleaning and EDA of the data. 

Notebook 2: Data Cleaning / EDA

This notebook is comprised of the datacleaning and EDA initally for two seperate datasets ("Personal Finance" and "Financial Independence") that eventually became one. My initial plan was to feed the model only the 'title' column as a feature. After initial model I believed giving the model additional text data would help performance, so I went back and did additional cleaning to add the 'selftext' column as a feature as well. 

Notebook 3: Inital Modeling

My initial approach was to run the Tfid Vectorizer through a pipeline with several different models while utilizing a gridsearch. The models used were Logistic Regression, Decision Tree, Multinomial Naive Bayes, KNeighbors, Random Forest, AdaBoost, and finally Stacking the best performing models. 

Notebook 4: Secondary Modeling

In this notebook I attempted to improve model performance by giving the the selftext of each post combined with the title of each post. The model performance was around the same range with a few doing significantly worse, and some incrementally increasing. 

## Methodology, Inferences, & Assumptions:

My initial approach was to run the Tfid Vectorizer through a pipeline with several different models while utilizing a gridsearch. My thought was that since Tfid gives weights to the vectorized words, the overall performance might suffer, it would help more accurately predict the reddit. The models used were Logistic Regression, Decision Tree, Multinomial Naive Bayes, KNeighbors, Random Forest, AdaBoost, and finally (Stacking the best performing model). 

I used a pipeline to combine the estimator and the transformer together, and gridsearch to automate utilizing the best hyper parameters of the vectorizer. 

I initially thought title would be sufficient data to feed the model, but noticed a high misclassification rate on all the models. I decided to use F1 as the benchmark for evaluating model performance, and in the second round of modeling, included subtext and title together. This was done because many selftext fields were missing (particularly in the financial independence subreddit). My approach was to convert those missing values to empty strings, and concatenate selftext and title. So, if a cell is missing the value, my assumption is that it does not hurt the model, but if it has the data, it would help train the model. The same models were tested in secondary modeling. 

Note: F1 was used to differentiate model performance since it is designed to work well on inbalanced data. 

## Conclusions & Recommendations:

Considering the overlap of the topics I think model performance was okay. The best performinig model was a stacking model composed of Naive Bayes, AdaBoost, and Random Forest, with Logistic Regressor as the final estimator. It ultimately over predicted 1's (the personal finance subreddit - false positives), partially due to the imbalance of classes. There were two times as many false positives as false negatives.


With more time, I would have explored if word length, and word count would have improved model performance. In addition, methods of balancing the class imbalance. 

For example:
1. Oversampling the minority class / undersampling the majority class
2. Gridsearching with balanced accuracy
3. Creating synthetic data points with the minority class


