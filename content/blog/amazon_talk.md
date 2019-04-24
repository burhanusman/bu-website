---
title: "Machine Learning at Amazon"
subtitle: "A talk I attended by an ML engineer"
date: 2019-04-06T14:09:17+05:30
draft: false
tags: ["AI","ML"]
---
Recently I attended a talk by Mr Part Gupta, an ML engineer at Amazon. It was
mostly about the Machine Learning use cases at Amazon. The talk was quite
informative as I had attended few courses on Machine Learning and Information
Retrieval. This post is a summary of the talk.

*****

**Machine Learning Use Cases @Amazon.**

1.  **Product Recommendation:** Recommend the *right product* to the *right
customer* in the *right place* at the *right time*. <br> Challenges:<br>  —
*Scale*: Amazon has hundreds of millions of users. Personalised product
recommendations are to be made to each one of them.<br>  — *Personalisation*:
Product preference may vary greatly across different users.<br>  — *Real Time:*
The recommendations should happen in real-time. This requires that there is low
latency.<br>  — *Cold-start:* This is a problem with any recommender system. How
to recommend a product to a new user (since recommendations usually use a users
past browsing data on the platform). Also, to whom to recommend new products
which are added to the platform.
1.  **Product Demand and Forecasting** : Given past sales of a product in every
region, predict regional demand up to one year in future. <br> This is important
for Amazon because often they stock-up the inventory at some of the Fulfilment
Centres<br> *Challenges*:<br>  — *Scale: 20*+ million products fulfilled by
Amazon alone.<br>  — *New Product*: If a new product is added to the platform,
how to predict the demand for it since we don’t have past sales data.<br>  —
*Seasonal*: Many products have demands varying with season. How to model
that?!<br>  — *Demand Spikes*: External events might trigger demand spikes which
might not be directly modelled from previous sales data.<br>  — *Regionalised*:
Since the demand for different regions across the world differs drastically, how
to incorporate these variations in the model.
1.  **Product Classification**: Given a product description from a seller, map it to
the appropriate product category. Amazon maintains a product category which is
structured as a tree, and final categories lying in one of the leaf nodes.<br>
Challenges: <br>  — *Scale* : Number of product categories are high, more than 1000. Classifying things into these many categories is gonna be a task.<br>  —
*Fuzzy Class definitions*: Often the product categories are fuzzy because the
nature of products is so. <br>  — *Multi-label and Multi-class*: Products might
belong to more than one category. <br>  — *Incorrect/Missing data*: The product
description might have some missing values ( like the title). How to deal with
those.<br>  — *Product Vs Accessories:* It’s often hard to distinguish between
the descriptions of a product and some of its accessories.<br>  — *Training data
quality*: Training data may be badly labelled, or often there are few products
in the training data for a particular category.
1.  **Product Matching:** Given product information, find duplicate product listings
in the Amazon category. <br> Challenges:<br>  — *Scale*: The Amazon catalog
contains 100+ million product listings. Looking for duplicates among these
listings is gonna be challenging.<br>  — *High precision requirement*: It’s very
important that only the *same* products are listed as on listings. If not a
hell-lot of problems are gonna happen, customer getting the wrong good for
starters.<br>  — *Incorrect/Missing Data*: Again, some of the descriptions might
have missing inputs. The model should take care of these.<br>  — *Variations*:
Products might be subtly different, and they should be listed separately. The
model should be able to take care of these small variations.
1.  **Product Search:** This is probably the most important ML task at Amazon. Given
a partial query, find the right product for the right customer, in the right
place at the right time. This statement summarises any Information Retrieval
task.
1.  **Ad-Click Probability:** Predict the performance (click-through rates,
conversion rate) of an ad. <br> Challenges:<br>  — *Sparsity of the training
data*: Ad-Clicks are really rare (How many time do you click on an ad on any web
page ?!). Hence the training data would be imbalanced towards no-clicks.<br>  —
*Latency*: The ads are placed according to their relevance and also by factoring
in the real-time bidding that’s happening. Hence the prediction is to be done in
a very short time, every time.<br>  — *Explore and exploit*: The popular
reinforcement learning paradigm is to be used here because the creatives are
changing dynamically and customer interests keep changing.
1.  **Information Extraction From Reviews:** Extract product attributes and ratings
from reviews.<br> Challenges: <br> *— Diverse Product Attributes:* Since the
products are diverse, so would the attributes. *—Informal Styles of the
comments:* Often the comments are written in an informal style making it
difficult to use conventional IR methods<br>  — *Short Text*: Many of the
comments are really short and extracting useful information might be difficult
1.  **Visual Search:** Recognise products in an image and map it to the Amazon
Catalog<br> Challenges : <br>  — *Detecting a product from the image:*The image
to be searched would be of any kind, and detecting a specific product in that
image would be challenging. *— Wide variety of products in the Amazon category:* Sifting through the Amazon catalog containing millions of images is also
challenging.
1.  **Speech Recognition:** With Alexa in the scene, this is a major use case for
Amazon.<br> Challenges: <br>  — *Real-Time Recognition:* The speech is to be
recognised and responded on the fly.** — *Unconstrained Environment*: Need to
deal with the background noise<br>  — *Speaker Adaptation*: Adapt and involve
specific to the current user.<br>  — S*peaker Independent*: Generalisability to
new users<br>  — *Word Error Rate*: Need to decrease the amount mistakes done in
recognition because it impacts user experience
1.  **Deal Ranking:** Rank Deals to maximise relevance or revenue* —
Personalisation: *Personalised deals to be offered to users according to their
past buying habits.*— Short-duration:*The deals run for a short time.
Optimisation to be done considering that.
1.  **Question and Answering:**  Answer user’s questions in any context — Echo,
Mobile, Desktop, Apps etc<br>  — *Complexity and Variability of the questions:* Open-ended *— Source of information:* It’s important to choose the right source
of information to answer user queries — especially in the era of fake news!<br> 
*—High Precision and Recall:*— Variability in customer-created content:* The
answers would differ from customer to customer, based on their history, buying
habits, wish-lists, reminders etc.
