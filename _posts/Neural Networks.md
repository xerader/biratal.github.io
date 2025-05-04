---
title: Definition
date created: Monday, November 25th 2024, 2:28:03 pm
date modified: Monday, November 25th 2024, 3:08:36 pm
Reference:
  - http://neuralnetworksanddeeplearning.com/
  - Bishop Chapter 5
---
#engs106 #machinelearning 
# Definition
Neural networks are computational models inspired by the human brain. They consist of layers of interconnected nodes (neurons) that process input data to discover patterns and make decisions. In the mathematical sense, the neuron is just a function that outputs a number. This number is called it's [[Activation functions|activation]]. Which is a number between 0-1.
# Layers
## Structure
The structure is generally made through three different parts of [[Layers]]. The idea as we saw in the [[Perceptron Model]] is to adjust the basis function $\phi$ around the input variables $x$ as well as the parameter $\theta$, or the weight $w$ as we call in this part. 
### Input Layer
This takes in the raw input features. Each neuron in this layer represents an input feature
### Hidden Layer
This can be one or more layer where the data is transformed. Weights and biases are applied to the inputs are passed through an [[Activation functions|activation function]]
### Output Layer
This is the network's final output.  The structure of this layer will be dependent on the task. Such as classification, regression etc. 

## How it Works
The activations in one layer leads to the activations in the other layer. This carries on, until the output layer. The neuron in the final layer which has the highest activation will be the networks output choice, or prediction. This could be what number an image of a handwritten number is, or what is the prediction of blood glucose after 30 minutes.

## Why Layers?
Analogous to how we think. How do we know something is an apple? One could be that it's red, or that it's shaped like an apple, maybe it tastes good. 

All of these are characteristics about what an apple is. Each of these characteristics could perhaps be a neuron in the second to last layer of a neural network. And the activation of these neurons would activate the "apple" neuron in the output layer. 

It provides a systematic way of approaching machine learning-based systems without making it too difficult. In this example we can see how in the image below, the second layer looks at pieces that would make up the "loop" of the 9. The second last combines them to create the two part of a "9".  

![[Pasted image 20241125145718.png| center| 300]]

# Weights
Weights are a number that are applied between the connections of the nodes/neurons in one layer to the ones in the other layer. The higher this number, the greater contribution that node provides. The weights are numbers that specify the strength of the connection. 

The value of the neuron in the second layer would then just be the weighted sum 
$$
\text{weighted sum} = \sum w_{n}a_n 
$$
So the value of neuron $n_{21}$ (first neuron in the second layer) would just be the sum of all the connections times the activation for the first layer. 

As connections for each neuron in the second layer will be different, each neuron may be focused on a different thing. This could be maybe a chunk of pixels for an image. 

For a case where we have $100$ neurons in the first layer and $10$ in the second layer we would have 
$$
\text{ total number of weights} = 100 \times 10 = 1000
$$
Just between one layer and the next. 


# Representation
The representation of these calculations is often shown as a matrix: 
$$
\left[\begin{array}{cccc}
w_{0,0} & w_{0,1} & \cdots & w_{0, n} \\
w_{1,0} & w_{1,1} & \cdots & w_{1, n} \\
\vdots & \vdots & \ddots & \vdots \\
w_{k, 0} & w_{k, 1} & \cdots & w_{k, n}
\end{array}\right]\left[\begin{array}{c}
a_0^{(0)} \\
a_1^{(0)} \\
\vdots \\
a_n^{(0)}
\end{array}\right]+ \left[\begin{array} \\
b_{0} \\
b_{1} \\
\vdots \\
bn
\end{array}\right]=\left[\begin{array}{c}
? \\
? \\
\vdots \\
?
\end{array}\right]
$$
where the matrix on the left are the weights of the individual connections and then adding the bias. So technically this is just a bunch of matrix multiplications. We can also write this as
$$
a^{1} = \sigma(Wa^{0} + b)
$$
Where $W$ is the matrix which contains all the weights, $a$ is a vector which defines the activation, and $b$ is the bias. 


## Notation of weights
The following notation is used in this section 
$W^{l}_{jk}$ is the weight for this connection from the $k^{th}$ neuron to the ($l-1$)$^{th}$ layer
to the $j^{th}$ neuron in the $l^{th}$ layer. Basically, the weight of the neuron in the previous layer to another neuron in the next layer. 

The entries of the weight matrix $W^{l}$ are the weights connecting to the $l^{th}$ layer of neurons. That means that the entry in the $j^{th}$ row and the $k^{th}$ column is $W^{l}_{jk}$.  
![[Pasted image 20241214082132.png|375|center|475]]
## Notation of biases
Similarly, we have: 
$b^{l}_{j}$ is the bias of the $j^{th}$ neuron to the $l^{th}$ layer. We should note that the bias is at the level of a neuron to a layer. So the number of biases is $\text{num of neurons} \times \text{ number of layers}$
![[Pasted image 20241214082405.png|500|center|350]]
With these notations, we can know that the activation of $a^{l}_{j}$ that is the $j^{th}$ neuron in the $l^{th}$ layer, is related to the activations in the $(l-1)^{th}$ layer. In other words, the activation of a neuron is given by the values of the activations in the previous layer, along with the respective weights and biases. We can write this in our new notation as 
$$
a^{l}_{j} = \sum _{k}(W^{l}_{jk}a^{l-1}_{k} + b^{l}_{k})
$$
$W^{l}_{jk}$ is the weight for this connection from the $k^{th}$ neuron to the ($l-1$)$^{th}$ layer
to the $j^{th}$ neuron in the $l^{th}$ layer. Basically, the weight of the neuron in the previous layer to another neuron in the next layer. 

Another way to think about this is as follows: 
1. We have a bunch of values in the $l^{th}$ layer. 
2. We want to find the value of the first neuron in the $l+1^{th}$ layer. 
3. The value of the first neuron is determined by the activations of all the neurons in the $l^{th}$ layer. This is our INPUT vector 
4. Each of those neurons have a specific weight or importance level to the next neuron. We multiply the values of each of those activations with the weight and add all of that up to get an activation value for the neuron we are thinking of. 
5. 
writing this in a compact way, we can also do: 
$$
a^{l} = \sigma(W^{l}a^{l-1} + b^{l})
$$
where $\sigma$ is the **vectorization** or the [[Activation functions|activation function]]
## Weighted Input
We can define an intermediate quantity called the *weighted input* to the neurons in the layer $l$ this would be 
$$z^{l}\equiv w^{l}a^{l-1} + b^{l}$$
So without the activation function $\sigma$ this is what's there just before. This can be useful later on

# Learning
Learning is just altering these individual weights and biases so that we get the final output.

## Compressing
The issue with this is that the weighted sum may yield a number which is not in the range of 0-1. To counteract this we use an [[Activation functions|activation function]] such as the sigmoid function to compress this. We can also use it to [[Activation functions#Bias|bias]] our data or what we are looking for. The bias can be thought of whether a particular neuron gets activated more often than not

## Execution
The way this is incorporated into the learning phase is as follows: 
1. All biases and weights are randomly assigned
2. The output of the output layer is used as an input into the [[Cost Function|cost function]]

However, our goal is to **minimize** the cost function. To do this, we use [[Gradient Descent]]



![[Gradient Descent]]

So this gives us an output of how we should change the weights in our model. The algorithm that is used to implement this efficiently is called [[Backpropagation|backpropagation]]. 

## Some weights matter more
From the algorithm we can see that the results of the cost function vary depending for each weight or neuron. What this means is that some neurons are more important than others. In my own research I saw that, when predicting the blood glucose levels of a type 1 diabetes patient, random things can definitely happen. 