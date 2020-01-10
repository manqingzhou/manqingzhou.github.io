---
layout: post
title: Introduction to machine learning(Part One)
subtitle: Supervised models
comments: false
---
Welcome to the world of **machine learning** and **deep learning**. The main idea behind it is to train machine to learn from data so it can solve new cases even when the data changes. Besides, there are different types of learning tasks such as supervised learning(classification, regression, time series prediction) or unsupervised learning(clustering). Here, I need to touch on reinforcement learning in case i get confused in the future. So, there would be reward and penalty in reinforcement learning and the outcome is to choose best policy to maxmize rewards and avoid penaltie through learning from the past.

## Table of Contents
- [Classification models](#classification-models)
- [Model fitting and selection](#model-fitting-and-selection)

## Classification models
Outputs are categorical and inputs are anything. Goal is to select correct class(label) for new inputs.The simplest case is a choice between 1 and 0.
<img src="https://manqingzhou.github.io/img/posts/simple-classification.png" alt="0 or 1" align="center"/>
Here, I need to address the difference between classification and regression . In the latter case, outputs are continnuous. But the goal is similar which is to predict outputs accurately for new inputs. We can use it to predict the price of astock in 6 months time.
Before we dig into those complicated classification models, I want to list few examples where we can use those models and what we need to do before throwing bunch of stuff into our models. To start off, imagine predict whether a patient has cancer or not. Also, we can check if it is going to rain tomorrow based on temperature, humidity etc. The graph below is a vivid demonstration of inputs and outputs(matrix).

<img src="/img/posts/feature.png" alt="input and output" align="center"/>
Once we got a feature matrix, the following question is how to normalize features. This is because most of clssifiers calculate the distance between two points.

There are some ways to scale the range of a feature. The one I typically use is Min-max normalization

Okay, let me introduce you the first model: K-Nearest Neighbor(KNN). In one word, similar things are near each other. The implentation is shown below:
```
---
def knn(data, query, k, distance_fn, choice_fn):
    neighbor_distance = []
    for index, data_point in enumerate(data):
        distance = distance_fn(data_point[:-1],query)
        neighbor_distance.append((distance,index))
    sorted_neighbor_distance = sorted(neighbor_distance)[:k]
    k_nearest_labels = [reg_data[i][1] for distance, i in sorted_neighbor_distance]
    
    return k_nearest_labels, choice_fn(sorted_neigbor_distance)
---
```
```
---
def euclidean_distance(point1, point2):
    sum_squared_distance = 0
    for i in range(len(point1)):
        sum_squared_distance += math.pow(point1[i] - point2[i], 2)
    return math.sqrt(sum_squared_distance)
---
``` 
SOOOO,isn't it perfect fit for recommendation system?? [More details can be
checked here](https://towardsdatascience.com/machine-learning-basics-with-the-k-nearest-neighbors-algorithm-6a6e71d01761)

Next, I want to introduce SVM.


