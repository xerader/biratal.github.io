---
title: Parameters
date created: Friday, November 1st 2024, 10:48:43 am
date modified: Monday, February 10th 2025, 10:39:58 am
---
# Parameters
In clustering we primarily have two different parameters to look at. 
$\epsilon$ is the distance between points in a cluster
$\rho$ is the distance between the centroids of individual clusters. 
Remember the density based clustering algorithms I used for the Mitra lab work. We altered the $\epsilon$ values for this. 
#qbs177 


Before this, we want to review [[Hypothesis Tests]]. 
![[Neyman-Pearson paradigm#Types of Errors]]

## Issues with Multiplicity
Recall that if $X_{1}, X_{2}, \dots,X_{M}$ are independent, 
$$
Pr(X_{1}, X_{2}, \dots, X_{M})= \prod_{i=1}^{N} P(X_{i})
$$
What is the probability of at least one type 1 error across the $M$ tests? This is given by:
$$
\alpha _{FW} = 1-(1-\alpha)^{M}C
$$

### Example: Simple coin toss 
Consider a single coin toss 
$$
Pr(H) = Pr(T) = 0.5
$$
The probability of at least one head would be given by 
$$
Pr(H \geq 1) = Pr(H) = 0.5
$$
#### Coin is tossed 10 times. 
Well in that case, 
$$
Pr(H = 10) =1 - (0.5)^{10} = 0.99
$$
The probability of at least one Type $1$ error. $0.05$. That is, 
$$
\alpha = 0.05
$$
Accordingly, 
