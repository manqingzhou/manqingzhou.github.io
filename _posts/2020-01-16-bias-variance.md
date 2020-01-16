---
layout: post
title: Bias Versus Variance
comments: false
---
Whenever we think about model prediction, the first thing pops up is always prediction errors(bisa and variance). Understanding of these errors would help us avoid the mistake of overfitting and underfitting.

**WHAT IS BIAS?**

Bias is the difference between the average prediction of our model and the the correct value which we are trying to predict. 

**WHAT IS VARIANCE?**
Let me put this way, model with high variance pays a lot of attention to training data and does not generalize on the data which it hasn't seen before. It performs well on training but has high error on test data.
<img src="/img/posts/variance-bias.png" alt="demonstration" align="center"/>

In supervised learning, **underfitting** means YOUR model messes up the pattern of the data. The prediction is totally wrong! It happens when we have very less amount of data to build an accurate model. Or, we use the wrong method fot data set. In contrast,**overfitting** happens when our model try to classify every single data point. Usually, these models have low bias and high variance.
<img src="/img/posts/underfitting-overfitting.png" alt="demonstration" align="center"/> 

**TOTAL ERROR**

Like always, we need to minimize the error function `Total Error = Bias**2 + Variance + Irreducible Error`
Here,I want to emphasize the with the increase of algorithem, the bias will go down while the variance goes up. That is why it is important to find a good balance for it.


