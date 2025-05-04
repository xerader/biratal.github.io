---
title: Lecture 5
tags:
  - "#engs106"
  - "#machinelearning"
Ref: 
date created: Monday, February 3rd 2025, 4:13:55 pm
date modified: Monday, February 3rd 2025, 4:14:11 pm
---
# Lecture 5
## Training Data
We start with out [[Logistic Regression Hypothesis and Frequentist method|Hypothesis setting]]. As there are unlimited $h_{\theta}$ possible, we want to find out what is the best one. That is find the parameter $\theta$. This is the primary goal of Machine Learning.  

## Training error/Empirical Risk
This is the error for the **training set**. 
$$
\hat{\epsilon}(h) = \frac{1}{m} \sum_{i=1}^{m} 1(h(x^{(i)})\neq y^{(i)})
$$
Where $1$ is a function that returns whether the inside is true or not. This counts the number of times a "mistake" is made. That is when $x^{(i)} \neq y^{(i)}$. 

$$
\epsilon(h) = P(h(x )\neq y)
$$
What's the probability that for a given point, you'll miss the target with the hypothesis $h$. 

The **generalization error** is the probability that a random point misses the target. This is also known as the **test error**

What we want to know is by how much does $\hat{\epsilon}(h)$ estimate $\epsilon(h)$? 

**That is, how effective is our hypothesis $h$? Ideally, the training error is a good estimate of the generalization. However, this is usually not the case.** 

We can define this as follows: 
$$
\hat{h} = \arg \min \hat{\epsilon}(h)
$$
The arg min is a notation that shows me at what argument of $x$ gives me the minimum. So for a function $f(x) = y$, the value of $x$ where $y$ is minimized is the arg min. 

Accordingly, $\hat{h}$ is the hypothesis that gives the smallest training error. 

$$
h^{*} = \arg \min \epsilon(h)
$$
And $h^{*}$ is how close the $h$ is close to the $\hat{h}$. That is how close is our hypothesis to the ideal one. 

## Test Error
This is given by 
$$
\epsilon(h) = P(h(\vec{x})\neq y)
$$
Where $\vec{x}$ and $y$ are randomly chosen. For this we make the **PAC** assumption. That is, Probably and  Appropriately Correct 

