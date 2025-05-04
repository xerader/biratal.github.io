---
title: Definition
tags:
  - "#engs106"
  - "#machinelearning"
  - "#statistics"
Ref: 
date created: Sunday, January 19th 2025, 4:33:37 pm
date modified: Monday, January 20th 2025, 5:05:09 pm
---

# Definition
The amount of information can be thought of as the "degree of surprise" on observing a random variable $x$. If we are told that a highly improbable event has occurred, we will gain more information by observing the value $x$ than if something expected happening, and more than something that is certain to happen. 

## Information
This is a quantity signified by $h(x)$ that is a monotonic function of the probability $p(x)$ that expresses the information content. If we have two events, that are unrelated, then the information gained by observing both of them together or separately can be represented as: 

$$
h(x, y) = h(x) + h(y)
$$
Two unrelated events will be statistically independent and so, 
$$
p(x, y) = p(x)p(y)
$$
This gives us the relation 
$$
h(x) = -\log_{2}p(x)
$$
Where the negative sign is there to ensure that the information is positive.

## Entropy
The expectation of $h(x)$ is the entropy. It can be thought of the average amount of information that is transmitted. 

$$
H[x] = -\sum_{i=1}^{} p(x)\log_{2}p(x)
$$
This is the **entropy** of the random variable $x$. This let's us sidestep the problem of taking the log of 0 as $\lim_{ p \to 0 }p\ln p = 0$. 

$$
\prod_{i=1}^{N} x(y + 3\alpha)
$$
