```python
# Load libraries
import os
import re
import fileinput
import sys
from glob import glob
import shutil


# Create path to content
path = 'content/'
```

## Find All Jupyter Notebooks


```python
# Find all jupyter notebooks in all content folders
all_ipynb_files = [os.path.join(root, name)
                   for root, dirs, files in os.walk(path)
                       for name in files
                           if name.endswith((".ipynb"))]

# Remove all notebooks from checkpoint folders
ipynb_files = [ x for x in all_ipynb_files if ".ipynb_checkpoints" not in x ]
```


```python
all_ipynb_files
```




    ['content/notes\\DeepLearning\\Toy Classification Pytorch\\Toy_Classification_Pytorch.ipynb',
     'content/notes\\Statistics\\Plotting a Normal Curve.ipynb']




```python
# For each file
for file in ipynb_files:
    # Convert into markdown
    print(os.system('jupyter nbconvert --to markdown {file}'.format(file=file)))
```

    -1
    1
    


```python
os.listdir('content/notes\\DeepLearning/Toy Classification Pytorch\\Toy_Classification_Pytorch.ipynb')
```


    ---------------------------------------------------------------------------

    NotADirectoryError                        Traceback (most recent call last)

    <ipython-input-19-8c5afa9c29bd> in <module>
    ----> 1 os.listdir('content/notes\\DeepLearning/Toy Classification Pytorch\\Toy_Classification_Pytorch.ipynb')
    

    NotADirectoryError: [WinError 267] The directory name is invalid: 'content/notes\\DeepLearning/Toy Classification Pytorch\\Toy_Classification_Pytorch.ipynb'



```python
os.system('jupyter nbconvert --to markdown {file}'.format(file='make.ipynb'))
```




    0




```python
os.system('jupyter nbconvert --to markdown {file}'.format(file='content/notes\\Statistics\\Plotting a Normal Curve.ipynb'))
```


```python

```
