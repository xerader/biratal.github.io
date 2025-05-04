---
title: Definition
date created: Wednesday, December 4th 2024, 2:58:58 pm
date modified: Wednesday, February 5th 2025, 5:21:52 pm
Ref: https://towardsdatascience.com/convolutional-neural-networks-explained-9cc5188c4939
tags:
  - "#engs106"
  - "#machinelearning"
---
# Definition
These are a type of [[Other Fields/Machine Learning/Neural Networks]] that is best at processing image with a grid-like structure or topology, such as an Image. This is a feed-forward artificial neural network. The calculation that is performed at each layer is a "convolution". 

# Architecture
They generally have three [[Layers]]: 
1. a convolutional layer
2. a pooling layer
3. a fully connected layer

![[Pasted image 20241204150100.png|center|650]]

## Convolution Layer
### The Idea
The majority of the computation happens here. In essence it is a matrix operation between a kernel and the data. The "depth" of the data and the kernel must be the same, but the kernel will almost always be much smaller in dimension to the data itself. 

When we see something with our eyes, we don't look at everything all at once. Maybe at a glance we see a cup. When we look more closely we'll see the details of the cup. Only things that are right in front of us, is what we are looking at. That's kind of how a CNN works as well. It only looks at things in it's **receptive field**, or the kernel. 

https://www.ibm.com/topics/convolutional-neural-networks

The kernel can also be thought of as a "filter". The way this works is that the kernel applies a sliding window across the entire data. As it does this, it finds out what exactly is inside the data, and the kernel operations find what is "seen" within it. 
![[Pasted image 20241204151626.png|325|center|425]]
The output  of the kernel layer is a series of dot product of the input and the kernel. This is called the **feature map**, **activation map** or a **convolved feature**. 

### Hyperparameters
The hyper parameters that are used are 

**The number of filters**
This affects the "depth" of the output. This means how many feature maps are created. I think feature maps can only be in 2D, so that means you can have $n$ number of 2D feature maps for a 3D feature map. Like when you are processing an image that has different channels.

**Stride**
This is the number of pixels that the kernel moves over the input matrix. Larger strides give smaller inputs (makes sense) 

**Zero-padding**
This is when the kernel does not fit the input image. So all elements that are outside of the input matrix are set to zero. this produces a larger or equally sized output. We have
- valid padding, or no padding
- same padding, so that the output layer is the same size as the input layer
- full padding, that increases the size of the output by adding zeros the place around the input #confusion why do this? 

After each of these an [[Activation functions#Rectified Linear Unit|ReLU]] function is applied for non linearity.

## Mathematical Approach
Say we have a 6x6 image that is all black on the left and all white on the right. (1 on left and 0 on the right). So this is 36 nodes on vectorizing it. 

Out of the 36 nodes, we need to connect it to 9 things. Those 9 parameters can be represented as 9 nodes. These are the parameters. Those 9 parameters will be shared among all of the nodes. So, after training we have, 
$$
\begin{bmatrix}
1 & 0 & -1 \\
1 & 0 & -1 \\
1 & 0 & -1
\end{bmatrix}
$$
Which will being to detect the edges
