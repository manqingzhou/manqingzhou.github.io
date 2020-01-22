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

**What is a confusion matrix**

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

**Different kernels functions in SVM**

1. Linear Model
2. Polynomial kernel
3. Radial basis kernel
4. Sigmoid kernel

Future implementation code will be provided.

**Explain Decison Tree algorithm in detail**

To start off, it is a supervised machine learning algorithm mainly used for the **Regression and Classification**. The final result is a tree with decision nodes and leaf nodes. Decision tree can handle both categorical and numerical data.

Dont forget information gain and entropy in decision tree algorithm. Entropy checks the node impurity(0 if the sample is equally divided)
<img src="/img/posts/entropy.png" alt="TP FN FP TN" align="center"/>
Information gain is used to split the tree.(The goal is to find the highest information gain)
<img src="/img/posts/info-gain.png" alt="TP FN FP TN" align="center"/>

**What is pruning in Decision Tree**

When we remove sub-nodes of a decision node, this process is called pruning or opposite process of splitting. If you wanna your tree to be robust at predicting(reduce the complexity of the model), you gotta cut some useless branches to avoid overfitting. Isnt like in nature, when you wanna the peach tree to be robustly growing.

**Ensemble learning**

To be honest, it is my first time heard aboot it, eh? But the function is just like its name, it is the art of combining deiverse sets of individual models to improvise on the stability and predictive power of the model. 

Bagging? isnt it vivid, a pile of bags stacked together?
The main idea is to divide original data into multiple data sets and build the same number of models. In the end, it just combines classifiers

**Random Forest**
**cross-validation on a time-series data set**
Check my time series post on my home page to see a real-life example.
**What is logistic regression, give me an example of it**
**Do you understand the term normal distribution(its kind of like everyone knows what it looks like, but you gotta speak out its features)**
**How do you define the number of clusters in a clustering algorithms**

As we know, we use the sum of sqaure to the **C** to decide which cluster the data point belongs to. So, we would plot **WSS(Within sum of squares)** to check the turning point(i guess you can also call it a elbow curve)  

The turning point here means you dont see much decrease in WSS.

**What is deep learning**

WOOW I hate it cuz i havent study a bit about it. But i am gonna use a real-life example to help me better understand it.
Lets just say its a huge number of hidden layers???

**Do we have to know regularisation?**

The model predictions should then minimize the loss function calculated on the regularized training set

**Tell me about reinforcement learning**

I LOVE TO EXPLAIN IT CUZ I TOOK A COURSE ABOUT IT!!! In one word, we use reward and penalty to teach machine find the best policy ever!plz check my github code:self-driven cab for more details.

