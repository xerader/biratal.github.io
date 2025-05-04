---
title: Default
tags: 
Ref:
---

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

![[Pasted image 20250413151138.png|400|center]]

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

