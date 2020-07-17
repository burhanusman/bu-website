# How to Convert Integers to Strings in Pandas DataFrame



```python
import pandas as pd
```

## Read DataFrame


```python
df=pd.DataFrame([["Apple",10,50],["Mango",20,40],["Banana",55,20]],columns=["Fruit","Qty","Price"])
```


```python
print (df)
print (df.dtypes)
```

        Fruit  Qty  Price
    0   Apple   10     50
    1   Mango   20     40
    2  Banana   55     20
    Fruit    object
    Qty       int64
    Price     int64
    dtype: object
    

As you can see above, the Fruit column is a string object (dtype is object) and the other columns are both int64

### Convert Qty Column to string
We could use the apply(str) method to convert a single column to string type. 


```python
df.Qty.apply(str)
```




    0    10
    1    20
    2    55
    Name: Qty, dtype: object



### Convert all the columns to string
For converting all the columns to string, we could use the applymap(str) method


```python
df=df.applymap(str)
```


```python
print (df.dtypes)
```

    Fruit    object
    Qty      object
    Price    object
    dtype: object
    
