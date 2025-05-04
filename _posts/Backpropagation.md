---
title: Backpropagation
date created: Friday, December 13th 2024, 8:06:33 pm
date modified: Friday, December 13th 2024, 8:06:47 pm
Reference: http://neuralnetworksanddeeplearning.com/chap2.html#warm_up_a_fast_matrix-based_approach_to_computing_the_output_from_a_neural_network
---
 Definition
Backpropagation is an algorithm that shows how for a single training example, how the weights and biases should be nudged. It's also an understanding of how changing the weights and the biases in the network changes the cost function. 

In other terms, it is a way of leveraging the chain rule from multi-variate calculus to find the gradient of the cost function.
# Problem 

> [!weekly]- Reminder on notation
> ![[Other Fields/Machine Learning/Neural Networks#Representation]]

During the training of a neural network, the objective is to make the final neuron which gives the output be positively "nudged" compared to the other neurons. For example, in the hand written number detection problem, if the number 9 is to be detected, we want (with each epoch), the weights and biases that decide that 9 is the output to be such that weight of the cost function for 9 is increased. 

This can be done in 3 ways. First, the activation of each neuron is simply 
$$
a^{l}_{j} = \sum _{k}(W^{l}_{jk}a^{l-1}_{k} + b^{l}_{k})
$$
now from this equation we can see that the way we change what $a_{i}$ is we can 
1. Increase the bias $b$
2. Increase the weights. This works best when $w_{i}$ is changed in proportion to $a_{i}$. For example, the neurons in the previous layer which contribute the most to 9 have their weights increased proportionally. That is increase those which have the highest activation. 
3. Change what $a_{i-1}$ is. Or change what the activation in the previous layer is. 

# Computing 

The ultimate goal of backpropagation is to compute the partial derivatives $\frac{ \partial C }{ \partial w }$ and $\frac{ \partial C }{ \partial b }$. of the cost function $C$ with respect to the weight. We are using the Quadratic cost function here. 

![[Cost Function#Quadratic cost]]

The way this is done is by considering an intermediate quantity, error, as
$$
\delta^{l}
$$

which is a vector of the errors for the $l^{th}$ layer. 

For backpropagation two assumptions are made. 
# Assumptions
## The Cost function  is  $C = \frac{1}{n}\sum _{x}C_{x}$
That is, that the cost function can be written as the average of the individual cost functions for each training example. This holds true for most of the generally used cost functions, including the one above

This is where statistics comes into play. It is very costly (in terms of computation) to calculate the cost function. What we leverage is that by averaging a subset, we get an [[Estimating|estimate]] of what the cost function will actually be. We know from the central limit theorem, that as the sample size increases, the mean of the distribution converges to the true value. 

That means that we calculate a subset of $\frac{ \partial C_{x} }{ \partial w }$ and $\frac{ \partial C_{x} }{ \partial w }$ for a single training example and then recover $\frac{ \partial C }{ \partial w }$ and $\frac{ \partial C }{ \partial b }$ by averaging over the training examples. With this assumption in mind, we'll suppose that the training example $x$ has been fixed. 

## The cost can be written as a function of the outputs
That is, 
$$
\text{cost } C = C(a^{L})
$$
![[Pasted image 20241214092430.png|center|400]]
This lets us write the cost for a single training example as follows 
$$
C = \frac{1}{2}(y - a^{L})^{2} = \frac{1}{2}\sum _{j}(y_{j}- a^{L}_{j})^{2}
$$
# Error 
The error is an intermediate quantity $\delta^{l}_{j}$. 
![[Pasted image 20241224093812.png|center|425]]
The error can be thought of as a demon residing in one of the neurons. We know that the activation of the $j^{th}$ neuron can be written as 
$$
a^{(L)}_{j} = \sigma(z^{(L)}_{j})
$$
however, the error introduces a quantity $\Delta z^{l}_{j}$ such that what actually happens is 
$$
a_{j}^{(L)} =\sigma(z_{j}^{(L)} + \Delta z^{l}_{j})
$$
This change propagates through all the layers in the network, and changes the overall cost by 
$$
\frac{ \partial C }{ \partial z^{l}_{j} } \Delta z^{l}_{j}
$$
We assign the loss function in a way such that a value of $\Delta z$ is used to make the cost smaller for the $j^{th}$ neuron. If $\frac{ \partial C }{ \partial z^{l}_{j} }$ is close to zero, then changing the $z$ or the weight, does not really change the cost function at all. So the value of $\Delta z$ would be very small. So in a heuristic (loosely defined) sense, this can be thought of as the *error* of the neuron. That is, how far it deviates from the ideal value of $z_{j}$ that would give the ideal $a_{j}$.  

This lets us define the error as
$$
\delta^{l}_{j} \equiv \frac{ \partial C }{ \partial z^{l}_{j} }
$$
### Note
While we know the thing actually changing the cost function is the activation $a_{j}$. However, it turns out that this makes the algebra much more difficult later on. So thinking of it as $z$ as the parameter that changes the error is easier, and not incorrect. 

# Intuitive proving
This is based on this [3Blue1Brown video](https://www.youtube.com/watch?v=tIeHLnjs5U8&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=4)and the reference for this note. This does make sense, but  the next section which has a more rigorous proof made more sense to me. 

To make this easier, we can represent the cost as follows: 
$$
C_{0}(\dots) = (a^{(L)}-y)^{2}
$$
What this means, is that the cost is the difference between the target output $y$ and the activation of the final neuron in the $L^{th}$ layer $a^{(L)}$ squared. We can write $a^{(L)}$ as 
$$
a^{(L)} = \sigma(a^{(L-1)}w^{L} + b^{L})
$$
The right hand side of this is used extensively in mathematics, and subsequent derivations. So we can represent this as the intermediate $z^{(L)}$ which is
$$
\begin{align}
z^{(L)}  & =  (a^{(L-1)}w^{L} + b^{L}) \\
 a^{(L)} & = \sigma(z^{(L)})
\end{align}
$$
The idea of backpropagation is to find how the cost function changes with the weight of of the last neuron. Or in terms of partials, $\frac{ \partial C_{0} }{ \partial w^{(L)} }$ 
Thinking about it logically, a change in $w$ gives us a change in $z$ which gives us a change in $a$ which is what ultimately changes $C$. So we can actually rewrite this as 
$$
\frac{ \partial C_{0} }{ \partial w^{(L)} } = \frac{ \partial C_{0}   }{ \partial a^{(L)} }\frac{ \partial a^{(L)} }{ \partial z^{(L)} } \frac{ \partial z^{(L)} }{ \partial w^{(L)} }   
$$
Now if we compute the relevant derivatives, we get
$$
\begin{align}
\frac{ \partial C_{0} }{ \partial a^{(L)} }  & =  \frac{ \partial (a^{(L)}-y)^{2} }{ \partial a^{(L)} }  \\
 & = 2(a^{(L)} - y)(1)
\end{align}
$$

![[Activation functions#Derivation of the sigmoid]]
$$
\begin{align}
\frac{ \partial a^{(L)} }{ \partial z^{(L)} }  & = \sigma(z^{(L)})'  \\
 & = \sigma(z^{(L)})(1 - \sigma(z^{(L)}))
\end{align}
$$
$$
\begin{align}
z^{(L)}  & =  (a^{(L-1)}w^{L} + b^{L}) \\  
\frac{ \partial z^{(L)} }{ \partial w^{L} }  & = a^{(L-1)}
\end{align}
$$
## Cost function with respect to weight
Putting this all together, we get

$$
\begin{align}
\frac{ \partial C_{0} }{ \partial w^{(L)} }  & =  2(a^{(L)} - y) \cdot \sigma(z^{(L)})(1 - \sigma(z^{(L)})) \cdot a^{(L-1)}
\end{align}
$$
However, this is the cost for a specific training example. (in this case it is for $C_{0}$). Hence, the average of the direction of the cost function across all the training examples gives us an overall picture of the change of the cost function with the weight. 

$$
\frac{ \partial C }{ \partial w^{(L)} } = \frac{1}{n}\sum_{k=0}^{n-1}  \frac{ \partial C_{k} }{ \partial w^{(L)} }
$$
## Cost function with respect to the bias
This itself, is one component of the gradient of the cost. We have only found a general equation for the change of $w$ in a single layer. This will also be the case for the biases in the other layers as well. 

$$
\frac{ \partial C_{0} }{ \partial b^{(L)} } = \frac{ \partial C_{0}   }{ \partial a^{(L)} }\frac{ \partial a^{(L)} }{ \partial z^{(L)} } \frac{ \partial z^{(L)} }{ \partial b^{(L)} }   
$$
Which simplifies to 
$$
\begin{align}
\frac{ \partial C_{0} }{ \partial b^{(L)} }  & =  2(a^{(L)} - y) \cdot \sigma(z^{(L)})(1 - \sigma(z^{(L)})) 
\end{align}
$$

## Cost function with respect to the activation in the previous layer

$$
\frac{ \partial C_{0} }{ \partial a^{(L-1)} } = \frac{ \partial C_{0}   }{ \partial a^{(L)} }\frac{ \partial a^{(L)} }{ \partial z^{(L)} } \frac{ \partial z^{(L)} }{ \partial a^{(L-1)} }   
$$
$$
\begin{align}
\frac{ \partial C_{0} }{ \partial a^{(L-1)} }  & =  2(a^{(L)} - y) \cdot \sigma(z^{(L)})(1 - \sigma(z^{(L)}))\cdot w^{(L)}
\end{align}
$$
Now this can be iterated back recursively to find how the $z^{(L-k)}$ and subsequent layers would behave with respect to this. 


# Proofs for the Equations for Backpropagation
This part of the note is more based on the proof from the t

There are 4 equations for Backpropagation. These are: 
1. Error in the output layer, $\delta^{L}$
2. Error in $\delta^{L}$ in terms of $\delta^{L+1}$, that is the error in the next layer
3. The rate of change of the cost with respect to the bias 
4. The rate of change of the cost with respect to any weight in the network 

## Error in the output layer 
By definition, we know that 
$$
\delta^{L}_{j} = \frac{ \partial C }{ \partial z^{L}_{j} }

$$
Since we want to know the error in the output layer, we can use the chain rule to get the following:
$$
\begin{align}
\delta^{L}_{j}  & =  \frac{ \partial C }{ \partial z^{L}_{j} } =\sum_{k}^{} \frac{ \partial C }{ \partial a^{L}_{k} } \frac{ \partial a^{L}_{k} }{ \partial z^{L}_{j} }  
\end{align}
$$
Initially I was confused as to why we are summing over all the neurons $a_{k}$ in the last layer. We are interested in seeing how the cost function changes according to the input to one neuron, that is $z_{j}$. The cost changes **independently** based on the output of the final activations for each of the neurons. So we need to find the contribution each individual neuron makes to the total cost function, with respect to the input $z_{j}^{L}$. In a way, this step is just a formality, but it was confusing. 

Even in probability, when we have two events that are independent, the probability that at least one occurs is just the sum of the two minus the probability that they both occur. Because they are independent. That's where the summing over comes from. We are finding the total contribution to the cost function. 

But, we know that $z_{j}$ will only affect the change of $a_{j}$. That is, when $k=j$. Hence, the other summations vanish, and we get: 

$$
\delta^{L}_{j} = \frac{ \partial C }{ \partial a^{L}_{j} }\frac{ \partial a^{L}_{j} }{ \partial z^{L}_{j} }  
$$
However, we know that $a_{j} = \sigma(z_{j})$. So the partial derivative, is just the derivative of $\sigma(z_{j})$. or, 

$$
\begin{equation}
\delta^{L}_{j} = \frac{ \partial C }{ \partial a^{L}_{j}}\sigma'(z^{L}_{j}) 
\end{equation}
$$
The above equation can be rewritten as : 
$$
\delta^{L} = \nabla _{a}C \odot \sigma'(z^{L})
$$
Where $\nabla _{a}C$ is a vector who's components are the partial derivates $\frac{ \partial C }{ \partial a^{L}_{j} }$. It expresses the rate of change of the cost function with respect to the output activations. 

In the case for when $C$ is the quadratic cost function, we have: 
$$
\delta^{L} = (a^{L}-y)\odot \sigma'(z^{L})
$$
This is now in the state that can be calculated by a computer. 
## Error in the next layer
We now want to rewrite the cost in terms of the derivative of the next layer. So, 

$$
\begin{align}
\delta^{L}_{j}  & = \frac{ \partial C }{ \partial z^{l}_{j} } \\
  & =\sum \frac{ \partial C }{ \partial z^{l+1}_{k} }\frac{ \partial z^{l+1}_{k} }{ \partial z^{l}_{j} } \\
 & = \sum\frac{ \partial z^{l+1}_{k} }{ \partial z^{l}_{j} } \delta^{L+1}_{k}  
\end{align}
$$
The first derivative can be evaluated as follows
$$
z^{l+1}_{k} = \sum_{j=1}^{N}  w_{kj}^{l+1}a^{l}_{j}+ b^{l+1}_{k}
$$

Interpreting this in words: 
- the input $z_{k}$ is the input to the $k^{th}$ neuron in the $l+1^{th}$ layer. 
- This is equal to the sum of the activations of all of the $j^{th}$ neurons in the $l^{th}$ layer after having their weights adjusted. The matrix which does this adjusting is $w_{kj}$ which gives us the inputs from the $j^{th}$ neuron to the $k^{th}$ neuron. At the end, we have the bias to the $k^{th}$ neuron. 

Now, we want to find out how does this change, with respect to the input to the $j^{th}$ neurons. This would be, 

$$
\begin{align}
\frac{ \partial z^{l+1}_{k} }{ \partial z^{l}_{j} }  & = w^{l+1}_{kj}\sigma'(a^{l}_j) 
\end{align}
$$
As any neuron which is not the $j^{th}$ neuron will not be affected. Similar to the previous step. This gives us the form: 

$$
\delta^{l}_{j}= \sum_{k=1}^{N} w^{l+1}_{kj}\delta^{l+1}_{k}\sigma'(z^{l}_{j})
$$

>Reminder on notation
>The notation $w_{jk}$ defines the connection TO $j$ FROM $k$. It's confusing and I wish this book used a different notation here, but basically, this $k$ is different from the $k$ used in the previous section. 
>An easier way to think of this would be: we want to identify the weight matrix in terms of the **next** layer. In order to do that, we go FROM $j$ TO $k$




Similarly to the previous section, we can present this in terms of the Hadamard product
$$
\delta^{l}_{j} = (w^{l+1})^{T}_{}\delta _{}^{l+1}\odot\sigma'(z^{l})
$$
If we know the error $\delta^{l+1}$ in the $l+1^{th}$ layer, applying the transpose of the weight matrix can be though of moving the error backward through the network. 

If we think of the weight matrix and moving us to a space from one error to the next, it's inverse would bring us back to the original position or the error in the $l^{th}$ layer. The Hadamard product move the error through the activation layer, and gives us the error $\delta^{l}$ in the weighted input to layer $l$. 

$\delta^{l}$ can be thought of as the change in the Cost function as per the the change in the weighted input $z^{l}$. With these two equations 
$$
\begin{align} \\
\delta^{l}  & = (a^{l}-y)\odot \sigma'(z^{l}) \\

\delta^{l}_{}  & = (w^{l+1})^{T}_{}\delta _{}^{l+1}\odot\sigma'(z^{l})
\end{align}
$$
We can find the error in any layer. That is, by getting the error of the last layer, we can then move backwards, to get the error in any layer. 

## Rate of change of cost with respect to the bias
Similarly, 
$$
\delta _{j}^{L} = \frac{ \partial C }{ \partial z_{j}^{L} } 
$$
Using the chain rule again, 
$$
\begin{align}
\delta^{L}_{j}  & = \sum _{k}\frac{ \partial C }{ \partial b^{L}_{k} }\frac{ \partial b^{L}_{k} }{ \partial z^{L}_{k} }   \\
 & = \frac{ \partial C }{ \partial b^{l}_{j}} \frac{1}{\frac{ \partial z^{L}_{j} }{ \partial b^{l}_{j} } } \\
 &= \frac{ \partial C }{ \partial b^{l}_{j} } \frac{1}{1}  \\
\delta^{l}_{j}  & = \frac{ \partial C }{ \partial b^{l}_{j}} 
\end{align}
$$
With the previous two equations, know how to compute $\delta^{l}$. As the rate of change of bias is the same as $\delta^{l}$ we can write this more generally as 
$$
\frac{ \partial C }{ \partial b }  = \delta
$$
In the case where $\delta$ is being evaluated at the same neuron as the bias $b$. 
## Rate of change of weight with respect to the bias 
Similarly, 
$$
\delta _{j}^{L} = \frac{ \partial C }{ \partial z_{j}^{L} } 
$$
$$
\begin{align}
\delta^{L}_{j}  & = \sum _{k}\frac{ \partial C }{ \partial w^{L}_{jk} }\frac{ \partial w^{L}_{jk} }{ \partial z^{L}_{k} }   \\
 & = \frac{ \partial C }{ \partial w^{L}_{jk}} \frac{1}{\frac{ \partial z^{L}_{j} }{ \partial w^{L}_{jk} } } \\
 &= \frac{ \partial C }{ \partial w^{L}_{jk} } \frac{1}{a^{l-1}_{k}}  \\
a^{l-1}_{k}\delta^{l}_{j}  & = \frac{ \partial C }{ \partial w^{L}_{jk}} 
\end{align}
$$
This lets us know how to compute the change in the weights in terms of the previous activation and the error. We know what this is from the other equations. So, we can write this as: 
$$
\frac{ \partial C }{ \partial w } = a_{\text{in}}\delta _{\text{out}}
$$
where $a_{in}$ is the activation of the neuron input to the weight, and $\delta _{out}$ is the error of the neuron output from the weight $w$. 
![[Pasted image 20241226211757.png|center|320]]
We can see from this, that when the activation is small, $a_{in} < \epsilon$, then the rate of change is also very small. In other words, the weights output from low-activation neurons learn very *slowly*. 

Also based on the [[Activation functions#Definition|sigmoid function]], we see that at later values, the function is very flat. Hence, if the activation is very high, or very low, the change is minimal. This is called the "saturation" point. 

## Findings from the equation
A weight will learn slowly if either the input neuron is low activation, or if the output neuron has saturated. 

This is an interesting idea as to why other activation functions, such as ReLU are used. 

# The Algorithm
This can be written in the form of an algorithm as follows
## Input
$x$ is the input. It's a vector that sets the activation $a^{1}$ for the input layer. 

## Feed forward
For each $l = 2, 3, \dots, L$ compute 
$$
z^{l} =w^{l}a^{l-1} + b^{l}
$$
and 
$$
a = \sigma(z^{l})
$$
## Output error 
The error in the final layer can be calculated as follows
$$
\delta^{L} = \nabla _{a}C \odot \sigma'(z^{L})
$$
## Backpropagate the error
For each layer, calculate
$$
\delta^{l} = ((w^{l+1})^{T}\delta^{l+1})\odot \sigma'(z^{l})
$$
## Output
The gradient of the cost function is given by 
$$
\frac{ \partial C }{ \partial w^{l}_{jk} }= a^{l-1}_{k}\delta^{l}_{j} 
$$
and with 
$$
\frac{ \partial C }{ \partial b^{l}_{j} } = \delta^{l}_{j}
$$
A **reminder** that the gradient is a vector with the changes to the weight and the biases. 


> [!weekly]- Exercises
>![[Exercises on Backpropagation]]


![[Stochastic Gradient Descent]]

# What next? 
There are other questions related to back propagation, like the proofs themselves, and how they came up. 