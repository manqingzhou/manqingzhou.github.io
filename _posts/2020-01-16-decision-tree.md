---
layout: post
title: Decision trees
subtitle: Different tree models
comments: false
---
Why call it a decision tree? This is because you make a bunch of choices until you get to the final decision and the processes are shaped like a tree with all those branches.

**Regression trees**

Trees are drawn upside down. The final regions are termed `leaves`. `Node` is where a split occurs.

To create a regression tree, we use the mean of the response and a greedy approach which focuses on the current step, rather than looking ahead and making a split that will result in a better prediction in a future step.

**Classification tree**

It is very similar to a regression tree. However, we cannot use the mean value of the response, so we now predict the most commonly occuring class in a region.

