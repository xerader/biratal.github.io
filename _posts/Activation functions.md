---
title: Definition
date created: Monday, November 25th 2024, 3:13:29 pm
date modified: Wednesday, February 5th 2025, 4:08:19 pm
---
#machinelearning 
# Definition
They are generally denoted by $h(x)$. You need this to get the extra "non-linearity" of the model. Otherwise it'll just be a linear model. 
## Sigmoid Function
The weighted sum or result of each neuron in a layer may yield an output. We want to squish this output into a range that we are are working with. A good way to squish this is to use something like the sigmoid function
$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$
 However this is a lot older now, and most actually use ReLU


![[Pasted image 20241125151337.png|center||475]]
### Derivation of the Sigmoid

^fdefcb

The derivation is  as follows:  
$$
\begin{align}
\sigma(x)  & = \frac{1}{1 + e^{-x}} \\
\frac{ \partial \sigma(x) }{ \partial x }  &  = -\frac{1}{1 + e^{-x}}^{2}\times \frac{1+e^{-x}}{\partial x} \\
 & =\sigma ^{2} \times e^{-x} \\
 & =\sigma \times \frac{e^{-x}}{1+e^{-x}} \\
 & = \sigma \times \frac{(e^{-x}-1 +1)}{1 + e^{-x}} \\
 &  = \sigma \times \left(\frac{1+e^{-x}}{1 + e^{-x}} -\frac{1}{1 + e^{-x}}\right) \\
\sigma' & = \sigma(1 - \sigma)
\end{align}
$$

## Non Linearity
An important thing with activation functions is that they introduce something called "non-linearity". 

Activation functions cannot be linear because neural networks with a linear activation function are effective only one layer deep, regardless of how complex their architecture is. Input to networks is usually linear transformation (input * weight), but real world and problems are non-linear
## Rectified Linear Unit

This is a function that sets negative values to 0 and does nothing to the positive values. Turns out that for DNN this works a lot better. 
![[Pasted image 20241125160014.png|525|center|475]]
Pros: 
- Your number will almost never be at 0, so this not being differentiable is not that big a problem. 

# Bias
In the case where we want to have a bias for the weighted sum. For example, only a weighted sum that's over 10 is useful to us. Then our sigmoid function just becomes 

$$
\sigma(x) = \frac{1}{1 + e^{-x}} - \text{ bias}
$$
## Tanh
The tanh activation function is given by 
$$
\begin{align}
h(x)  & = \tanh(x) \\
 & = \frac{e^{x} - e^{-x}}{e^{x} + e^{-x}}
\end{align}
$$
