---
title: Lecture 5
tags:
  - "#machinelearning"
  - "#engs106"
Ref:
date created: Monday, February 3rd 2025, 4:15:15 pm
date modified: Monday, February 3rd 2025, 8:52:09 pm
---
# Lecture 5
## Definition
We ideally want our training error to be a good assumption for our test error. This comes in clutch later on when we can use the training loss to "learn" on. 

We can think of $h$ as a [[Space|space]] of hypothesis. We want to find how close is $\hat{e}(h)$ to $e(h)$? That is how close is the test loss to the training loss? 

Let $Z$ be a binary RV. In this case, we have 
$$
Z = 1(h(\vec{x} \neq y ) 
$$
where $\vec{x}, y \sim D = \{ \vec{x}, y \}$ where $\vec{x} \in \mathbb{R}^{n}$ and $y \in \mathbb{R}$. Hence, in this case, we have a binary RV as follows: 

$$
binaryRV = \begin{cases}
1  \quad h(\vec{x})\neq y\\  
0 \quad h(\vec{x})= y
\end{cases}
$$
That is, if the model is wrong, then we output $1$, and if it's not wrong we output $0$. This is a binary example right now I guess. Continuous is what's done in practice. 

In average what would the value of $Z$ be? It would be the [[Training and Test Error#Test Error|Test Error]] of $h_{\theta}$ in this case. That is, 
$$
E(Z) = \epsilon(h)
$$
We also defined the training error as 
$$
\hat{\epsilon}(h) = \frac{1}{m} \sum_{i=1}^{N} 1(h(x^{(i)})\neq y^{(i)})
$$
However, this can now be written in terms of $Z_{i}$ so
$$
\hat{\epsilon}(h) = \frac{1}{m}\sum_{i=1}^{N} Z_{i}
$$
## Hoeffding's Inequality
Suppose we have a bunch of $Z$'s, $Z_{ 1}, \dots, Z_{n}$. Then we can define 
$$
\begin{align}
P(Z = 1)  & = \phi \\
P(Z = 0) &  = 1- \phi
\end{align}
$$
Then we can define the expected value as: 
$$
\hat{\phi} = \frac{1}{n}\sum_{i=1}^{N} Z_{i}
$$
This has the boundary such that for any $\gamma >0$, 
$$
P(|\hat{\phi} - \phi|> \gamma) \leq 2e^{-2\gamma ^{2}N}
$$
That is, The probability that the mean $\hat{\phi}$ is off from the true value $\phi$ is bounded by the $2e^{-2\gamma ^{2}N}$ factor. This lets us answer **How close is the training error to the test error**. 
## Difference between Training and Test Error
We want the probability that the difference between the two is off by $\gamma$
$$
P(|\hat{e}(h)- e(h)|) > \gamma
$$
Now, our training error is just: 
$$
\hat{\epsilon}(h) = \frac{1}{N}\sum_{i=1}^{N} Z_{i} 
$$
And now, from the Hoeffding's Inequality, we know that the probability of these is bounded by $\gamma$. 
In other words, 
$$
P(|\hat{\epsilon}(h) - \epsilon(h)|<\gamma) \leq 1- 2e^{(-2\gamma ^{2}N)}
$$
 We want the probability that we stay within this bound to be a certain amount. 

### Minimizing Training Error
If we chose a hypothesis function that has the smallest training error, we get the following: 
$$
\hat{h} = \text{arg min }(\hat{\epsilon}(h))
$$
Now we want to find how close is the $\hat{h}$ hypothesis, to $h^{\star}$ where we minimize the testing error. 
$$
h^{\star} = \text{ arg min } \epsilon(h) 
$$
And we want to find out how close these are. The whole problem that arises here is that we don't know what $h^{\star}$ is. That's by definition. 

## How Large Should Our Training Set Be?
Let's say that we have the probability that there exists a hypothesis function such that the inequality is met. 
$$
P(\exists h_{i} ) s.t |e(h_{i}) - \hat{e}(h_{i})|> \gamma)
$$
We know from probability that 
$$
\begin{align}

P(A \cup B)  & = P(A) +P(B) - P(A\cap B) \\
 P(A\cup B)  & \leq P(A) + P(B)
\end{align}
$$

And the term we have above, is basically a union. What is the probability of this, or that or that or that (where the that's are different values of $i$). Each one of these has their own Hoeffding's inequality. So, we have: 
$$
P(\exists h_{i} ) s.t |e(h_{i}) - \hat{e}(h_{i})|> \gamma) \leq \sum_{i=1}^{K} 2e^{-\gamma ^2{2}N}
$$
So what we get with this is: 
$$
P(\exists h_{i} ) s.t |e(h_{i}) - \hat{e}(h_{i})|> \gamma) \leq  K2e^{-\gamma ^2{2}N}
$$
Where $K$ is the number of hypothesis. 
### Size of Training Set
Now, let's find the probability that there does **not** exist a hypothesis where the difference between the training and test error is greater than $\gamma$ would be 

$$
P(\cancel{ \exists } h_{i} ) s.t |e(h_{i}) - \hat{e}(h_{i})|> \gamma) \geq  1 - K2e^{-\gamma ^2{2}N}
$$
Let's call $2Ke^{-\gamma ^{2}2N}$ as $\delta$. Given $\delta$, we want to have it be as small as 1. This is because we want there to exist a hypothesis that has a small difference. Another way is how large should $N$ be in this case? In this case $N$ is our training set. 
$$
N \geq \frac{1}{2\gamma ^{2}} \log\left(\frac{ 2k}{\delta}\right)
$$
## How close Are $\hat{h}$ and $h^{\star}$?
We know that $\epsilon(\hat{h})$ is the smallest, by definition. So in terms of the inequality, we have: 
$$
\epsilon(\hat{h}) \leq \hat{\epsilon}(\hat{h}) + \gamma
$$
From this, we have the ERM hypothesis that is
$$
ERM \leq \hat{\epsilon}(h^{*}) + \gamma
$$
We know that $h^{\star}$ minimizes the test error. However, we know that if we compute the error of this. 

Now, if we compute the error of $h$, that is: 
$$
\leq\epsilon(\hat{h^{*}}) + \gamma + \gamma
$$
The reason for this, is that we know that $\hat{\epsilon}(h)$ is bounded, and then $\hat{\epsilon}(h^{\star})$ is also bounded. 

### Result
So from this, what we get is: 
$$
\begin{align}
 |\epsilon(h) - \hat{\epsilon}(\hat{h})| & <\gamma \\
\epsilon(h) \leq\hat{\epsilon}(\hat{h})  & + \gamma \\
\epsilon(\hat{h})\leq\epsilon(h)  & + \gamma \
\end{align}
$$
Is what we can determine . 

$$
\epsilon(\hat{h}) \leq\epsilon(h^{\star}) + 2 \gamma
$$
## Theorem: Generalization Bound
Suppose $H$ is the hypothesis space and $m$ is the number of training samples, and let's say $\delta$ is a fixed value.  $1 - \delta$ is the probability that there does not exist a hypothesis that meets the inequality. So , 
$$
\epsilon(\hat{h}) \leq \text{min }  \epsilon(h) +  2 \sqrt{ \frac{1}{m} \log\left( \frac{2k}{\delta} \right) }
$$
In this case, $\epsilon(\hat{h})$ is the **true** error, or the generalization error, of the chosen hypothesis. That is it's the probability that $h$ makes a mistake on new data. We select $\hat{h}$ based on training data. Similarly, $\epsilon(h)$ is the true error of a hypothesis $h$. That means the error (or test error) of a hypothesis $h$ in the space
 
The first term, represents the error of the best possible hypothesis in the given hypothesis space.
.What this means, is that the training error is close to the training error by the amount in the $2$. 
$$
H = \{ h_{1}, h_{2}, \dots,h_{k} \}
$$
What this means, is that a smaller hypothesis space means our bias is increased.  What this does is captures bias invariance. 

However, in this case $k$ is assumed to be a finite number of hypothesis. If $k$ is infinite, then what happens? The $k$ captures the size of the hypothesis class. 

### VC Dimension
if $H$ is our hypothesis space![[1_qFUj7Ivs5TnZoULaic3Z2w.png|center|425]]
Instead of $k$, it uses the $VC$ dimension of space. We won't be doing this, and is outside the scope of the lecture. 

### Bias variance Trade off
This bound captures the classic **bias-variance tradeoff**:
- If you choose from a **larger hypothesis space** (larger $k$), you have a better chance of picking a low-error hypothesis, but the risk of overfitting increases.
- If you have **more training data** (larger $m$), you can generalize better, reducing the gap between training and true error.

# Summary
The main takeaway of this section is that it is in our interest to find out how close the training error and the testing error are. These are bounded by an inequality which can be used to determine that the hypothesis that gives the smallest training error is bounded by the training error. 