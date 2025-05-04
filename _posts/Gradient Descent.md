---
title: Gradient Descent
date created: Friday, November 29th 2024, 3:06:42 pm
date modified: Friday, November 29th 2024, 3:06:45 pm
---
# Definition 
Gradient descent is _an optimization algorithm used to train machine learning models_ by minimizing errors between predicted and actual results.
# The Problem 

We want to minimize the [[Cost Function|cost function]]. One way to do that is to take the derivative of the function $J(\theta)$. However, as the number of parameters in $J(\theta)$ get larger, this problem becomes exponentially more difficult. 

![[Cost Function]]
# Thinking 
a cool way to think about this is that the cost function is a surface above the x-y plane which is the input. We want to find the direction of the steepest descent
![[Pasted image 20241129151741.png|425|center|225]]

Instead of finding the **global minimum** we can try to find the **local minimum**. This can be done by doing the following. We can randomly pick a position in the cost function, and find it's slope. Then move in the direction of the slope so that it is minimized. 

This can be done where the value $\delta$ in $J(\theta + \delta)$ is proportional to the slope of the cost function
$$
\frac{dJ(\theta)}{d\theta} \propto \delta
$$
This way as the slope decreases, the magnitude of the vector we are moving along decreases as well. This is referenced to by the negative of the [[Gradients|gradient]] of the function.

Hence the result of the gradient descent is as follows: 
If we have the weights for our neurons in a [[Other Fields/Machine Learning/Neural Networks|neural network]] be 
$$
W = 
\begin{bmatrix}
a \\
b \\
c \\
d
\end{bmatrix}
$$
The direction that each of these should be nudged to minimize the loss function should be 
$$
-\nabla C(W) = \begin{bmatrix}
a' \\
b' \\
c' \\
d'
\end{bmatrix} 
$$
