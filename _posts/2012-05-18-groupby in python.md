
## Overview
* The Basics 

* Making it Useful

* When it Gets Complicated

## The Basics
Honestly, most of the documentation for itertools makes me want to claw my eyes out. On that note, here is a step by step introduction to one of the more useful functions in intertools: groupby().



Let's say we have a list of pets...

```python
Pets=['Rat','Owl','Owl','Rat','Toad',
'Newt','Cat','Owl','Toad']
```



We want to group this list of pets by kind to look like this:

```python
Pets=[['Cat'],
['Newt'],
['Owl', 'Owl', 'Owl'],
['Rat', 'Rat'],
['Toad', 'Toad']]
```
To do this we will need to..

1. import itertools

2. sort the data (this is important)

3. give the categories of pets a name. I chose pet_type

4. call the groups of pets something. I chose pet_group



Now every time you loop through groupby(pets), we can print off the pet_type and the members of pet_group


```python
from itertools import groupby
Pets=['Rat','Owl','Owl','Rat','Toad',
'Newt','Cat','Owl','Toad']
Pets=sorted(Pets)
for pet_type, pet_group in groupby(Pets):
   print pet_type
   print list(pet_group)
```
```
>>> 
Cat
['Cat']
Newt
['Newt']
Owl
['Owl', 'Owl', 'Owl']
Rat
['Rat', 'Rat']
Toad
['Toad', 'Toad']
```
Now notice something important: I have to convert pet_group to a list before
printing it. Otherwise, I end up printing a group object.



## Making it Useful


groupby() is useful for two things:

1. identifying the unique categories in a list: making a list of all pet_type

2. partitioning the list by category: making a list of all pet_group



This is done in a simple way below:
```python
from itertools import groupby
pet_types=[]
pet_groups=[]
Pets=['Rat','Owl','Owl','Rat','Toad','Newt',
'Cat','Owl','Toad']
Pets=sorted(Pets)
for pet_type, pet_group in groupby(Pets):
   pet_types.append(pet_type)
   pet_groups.append(list(pet_group))
```



Our list of unique categories...
```
>>> pet_types
['Cat', 'Newt', 'Owl', 'Rat', 'Toad']
```

Our partitioned list ....
```
>>> pet_groups
[['Cat'], ['Newt'], ['Owl', 'Owl', 'Owl'], ['Rat', 'Rat'], 
['Toad', 'Toad']]
```
## When it Gets Complicated
Lets say instead of having a simple list you need to group by column. Say you need
```python
[['Snape', 'Prof'],
['BuckBeak', 'creature'],
['Harry', 'student'],
['Ron', 'student'],
['Hermione', 'student']]
```
Converted to...

```python
[
 [['Snape', 'Prof']],

 [['BuckBeak', 'creature']],

 [['Harry', 'student'], 
 ['Ron', 'student'], 
 ['Hermione', 'student']]
 ]
```
The groupby function can accept keys to group by, so to get it to group by a particular column...

```python
from itertools import groupby

Hogwarts=[['Snape', 'Prof'],
['BuckBeak', 'creature'],
['Harry', 'student'],
['Ron', 'student'],
['Hermione', 'student']]

categories=[]
groups=[]

#write the key so the groupby function
#knows it is grouping by the second column

second=lambda x:x[1]

#run loop
for category , group in groupby(Hogwarts,key=second):
    categories.append(category)
    groups.append(list(group))
```

which will give you:

```
>>> groups
[[['Snape', 'Prof']],

 [['BuckBeak', 'creature']], 

[['Harry', 'student'],
 ['Ron', 'student'], 
['Hermione', 'student']]]

>>> categories
['Prof', 'creature', 'student']
```
The only catch is that you need to have the data presorted by the column you are grouping.
