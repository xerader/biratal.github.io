---
title: Training Factors
date created: Tuesday, November 5th 2024, 9:27:08 am
date modified: Monday, November 25th 2024, 1:51:55 pm
---
Note, these may turn into their own notes later on


# Training Factors
These are factors that we take into consideration when training models. These are 
1. Data Quality
	1. The accuracy and relevance of the data
2. Data Size
	1. The amount of data. Larger sample sizes.
3. Feature Selection 
	1. Which variables to include in the model
		1. Could using too many variables give us a worse determination of the relations we want. Done 
		
4. Hyperparameter Tuning
	1. The optimization of model parameters that are set before training. This is like the learning rate, the depth of trees in [[Random Forest Process]], number of layers for a [[Other Fields/Machine Learning/Neural Networks]]. 
5. Training Duration
	1. Amount of time spent training that can effect overfitting and underfitting. 

Potato pie is yummy

# Model Complexity
The intricacy of the model structure which includes the number of parameters and the types of models that are being used. 

This includes things like the architecture of the model (layers nodes etc.) and also the parameter count. Such as the parameters that would allow a model to learn more complex relations. 

Trade-off in complexity. There is a trade off between model complexity and the risk of overfitting. Simpler models may generalize better. More complex ones can begin to model the noise instead of the underlying trends. 


# Sampling Horizon
The range or window of data that is used to make predictions. 

A Forecasting horizon is how far into the future the model aims to predict. The training horizon is the length of historical data that is used to train the model. Too short a history will not capture the entire trend. 

Rolling windows or expanding windows are using in sampling horizons to make sure the models are trained only on the most relevant data. 

# Dependencies
These are the relationships between different parts of the input data across time or sequence steps. For example, the meaning of words later in a sentence can depend on words earlier on in the sentence. 

"It's not that that can't happen". The second "that" references something different to the first "that". The first that changes what the previous means. These dependencies need to be captured in an ML algorithm

# Gradients

## Vanishing and Exploding Gradients
There are gradient-based optimization methods like [[Other Fields/Machine Learning/Neural Networks#Back propogation|back propagation]]. When these gradients become too small, the learning is very slow and it is difficult for the model to learn long-range dependencies. 


# RMSE
Root mean squared data is 
$$
RMSE = \sqrt{ \frac{\left( \sum^n_{i = 1}(x_i - \bar{x}) \right)}{n} }
$$
# Long Short Term Memory (LSTM)
Type of [[Other Fields/Machine Learning/Neural Networks#RNN| Recurrent Neural Network]] that is designed to capture the long and short term [[#Dependencies]] in sequential data. This makes it useful for tasks when it is important to remember the information over a long period of time. 

Usual RNNS can struggle with learning long-term dependencies due to issues with vanishing and exploding gradients. 


# Overfitting


# LOOCV
