## Types 
View type of data:
`type(1)`
`type("Hello")`
`type(varName)`

#### Reassigning Types
```python
a = 100
# <class 'int'>
type(a)
# What if we want a to be a string
a = str(a)
# str will take an int and turn it into a string. Puts the string "100" in memory and then looks at the left hand side and points a to the value "100" in memory.
a
# print is implied in python interactive shell
# '100' we can see it's a string
a=float(100)
# Converts int 100 into a floating point number
a
# 100.0
type(a)
# <class 'float'>
int(100.9)
# 100
# Casting a float as an integer runs the floor operation not round()
```

`int("5") + 5`
Addition operators don't work with strings and integers. We can use `str()` or `int()` to make them the same type. 
Adding ints/floats uses mathematical addition.
Adding strings together concatenates them together.
**Python's methods do all the work.**

---
## Integers
`1`,`9123`
Whole numbers.

## Floats
`3.121234123`
Real numbers accurate to 16 decimal places

When comparing floats you can use round() or format()
`0.1 + 0.2 == 0.3` is false.
`round(0.1 + 0.2,2) == round(0,3,2)` is true.

`format(0.1 + 0.2,'3.1f') == format(0.3,'3.1f')`
https://0.30000000000000004.com/

## Strings
`"This is a string"`
Strings are letters, special characters, spaces, digits which are enclosed in quotation marks or single quotes.
```python
###################
## EXAMPLE: strings 
###################
hi = "hello there"
name = "ana"
greet = hi + name  # String's are stuck together
print(greet)
greeting = hi + " " + name # We need an implicit space
print(greeting)
silly = hi + (" " + name)*3
print(silly)  
```


## Bytes
A collection of bytes with string-like capability.

# Compound data types
Data types that are made up of other data types.

## Tuples
`("Group","of","Values")`
Sequences of anything, a collection of data. They can contain elements which are anything. They are immutable. Once we create it, we cannot modify it. 
They're represented with parentheses.
```python
te = ()		# Empty tuple
t = (2, "mit", 3)	# Elements are seperated by ,
t[0]				# Evaluates to 2
(2,"mit",3) + (5,6) # We get (2, 'mit', 3, 5, 6)
t[1:2]				# Evaluates to ("mit",) the extra comment means a tuple with one element
len(t)				# Evaluates to 3
```
~~t[1] = "test"~~ we cannot do this. Tuples are immutable.

Tuples can be used to swap variable values
This does **not** work.
```
x = y
y = x 
```
This works
```python
temp = x
x = y
y = temp
```
This also works with tuples
```python
(x,y) = (y,x)
```

We can also use tuples to return more than one value from a function.
Functions can only return one object from a function, and if we return a tuple object we can return as many values we put inside the tuple object.
```python
def quotient_and_remainder(x, y):
    q = x // y
    r = x % y
    return (q, r)
    
(quot, rem) = quotient_and_remainder(5,3)
print(quot)
print(rem)
```

### Manipulating Tuples
```python
def get_data(aTuple):
    """
    aTuple, tuple of tuples (int, string)
    Extracts all integers from aTuple and sets 
    them as elements in a new tuple. 
    Extracts all unique strings from from aTuple 
    and sets them as elements in a new tuple.
    Returns a tuple of the minimum integer, the
    maximum integer, and the number of unique strings
    """
    nums = ()    # empty tuple
    words = ()
    for t in aTuple:
        # concatenating with a singleton tuple
        nums = nums + (t[0],)   
        # only add words haven't added before
        if t[1] not in words:   
            words = words + (t[1],)
    min_n = min(nums)
    max_n = max(nums)
    unique_words = len(words)
    return (min_n, max_n, unique_words)



# apply to any data you want!
tswift = ((2014,"Katy"),
          (2014, "Harry"),
          (2012,"Jake"), 
          (2010,"Taylor"), 
          (2008,"Joe"))    
(min_year, max_year, num_people) = get_data(tswift)
print("From", min_year, "to", max_year, \
        "Taylor Swift wrote songs about", num_people, "people!")
```

## Lists
If you need a list of a fixed size, you can initialize it like
`newlist = [default vlaue] * <size of the "array">`

Slicing and Math also works on lists. For example you could do the following
```python
a=["this","is"]
b=["a","test"]
c=a+b
d=c[::-1]
```
`["This","is","a","list",1,2,3.142]`

Avoid mutating a list as you are iterating over it.
```python
L1 = [1, 2, 3, 4]
L2 = [1, 2, 5, 6]

def remove_dups(L1, L2):
    for e in L1:
        if e in L2:
            L1.remove(e)
```
Python uses an internal counter to keep track of index it is in the loop. Mutating changes the list length, but python doesn't update the counter. So the loop never see's element 
2.
Instead we can do this
```python
def remove_dups_new(L1, L2):
    L1_copy = L1[:]
    for e in L1_copy:
        if e in L2:
            L1.remove(e)
```

Lists are mutable objects. They're denoted with []. 
```python
a_list = []
L = [2, 'a', 4, [1,2]]
len(L) 						# Evaluates to 4 
L[0] 						# Evaluates to 2
L[2] + 1					# Evaluates to 5
L[3]						# Evaluates to [1,2]
L[4]						# Error

i = 2
L[i-1]						# Evaluates to 'a' as L[1] is 'a'
```
len() of list tells us how many elements are in a list.

As lists are mutable, assignging a new value to an element changes it's value.
```python
L = [2, 1, 3]
L[1] = 5
```
L is now `[2, 5, 3]`
We haven't created a new object in memory, we have just modified the memory.

Iterating over a list
```python
total = 0
for i in L:
	total += i
print total
```
This is better than doing something like this 
```python
total = 0
for i in range(len(L)):
	total += L[i]
print total
```

### Adding elements
We can add elements to the end of a list with `L.append(element)`
for example
```python
L = [2, 1, 3]
L.append(5)			--> L is now [2, 1, 3, 5]
```

Lists are Python objects (everything in Python is an object)
objects have data and they have methods and functions.
We can access this information with object_name.do_something()

In anaconda once we have our L we can put a . after it so `L.` and press tab and view the methods and functions we can do against it.

We can also concatenate lists together, using the `+` operator to give a new list.
```python
L1 = [2,1,3]
L2 = [4,5,6]
L3 = L1 + L2
```
L3 evaluates to `[2, 1, 3, 4, 5, 6]` and L1 and L2 are unchanged

```python
L1.extend([0,6])
```
L1 is mutated to `[2, 1, 3, 0, 6]`
L1 is mutated directly. 

You can `insert(position, value)` where the position is a positive or negative number.

You cannot assign beyond `len(list)-1`.


### Removing elements
To delete an element at a specific index
`del(L[index])`

Remove element at end of the list
`L.pop()`
This also returns the returned element

Remove specific element 
`L.remove(element)`
It looks for the element, and then it removes it.
If the element occurs multiple times, it'll remove the first occurence
If the element is not in the list, it returns an error.

```python3 
s = "I<3 cs"
list(s)				# Evaluates to ['I', '<', '3', ' ', 'c', 's']
s.split('<')		# Returns ['I', '3 cs'] if .split() splits on spaces

L = ['a','b','c']
'_'.join(L)			# Returns 'a_b_c'
''.join(L)			# Returns 'abc'
```

### Sorting Lists
```python
L=[9,6,0,3]
sorted(L)			# returns sorted list, does not mutate L
L.sort()			# mutates L=[0,3,6,9]
L.reverse()			# reverses L
```

If we try something like this
```python
warm = ['red', 'yellow', 'orange']
sortedwarm = warm.sort()
```
`sortedwarm` would be none as .sort() mutates the List, and does not return a mutated sorted version of the list.
```python
cool = ['grey', 'green', 'blue']
sortedcool = sorted(cool)
```
`sorted()` on the other hand does not mutate the list, instead it returns a sorted version of the list.

We can pass the argument `reverse=True` to either functions to sort in reverse order.
Both methods also optionally accept a "key" which produces an element to sort on.


```python
def lowercase(color):
	return color.lower()
	
cool = ['grey', 'Green', 'Blue']

sorted(cool)
# ['Blue', 'Grey', 'green']
sorted(cool, key=lowercase)
# ['Blue', 'green', 'Grey']

```

### Aliases
```python
warm = ['red', 'yellow', 'orange']
hot = warm
hot.append('pink')
print(hot)
print(warm)
# hot and warm are the same thing so it would print the same thing
```
This could be an unwanted side affect.

### Cloning
To clone a list
we can do something like this
```python
chill = cool[:]
```
`[0:len(list)]` is what `[:]` is. This takes every element and create a new list and assign it to a new variable.
```python
cool = ['blue', 'green', 'grey']
chill = cool[:]
chill.append('black')
print(chill)
print(cool)
```
It would print 
```python
['blue', 'green', 'grey', 'black']
['blue', 'green', 'grey']
```

If we just do `blist = alist` it makes a pointer, not a copy.
To make a copy we use `clist=list(alist)`.

However, when we use `list()` only the outer lists are independent. If it is a list of lists, the inner lists are just pointers to each other. To make a copy of a list of lists, use the list method `deepcopy()`.

### String to Lists
We can use the string `split()` method to convert a string to a list.
```python
print("THIS IS A STRING CONVERTED TO A LIST BY .split()".split())
['THIS', 'IS', 'A', 'STRING', 'CONVERTED', 'TO', 'A', 'LIST', 'BY', '.split()']
```

We can use the string `.join()` method to convert a list of strings to a string. (The list must only contain strings).
```python
" ".join(["This","is","a","string"])
'This is a string'
```
The string which is having the `join()` method called on it is used as the seperator.

### Other Useful methods
`index(value)`, to look up where a value is in the list.

`count(value)`, to count occurences of an item in the list

`sum([])` adds all the integers in the list
- `sum([2,4,6])` returns 12

`zip([][])` groups together items are position 0 from each input list followed by items at position 1, and so on.
```python
>>> a=[1,'a',4]
>>> b=[2,'b',5]
>>> list(zip(a,b))
[(1, 2), ('a', 'b'), (4, 5)]
```

Run function on a list or iteratable value.
`map(func(),[])`
```python
list(map(ord, ["A","B","C"]))
list(map(ord, "ABC"))
[65, 66, 67]
```

```python
>>> def addint(x,y):return int(x)+int(y)
... 
>>> list(map(addint, [1,'2',3],['4',5,6]))
[5, 7, 9]
```


## List Comprehension
```python
newlist = []
for x in [1,2,3,6,7,8,22,42]:
	if x < 6:
		newlist.append(x+1)
		
newlist = [x + 1	for x in [1,2,3,6,7,8,22,42]	if x < 6 ]
```
`newlist = [<expression> for <iterator> in <list> <filter>]`
Expression is the value that goes in the new list.
Iterator variable.
An old list to go through
A filter that is applied to the elements before adding them to the list.
```python
[a for a in [1,2,3,4] if a > 2]
[3, 4]
[int(a) for a in "1 2 3 4".split()]
[1, 2, 3, 4]
[(lambda x:x.upper())(x) for x in "make upper"]
['M', 'A', 'K', 'E', ' ', 'U', 'P', 'P', 'E', 'R']
```

## Multidimensional Lists
`array = [[initialvalue] * width for x in range(height)]`
`array = [['xyz'] * 2 for i in range(3)]`
`[['xyz', 'xyz'], ['xyz', 'xyz'], ['xyz', 'xyz']]`
## Dictionary
`{"Key1":"Value1","Key2":"Value"}`
Rather than indexing on integers, we index on the item of interest. 
A dictionary 
Key 1 - Val 1 
Key 2 - Val 2 
Index just by the name.

Store pairs of data, key and value
```python
my_dict = {}			# empty dictionary
grades = {'Student':'B', 'Student2':'C', 'Student341':'A'}
		# key1:val1 , key2:val2
```
This creates pairings of those labels and the values associated with them.
We can then lookup a dictionary
Looks up the key, returns the value associated with the key, if the key isn't found we get an error.
```python
grades['Student']		# Evaluates to 'B'
grades['Studnet00']		# gives a KeyError as 'Student00' pairing key doesn't exist
```

We can add an entry.
```python
grades['Student00'] = 'A'
```

We can test if key in dictionary
```python
'Student' in grades		# Returns True
'Student300' in grades 	# Returns False
```
 
 
We can delete entry
```python
del(grades['Student'])
```
In the dictionary grades, find the entry associated with that key, remove it.

We can copy a dictionary
`grades2 = dict(grade)`
Doing `grades2 = grades` just creates a pointer to grades.

iterable is something we can walk down.
Get an iterable that acts like a tuple of all keys
```python
grades.keys()			# Returns all the keys (student names)
```
Get an iterable that acts like a tuple of all values
```python
grades.values()			# Returns all the values (grades)
```

The keys need to be unique. They also need to be immutable. They can only be things like ints, floats, strings, tuples, booleans. We can have any immutable type as the key. 

### Looping through Dictionary
`.items()` returns a view of tuples with the keys and values.
```python
>>> thedict={'a':'alpha','b':'beta','c':'charlie'}
>>> for eachkey,eachvalue in thedict.items():
...     print(eachkey,eachvalue)
... 
a alpha
b beta
c charlie
```

dict
- matches "keys" to "values"
- look up one item by another item
- no order is guaranteed
- key can be any immutable data type

### Common Dictionary Methods
View of the keys
`dict.keys()`
View of the values
`dict.values()`
View of tuples containg (key, value)
`dict.items()`
In Python2 these methods return a list of items, but in Python3 these return an object known as a "view".

### Counting frequencies of words in song lyrics
```python
def lyrics_to_frequencies(lyrics):
    myDict = {}
    for word in lyrics:
        if word in myDict:
			# increase the value of the key:value pair by 1
            myDict[word] += 1
        else:
			# if it isn't in the dictionary create a new key:value
			# the key is the word and the value is 1
            myDict[word] = 1
    return myDict
```

As .values() returns something iterable we can call max() on it giving us the max value. 
```python
def most_common_words(freqs):
    values = freqs.values()
    best = max(freqs.values())
    words = []
    for k in freqs:
        if freqs[k] == best:
            words.append(k)
    return (words, best)
    
def words_often(freqs, minTimes):
    result = []
    done = False
    while not done:
        temp = most_common_words(freqs)
        if temp[1] >= minTimes:
            result.append(temp)
            for w in temp[0]:
                del(freqs[w])  #remove word from dict
        else:
            done = True
    return result
    
print(words_often(beatles, 5))
```
```python
she_loves_you = ['she', 'loves', 'you', 'yeah', 'yeah', 
'yeah','she', 'loves', 'you', 'yeah', 'yeah', 'yeah',
'she', 'loves', 'you', 'yeah', 'yeah']
```

### Specialty Dictionaries
**defaultdict** will create any key that you query and set it to a default value
newobject = defaultdict(`<function to call for empty keys>`)
```python
def new_val():
	return []
	
from collections import defaultdict
list_of_ips = defaultdict(new_val)
list_of_ips['src#1'].append('dst')
list_if_ips['src#2']
# {'src#1': ['dst'], 'src#2': []})
```


Counter will automatically count the number of times a key is set.
```python
>>> from collections import Counter
>>> word_count=Counter()
>>> she_loves_you = ['she', 'loves', 'you', 'yeah', 'yeah', 
... 'yeah','she', 'loves', 'you', 'yeah', 'yeah', 'yeah',
... 'she', 'loves', 'you', 'yeah', 'yeah']
>>> word_count.update(she_loves_you)
>>> word_count.most_common(10)
[('yeah', 8), ('she', 3), ('loves', 3), ('you', 3)]
>>> word_count['she']
3
>>> word_count.update(['was','is','you','was'])
>>> word_count['she']
3
>>> word_count['you']
4
>>> word_count.subtract(['she'])
>>> word_count['she']
2
```

```python
import requests
from collections import Counter
c = Counter()
webcontent = requests.get('http://metasploit.com').content
c.update(webcontent.lower().split())
# we use list() to capture a copy of the keys before we begin modifying it as we would be modifying something we're iterating over
for k in list(c.keys()):
	if b"<" in k: del c[k];continue
	if b">" in k: del c[k];continue
	if b"=" in k: del c[k];continue

print(c.most_common(8))
```