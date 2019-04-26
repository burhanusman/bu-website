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

1. Study the data well. Look for imbalances and biases, variation and noise. 