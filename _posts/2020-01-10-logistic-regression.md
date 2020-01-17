---
layout: post
title: Infamous Logistic Regression
subtile: Logistic Regression
comments: false
---
What exactly is logistic regression. For binary classification, logistic regression computes the posterior probability of class C1 as a logistic sigmoid acting on a **linear function** of the feature vector x: `p(C1|x)=y(x)=σ(wTx)`.


σ (.) is the logistic sigmoid function. `σ(a)=1/(1+exp(-a))` + `d(σ)/d(a)=σ(1-σ)`.

Now the goal is to maximize the conditional likelihood p(**t**/w).
- we take the log to work with the equation and minimize the negative term.
- To find the minimum of the error, we use simple gradient descent.





