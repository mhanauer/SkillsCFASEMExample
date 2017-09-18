---
title: "Equations and example of simple CFA and SEM"
output: html_document
---
Here we have a simple example of a confirmatory factor analysis (CFA) with four items that compose a single construct in this example visual.  The first box to check is the model's identification.  We cannot assess how well the model we are describing is doing unless we have know that the model is identified.  If the model is underidentified than there are more degrees of freedom than parameters being estimated.  We can calculate the degrees of freedom using the following fomrula q(q+1)/2 where q = the number of items.  Therefore we have, 4*(4+1)/2 10 degrees of freedom and are estimating a total of 7 parameters, which are described below.
```{r}
library(lavaan)
data(HolzingerSwineford1939)
dat = HolzingerSwineford1939
head(dat)
# Calculate degrees of freedom through formula 
```
Intercept fixed a zero.  
$${x_{1} = \lambda_{11}(\xi_{1})+ \delta_{1}}~~~ (1.1)$$ $$ 
$${x_{2} = \lambda_{21}(\xi_{1})+ \delta_{2}}~~~ (1.1)$$ $$ 


$${x_{3} = \lambda_{31}(\xi_{1})+ \delta_{3}}~~~ (1.1)$$ $$ 
$${x_{4} = \lambda_{41}(\xi_{1})+ \delta_{4}}~~~ (1.1)$$ $$

\documentclass{article}
\usepackage{amsmath}
\begin{document}
\[
\begin{bmatrix}
    \theta_{11} & 0  & 0 & 0\\
    0  & \theta_{22}  & 0 & 0 \\
    0 & 0 & \theta_{33} & 0 \\
    0 & 0 & 0 & \theta_{44}\\
\end{bmatrix}
\]
\end{document}

\documentclass{article}
\usepackage{amsmath}
\begin{document}
\[
\begin{bmatrix}
    \phi_{1}\\
\end{bmatrix}
\]
\end{document}

Equations 1.1 through 1.4 are the equations for the items.  In this example, each item has a fixed intercept at 1, with a regression weight of lambda multiplied by the latent variable xi.  Then we add the unique error term for that item delta.  

Equation 2 is the variance covariance matrix for the deltas.  In this model, I am assuming that error terms are uncorrelated with variances equal to what the model estimates.

Equation 3 is the variance covariance matrix for the phis, which in this case there is only one, because we only the variance for the latent construct visual and no other covariances or variances, because there are on other latent constructs in this example.    


Now we can conduct the CFA with one construct loading onto three items an estimation of the error terms being correlated.
```{r}
model1 = 'visual =~ x1 + x2 + x3 +x4'
fit <-lavaan:::cfa(model1, data=dat)
summary(fit, fit.measures = TRUE)
```
Number of observations = Total number of data points, which is 301
Estimoatr = Says that I used the maximum likelihood estimator to find the parameter estimates
Minimum Function Test Statistic = Test statistic to assess if the model implied specifications and data are statistically signifcnatly different.  This statistic is almost always significant.

Model test baseline model = Tests whether the my model is a better fit for the data than a null or empty model.  

CFI/TFI = a value of .935 means that our model is 93.5% better than the null 
TFI = similar interpretation
RMSEA = This is average amount of residual or error the model between the data implied and model covariance structure.

SRMR = standardized version of the RMSEA

Latent variables = These are interpreted just like a covariate in a regression model.  The first item is 1, because we need one item to serve as the comparision for all other items.  

Finally, we can plot the model to help us visualize what it looks like using the semPlot package
```{r}
library(semPlot)
semPaths(fit, title = FALSE, curvePivot = TRUE)
```
Now we can move to an example using SEM.  Here we will expand the model


Save this for SEM
\documentclass{article}
\usepackage{amsmath}
\begin{document}
\[
\begin{bmatrix}
    \phi_{11}       & \phi_{12} \\
    \phi_{21}       & \phi_{22} \\
\end{bmatrix}
\]
\end{document}


