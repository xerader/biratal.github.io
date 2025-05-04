---
title: Curse of Dimensionality
tags: 
Ref:
date created: Friday, January 17th 2025, 3:02:47 pm
date modified: Tuesday, April 15th 2025, 4:00:36 pm
---
Think links to [[Covariance and Correlation]]. 
#qbs177 #machinelearning #statistics #qbs108
#haru
# Curse of Dimensionality
When our **feature dimension** is high, we need more training points to capture the variance of the features. By reducing the number of features using PCA, we can simplify our dataset. 

# PCA
## Definition
I heard that PCA is a technique that is used to simplify a dataset. And there is something

 It's a linear transformation that chooses a new coordinate system for the data set such that the greatest variance by any projection of the data set comes to lie on the first axis (then called the first principle component), the second greatest variance was. 

## Geometrical Interpretation
Consider the new coordinate system where one of the axes is along the direction of the line. 

Given a set of points, how do we know if they can be compressed like in the previous example? 

You can look at the correlation between the points 
The tool for doing this is called the PCA. 

## Derivation
Assume we have a dataset $X$. Where each row is a sample and column is a feature. We want to project these points into a new vector $w$. Such that the variance is maximized.  For all data points, we have

$$
y = Xw
$$
The variance is given by 
$$
\begin{align}
Var(Y)  & = \frac{1}{N}\sum_{i=1}^{N} (y_{i} - \bar{y})^{2} \\
  & = \frac{1}{N}\sum_{i=1}^{N} (u^{T}(x_{i}- \bar{x})(x_{i}- \bar{x})u) \\
 & =u^{T}\left[ \frac{1}{N} \sum_{i=1}^{N} (x_{i}- \bar{x})(x_{i} - \bar{x})^{T}\right]u
\end{align}
$$
 now $(x_{i}- \bar{x})(x_{i}- \bar{x})^{T}$ is the Covariance matrix. We can represent this as $C$. Now we want to maximize the variance that. 

> Remember that when we want to OPTIMIZE, we use  LAGRANGE Multiplier

In this case, 

$$
L(u, \lambda) = u^{T}Cu - \lambda(u^{T}u - 1)
$$
Is the [[Multinomial#Lagrange Multiplier|Lagrangian]] equations. By taking the derivative with respect to $u$ in this case, we get: 
$$
\nabla _{u}L = 2Cu - 2\lambda u = 0
$$
By Simplifying, we get: 
$$
Cu = \lambda u
$$

## Eigenvalues and Eigenvectors
By finding the eigenvalues and eigenvectors of the covariance matrix, 

Hence, in this case, lets define $X$ as a $N \times n$ matrix with the following columns
$$
X = [X_{1} - \bar{X}, X_2-\bar{X}, \dots, X_{n} - \bar{X}_{n}]
$$
Let 
$$
Q = XX^{T}
$$
be the $N \times N$ matrix where we know that 

- Q is a square
- It is symmetric
- It is the covariance matrix
- It can be very large (in vision, $N$ is often the number of pixels in an image)

## PCA Theorem

$$
X_{j} = \bar{X} + \sum_{i=1}^{n} g_{ji}e_{i}
$$
## Compressing Data

Assuming that $\lambda _{i} \approx 0$ for $i \geq k$. 
Then, 


# Singular Value Decomposition 
You can decompose any matrix into three other factors or other matrices. This is written as 

$$
 A = U \Sigma V^{T}
$$
Here, $U$ is a n orthogonal matrix, $\Sigma$ is a diagonal matrix (Covariance?) and $V$ is orthogonal as well. $U$ and $V$ represent orthogonal spaces where 



