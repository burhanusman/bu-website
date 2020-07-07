# Display Size of Variables


```python
import sys
import numpy as np
```


```python
a=np.zeros((10,10))
b=np.zeros((100,100))
c="This is a string"
```


```python
def sizeof_fmt(num, suffix='B'):
    for unit in ['','Ki','Mi','Gi','Ti','Pi','Ei','Zi']:
        if abs(num) < 1024.0:
            return "%3.1f %s%s" % (num, unit, suffix)
        num /= 1024.0
    return "%.1f %s%s" % (num, 'Yi', suffix)
```


```python
for name, size in sorted(((name, sys.getsizeof(value)) for name, value in locals().items()),
                         key= lambda x: -x[1])[:10]:
    print("{:>30}: {:>8}".format(name, sizeof_fmt(size)))
```

                                 b: 78.2 KiB
                                 a:  912.0 B
                               _ii:  576.0 B
                               _i4:  576.0 B
                               _i5:  576.0 B
                               _i6:  576.0 B
                               _i7:  576.0 B
                               _i8:  576.0 B
                               _i9:  576.0 B
                              _i10:  576.0 B
    
