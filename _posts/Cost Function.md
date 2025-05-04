---
title: Definition
date created: Friday, November 29th 2024, 2:58:42 pm
date modified: Wednesday, February 5th 2025, 4:55:30 pm
tags:
  - "#engs106"
---
# Definition
The cost function is a function that measures the "cost" associated with a specific set of parameters, and primarily represents how well the model predicts the observed data. The goal in ML is generally to minimize the cost function. The way this is typically done in machine learning is through algorithms such as [[Gradient Descent|gradient descent]]. This would mean that we have a set of parameters that predicts the observed data pretty well. 

# Mean Square Error
A very common method is the Mean Squared Error (MSE) function. 

$$
J(\theta) = \frac{1}{m} \sum _{i = 1}^{m} (h(x_{i}) - y_{i})^{2}
$$
In this case, $h$ is the predicted value for a given input $x_{i}$ and $y_{i}$ is the actual output. We want to minimize the cost function $J(\theta)$. 

# Quadratic Cost
$$
C = \frac{1}{2n}\sum _{x} ||y(x) - a^{L}(x)||^{2}
$$
Where $n$ is the total number of training examples. The sum is over the individual training examples $x;y = y(x)$ is the desired output

$L$ is the number of layers in the network, and $a^{L} = a^{L}(x)$ is the vector of the output of the activations when $x$ is the input. 

## Entropy Loss
$$
\Sigma p\log \hat{p}
$$
# Binary Variable
Suppose our label is $(y, 1-y)$. So, 
$$
\begin{align}
p  & = (y, 1-y) \\
\hat{p}  & = (\hat{y}, 1-\hat{y})
\end{align}
$$
Then our loss will look like 
$$
CE-loss = -(y\log \hat{y} + (1-y)\log(1-\hat{y}))
$$
In that case the $CE-loss$ would be $-\log \hat{y}$ 
In this case, $\hat{y}$ should be $1$. If our $y$ is close to 