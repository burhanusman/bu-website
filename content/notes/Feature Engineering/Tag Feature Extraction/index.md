---
title: "Tag Feature Extraction"
date: 2019-04-06T21:54:24+05:30
draft: false
---
# Converting tags into features
This note is about converting a set of tags in each item to a set of features


```python
import pandas as pd
import numpy as np
from sklearn.feature_extraction.text import CountVectorizer
```


```python
train=pd.read_excel("data/Participants_Data_Final/Data_Train.xlsx")
test=pd.read_excel("data/Participants_Data_Final/Data_Test.xlsx")
```


```python
train.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TITLE</th>
      <th>RESTAURANT_ID</th>
      <th>CUISINES</th>
      <th>TIME</th>
      <th>CITY</th>
      <th>LOCALITY</th>
      <th>RATING</th>
      <th>VOTES</th>
      <th>COST</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CASUAL DINING</td>
      <td>9438</td>
      <td>Malwani, Goan, North Indian</td>
      <td>11am – 4pm, 7:30pm – 11:30pm (Mon-Sun)</td>
      <td>Thane</td>
      <td>Dombivali East</td>
      <td>3.6</td>
      <td>49 votes</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CASUAL DINING,BAR</td>
      <td>13198</td>
      <td>Asian, Modern Indian, Japanese</td>
      <td>6pm – 11pm (Mon-Sun)</td>
      <td>Chennai</td>
      <td>Ramapuram</td>
      <td>4.2</td>
      <td>30 votes</td>
      <td>1500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CASUAL DINING</td>
      <td>10915</td>
      <td>North Indian, Chinese, Biryani, Hyderabadi</td>
      <td>11am – 3:30pm, 7pm – 11pm (Mon-Sun)</td>
      <td>Chennai</td>
      <td>Saligramam</td>
      <td>3.8</td>
      <td>221 votes</td>
      <td>800</td>
    </tr>
    <tr>
      <th>3</th>
      <td>QUICK BITES</td>
      <td>6346</td>
      <td>Tibetan, Chinese</td>
      <td>11:30am – 1am (Mon-Sun)</td>
      <td>Mumbai</td>
      <td>Bandra West</td>
      <td>4.1</td>
      <td>24 votes</td>
      <td>800</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DESSERT PARLOR</td>
      <td>15387</td>
      <td>Desserts</td>
      <td>11am – 1am (Mon-Sun)</td>
      <td>Mumbai</td>
      <td>Lower Parel</td>
      <td>3.8</td>
      <td>165 votes</td>
      <td>300</td>
    </tr>
  </tbody>
</table>
</div>



### We'll be dealing with the cuisines column which has different cuisines corresponding restaurant
We'll take a look at train and test cuisines separately to see if there are more cusines in test


```python
train_cuisines=set()
for cus_list in train.CUISINES.apply(lambda x:[j for j in [i.strip(' ') for i in x.split(",")] if j]):
    for item in cus_list:
        train_cuisines.add(item)
test_cuisines=set()
for cus_list in test.CUISINES.apply(lambda x:[j for j in [i.strip(' ') for i in x.split(",")] if j]):
    for item in cus_list:
        test_cuisines.add(item)
```

## Checking if test has tags that's not in train data
It seems so, and we would need to deal with those at the end


```python
test_cuisines.difference(train_cuisines)
```




    {'Brazilian', 'Falafel', 'Fish and Chips', 'Hawaiian', 'Mishti'}



We'll be using the CountVectorizer from sklearn package. We'll show how not to do it first.
We'll look at some of the cuisines


```python
list(train_cuisines)[15:20]
```




    ['Thai', 'Konkan', 'Modern Indian', 'Sindhi', 'Moroccan']



As you can see 'Modern Indian' is one of the cuisine. 
But if we use the CountVectorizer directly we get it split into two as below


```python
vectorizer=CountVectorizer()
vectorizer.fit(list(train.CUISINES))
vectorizer.get_feature_names()[80:85]
```




    ['middle', 'mithai', 'modern', 'momos', 'mongolian']



Hence we define a custom tokenizer as below


```python
vectorizer=CountVectorizer(lambda x:[j for j in [i.strip(' ') for i in x.split(",")] if j])
vectorizer.fit(list(train.CUISINES))
vectorizer.get_feature_names()[75:80]
```




    ['mithai', 'modern australian', 'modern indian', 'momos', 'mongolian']



## Adding new features to the train and test datasets


```python
count_features_train=pd.DataFrame(vectorizer.transform(list(train.CUISINES)).todense(),columns=vectorizer.get_feature_names())

train=pd.concat([train,count_features_train],axis=1)

count_features_test=pd.DataFrame(vectorizer.transform(list(test.CUISINES)).todense(),columns=vectorizer.get_feature_names())

train=pd.concat([test,count_features_test],axis=1)
```


```python
train.shape
```




    (4231, 133)




```python

```
