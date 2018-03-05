
## Types of Sorting

* Reverse Sort

* Sorting by Other Criteria

* Sorting by Column

* Sorting with a Dictionary











## Simple Sort
python has a function to sort a list alphabetically or numerically. 
Let's say we have a list of people and creatures at Hogwarts and a list of housepoints... 
```python
Hogwarts=['Harry','Hagrid','Ron','BuckBeak','Snape']
Housepoints=[100,200,300,40,0]
To sort, we simply use the built in function:
Hogwarts_sorted=sorted(Hogwarts)
Housepoints_sorted=sorted(Housepoints)
```
```
>>> Hogwarts_sorted
['BuckBeak', 'Hagrid', 'Harry', 'Ron', 'Snape']
>>> Housepoints_sorted
[0, 40, 100, 200, 300]
>>>
``` 
## Reverse Sort
If you would like to reverse the ordering: 
```python
Hogwarts_sorted=sorted(Hogwarts, reverse=True)
```
```
>>> Hogwarts_sorted
['Snape', 'Ron', 'Harry', 'Hagrid', 'BuckBeak']
```
## Sorting by Other Criteria
Lets say you want to sort by another criteria, like the second letter;
or by length. Do do this, you need to create a key for the sort function to use: 
```python
letter_key=lambda x : x[1]
length_key=lambda x: len(x)

Hogwarts_byletter=sorted(Hogwarts,key=letter_key)
Hogwarts_bylength=sorted(Hogwarts,key=length_key)
```
```
>>> Hogwarts_byletter
['Harry', 'Hagrid', 'Snape', 'Ron', 'BuckBeak']
>>> Hogwarts_bylength
['Ron', 'Harry', 'Snape', 'Hagrid', 'BuckBeak']
```
## Sorting by Column
Many times you will import data from an excel or csv file and have a list of lists that needs to be sorted by column. There is an easy way to do this using the sort function. In the same way that we sorted by the second letter of a string, we can sort a set of lists (rows) by one of the columns.


Lets say we have the following data:   
```python
[['Harry','student'],
['Hagrid','Prof'],
['Ron','student'],
['Hermione','student'],
['BuckBeak','creature'],
['Snape','Prof']]
```

```python
Let's sort by the second column..
Hogwart_members=[['Harry','student'],
                ['Hagrid','Prof'],
                ['Ron','student'],
                ['Hermione','student'],
                ['BuckBeak','creature'],
                ['Snape','Prof']]

#key tells sort to look at second element 
our_key=lambda member:member[1]

Hogwart_members=sorted(Hogwart_members, key=our_key)
```

```
>>> Hogwart_members
[['Hagrid', 'Prof'], 
['Snape', 'Prof'], 
['BuckBeak', 'creature'],
['Harry', 'student'], 
['Ron', 'student'],
['Hermione', 'student']]

```
 The data is now sorted by the second column into
* Prof
* creature
* student


The reason the Prof category appears first is because the sort function
considers capital letters to be higher priority then lowercase letters.
P>c>p.

     

## Sorting with a Dictionary
If you have a key for sorting, then simply make a dictionary out of it and apply it as a function. For example if we wanted to sort students by house points...
```python
Students=['Hermoine','Ron','Harry']
housepoints={'Hermoine':500,'Harry':300,'Ron':45}
lookup= lambda x: housepoints[x]
Students=sorted(Students,key=lookup)
```
```
>>> Students
['Ron', 'Harry', 'Hermoine']
```
Well that's all for now. Next post we will look at how to pair sort with a grouping function.
