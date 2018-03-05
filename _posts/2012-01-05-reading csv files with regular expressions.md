Python has a csv reader. It converts each line in the csv file into a list.
The csv reader can interpret two default versions or 'dialects' of csv

* 1) comma

* 2) tab

To open the csv file "normal.csv" below, 

``` 
Creature,Legs,Eyes
Dog,4,2
Cyclops,2,1
Spider,8,6
```

use the csv module like this: 

```python
import csv
with open("normal.csv", "rb") as mycsv:
    mycsvlines = csv.reader(mycsv)
    for row in mycsvlines:
        print row

```

```
['Creature', 'Legs', 'Eyes']
['Dog', '4', '2']
['Cyclops', '2', '1']
['Spider', '8', '6']
```
Note that in Python 2.5 and above close() is called automatically if the "with" statement is used.

To open a tab-delimited file "normaltab.csv" that is listed in csv format ...
```
Creature    Legs    Eyes
Dog    4    2    
Cyclops    2    1
Spider    8    6
```

... you can just define the delimiter in the module.

```python
with open("normaltab.csv", "rb") as mycsv:
    mycsvlines = csv.reader(mycsv,delimiter='\t')
    for row in mycsvlines:
        print row
```

```
['Creature', 'Legs', 'Eyes']
['Dog', '4', '2', '']
['Cyclops', '2', '1']
['Spider', '8', '6']
```
You may come across a file where you have a strange combination of delimiters.

See below: 
```
Creature;Legs-Eyes
Dog;4-2
Cyclops;2-1
Spider;8-6


```

In this case, you do not need to create a brand new dialect. 
It is really better to just import regular expressions and use
reg.split.

``` python
import re
with open("weird.csv", "rb") as mycsv:
    mycsvlines = csv.reader(mycsv)
    for row in mycsvlines:
        print re.split('[;-]+',row[0])
#Python 2.5 and close() called automatically using the "with" statement
```
```
['Creature', 'Legs', 'Eyes']
['Dog', '4', '2']
['Cyclops', '2', '1']
['Spider', '8', '6']
```

Happy data munging.
