---
title: Underfitting
tags:
  - "#qbs108"
Ref:
date created: Tuesday, April 22nd 2025, 3:32:42 pm
date modified: Tuesday, April 22nd 2025, 4:54:27 pm
---
![[Pasted image 20250422153400.png]]

# Underfitting
- When the model does not capture the entire complexity of the data

## Bias and Variance
Bias is like the **accuracy** of the model. 
Variance is the **spread** of the results of the data. 

![[Pasted image 20250422154714.png|center|425]]

# Ensemble Learning
- Combine multiple models to improve performance 
**Pros**
- Low Variance
- Fast, do not need hyperparameter tuning
**Cons**
- High bias
- Not adequate for complex problems/datasets
## Base Learners
- The individual models are weaker 

**Diversity**
- If you have different models, such as model 1 and model 2. It maybe that one model is better at classifying something, and the other is better at regression. 

**Aggregation Methods**
- Majority voting (Classification)
- Averaging (Regression)
- A Meta-learner assigns different weights to the prior models in this case. This is for a weighted average

## Stacking
- Combine different base learners that feeds into another model that is the same
- This has a risk of **overfitting**, and has a **longer train time**. 

## Bagging (Bootstrap Aggregating)
Often you don't know the distribution of the training data looks like. Why? I guess if it's an LLM or something. Good for training models prone to high variance 
- Train multiple models on random subsets from the data **with replacement**. This is called [[Bootstrap|bootstrapping]]. 

# Random Forest
## Training
- Ensemble learning method to combine multiple methods
- Create multiple bootstrap replicates from the dataset
- Train a decision tree on each bootstrap replicate
	- Use a random subset of features at each split 
	- The feature size is a constant fraction, e.g., the square root, of all features
- Each decision tree is deep with no pruning
	- Stopping criterion: A leaf has too few examples or the max depth is reached
	- Each tree is high variance and low bias 
- Aggregate the tree predictions using majority voting (classification) or averaging (regression). 
### Hyperparameters
- Number of trees
- Max tree depth
- Min samples per leaf
- Num of features at each split 
### Feature Importance
- Measures feature importance by measuring the decrease in impurity (entropy or Gini impurity) for each feature across all trees
## Evaluating RF (Out of Bag)
- Samples that are not using in Tree $T_{1}$ are used for evaluation. Similarly for the other Trees. 

# AdaBoost and Boosting
## Method
- Weighting different decision trees by different weights accordingly. 
- Train a base learner on the entire dataset
- Sequentially train additional learners focusing on misclassified instances
	- Update the instance weights to emphasize difficult examples

**Iterative Method**
For each iteration $t$, 
- Weigh each training example based on how incorrect it classified on the last iteration
- Learn a base learner - $h_t$
- Weigh the base learner based on how well it fits the training set - $\alpha _{t}$

**Aggregation**
Classification: $H(X) = sign\left( \sum _{t}\alpha _{t}h_{t}(X) \right)$
Regression: $H(X) = \sum_{t}^{}\alpha _{t}h_{t}(X)$

# Gradient Boosting Process
- Initialize the model with a constant function. 
- Sequentially train base learners on the negative gradients of the loss function. 
- Instead of predicting the value, it is to predict the error at each RF. 
	- Compute the residuals from the current model 
	- Fit a new learner on those errors
	- Update the model by adding this new learner multiplied by a learning rate 
- Repeat until a stopping criterion is met. 




