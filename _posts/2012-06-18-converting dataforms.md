A short cheat sheet for converting between data types and data containers in python:

## data types
```python
x=12.34
print int(x) #converts x to an integer
print float(x) # converts x to a float
print str(x) #converts x to a string
print type(x) #gives the data type of x
```

```
>>> 
12
12.34
12.34
type 'float'
```

## container types:

```python
import numpy as np
a_list=[1,2,3,4]
print a_list
#1.list into array
a_array=np.array(a_list)
print a_array
#2. array into list
a_list=list(a_array)
print a_list
#3. list and array to tuple
a_tuple=tuple(a_list)
print a_tuple
a_tuple=tuple(a_array)
print a_tuple
```
```
>>> 
[1, 2, 3, 4]
[1 2 3 4]
[1, 2, 3, 4]
(1, 2, 3, 4)
(1, 2, 3, 4)
```

