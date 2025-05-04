---
title: Regression
date created: Monday, December 9th 2024, 3:29:26 pm
date modified: Thursday, January 16th 2025, 10:30:26 am
---
#qbs177 #statistics #machinelearning  #qbs121 
# Regression
The objective of regression is to predict the value of continuous target variables, given the value of a $D$ dimensional [[Vectors|vector]] $x$ as an input. Most of this is based on the idea of a [[Linear Model]]
*
- Regression models are simple, easy to interpret and understand
- They are robust. Lets you add non-linear terms in it as well.
- They allow us to include confounders inside the statistical model. 
- You can compare models directly, and can be used to compare. 
- Can work well as a approximations of more complex models. (Taylor Expansions) 

## Model
A linear regression is of the form 
$$
p(y|x, \theta) = N(y|w^{T}x, \sigma ^{2})
$$
They can also be used to model non-linear relationships by defining a function in terms of $x$ which is non-linear. Such that $\phi(x)$ replaces $x$ above. This is called the **basis function expansion**

The general way to do this would be 
$$
Y = \beta0 + \sum_{i=1}^{N} \beta_{i}f(x_{i}) + \epsilon
$$

![[Confounding]]

## Multiple Linear Regression.
In this case, you think about it as a vector. So you get it as follows: 

$$
Y = XB  +E
$$
Where, 
$$
Y^{n} = b_{0} + X_{1}^{n}b_{1} + \dots + X_{m}^{n}b_{m} + e^{n}
$$
## Assumptions
Errors are independently and identically distributed. They follow the same distribution with mean - and homogeneous variance: 
$$
e^{i} \sim N(0, \sigma ^{2})
$$
Matrix has full rank . That is there are no linear dependencies between columns

Requires observations to be independent 
-- Examples: 
- Individuals in the study are unrelated and not clustered
- No multiple measurements on the same subject 

Predictors are either metric or binary. 

## Model Estimation
Idea: 
- Chose $B_{i}$ to minimize sum of squared distances between observations and hyper plane (prediction) 
- leas square estimate - LSE 

Best unbiased estimator (Gauss-Markov): 
$$
B = X(X'X)^{-1}X'Y
$$
## Significant Testing

### Wald Test
The regression coefficient $b$ should be 0 under the null hypotheses. That is, that these predictors have no effect on the outcomes. Hence, under the null hypotheses $H_{0}$, we would have: 
$$
W = \frac{\hat{b}}{\hat{SE}\hat{b}} \stackrel{asymp}{\tilde{}} N(0, 1)
$$
. 

## Likelihood
We have a lot of observations. What would be the best $u$ and $\sigma ^{2}$ that could represent this information. That is, $$
L(\mu, \sigma ^{2}|data)
$$
Or, 
$$
P(data|P)\sim L(P|data)
$$
## Maximum-Likelihood
### Rationale
1. All models are wrong
2. Some models are better than others
3. Chose the model with the highest likelihood from a family of models
$$
L(\hat{P}|data)= \max_{p}L(P|data)
$$
From the family of statistical models, the maximum likelihood model yields the one that best represents our data. 
### Likelihood-ratio Test
This is a way of finding out which model is better. Compare the maximum-likelihood models of the model which contains the variable, and one that does not contain the variable. 

In this case, we get $\hat{\theta}$ from the [[#Model estimation]] which gives us $B$. 
$$
\Lambda = \frac{L(\hat{\theta}|data, H_{0})}{L(\hat{\theta}|data, H_{A})} = \frac{L(\text{ model without the variable})}{L(\text{ model with the variable})}
$$
$$
G = -2\ln \Lambda = 2(\ln _{A} - \ln L_{0})\sim ^{asymp}X^{2}
$$
So $G$ is the difference in the number of model parameters. The LRT allows us to simultaneously test the significance of multiple variables
## Goodness of Fit of the Model
$$
R^{2} = \frac{Var(\hat{Y})}{Var(Y)} \in[0, 1]
$$
![[Pasted image 20250113113105.png]]
A good $R^{2}$ (higher) would mean that there is a relation between $x$ and $y$. 


## Linear Regression Models in R (I)

## Odds Ratios from a Logistic Regression Model
![[Pasted image 20250115103538.png|center|425]]
![[Pasted image 20250115103552.png|center|425]]![[Pasted image 20250115103612.png|center|425]]
![[Pasted image 20250115103641.png|center|425]]
## Logistic Regression in R
For a generalized linear model, you need to do a `glm` in R. Then you will have
```{r}
logreg.result = glm(affection ~ SNP1, data = assoc.data, family = binomial(logit))
```
Is an example of the code. 

## Modelling Non-linear Associations
$$
Y = a + bX + cX^{2} + \epsilon
$$
can be modelled by a linear model even if it is a quadratic one. The thing is that the coefficients themselves, are linear. So it's non-linear with respect to the feature. But it is linear with respect to the coefficients. 

So you can still do a linear model even when the variables themselves are not. 

### Lowes Curves
Adds curves to our linear models. 