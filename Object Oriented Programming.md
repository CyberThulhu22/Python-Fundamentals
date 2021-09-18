Everything in python is an object (and has a type)
- can create new objects of some type
- can manipulate objects
	- for example with a list, you can append items.
- can destroy objects
	- explicity with *del*
	- forget about them
	- python with reclaim destroyed/inaccessible objects in memory (garbage collection)

What are objects?
Objects are a data abstraction, that consist of:
1. Internal representation through data attributes
	-	For example with a car, like the blueprint, the color of the wheels, the dimensions etc. What data abstractions make up the car.
2. An interface for interacting with object 
	-	through methods (procedures/functions)
	-	defines behaviours but hides implementation
	-	For example with a car, what are ways you can interact with it, paint the car, have the car make a noise, or drive the car.

We have a data type of list. 
We think of it in two ways, how does python behind the scenes view lists? And the second is how do you interact with list objects.
For example we have the list `L`.

To answer our first question of lists behind the scene:
The value at a specific index. For example at index 0, it has the value 1. The second thing that represents lists, is a pointer. Internally this pointer tells python the memory location of the element at the next index. We don't need to know this, the representations are abstractions, we don't need to know the internal workings to use Lists.

OOP allows us to bundle this data, an internal representation, and ways to interact with this data into packages. We can create objects with these packages. Ultimately, this allows us contribute to decomposing and abstracting our code. 

We can create our own data types with classes. 
Creating the class involves:
- class definition
- class name is the type
- defining class name
- defining class attributes (data representations, and how you can interact with the object)
- for example, someone wrote code to implement a list class
- class defines data and methods common across all instances

Using the class involves
- creating new instances of objects (creates a new object that has type of your class)
- doing operations on the instances
- for example `L=[1,2]` and `len(L)`
- instance is one specific object
- data attribute values vary between instances
- instance has the structure of the class

## Demonstrating OOP by creating a Co-ordinate class

Firstly, we have to tell python we're defining our own type.
```python
class Coordinate(object):
	#define attributes here
```
`class <name/type>(<class parent>):`
An `object` is the very basic type in Python.
The word `object` means that `Coordinate` is a Python object, inherting all an `object`'s attributes. `Coordinate` is a subclass of `object`. `object` is a superclass of `Coordinate`.

Attributes are data and procedures that belong to the class. This means the data and the procedures that we're going to write only work with the object of this type. 
The *data attributes*
- Think of data as other objects which make up the class
- For example, a co-ordinate is made up of two numbers (x,y)

The *methods*
- A method is a function that is attached to an object.
- A method is a function that only works this particular type of object(class)
- how to interact with the object
- For example, you can define a distance between two co-ordinate objects, but there is no meaning to a distance between two list objects.

### How to create an instance of a class
We need to start by defining how to create an instance of object
We use a special method called `__init__` to initialize some data attributes.
```python
class Coordinate(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y
```
This tells python that when you create an object of this type (Coordinate), call this function. `self` is a placeholder for any instance where you create the object. 
`.` tells python to look for data value of that object. so `self.x` tells python to look for data value `x` that belongs to that class. 
After the `__init__` the first parameter is always `self` by convention. 
`self.x` means the x co-ordinate of the Coordinate data object is whatever value was passed in. 

We can create an instance of this class by calling it and passing arguments for it. We do not need to pass argument for *self* as Python does this automatically. For example with `c = Coordinate(3,4)` Python knows that *self* is `c`.
```python
c = Coordinate(3,4)
origin = Coordinate(0,0)
print(c.x)
print(origin.x)
```
Data attributes of an instance are called instance variables.

`print(isinstance(c, Coordinate))` we can use isinstance() to check if an object is a Coordinate.

### Defining a Method
Other that *self* and dot notation, methods behave just like functions (take parameters, do operations, return).
```python
class Coordinate(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def distance(self, other):
        x_diff_sq = (self.x-other.x)**2
        y_diff_sq = (self.y-other.y)**2
        return (x_diff_sq + y_diff_sq)**0.5
```
(self, other)
we can use *self* to use it to refer to any instance
we can use *other* as another paramter to method
When referring to classes, we always to see whose data attribute we are accessing. The dot notation is used to access data. 

### Using a method
```python
c = Coordinate(3,4)
origin = Coordinate(0,0)

#conventional way
print(c.distance(origin))
#c is the object to call method on (self) (self implied to be c)

#equivalent to
print(Coordinate.distance(c, origin))
#Coordinate is the name of the class
#.distance is name of method
#in parentheses we pass parameters (including self as this is the object to call the method on)
```

### Print representation of an object
Without an implict definition for printing the object we get an uninformative print representation by default.
We can implicitly define a `__str__` method for a class, Python calls this method when used with *print* on your class object. 
We can choose what it prints out, what we want it to show!
If we want to print `<x,y>`, something more informative.
```python
class Coordinate(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y
	def __str__(self):
		return "<" + str(self.x) + "," + str(self.y) + ">"
    def distance(self, other):
        x_diff_sq = (self.x-other.x)**2
        y_diff_sq = (self.y-other.y)**2
        return (x_diff_sq + y_diff_sq)**0.5
```
`__str__` MUST return a string. It also only takes *self* as we are calling print on the object itself.

### Special Operators
https://docs.python.org/3/reference/datamodel.html 3.3.8
`+,-,<,>,len(),print` and many other
These can be overridden to work with our class.
We can define them like such
`__add__(self, other)`		-> self + other
`__sub__(self, other`		 -> self - other
`__eq__(self,other)`		  -> self == other
`__lt__(self,other)`		  -> self < other
`__len__(self,other)`		 -> len(self)
.. and others
If you do not implement one of these methods for example `__add__` and try to add two objects of that type we will get an error as python doesn't know how to add these two objects. We can tell it how to do that by implementing that special operator.

### Fraction Object
```python
class Fraction(object):
    """
    A number represented as a fraction
    """
    def __init__(self, num, denom):
        """ num and denom are integers """
        assert type(num) == int and type(denom) == int, "ints not used"
        self.num = num
        self.denom = denom
    def __str__(self):
        """ Retunrs a string representation of self """
        return str(self.num) + "/" + str(self.denom)
    def __add__(self, other):
        """ Returns a new fraction representing the addition """
        top = self.num*other.denom + self.denom*other.num
        bott = self.denom*other.denom
        return Fraction(top, bott)
    def __sub__(self, other):
        """ Returns a new fraction representing the subtraction """
        top = self.num*other.denom - self.denom*other.num
        bott = self.denom*other.denom
        return Fraction(top, bott)
    def __float__(self):
        """ Returns a float value of the fraction """
        return self.num/self.denom
	#inverse is our own function
    def inverse(self):
        """ Returns a new fraction representing 1/self """
        return Fraction(self.denom, self.num)
```

```python
a = Fraction(1,4)
b = Fraction(3,4)
c = a + b # c is a Fraction object
print(c)
print(float(c))
print(Fraction.__float__(c))
print(float(b.inverse()))
##c = Fraction(3.14, 2.7) # assertion error
##print a*b # error, did not define how to multiply two Fraction objects
```

# OOP Recap
Animal abstract data type
```python
class Animal(object):
    def __init__(self, age):
        self.age = age
        self.name = None
```

```python
	# getters
	def get_age(self):
        return self.age
    def get_name(self):
        return self.name
```
Getters return the values of any data attributes.

```python
	# setters
	def set_age(self, newage):
        self.age = newage
    def set_name(self, newname=""):
        self.name = newname
```
Setters set the data attributes to whatever is passed in.

```python
	def __str__(self):
        return "animal:"+str(self.name)+":"+str(self.age)
```        
This tells python how to print an object of this type.

Instantiation creates an instance of an object.
```python
a = Animal(3)
```
dot notation is used to access attributes (data and methods). Better to use getters and setters to access data attributes.
```python
a.age			# Allowed but not recommended
a.get_age()
```
Classes and oop is used to abstract data. We should be abstracting these data attributes. Users should not need to know how the class is made up, they should just know how to use the class. 

Author of the class definition also may change data attribute variable names. So, if you are accessing data attributes outside the class and class definition changes, you may get errors.
So, outside of class, use getters and setters (`a.get_age()` **NOT** `a.age`),
- good style
- easy to maintain code
- prevents bugs

Some example of bad style allowed by pythonwhen accessing data attributes (don't do this):
`print(a.age)` we're allowed to access data from outside class definition
`a.age = 'infinite'` we're allowed to write data from outside class definition
`a.size = "tiny"` we're allowed to create data attributes for an instance from outside class definition
BAD STYLE!!! Don't do this.

## Default Arguments
Default argument for formal parameters are used if no actual argument is given.
```python
    def set_name(self, newname=""):
        self.name = newname
```
For example the default would be used here.
```python
a = Animal(3)
a.set_name()
print(a.get_name())
```
Remember we've said we need to pass in parameters other than *self*. However, this is okay as *newname* has a default argument. 
This default argument is shown by this 
```
newname=""
```
This tells Python that if no parameters are passed in, use what is there by default.

Argument passed in is used here
```python
a = Animal(3)
a.set_name("luffy")
print(a.get_name())
```

# Inheritance
## Hierarchies
The great thing about OOP is abstraction. 
- parent class
	(superclass)
- child class
	(subclass)
	- inherits all data and behaviours (methods) of parent class
	- add more info 
	- add more behaviour 
	- override behaviour

So imagine an *Animal* class, this is our parent class. Inheriting from this *Animal* class we have these child classes (subclasses): *Person, Cat, Rabbit*. Whatever an *Animal* can do a *Person* can do, and a *Cat*, and *Rabbit*. So the child classes inherit the data and methods of the parent *Animal* class. 

### Parent Class
```python
class Animal(object):
```
`object`, everything is an object, the class *object* implements basic operations in Python such as binding variables, etc. 

### Subclass
Now let's create a subclass of `Animal`.
Everything that an *Animal* can do, a *Cat* can do, like the getters and setters. 
```python
class Cat(Animal):
    def speak(self):
        print("meow")
    def __str__(self):
        return "cat:"+str(self.name)+":"+str(self.age
```
We've added new functionality with `speak()`.
Instance of type *Cat* can be called with new methods. Instance of type *Animal* gives an error if it's called with *Cat*'s new method. 
`__init__` is not missing as it uses the `Animal` version (Python see's there is no `__init__` in this particular class so it looks to the parent class `Animal`).
We're also over-riding the `__str__`, priting a different message. When you call a method on a class, Python looks to see if the current class has a definition for that method, if not it looks at the parent, and then the next until it finds a definition. 

```python
class Person(Animal):
    def __init__(self, name, age):
        Animal.__init__(self, age)	# Call Animal constructor
        self.set_name(name)			# Call Animal's method
        self.friends = []			# add a new data attribute
```
We can see here we've overwritten the `__init__` method. We call the Animal constructor so we can create a name and age for it. We can then set the name and create friends for it. 

We then have new methods
```python
    def get_friends(self):
        return self.friends
    def speak(self):
        print("hello")
    def add_friend(self, fname):
        if fname not in self.friends:
            self.friends.append(fname)
    def age_diff(self, other):
        diff = self.age - other.age
        print(abs(diff), "year difference")
    def __str__(self):
        return "person:"+str(self.name)+":"+str(self.age)
```

Once we have the *Person* type we can have a *Student* type.
```python
class Student(Person):
    def __init__(self, name, age, major=None):
        Person.__init__(self, name, age)    
        # Python already knows how to initialize Person so ask's Python to do that
        self.major = major
    def __str__(self):
        return "student:"+str(self.name)+":"+str(self.age)+":"+str(self.major)
    def change_major(self, major):
        self.major = major
    def speak(self):
        r = random.random()
        if r < 0.25:
            print("i have homework")
        elif 0.25 <= r < 0.5:
            print("i need sleep")
        elif 0.5 <= r < 0.75:
            print("i should eat")
        else:
            print("i am watching tv")
```
Remember to `import random` as we use the `random` class. `import random` brings in methods from the `random class.` 

```python
s1 = Student('alice', 20, "CS")
s2 = Student('beth', 18)
# We have init'd two students, one with a default argument
```

## Class Variables
So far we've seen instance variables. `self.age`. These are common between all of the instances of the class, they all have this variable. But the value of the variable is different throughout the classes. 

Class variables are defined inside the class definition but outside the init. Inside the init it tells us how to create a Rabbit object. 
`tag = 1`
We then create an instance variable `self.rid` and we set it to the value of the accessed class variable.
```python
        self.rid = Rabbit.tag
        Rabbit.tag += 1
```
The `__init__` causes the `tag` to be +=1. So when we create any other instances of Rabbit, they'll be accessing the updated value of tag, instead of the old one. 

Class variables are a shared variable part of the Class. They can be updated but they can't be called with `self` they need to be called directly for example with `Rabbit.tag`. Class variables are shared with all instances, so they can all modify them. But the instance variables are ONLY for that particular instance. 
```python
class Rabbit(Animal):
    # a class variable, tag, shared across all instances
    tag = 1
    def __init__(self, age, parent1=None, parent2=None):
        Animal.__init__(self, age)
        self.parent1 = parent1
        self.parent2 = parent2
        self.rid = Rabbit.tag
        Rabbit.tag += 1
    def get_rid(self):
        # zfill used to add leading zeroes 001 instead of 1
        return str(self.rid).zfill(3)
    def get_parent1(self):
        return self.parent1
    def get_parent2(self):
        return self.parent2
    def __add__(self, other):
        # returning object of same type as this class
        return Rabbit(0, self, other)
		# set's the parents to the two being added together
    def __eq__(self, other):
        # compare the ids of self and other's parents
        # don't care about the order of the parents
        # the backslash tells python I want to break up my line
		# compare rid or would loop
        parents_same = self.parent1.rid == other.parent1.rid \
                       and self.parent2.rid == other.parent2.rid
        parents_opposite = self.parent2.rid == other.parent1.rid \
                           and self.parent1.rid == other.parent2.rid
        return parents_same or parents_opposite
    def __str__(self):
        return "rabbit:"+ self.get_rid()

print("\n---- rabbit tests ----")
print("---- testing creating rabbits ----")
r1 = Rabbit(3)
r2 = Rabbit(4)
r3 = Rabbit(5)
print("r1:", r1)
print("r2:", r2)
print("r3:", r3)
print("r1 parent1:", r1.get_parent1())
print("r1 parent2:", r1.get_parent2())

print("---- testing rabbit addition ----")
r4 = r1+r2   # r1.__add__(r2)
print("r1:", r1)
print("r2:", r2)
print("r4:", r4)
print("r4 parent1:", r4.get_parent1())
print("r4 parent2:", r4.get_parent2())

print("---- testing rabbit equality ----")
r5 = r3+r4
r6 = r4+r3
print("r3:", r3)
print("r4:", r4)
print("r5:", r5)
print("r6:", r6)
print("r5 parent1:", r5.get_parent1())
print("r5 parent2:", r5.get_parent2())
print("r6 parent1:", r6.get_parent1())
print("r6 parent2:", r6.get_parent2())
print("r5 and r6 have same parents?", r5 == r6)
print("r4 and r6 have same parents?", r4 == r6)
```
