---
layout: post
title: Discriminant Analysis
subtitle: A dimensionality reduction technique
---
In one sentence, Linear Discriminant Analysis use the information from features to create a new axis and projects the data to this new axis to minimize the variance and maximize the distance between the mean of two classes.
Before breaking up the algorithm, I want to talk little about the math behind it.

The first one is scatter matrix which is used to understand the relation between two variables. This is also used in lots of dimensionality reduction senarios. If there are k variables, scatter matrix will have k*k matrix.
<img src = "/img/posts/scatter.png" alt="scatter math problem" align="center"/>
[Detail](https://medium.com/@raghavan99o/scatter-matrix-covariance-and-correlation-explained-14921741ca56)

Steps:
1. Compute the within class and between class scatter matrix
2. Compute the eigenvectors and corresponding eigenvalues for the scatter matrices
3. Sort the eigenvalues and select the top k
4. Create a new matrix containing eigenvectors that map to the k eigenvalues
5. Obtain new features by taking the dot product of the data and the matrix from 
Here, I put the significant steps:
```
#since we clear the s every single time,it is within class scatter matrix
within_class_scatter_matrix = np.zeros((13,13))
for c, rows in df.groupby('class'):
    rows = rows.drop(['class'], axis=1)
    s = np.zeros((13,13))
    #start from the first row
    for index, row in rows.iterrows():
    
           x, mc = row.values.reshape(13,1), class_feature_means[c].values.reshape(13,1)
             
           s += (x - mc).dot((x - mc).T)#this matrix is 13*13
           
         
           within_class_scatter_matrix += s
```
```
feature_means = df.mean()
between_class_scatter_matrix = np.zeros((13,13))
for c in class_feature_means:
    n = len(df.loc[df['class'] == c].index)
    mc, m = class_feature_means[c].values.reshape(13,1), feature_means.values.reshape(13,1)
    between_class_scatter_matrix += n * (mc - m).dot((mc - m).T)
eigen_values, eigen_vectors = np.linalg.eig(np.linalg.inv(within_class_scatter_matrix).dot(between_class_scatter_matrix))
```
```
eigen_values, eigen_vectors = np.linalg.eig(np.linalg.inv(within_class_scatter_matrix).dot(between_class_scatter_matrix))
pairs = [(np.abs(eigen_values[i]), eigen_vectors[:,i]) for i in range(len(eigen_values))]
eigen_value_sums = sum(eigen_values)
print('Explained Variance')
for i, pair in enumerate(pairs):
    print('Eigenvector {}: {}'.format(i, (pair[0]/eigen_value_sums).real))
```
The result would maximize the seperation between classes.

