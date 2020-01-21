---
layout: post
title: Something You Need to Know About Data Science Interview
---
**What is difference between supervised and unsupervised models**
Are we training labelled data or we just try pur those similar data points into the same cluster?

**What is bias, variance trade-off**

They have different trend lines. Bias is like model is too simple and its prediction is somehow WRONG! While in the case of variance, you pays a lot of attention to training data, for example, you wanna perfect fit for seperating two classes. As a result, it has high error on test data.

Low bias - of course decision tree(with all those beautiful branches),SVM(that perfect hyperplane),K-NN(mama,lets find our k number neighbors, but not too many to bring higher bias)
High bias - Linear Regression, Logistic Regression

**What is exploding gradients**

Gradient is the **direction and magnitude** calculated during training of a neural network that is used to update the network weights in the right direction.

Exploding gradients are a problem where **large error gradient** accumulate and result in very large updates to neural network model weights during training.

*What is a confusion matrix**

First, it is a 2X2 table, not 3X3 or 4X4 table. The output provided by the **binary classifier**. With it, we can also calculate accuracy, sensitivity precision and recall. The graph is shown below:
<img src="/img/posts/confusion-matrix.png" alt="TP FN FP TN" align="center"/>
Let me feed u the content. FN: The test of herpes is acutually positive and you predict that it is negative. As a result, it is a absolutely false/incorrect negative!!!

It is obviously that accuracy rate is (TP+TN)/(P+N). Sensitivity = TP/P, Precision(the truth of positive) = TP/(TP+FP).

**Tell me what do you know about a ROC curve**

A **ROC** is a graphical representation of the contrast between true positive rates and false positive rates.
<img src="/img/posts/ROC.png" alt="Fasle positive raate against True positive rate" align="center"/>

**What is selection Bias**

Selection bias occurs when sample obtained is not representative of the population intended to be analysed. A simple scenario, the company want to see which layout of the webiste would attract more customers. And everysinlge time, the user can choose layout A or layout B. Here goes the selection bias when u let the user makes the decisions. What if some users dont like changes, they are more likely to click on layout A.

**Explain SVM algorithm in detail**

It can a supervised model which can be used for both **regression and classification**. It uses hyper planes to seperate different classes based on some kernal functions. 

**What are support vectors in SVM**

We are trying to find the hyperplane that maximize the margin,we need to find another line that marks the distance from the classifier(hyperplane) to the closet data points.   

**Explain Decison Tree algorithm in detail**

