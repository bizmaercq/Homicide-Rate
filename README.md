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

We can rewrite the model in the partialled-out form as:

    Y˜ = βD˜ +ǫ,    E(ǫD˜) = 0, (1)

where Y˜ and D˜ are the residuals left after predicting Y and D using Z,
namely,

``` 
Y˜ := Y − ℓ(Z), D˜ := D − m(Z),
   
```

where ℓ(Z) and m(Z) aredefined as conditional expectations of Y and D
given Z:

    ℓ(Z) := E[Y | Z],   m(Z) := E[D | Z].

The equation EǫD˜ = 0 above is the Normal Equation for the population
regression of Y˜ on D˜. This implies the following result:

Theorem (Frisch-Waugh-Lovell for Partially Linear Model) The population
regression coefficient β can be recovered from the population linear
regression of Y˜ on D˜:

    β = argminE(Y˜ − bD˜)2 = (ED˜ 2)− 1ED˜Y˜ , b

where β is uniquely defined if D can not be perfectly predicted by Z,
i.e. ED˜2 \> 0.

## Estimation of β: The Procedure

1.  Our estimation procedure for β in the sample will mimic the
    partialling out procedure in the population.
2.  In order to avoid thepossibility of overfitting we rely on sample
    splitting. Wehave data (Yi,Di ,Zi )ni=1. We randomly split the data
    into two halves: one half will serve as an auxilliary sample, which
    will be used to estimate the best predictors of Y and D, given Z,
    and then estimate the residualized Y and residualized D. Another
    half will serve as the main sample and will be used to estimate the
    regression coefficients.
3.  Let A denote the set of observation names in the auxiliary sample,
    and M the set of observations names in the main sample.

#### Step 1:

Uusing auxiliary sample, we employ modern nonlinear regression methodsto
build estimatorsbℓ(Z) and mb(Z) of thebest predictors ℓ(Z) and m(Z).
Then, using themain sample, we obtain theestimatesof theresidualized
quantities:

    Yˇi = Yi − bℓ(Zi), Dˇi = Di − mb(Zi ), for each i ∈ M, 

and then using ordinary least squaresof Yˇi on Dˇi obtain the estimateof
β, denoted by βb1 and defined by the formula:

    βb1 = argmin ∑ (Yˇi —bDˇi )^2.       b i∈M

#### Step 2:

we reversetheroles of theauxiliary and main samples, repeat Step 1, and
obtain another estimateof β, denoted by βb^2.

#### Step 3:

we taketheaverage of thetwo estimatesfrom Steps1 and 2 obtaining
thefinal estimate:

``` 
    βb = 21βb1+ 21βb2.
```

## Inference Result: Theory
