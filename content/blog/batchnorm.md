---
title: "BatchNorm"
subtitle: "Understanding how it works"
date: 2019-08-12T14:09:17+05:30
draft: false
tags: ["AI","ML"]
---
I had a hard time wrapping my head around on why BatchNorm was used until I read 'deeply' about it. I'll try explaining the concept and the reason why it works.

### Normalization and Standardization in machine learning 
Although Normalization and standardization are often used interchangeably, it's good to know the difference between them.


>**Normalization**: Normalization means to scale a variable to have a values between 0 and 1    
>**Standardization**:  Standardization transforms data to have a mean of zero and a standard deviation of 1

Before we understand why batchnorm is useful, we better understand why standardization is used in machine learning algorithms. 

The short answer is it helps in setting hyper-parameters and initial conditions that work. This is because we have thumb rules that have been developed (like learning rate ε =0.1) for standardised values.The main reason for standardization is that it makes optimization easier. 

### What is BatchNorm:
The concept is so simple that you start thinking why no one thought about it before the actual paper. This often happens, like in magic, where you see the trick is so easy once you know how it is done.
In Batchnorm, we normalise the activations from a hidden layer across a batch. We also scale it up using learnt parameters. 

![Example image](/static/batchnorm.png) 


### How it helps:
1. *Train Faster*: It is shown from experiments that networks which implements batchnorm between some of their layers train faster than ordinary networks. This is because the optimisation converges quickly.

2. *Less sensitive to choice of parameters*: Another great thing of using batchnorm is that it makes the network less sensitive to hyperparamter choice. This is a boon to all deep learning practitionaers because it's one area where a lot of time is spent while developing the model.

### Why BatchNorm works?
**The wrong answer - Internal Covariance Shift:**

The original batchnorm paper says that it works because it reduces internal covariacnce shift.

Covariance shift is a phenomenon where the input distribution to a learning algorithm keeps changing and hence the algorithm doesn't learn a lot. This happens because every learning algorithm tries to minimizing the loss where the training examples densely populated.  Hence the distribution changes higher density regions also change. 

Something similar happens with the internal layers of a neural network too. The input of these layers keep changing because it's dependent on previous layers and they keep changing. Hence what we do normalize the input after each layer so the next layer always gets signals with a same mean and variance every time. 
 
> Training Deep Neural Networks is complicated by the fact that the distribution of each layer’s inputs changes during training, as the parameters of the previous layers change. This slows down the training by requiring lower learning rates and careful parameter initialisation, and makes it notoriously hard to train models with saturating nonlinearities.

> If, however, we could ensure that the distribution of nonlinearity inputs remains more stable as the network trains, then the optimiser would be less likely to get stuck in the saturated regime, and the training would accelerate.


### A better possible answer: Interaction between layers

Although in the actual Batchnorm paper, covariance shift was said to be reason for batchnorm working, in later papers it's claimed that this is wrong. Rather they point to the fact that batchnorm reduces interactions between the layers which is not accounted for during the backprop.

Many of the deep learning optimization techniques use only first derivative to make gradient updates under the assumption that other layers do not change. This assumption is fundamentally wrong and batch-norm sort of helps to deal with the failed assumption.

To see why this is, we could go to the basics and understand backprop a bit better. So backprop (generally) uses first derivatives to make gradient updates. An underlying assumption here is that the higher-order derivatives are small and doesn't affect the optimization a lot. The fact is this is not always true. We could see this using an example as follows. 

### When to normalize?
Should we normalize before the activation function or after the activation function? Although normalizing z (before the activation) was suggested in the paper, it is often done the other way. Normalizing the activation make sense because that's what goes to the next layer, and it might help better to  decouple the layer interactions. 

### Conclusion
This was a skim through the actual math behind the batchnorm. From what I read, it seems like batchnorm is still not undrestood well and there is varied opiniion among researches on how it works. I'll hopefully keep the article updated with more in-depth analysis at a future point in time.

### References

 1. [Paperspace Blog](https://blog.paperspace.com/busting-the-myths-about-batch-normalization/)
 2. [Gradient Science Blog](http://gradientscience.org/batchnorm/)
 3. [Article on ML-Explained](https://mlexplained.com/2018/01/10/an-intuitive-explanation-of-why-batch-normalization-really-works-normalization-in-deep-learning-part-1/)
 
