# ISLR Chapter 2

### Systematic information f
If Y = f(X)+e, we say that f is a the systematic information that X provides about Y and e is the error term

### Why estimate f
* Prediction : Y = ~f(X)
Reducible Error: Estimating ~f so that it's closer to f
Irreducible error: e cannot be predicted by X, hence we cannot reduce that

* Inference : 
	* Which predictors are associated with the response?
	* What is the relationship between the response and each predictor?
	* Can the relationship between Y and each predictor be adequately summarized
	using a linear equation, or is the relationship more complicated?


## How to Estimate f?
Parametric Methods: 
It reduces the problem of estimating f down to one of estimating a set of parameters.
1. First we assume a functional form or shape for f
2. We fit the training data to that model and estimate the parameters.

If the chosen model is too far from the true f, then our estimate will be poor. We could try fitting a more flexible model -- with more parameters, but might lead to overfitting.
Overfitting - the model follows the noise closely.

Non-Parametric Methods:
**Advantage:** By avoiding the assumption of a particular functional form for f, they have the potential
to accurately fit a wider range of possible shapes for f.
**Disadvantage:** since they do not reduce the problem of estimating f to a
small number of parameters, a very large number of observations (far more
than is typically needed for a parametric approach) is required in order to
obtain an accurate estimate for f.


## Trade-Off between model accuracy(flexibility) and interpretability
The more flexible the approaches are, the less interpretable the become.
Linear regression is more flexible than Lasso, where some co-efficients go to zero. But Lasso is more interpretable in the sense it has less coefficients.


Semi-supervised Leaerning - n observations, m has response , n-m has no response labels
*No free lunch* in statistics: no one method dominates all others over all
possible data sets.


### Assessing Model Accuracy

#### Measuring the quality of the fit
Regardless of whether or not overfitting has
occurred, we almost always expect the training MSE to be smaller than
the test MSE because most statistical learning methods either directly or
indirectly seek to minimize the training MSE.
Overfitting refers specifically to the case in which a less flexible model would have yielded a smaller test MSE.  
Even if we don't change the flexibiltiy of a model, it can overfit right? Like a fixed NN. How do we explain that?

#### The Bias-Variance Tradeoff
expected test MSE, for a given value x0, can always be decomposed into the sum of three fundamental quantities: 
1. the variance of ˆ f(x0), 
2. the squared bias of ˆ f(x0) and 
3. 	the variance of the error variance terms

As a general rule, as we use more flexible methods, the variance will
increase and the bias will decrease. The relative rate of change of these
two quantities determines whether the test MSE increases or decreases. As
we increase the flexibility of a class of methods, the bias tends to initially
decrease faster than the variance increases. Consequently, the expected
test MSE declines. However, at some point increasing flexibility has little
impact on the bias but starts to significantly increase the variance. When
this happens the test MSE increases.


#### Model Accuracy in classification settings

**The Bayes Classifier:** Classifier that assigns each observation to the most likely class,
given its predictor values.
The Bayes classifier produces the lowest possible test error rate, called
the Bayes error rate.
the error rate at X = x0 will be 1−(maxj Pr(Y=j|X = x0))
The Bayes error rate is analogous to the irreducible error




K-Nearest Classifier:
For real data, we do not know the conditional distribution of Y given X, and so computing the Bayes classifier is impossible.

Many approaches attempt to estimate the conditional distribution of Y given X, and then classify a given observation to the class with highest *estimated* probability.

Given a positive in-
K-nearest
teger K and a test observation x0, the KNN classifier first identifies the neighbors
K points in the training data that are closest to x0, represented by N0.
It then estimates the conditional probability for class j as the fraction of
points in N0 whose response values equal j:
 Formula

**Choice of k:**  
	k=1 : Highly flexible model, learns all the noise.
	k=100 : Very conventional model
	K decides the flexibility of the model


Flexibilty vs Test Error - U-shape graph
Flexibiliy vs Train Error - Ever decreasing graph
Flexibility vs Interpretability - incverse relationship