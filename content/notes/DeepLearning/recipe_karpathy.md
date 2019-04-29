---
title: "Notes from Karpathy's Article on training NNs"
date: 2019-04-26T21:54:24+05:30
draft: false
---

### Two Observations he make:
1. Neural network training is tough and cannot be easily abstracted
2. A lot of things can wrong go while training a nueral network

>Now, suffering is a perfectly natural part of getting a neural network to work well, but it can be mitigated by being thorough, defensive, paranoid, and obsessed with visualizations of basically every possible thing.

### The recipe:

>If writing your neural net code was like training one, you’d want to use a very small learning rate and guess and then evaluate the full test set after every iteration.

1. Study the data well. Look for imbalances and biases, variation and noise. Filter and Search by labels and find any outliers in the data.

2. Set up a full training + evaluation skeleton and gain trust in its correctness via a series of experiments.  Train it, visualize the losses, any other metrics (e.g. accuracy), model predictions, and perform a series of ablation experiments with explicit hypotheses along the way.
	* Fix Random Seeds
	* No data augmentation at this stage
	* verify loss @ init.: If you initialize your final layer correctly you should measure 
	* log(1/n_classes) on a softmax at initialization.
	* set the bias well while inilization to avoid "hockey stick curves"
	* check with human baseline
	* input*independent baseline * train data with all zeros
	* overfit one batch and achieve minimum possible loss adding more layers and filters
	* verify decreasing loss by increasing the capacity
	* visualize after all the preprocessing
	* visualize prediction on test data, and get clues from it's dynamics
	* set manual loss and backprop to see the dependencies and see if everthing is in place
3. Getting the right model has two stages:
	* get a model large enough that it can overfit (i.e. focus on training loss) 
	* regularize it appropriately (give up some training loss to improve the validation loss
	* pick the simpleset model
	* use adam for optimizing
	* complexify only one at a time
	* do not trust learning rate decay defaults
4. Regularize
	* Get more data
	* data augmentation
	* creative augmentation  fake data
	* pretrain
	* stick with supervised learning
	* remove features with noise, try smaller images
	* smaller model size, replace fully connected layers with pooling layers
	* decrease batch size because it increase regularization
	* Use dropout
	* Increase wait decay
	* early stopping
	* try a larger model
	* Visualise first layer weights and make sure you are getting edges