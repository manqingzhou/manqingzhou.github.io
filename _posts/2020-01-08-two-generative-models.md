---
layout: post
title: Gaussian Classifiers and Naive Bayes
subtitle: Two Generative Models
comments: false
---
By the end of this article, you would understand how them work.
A generative model is actually estimating p(x|y) to then deduce p(y|x).In this case,if we learn the class-conditonal density p(x|Ck) through training, we are able to predict the label for the datapoint x
p(Ck|x) = p(x|Ck)p(Ck)/p(x)
<img src="/img/posts/model-difference.png" alt="two models" align="center"/>
Confused by all the mathematical stuff? Don't worry, this Naive Bayes example can save your brain cells.




