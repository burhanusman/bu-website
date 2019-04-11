---
title: "Zappos footwear classification"
subtitle: "How I built a simple ML system to do gender based footwear classification."
date: 2019-04-06T14:09:17+05:30
draft: true
tags: ["AI","ML"]
---
Recently I stumbled across the well labelled Zappos50K dataset and realised a lot of interesting use cases can be built with it. I decided to start with a simple binary classification model to classify footwear on the basis of gender.

### The Setup
I have used the Google Colab to do all the coding. You can easily try it yourself. For starters you would need to download the dataset from Univ. of Texas website.

```python
#Downloading and extracting the dataset
!wget http://vision.cs.utexas.edu/projects/finegrained/utzap50k/ut-zap50k-images-square.zip
!wget http://vision.cs.utexas.edu/projects/finegrained/utzap50k/ut-zap50k-data.zip
!unzip ut-zap50k-images-square.zip
!unzip ut-zap50k-data.zip
```

We’ll be using the easy-to-use *fastai* library to train and test the models. Colab has the library already installed in it. Below we’ll just import all the required libraries.

```python
#Importing the required libraries
!pip install mat4py   #For reading the .mat files in the dataset
import pandas as pd
import mat4py
from fastai.vision import *
from fastai.metrics import error_rate
```

Now we’ll need to arrange the data in a way suitable for training. The image-data.csv file contains the properties of each image like gender and brand. The image-path.mat file contains the relative path of all the images. For starter’s we’ll combine both the dataframe into one.

```python
image_paths = mat4py.loadmat("ut-zap50k-data/image-path.mat")
image_path=[i[0] for i in image_paths["imagepath"]]
meta_data=pd.read_csv("ut-zap50k-data/meta-data.csv")
meta_data["path"]=image_path
```

Since we are making a footwear classifier based on gender, we just need the following information: Given an image which gender does it belong to.
Also for simplification, we only take those images that are belong to either of the gender. That is, we drop all rows in which the Gender column is Boys/Girls/Unisexual etc.

```python
meta_data_clean=meta_data[-meta_data.Gender.isna()]
meta_data_clean=meta_data_clean[(meta_data_clean.Gender=="Women") | (meta_data_clean.Gender=="Men")]
meta_data_clean=meta_data_clean[["path","Gender"]]
```
There are folder names with ends with a period(.) and we need to do some cleaning for those path variables. We’ll replace the period(.) with 2%E — that’s how linux saves these file names.

```python
meta_data_clean.loc[meta_data_clean.path.str.contains("./",regex=False),"path"] = [i.replace("./","%2E/") for i in meta_data_clean.loc[meta_data_clean.path.str.contains("./",regex=False),"path"]]
```

Now we are all set to do the training. This is what we have currently:

1. A bunch of images of footwear belonging to either of the gender.
2. A data-frame with two columns — the path to an image and it’s corresponding label.

We’ll go with the standard way of using the fastai library.We’ll create an ImageDataBunch object from the dataframe. This splits the dataset into train and validation sets. The path specifies the root path where all the images are saved. The df specifies the dataframe holding the relative paths to the images and the corresponding labels. The size parameter refers to the input size of the images. And the bs refers to the batch-size.

>**Why do we need to specify the image size and batch size?**   
*Few things to understand here. If you are using the network architecture as a whole it would only take a fixed size of images. This is because there is a fully connected convolutional layer in between which has a fixed size of in-nodes. But that’s not the case with convolution or pooling layers, they can work on arbitrary size of inputs.  
Here, we are only taking the head of the network which consist of only conv and pooling layers. So the network can take and fixed size of images. The ImageDataBunch object is a data-loader and it would cut/expand the images to the given size.  
Batchsize is the parameter which decides how many images to be processed at once by the network. The system usually have memory constraints and it’s this parameter that we need to change when it says the system is out of memory.*

```python
data=ImageDataBunch.from_df(path="ut-zap50k-images-square/",df=meta_data_clean, size=224,bs=64)
```

Now we have the data in the required format, we instantiate a cnn-model. We need to specify which particular architecture we need to use. We’ll use the Resnet50 architecture. Do read this article if you want to learn about the architecture in depth.

```python
learn = create_cnn(data, models.resnet50, metrics=error_rate)
```

>**A primer for newbies on transfer learning**  
*We are using something called transfer learning here. We already have a network which was trained on huge amount of data — Resnet50 in the above case. We use the same network architecture along with the trained weights — so that we have something to start with. The idea is that it has learned to recognize many features on all of this data, and that we will benefit from this knowledge, especially if our dataset is small, compared to starting from a randomly initialized model . We train the model on the current dataset and hopefully the weights are updated in a way customised for performing well on the task at hand.*

### Learning Rate Finder
This is something which is to be done before we start training the neural network. We need to find the optimum range of learning rate for training. Learning rate is a parameter in a neural network optimization algorithm which decides how fast or slow the gradient decent happens.

>Most of the techniques used by fastai come from the paper Cyclical Learning Rates for Training Neural Networks by Leslie N. Smith. It’s a short and fun read, I’ll urge you to read it for a better understanding.The major theme of the paper is that instead of a keeping a fixed learning rate, we vary the learning rate between a max/min value cyclically. The paper also explains how to find the min and max values for the cycles. That’s done by linearly increasing the learning rate from a min value to a max value, plotting it and picking the range where the learning rate leads to less loss.

{{< gist burhanusman 26bfc105a38f6a6fcdbad38f6202ce53 >}}

We also need to unfreeze the network. What it means is that we are gonna make all the layer weights updatable. If not, only the head of the network is trainable. We use the one cycle policy where we change the learning rate for one cycle (two steps, an increasing one and a decreasing one). We calculate the validation rate and the error rate.


{{< gist burhanusman 1f2812076533577f3e89f732b04704f8 >}}

We are done with the training and we have a neural network that can identify footwear with an 8.7% error rate. Not bad. In fact if you look at some of those images that the network got wrong, we see that it’s not even easy for a human being to accurately predict those. Some are borderline differences, some probably had their manual labelling wrong, and some are very rare types of designs. We plot few of the images that the network got wrong here.

{{< gist burhanusman 7e762b9caa1f66adceb723b52353475a >}}


It’s interesting to see that the network is biased by color. Pink shoes are often misclassified as belonging to men, when it’s not. This is a part of the major discussion on how to avoid biases in AI systems.

### What Next?
There are a lot of other interesting things that can be done with this dataset. I intend to do some of them in the near future like similarity prediction, recommender system and attribute classification.