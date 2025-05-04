---
title: Exercises on Backpropagation
date created: Friday, December 27th 2024, 9:46:38 am
date modified: Friday, December 27th 2024, 9:46:48 am
tags:
  - "#exercises"
---
>Suppose we modify a single neuron in a feedforward network so that the output from the neuron is given by $f\left( \sum _{j}w_{j}x_{j} + b \right)$, where $f$ is some function other than the sigmoid. How should we modify the backpropagation algorithm in this case?

It would not need to be changed. There is nothing specific in the algorithm that makes use of the properties of the sigmoid function. It's just that the derivative of the function would be the derivative of $f$ when evaluating that particular neuron. So $z^{l}$ where $l$ is the layer for the neuron $j$ that is the altered one, would be different where $z^{l}_{j}$ would be the above function. And any equation where $z^{l}_{j}$ appears, the quantity of $\sigma'(z^{l}_{_{j}})$ would be different. 

>**Backpropagation with linear neurons** Suppose we replace the usual non-linear σ function with $\sigma(z) = z$ throughout the network. Rewrite the backpropagation algorithm for this case.

First, we can see that $a = z$ in this case. So, $\frac{ \partial a }{ \partial z }= 1$. That would change the equations accordingly. as 

$$
\begin{align}
\frac{ \partial C }{ \partial z }  & = \delta^{l} \\
 \delta^{L}& = \frac{ \partial C }{ \partial a }  \\
\end{align}
$$
That is, that is that the error of the output layer$\delta^{L}_{j}$ is just the derivative of $\frac{ \partial C }{ \partial a^{L}_{j} }$
or 
$$
\delta^{L} = \nabla _{a}C
$$
The error in the next layer would then be given by: 
$$
\delta^{l}_{j} = (w^{l+1})^{T}\delta^{l+1}
$$
The other two equations will stay the same. 
