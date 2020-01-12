---
layout: post
title: Introduction to machine learning(Part Two)
subtitle: Unsupervised models
comments: false
---
In the part of supervised models, I talked a lot about classification. In this article, I am just jump into unsupervised models and how they work differently. If you have any confusions about basic concepts about machine learning, you are welcome to read 'Part One'.

## Table of Contents
- [Unsupervised models](#unsupervised-models)
- [Feed-forward network](#feed-forward-networks)
- [Recurrent neural networks](#recurrent-neural-network)
- [Convolutional neural networks](#convolutional-neural-networks)
- [Platform](#platform)

## Unsupervised models
Inputs are continuous or categorical and we have no targets. Goal is to group data cases into a finite number of clusters so that within each cluster all cases have very similar inputs. That is why it is important to find an interesting way to visualize dat.
e.g. We can put emerging similar topics in one cluster for news.

<img src="/img/posts/cluster.png" alt="cluster" align="center"/>
All require a way to measure distance between two data points, e.g. the Euclidean distance.

First algorithm I am going to introduce is K-means. It is designed for a pre-defined number of cluster K by randomly initializing a center for each cluster.

Two simple steps:
E step:For all data points, assign each to the cluster whose center is closet tothis data point.
M step:Update each cluster's center to be the mean of all points assigned to that cluster
<img src="/img/posts/ME-Step.png" alt="M step plus E step" align="center"/>


## Feed-forward network
