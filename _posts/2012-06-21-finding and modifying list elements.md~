
## Overview
* Finding Elements in a List

* Modifying Elements in a List

* Filtering Elements in List

* Conditionally Replace Elements in List

* Putting Lists Together and Taking Them Apart

* Deleting Items From A List

## Finding Things in a List

To see check to see if something is in a list:

```python
Heroes=['Thor','Iron Man','Black Widow','Hulk','Iron Man']
#Let's see if Hawkeye is on the list
if'Hawkeye' in Heroes:
   print 'He is on the list'
else:
   print 'No love for archers :('
>>> 
```
No love for archers :(

To find an index of an element in a list by name:

```python
Heroes=['Thor','Iron Man','Black Widow','Hulk','Iron Man']
#finds index of first occurrence of 'Iron Man'
print Heroes.index('Iron Man')
>>> 
1 
```
## Modifying Things in a List

Mapping and list comprehensions are two different ways to modify values in a list.

First, a list comprehensions: [f(x) for x in S if P(x)] 

```python
#I want to create a list of doubled values
values = [2, 3, 9, 5]

# way 1
dblvals=[num*2 for num in values]
print dblvals
>>> 
[4, 6, 18, 10]
```
or we can use mapping map(function,values):

```python
# way 2
dbl=lambda x:x*2
dblvals2=map(dbl,values)
print dblvals2
>>> 
[4, 6, 18, 10]
```
 
## Filtering Elements in List

```python
values = [2, 3, 9, 5]
#I want to create a list of values less than 8
less8vals=[num for num in values if num<8]
print less8vals
>>> 
[2, 3, 5]
```
## Conditionally Replace Elements in List
```python
stuff=[a if a==0 else 2 for a in [0,1,0,3]]
>>> stuff
[0, 2, 0, 2]
```


## Putting Lists Together and Taking Them Apart

Pulling out a Column of Data:

```python
#------------------------------------------------
xyvals=[[1,200],[2,300],[3,400]]
xv=[coords[0] for coords in xyvals]
yv=[coords[1] for coords in xyvals]
>>> xv
[1, 2, 3]
>>> yv
[200, 300, 400]
>>> 
```

Putting Together Columns of Data

```python
#------------------------------------------------
newcoord=[[xv[i],yv[i]] for i in range(0,len(xv))]
>>> newcoord
[[1, 200], [2, 300], [3, 400]]
```

## Deleting Items From A List
```python
sets=[[1,'A'],[2,'Q'],[3,'C'],[4,'Q'],[5,'E'],[2,'A']]

#p: pair 
#pc: pair counter

pc=0
for p in sets:
    if p[1]=='Q':
        del sets[pc]
    pc=pc+1
>>> sets
[[1, 'A'], [3, 'C'], [5, 'E'], [2, 'A']]
```
