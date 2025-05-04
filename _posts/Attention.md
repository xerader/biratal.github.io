---
title: Attention
date created: Monday, December 30th 2024, 1:53:00 pm
date modified: Monday, December 30th 2024, 1:53:06 pm
---
#machinelearning #llms 
# Attention
Attention is the mechanism in the transformer that weighs and combines the representations from appropriate other tokens in the context from layer $k-1$ to build the representation for tokens in layer $k$.
![[Pasted image 20241228135258.png|center|425]]
We know from the static embeddings we saw before that words will have an embedding of the representation of the word. However, a word can mean different things based on **context**. Like

"The dog ran around the park because **it** was excited"
"The dog ran around the park because **it** was open"

The word **it** has multiple different meaning in this case. It's through analyzing the **context** parallelly that the transformer is able to find out the meaning of the word. This is called a **contextual embedding**.

## Context Window
The idea is that it uses the embeddings in the previous layer to define the embeddings in this layer. 

A **context window** is a range of words or tokens. This can be up to thousands of tokens. 

When processing the $x_{i}^{th}$ token, where $x_{i}$ represents the $i^{th}$ token, the contextual embedding model has access to $x_{1}\dots x_{i-1}$.  This can be generalized to look ahead as well. 

## Self-attention Layer
It maps inputs to outputs. Just like any other layer. 

![[Pasted image 20241230134048.png|center|425]]
We can see that in this case that $x_{i}$ uses the values behind it. 

## Simplified Version
Attention is a weighted sum of context vectors. 

Let us assume that the output $\alpha_{i}$ is the weighted sum of all the representations $x_{j}$ for all $j \leq i$; we'll use $\alpha _{ij}$ to mean how much $x_{i}$ should contribute to $\alpha_{j}$. 
$$
a_{i} = \sum_{j \leq i} \alpha _{ij}x_{j} 
$$
Each $\alpha _{ij}$ is a scalar that is used for weighing the value of the input $x_{j}$ when summing up the inputs to compute $a_{i}$. This is like the weights in a [[Other Fields/Machine Learning/Neural Networks#Weights|neural network]]. 

### Method of Weighing
The weights are assigned proportionally to how similar it is to the current token $i$. This is calculated using the dot product. 

$$
\begin{align}
\text{score}(x_{i}, x_{j}  )  & = x_{i}\cdot x_{j} \\
\alpha _{ij}  & = \text{softmax}(\text{score}(x_{i},x_{j}))  & \forall j \leq i
\end{align}
$$
So for $x_{3}$ there would be 3 scores calculated: a dot product with $x_{1}, x_{2}$ and $x_{3}$. These are then normalized by [[Softmax|softmax]] and the resulting probabilities are weights which indicate their proportional relevance to the current position $i$. 

Obviously, it will be highest with itself, but there may be other words which also give higher weights. The softmax assigns a weight to those as well. This is used to compute the weighted sum for $a_{i}$. 
