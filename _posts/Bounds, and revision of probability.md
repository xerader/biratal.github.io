---
title: Lecture 1
date created: Monday, January 6th 2025, 5:01:44 pm
date modified: Monday, January 6th 2025, 5:25:46 pm
---
#engs106
# Lecture 1

## Union Bound
We place these limitations
$$P\left( A_{1}\cup A_{n} \right)\leq \sum_{i=1}^{N}P(A_{i}) $$
$$
P(A \cup B) \leq P(A) + P(B)
$$
## Hoftdoing's Inequality (Chernoff bounds)
Where we assume $Z_{i}$ is a [[Dartmouth/Biostatistics/Distributions/Bernoulli Distribution|bernouli random variable]]. 
$$
\begin{align}
prob(Z_{i} = 1)  & = \phi \\
prob(Z_{j} = 0) & = 1 - \phi
\end{align}
$$
We define a [[Maximum Likelihood Estimation]] such that:
$$
\hat{\phi} = \frac{1}{k} \sum_{i=1}^{k} Z_{i}
$$
This is the average of the random variables, so the $\hat{\phi}$ is also a random variable.

Where $k$ is the number of random variables. 
Then, for any $\gamma >0$, we have: 
$$
P(|\hat{\phi}- \phi|>\gamma) \leq 2e^{-2\gamma ^{2}k}
$$
So, the probability that the estimator is less than a given value is given by the above bound. 

$$
S = \{ (x^{(i)}, y^{(i)}) \}^{n}_{i= 1}
$$
In this case, $x$ is a feature vector, and $y$ is the label for that feature. Both of them are part of vectors in $\mathbb{R}$. The $(x, y)$ pair is a **data point**. The $n$ signifies that we have $n$ points, which compromises our set. We also define this as having a discrete set. 

