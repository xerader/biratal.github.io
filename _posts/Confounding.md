---
title: Default
tags: 
Ref:
---
# Confounding
If we have two variables, an explanatory one and a result, we can just get a correlation. But most of the times we have a third variable that can be a confounder. 
![[Pasted image 20250113103705.png|center|425]]
Which then distorts the association between $E$ and $R$. For a better output, we need a physical activity. 

### Using Logistic Regression 
We can examine the association of a binary endpoint and predictor of interest while accounting for one or more confounders

![[Pasted image 20250123100945.png]]
The model above examines associations of $Y$ and $X$ while allowing for associations of $Y$ with covariate $Z_{1}$, $Z_{2}$, $Z_{3}$. 

The covariates could all be continuous or binary, for instance.

### Controlling Them
By sampling: **Matching**
Create pairs, triads etc. of observations from different phenotypic groups (e.g. cases - controls) with identical (or very similar) values for the confounder. 

In the analysis: **Adjusting**
Explicitly incorporate the confounder into the statistical model. This would be Regression

