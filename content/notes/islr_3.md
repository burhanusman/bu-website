# Linear Regression

## Simple Linear Regression

* Minimizes residual sum of squares (RSS) - equivalent to minimizing RMSE
* Popultaion regression line is un observed -it's the true model. True model + e gives at the whole popultaion
* What we can estimate is the least square regression line with the given data.
* The concept is analogous to popuation mean and sample mean.
* Least square estimates are unbiased. Proof? 
* We can also compute the standard errors of the estimates.
* The etimates


### Assessing the accuracy of the coefficient
1. We estimate the coefficient using least square criteria.
2. The estiamtes are unbiased
3. We estiamte the standard errors - for that we need to estiamte the variance of the error-term
4. We do a hypothesis test 

### Assessing the accuracy of the model

#### Residual Standard Error(RSE):
Even if we knew the true regression line, we would not be
able to perfectly predict Y from X. The RSE is an estimate of the standard deviation of . Roughly speaking, it is the average amount that the response
will deviate from the true regression line.

<math>\begin{equation}
\mathrm{RSE}=\sqrt{\frac{1}{n-2} \mathrm{RSS}}=\sqrt{\frac{1}{n-2} \sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2}}
\end{equation}</math>


#### R2 statistic


## Mutiple Linear Regression



## Potenitial Problems
1. Non-linearity of the response-predictor relationships.
	* Use Residual plots to identify non linearity
	* Do non-linear transformations
2. Correlation of error terms.
	* The standard errors that are computed for the estimated regression coefficients or the fitted values are based on the assumption of uncorrelated error terms. If in fact there
is correlation among the error terms, then the estimated standard errors
will tend to underestimate the true standard errors.


3. Non-constant variance of error terms.
* Heteroscadacity
* Weighted Least Squares
4. Outliers.

* An outlier is a point for which yi is far from the value predicted by the model. Outliers can arise for a variety of reasons, such as incorrect recording
* **studentized residuals:** computed by dividing each residual ei by its estimated standard
studentized
error
of an observation during data collection.
5. High-leverage points.

* observations with high leverage high leverage have an unusual value for xi
* changes the slope drastically
* In order to quantify an observation’s leverage, we compute the leverage statistic. A large value of this statistic indicates an observation with high leverage.
* The leverage statistic hi is always
between 1/n and 1, and the average leverage for all the observations is
always equal to (p+1)/n. So if a given observation has a leverage statistic that greatly exceeds (p+1)/n, then we may suspect that the corresponding
point has high leverage.
* 

6. Collinearity.
* Collinearity refers to the situation in which two or more predictor variables are closely related to one another.
* Two-way collinearity can be detected by a correlation plot but it cannot detect multicollinearity
* Multicollinearity: Can be detected by calculating VIF 
* Variation Inflation Factor: 