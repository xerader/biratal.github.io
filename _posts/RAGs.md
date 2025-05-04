---
title: RAGs
date created: Sunday, December 29th 2024, 8:49:56 am
date modified: Sunday, December 29th 2024, 8:51:17 am
Ref: https://web.stanford.edu/~jurafsky/slpdraft/14.pdf
---
#llms #machinelearning 
# Definition 
a **RAG** stands for retrieval-augmented generation. [[Other Fields/Machine Learning/NLP/Information Retrieval|Information Retrieval]] is used to retrieve documents that are likely to have information that can answer the question being asked. Then the LLM uses this input to answer the question 

It's made up of two components: 
1. The retriever
2. The reader

# Problems in LLMs
1. Hallucination 
2. Calibration $\to$ assume everything is correct
3. Up-to date information after release of the LLM. 

# RAGs
In the first part, we **retrieve** relevant passages from a text collection. For example, by using the dense retrievers of the previous section. In the second **reader** stage, the answer is generated via **retrieval-augmented generation**. 

![[Pasted image 20250103222648.png]]
In this case, we get the [[Information Retrieval#Inverted Index|index]] for the documents and use that along with other text as its prompt and then autoregressively generate a new answer, token by token. 

When looking at this probabilistically, we have the following:
$$
p(x_1, ..., x_n) = \prod_{i=1}^{n} p(x_i | R(q); prompt; [Q:]; q; [A:]; x_{<i})
$$
## Multi-hop architectures
For more complex questions. The query is used to get the documents, these are then appended to the original query for a second stage of retrieval. 

# Evaluating Question answering 
There are ways to evaluate a RAG. The idea is to have a set of questions and answers that the RAG model can be tested upon. It is ranked based on retrieval and question answering. It's one of the ways modern LLMs are tested. With retrieval is an **open book** task, and without is a **closed book** 

The format of the answer and the prompting also makes a difference

## Zero shot
Is when the prompt is just the question 

## few-shot
Is when the prompt also contains example answers. 