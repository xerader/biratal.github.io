---
excalidraw-plugin: parsed
tags:
  - excalidraw
excalidraw-open-md: true
References: https://web.stanford.edu/~jurafsky/slp3/9.pdf
---
#llms #machinelearning
# Definition
A transformer is a [[Other Fields/Machine Learning/Neural Networks|neural network]] with a specific structure that includes a mechanism called **self-attention** or **multi-head attention**. This can be thought of as a way of having a contextual representation of what a token means by looking at the surrounding tokens. This allows the model to learn how tokens relate to each other over large [[Notes on Linear Algebra#Span|spans]]. 

Some jargon:
The term **head** is used in transformers to refer to specific structured layers
![[Pasted image 20241211172408.png|center|450]]
A transformer is made of three major components, 
1. Input encoding
2. Transformer Blocks
3. Unembedding
![[Transformer 2024-12-30 13.28.10|center]]
# Input Encoding
This process an input token (like the word thanks) into a contextual vector representation. An [[Vector Semantics|embedding]] matrix $E$ and a mechanism for the encoding token position is used. The thing that makes this embedding different is that it also encodes the position of the word in the document. 

# Attention Head
This is the version of [[Attention|attention]] used in Transformers. 
- The representation of the current element when it is being compared to the previous ones. This is a **query**. This can also be thought of as a "question" 
- The representation of an element when it is a previous input that is being compared to the current element to find a weight. this is a **key**. That is that it is being compared to a query.  
- Finally we get a value which is the preceding element that gets weighted and summed up to compute the output for the current element. 

To capture these three different roles, we introduce weight matrices accordingly, 
$$
q_{i} = x_{i}W^{Q}, k_{i} = x_{i}W^{K}, v_{i} = x_{i}W^{V}
$$
These weights are projecting the input vector into the role it has to play. 
$$
\begin{aligned}
\mathbf{q}_i=\mathbf{x}_i \mathbf{W}^{\mathbf{Q}} ; \mathbf{k}_j & =\mathbf{x}_j \mathbf{W}^{\mathbf{K}} ; \quad \mathbf{v}_j=\mathbf{x}_j \mathbf{W}^{\mathbf{V}} \\
\operatorname{score}\left(\mathbf{x}_i, \mathbf{x}_j\right) & =\frac{\mathbf{q}_i \cdot \mathbf{k}_j}{\sqrt{d_k}} \\
\alpha_{i j} & =\operatorname{softmax}\left(\operatorname{score}\left(\mathbf{x}_i, \mathbf{x}_j\right)\right) \forall j \leq i \\
\mathbf{a}_i & =\sum_{j \leq i} \alpha_{i j} \mathbf{v}_j
\end{aligned}
$$
What I don't understand here is why are queries and keys different? Won't the representation of whether the word is current or previous be the same? 

![[Pasted image 20241230143412.png|center|425]]
