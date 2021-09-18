## Functions
Functions are a mechanism to achieve decomposition and abstraction. 

Abstraction, you do not need to know a projector works in order to use it.
- A projector for example is a black box. Don't know how it works, but we know the input and the output. This is the idea of abstraction
We can surpress details with abstraction.
Code can be thought of as a black box:
- cannot see details
- do not need to see details
- hide boring coding details
We can achieve abstraction with function specifications, or docstrings(function specification that tells anyone else who wants to use it, how to use it)


Decomposition, is when different devices work together to achieve a same, common, end goal.
You can create structure in code with decomposition. 
We divide code into modules:
- self contained
- used to break up code
- reusable
- organized
- keep code coherent
We'll achieve decomposition with functions, however it can also be achieved with classes.

Functions are reusuable pieces of code which are not executed until called.
Functions have:
- a name
- parameters (>=0)
- docstring (not necessary) (how you achieve abstraction)
- a body
- returns something


```python
def is_even_with_return( i ):
    """ 
    Input: i, a positive int
    Returns True if i is even, otherwise False
    """
    print('with return')
    remainder = i % 2
    return remainder == 0
```
`def` is a keyword, tells python that we're going to define a function
`is_even_with_return` then we have the name of the function, descriptive name 
`( i )` parameters or arguments, inputs into the function
`"""` This is the docstring, starts and ends with `"""`. It should have inputs, returns and what the function is going to do
Then there is the `body` of the function.
Everything indented is part of the function. 
When we call the function we can call it's name and give it it's parameters. for example
`is_even_with_return(3)`

When there is no *return* statement. Python automatically returns the value *None* if no *return* is given. This represents the absence of a value.

Inside a global scope for example you can have the variable `x` but when you are inside the scope of a function, you are in a different scope and you can have the variable `x` without affecting the global scope `x`.

However, if `x` isn't defined in a function scope it'll look in the global scope.

```python
def test(y):
	print(x)
	
x = 5
```
For example here python will look for the value of x outside of print.

In this example, we try to access `x` and increment it and reassign it. This is not allowed. This will cause an error.
```python
def h(y):
	x+= 1
	
x = 5
h(x)
print(x)
```
Global variables are frowned upon. They give you a way to avoid scope and it gets very messy! Defeats the purpose of functions. 
Inside a function, we **cannot modify** a variable defined outside, we can use global variables however.

## Scope
Scope is another word for enviroment.
Formal parameter gets bound to value of actual parameter when function is called.
**New scope/enviroment is created when we enter a function.** 
Scope is mapping of names to objects.

```python
def f(x):
```
x is our formal parameter as we assume x will have some sort of value.

The values that are passed into the function called e.g. `f(3)` are called actual parameters as they have actual values.

[Understand Python Sope Better](http://www.pythontutor.com/visualize.html#mode=display)

We can define a variable with global scope with `global()`. So `global varName`.

## Namespaces
Namespaces are containers that store variable names.  
- Global Variables are in the "Global" namespace
- Every Function has a separate "Local" namespace
- Every Class has a separate namespace.
- Modules imported with the syntax `import <modulename>` get their own namespace.
- Modules imported with `from <modulename> import *"` are added to the "Global" namespace.

## Function Arguments
Arguments can be assigned by default values, making them optional arguments.
```python
def myfunction(a, b, c=5):
	print(a, b, c)

myfunction(1,2,7)
# 1, 2, 7
myfunction(1,2)
# 1, 2, 5

# Keyword Arguments
myfunction(b=10, a=7, c=9)
# 7, 10, 9
```

We can declare what type of arguments are accepted by a function. However, typing is not enforced by Python.
```python
def add(num1:int, num2:int)->str:
	return num1+num2
	
# Function should return a string, but it returns an integer.
```

`pip install mypy`
We can use type checking modules to identify errors.
`python3 -m mypy add.py`


## Modules
We can save a program with our functions for example module_name.py. We can then `import module_name`.
To view the functions we can use `dir(module_name)`.
We can then use `module_name.function_name()`. 
This is better as it prevents name collisions. It also allows for greater code readability and knowing which module function is used where.  

Or we can do `from module_name import *`. This causes everything that's in that module into the global namespace. So we no longer need to use the `module_name` namespace any longer.
We can import specific functions with `from module_name import module_function`. 

To get help for a function
`help(module_name.function)`
This looks at the docstring of the function which is the first string in `""" """`.

When you import a function, Python looks in the directories in sys.path to find the code.
`python3 -c "import sys; print(sys.path)"`
You can add new directories with `sys.path.append('/new/path')`

### Dunder Name
When you import a program into a Python script it is executed. When you import programs the variable `__name__` will be `__main__` but if you are importing it the `__name__` will be the name of the Python script.

```python
# For what's available inside modules
import sys
def main():
	if not "-u" in sys.argv:
		sys.exit(0)
	print("You passed the argument" + sys.argv[1])

# Only executed when run V

if __name__ == "__main__":
	#Global variables go here
	main()
```

## Lambda Functions

`lambda <input> : <var> + 1`
`<var> + 1` is the output
Assign a variable to a lambda function (**NEVER DO THIS**)
```python
int = lambda number : number + 1
print(inc(5))
```

Drop the name with lambda in parentheses
```python
(lambda number : number + 1)(5)
```
We can pass lambda functions to functions like map() or sort().
```python
>>> customers=["Mike Mike","John Doe","Robinson Clayton"]
>>> sorted(customers, key=lambda x:x.lower() )
['John Doe', 'Mike Mike', 'Robinson Clayton']
>>> # Sort on lower case
... 
>>> sorted(customers, key=lambda x:(x.split()[1]+x.split()[0]).lower())
['Robinson Clayton', 'John Doe', 'Mike Mike']
>>> # Sort on Last First
... 
```
