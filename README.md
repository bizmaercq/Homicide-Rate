The Effect of Gun Ownership on Homicide Rates
================

## Content of this Repo

1.  data/Codebook.txt contains the name of the variables and a brief
    description.
2.  data/gun\_clean.Rdata: The dataset contains the variables used in
    the estimation.
3.  homicide\_rate.R estimates the effect of gun ownership on the
    homicide rate using double machine learning methods. Several methods
    are used to partial out the outcome and treatment variable from the
    control variables. The estimates are calculated by regressing
    partialled out outcome variable on partialled out treatment
    variable.
4.  functions/Cond-comp.R contains additional functions required to
    carry out the estimation.
5.  functions/Functions.R contains additional functions required to
    carry out the estimation.

## Inference using Modern Nonlinear Regression Methods

In this segment we consider inference for the modern nonlinear
regression. Recall the inference question: how does the predicted value
of Y change if we increase a regressor D by a unit, holding other
regressors Z fixed? Here we answer this question within the context of
the partially linear model,which reads,

    Y = βD + g(Z) + ǫ, E[ǫ|Z,D] = 0,

where Y is the outcome variable, D is the regressor of interest, and Z
is a high-dimensional vector of other regressors or features, called
“controls”. The coefficient β provides the answer to the inference
question. In this segment we discuss estimation and confidence intervals
for β. We also provide a case study, in which we examine the effect of
gun ownership on homicide rates.