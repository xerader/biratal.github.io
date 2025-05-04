---
title: Default
---
# Building on Backpropagation 
[[Backpropagation]] is often combined with the SGD learning algorithm. This is where the gradient for many different training examples is computed. In particular, given a mini-batch of $m$ training examples, the following algorithm is followed: 

## Input a set of training examples
## For each training example
For each $x$, set the corresponding input activation $a^{x, 1}$ and do:
### Feedforward
$$
z^{x,l} = w^{l}a^{x, l-1} + b^{l}
$$
and 
$$
a^{x,l}= \sigma(z^{x,l})
$$
### Output Error
$$
\delta^{x, l} =\nabla _{a}C_{x}\odot \sigma'(z^{x,l})
$$
### Backpropagate 
$$
\delta^{x,l} = ((w^{l +1})^{T}\delta^{x,l+1})\odot \sigma'(z^{x, l})
$$
## Gradient Descent
for each $l = L, L-1, \dots, 2$ the weights are updated according to the rule that 
$$
w^{l} \to w^{l} - \frac{\eta}{m}\sum _{x}\delta^{x,l}(a^{x, l-1})^{T}
$$
and the biases according to 
$$
b^{l}\to b^{l}-\frac{\eta}{m}\sum _{x}\delta^{x,l}
$$
