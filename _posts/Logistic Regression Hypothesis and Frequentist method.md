---
title: Lecture 2
tags: 
Ref:
date created: Wednesday, January 8th 2025, 4:01:50 pm
date modified: Monday, January 13th 2025, 4:46:51 pm
---
#engs106 #machinelearning 
# Lecture 2
## Hypothesis Function

We have a mapping from $x \to ^{h_\theta} y$ such that $h_\theta$ is called the **hypothesis** **model** or the **model**.
In the modern day, $h \in \mathbb{R}^{10^{11}}$ or so. 

![[Training and Test Error]]

## Frequentist Approach

For a dataset like

$$
D = \{ H, T, T, H, H \}
$$
That is iid, we want a hypothesis that assigns the coinflip to to the outcome, in terms of the [[Probability]]. By using a [[Bernoulli Distribution]] we can represent it as: 

$$
h_{\mu}(x) = p(x|\mu) = \mu^{x}(1-\mu)^{1-x}
$$
In order to find this hypothesis, you could define it as follows: 
$$
p(D|\mu) =h_{D, \mu}= \prod_{i=1}^{m} \mu^{x_{i}}(1- \mu)^{(1 - x_{i})}
$$
Where $x_{i}$ is the event. The $\prod$ comes from the fact that each event is **independent**. 
$$
\mu^{*} = \arg \max P(D|\mu)= \arg \max \prod_{i=1}^{m} \mu^{x_{i}}(1- \mu)^{(1 - x_{i})}
$$
So, we want to maximize $\mu$ such that the probability of seeing the data we have. This is the [[Maximum Likelihood Estimation]]

In order to find the maximum, we can take the derivative and set it to 0. Which gives us 

$$
\frac{ \partial p(D|\mu) }{ \partial \mu } = 0
$$
By using the product rule, we have: 
$$
\frac{ \partial     \prod_{i=1}^{m} \mu^{x_{i}}(1- \mu)^{(1 - x_{i})}}{\partial \mu}
$$
Which is difficult to evaluate as $m$ increases. By taking the $\log$ of this, we can sum these values, and move the exponents, so: 

$$
\log\left( \prod_{i=1}^{m} \mu^{x_{i}}(1- \mu)^{(1 - x_{i})} \right) = \sum_{i=1}^{m} x_{i}\log \mu + (1-x_{i})\log(1 -\mu)
$$
This is the **MLE**, or the maximum likelihood estimator of $\mu$. 

The goal in ML is to find out what this $\mu$ is . In the log form the derivative of this is much easier to take. The $\log$ is ok to use because it's a monotonic function, meaning that it's maximum will be at the same spot. We can take it and set it to 0 so that 
$$
0 = \sum_{i=1}^{m} \frac{x_{i}}{\mu} - \sum_{i=1}^{m} \frac{1}{1-\mu}(1-x_{i})
$$
Now, we can rearrange to find a value for $\mu$. We can rewrite the summation of $x_{i}$ as $q$ and we know that the $1$ will turn into just $m$ so we have, 
$$
\begin{align}
\frac{q}{\mu}  & = \frac{m - q}{1-\mu} \\
q - \mu q &  = m \mu - \mu q \\
\mu^{*}  & = \frac{q}{m}
\end{align}
$$
Which gives us the maximum likelihood estimator. When $m$ is small, the MLE is not a great estimator. This can also be called as finding the estimator in a way that minimizes the loss. This approach of reducing the loss is called the **frequentist** approach. 

The other one is the **Bayesian Approach** 

### Cost Function 
The cost function in this case would be 
$$
J = \begin{cases}
-\log(f_{w}(x')), \quad y = 1 \\
-\log(1- f_{w}(x')), \quad y = 0 
\end{cases}
$$

ug
# Lecture 3

Using the Bayesian approach to do this
# Benefits
- Can be applied in numerous different statistical problems in the same way

## Formula
The heart of the Bayesian method is about having a hypothesis, and then updating your belief based on the observed probabilities. This can be derived from the product rule as follows: 
$$
p(X|Y) = \frac{p(Y|X)p(X)}{p(Y
)}
$$
### Alternate Expression
The denominator can be expressed as: 

![[Pasted image 20250413151138.png|200]]
$$
p(Y) = \sum _{X} p(Y|X)p(X)
$$
We call $p(X|Y)$ the posterior, 
The likelihood $p(Y|X)$ and 
prior as $p(X)$ 
they have the relation such that: 
$$
posterior \propto likelihood \times prior
$$
$X$ represents the updated information as well. Given the door $C$ is opened, what happens next? Given that you have a high temp, what is the probability you are sick?
## Approach

For proofs we can look at [[HW2 - Math#Question 4]]

Instead of giving an exact value of where the $\mu$ statistic is, there is instead a probability distribution. That is, we define a something like $p(\mu) > \phi$

$$
\begin{align}
\int_{0}^{1} D(x) \, dx   & = 1 \\
P (\mu|a, b))  & =\left( \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \right)\mu^{a-1}(1-\mu)^{b-1} 
\end{align}
$$
This distribution is called the **beta** or $\beta$ distribution of $\mu$. 
The mean of this function is: 
$$
\mathbb{E}(\mu) = \frac{a}{a+b}
$$
The variance of this function is: 
$$
Var(\mu) =\frac{ a+b}{(a + b)^{2}(a + b + 1)}
$$
The $\Gamma$ function is as follows: 

$$
\Gamma(x)= \int_{0}^{\infty} t^{xt}e^{-t} \, dx 
$$
It has the following recursive nature: 
$$
\Gamma(x+1) = x \Gamma(x)
$$

The $\Gamma$ parts in the above equation are only present such that the probability of the distribution normalizes to 1. 

We can think of $a$ and $b$ as the effective numbers of getting 1 and 0. 

## Bayesian Coin Approach
If we have a coin, then let the probability of getting heads be $\mu$. Our **prior distribution** assumption is that we can get $\mu$ by: 
$$
P (\mu|a, b))   =\left( \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \right)\mu^{a-1}(1-\mu)^{b-1} 
$$
Now we **experiment** by producing a dataset $D$ which is equal to $\{ x_{1}, x_{2}, x_{3}, \dots, x_{n} \}$, then we count how many $H$ and $T$ we get. That is $\#H = \sum_{i=1}^{N}x_{i}$ where $x_{i} = H$. 
$$
p(D|\mu) = \prod_{i=1}^{N} \mu^{x_{i}}(1-\mu)^{1-x_{i}}
$$
From this we now **update** our belief as follows: 
$$
p(\mu|D) = \frac{p(D|\mu)}{p(D)}p(\mu)
$$
which is called the **posterior**. Now, we know that $p(\mu)$ is just the $\beta$ distribution. and that $p(D|\mu)$ is given by the product above. So, 
$$
\begin{align}
 & = \left( \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \right)\mu^{a-1}(1-\mu)^{b-1} \cdot \prod_{i=1}^{N} \mu^{x_{i}}(1-\mu)^{1-x_{i}} \\ \\
 & = C' \mu^{\left( \sum_{i=1}^{N} x_{i} \right) + a - 1} (\mu - 1)^{N - \left( \sum_{i=1}^{N} x_{i} \right) + b - 1}& \\
 & = C'\mu^{a+m-1} (1-\mu)^{b + (N -m) - 1}
\end{align}
$$
In this case, $C'$ is the normalizing constant. In general for Bayesian stats, what we actually have is 
$$
p(\mu|D) \propto p(D|\mu)p(\mu)
$$
and the $p(D)$ term normalizes this to 1. However, in our case the $\beta$ distribution does this for us. Hence, this can all be merged into the constant $C'$

A reminder, $m$ is the number of 1s, and $N-m$ is the number of 0s. On integrating the posterior, we get a value of the form 
$$
\frac{\Gamma(m+a + N -m + b)}{\Gamma(m + a)\Gamma(N -m + b)}
$$
Which is of the same form as the prior. This property of the $\beta$ distribution is why it is used in this case. 

In an $N$ Bernoulli experiment,  
$$ \begin{align}
P(\mu|a, b)  & = \beta(\mu|a, b) \\
p(\mu|D)  &  = \beta(\mu|a +m, b + (N-m))
\end{align}
$$
$\beta$ -> conjugate distribution.  So based on this, we can update the mean of the equation as follows: 

$$
\begin{align}

\mathbb{E}(\mu|D)  & = \frac{a+m}{a+ m +b + N -m } \\
 & = \frac{a + m}{a + b + N} 
\end{align}
$$
as $N$ increases, $m$ will also increase. Accordingly, when $N \to \infty$, we get: 
$$
\mathbb{E}(\mu|D) = \frac{m}{N}
$$

which is the answer we got from the [[Logistic Regression Hypothesis and Frequentist method|Frequentist]] approach. 
