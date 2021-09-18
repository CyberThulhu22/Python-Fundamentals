## Types of Knowledge
Declarative knowledge is a **statement of fact**. Something will happen etc.
An example is, the square of a number x is y such that y * y = x

Imperative knowledge is a recipe or "how to". How to make something happen. A bunch of steps.
Recipe for deducing square root of a number x (16)
1) Start with a guess,g 
2) If g * g is close enough to x, stop and say g is the answer
3) Otherwise, make a new guess by averaging g and x/g
4) Using the new guess, repeat process until close enough

## An algorithm is:
1) Sequence of simple steps
2) Flow of control process that specifies when each step is executing
3) A means of determing when to stop


## Basic Machine Architecture
Memory:
- Contains sequence of instructions
- Contains Data

Connected to the ALU
- Does primitive operations (+/-x)

The control unit contains the program counter for the sequence of instructions. Starts at the first instruction. The CU gets that instruction and sends it to the ALU. The ALU gets input from memory. And returns output back to memory. Then tells the CU and the control unit is incremented by 1.

Connected to input/output

## Basic Primitives
Turing showed you can compute anything with 6 primitives.
Move left, right. Read, write, scan and do nothing. With those 6 instructions and tape he showed you can compute anything.

A programming language provides a set of primitive operations that come with the language. Using these primitive constructs we can create expressions that are syntactically valid. Semantics is the meaning associated witht he syntactically correct string of symbols. In programming languages, the program you write only has one meaning. The computer does what you tell it to do. 
Syntactic errors are common and easily caught.
Static semantic errors (when your code isn't doing what you meant it to do)

## Objects
Everything is an object in python.
Programs manipulate data objects.
All objects can have a type that define the kind of things the programs can do to them. 
	For example if an object is 5, you can add other numbers, subtract other numbers. 

Objects are either 
- Scalar and cannot be subdivided (e.g. 5, very basic objects)
	int
	float
	bool *True* or *False*
	NoneType (special and has one value *None*)
- Non-scalar, can be subdivided (e.g. a list of numbers. It can be seperated as it's a sequence of numbers)

See the type of an object
`type()`

Type conversions (cast)
`type(object)`
For example `float(3)` converts 3 to 3.0
or `int(3.9)` truncates float 3.9 to integer 3. (doesn't round).

Once you have objects you can combine them with operators to form expressions. These expressions have a value, which has a type. 
Syntax for a simple expression is something like
`<object> <operator> <object>`

### Math Operators
If both are ints, result is int
If either or both are floats, result is float
`i + j`
`i - j`
`i * j` 
`i / j` --> Result is float (python3)

`i % j`  --> remainder of when i is divided by j 
`i ** j` --> i to the power of j 

#### Shortcuts
`a += 1` a = a + 1
`a -= 1` a = a - 1
`a *= 2` a = a * 2
`a /= 10` a = a / 10
`a //= 2` a = a // 2
`a %= 5` a = a % 5

**Remember it with**
`a=-1` is the incorrect order for the operators. It will assign `-1` to the variable `a`.

Precedence just like maths. If you want to put precedence to other, you can use brackets. Always use parentheses when doing math operations. 

**Be careful with**
When `x = 5`
Floor math operator (divided and drops decimal) `x = x // 2` = `2`.
In python2 `x = x / 2` = `2` which can cause compatability issues as in python3 it = `2.5`.

#### Stuff that isn't an Object
- Keywords. To view these we can `import keyword` and view `keyword.kwlist`.
- Literals (strings or number values we put in programs)
- Operators for calculations (`+,-,/,//,*,%,<<,^,|,&`)
- Delimiters which seperate parameters and build data structures (`, [] {} () :`)
- Comments `#`
- Preloaded variables, about 150 variables with values or code that are stored in the `__builtins__` module. We can view these with `dir(__builtins__)`
	- We can assign these preloaded variables to other variables and call these.
	- `mark = print` and `mark("Hello world")` would print "Hello world".
	- If you accidently modify a value we can restore it with `del print`.

### Bit Math Operators
`&`	bitwise AND format(0b10101010 & 0b00001111, "08b")
`|`	bitwise OR format(0b10101010 | 0b00001111, "08b")
`^`	bitwise XOR
Shifting to the left one place multiplies the value by two for each bit shifted.
`<<` shift bits left format(0b10101010 << 2, "08b")
`>>` shift bits right format(0b10101010 >> 3, "08b")
`~` bitwise complement format(~0b10101010, "08b")

## Variables
Variables are a label for some location in memory where we're going to store a value or object.

To view the variables you have created in your Python shell.
`globals()`

The equal sign is an assignment of a value to a variable name.
`variable = value`
The left is set to the value. This value is stored in computer memory. When assigning a variable, Python automatically assigns the type. Variables can point to the same value.

Expression on the right, evaluated to a value and the variable name on the left, ALWAYS ONLY ONE THING TO THE LEFT HAND SIDE! The expression on the right hand side is always evaluated first. 

When we write `pi = 3.14`
3.14 is stored in memory and then binded to the variable name *pi*.
When we do something like `pi += 1` we'll still have the old value of pi in memory but we'll have the new value in memory binded to pi. But we've lost the handle for this value. 

We can swap the contents of variables without using a temporary variable with tuples.
`a,b,c,d = d,c,b,a` This creates a tuple and extracts the values.

## Base Assignments
We can also assign integers in base2 and base16.

Hexadecimal assignment
```python
a = 0xff00
a = int("ff00", 16)
```
Even if we assign as hex it'll be stored as a decimal number. To see variable a as a hexadecimal we can call `hex(a)`.

Base2
```python
b = 0b11000101
b = int("0b11000101", 2)
```
To see integer value as a binary `bin(b)`


## Comparison Operators
Assume that *i* and *j* are variables.
Following comparisons evaulate to a Boolean
`i > j`
`i >= j`
`i < j`
`i <= j`
`i == j` --> equality test, *True* if *i* is the same as *j*
`i != j` --> inequality test, *True* if *I* is not the same as *j*
If comparing strings it looks at position in alphabet.

## Logic Operators on *bools*
*a* and *b* are variable names
`not a` --> *True* if *a* is *False*
					*False* if *a* is *True*
`a and b` --> *True* if both are *True*
`a or b` --> *True* if either or both are *True*

The Boolean `and` operator takes precedence over the `or` operator.
`True or True and False` = `True`
`(True or True) and False` = `False`

---

## Output
*print* is used to output stuff to console, it sends information to standard output.
If you `print(var1,var2)` python automatically inserts a space for you
If you don't want this you can use the `+` to concatenate strings.
```python
####################
## EXAMPLE: output 
####################
x = 1
print(x)
x_str = str(x)
print("my fav number is", x, ".", "x=", x)
print("my fav number is", x_str + "." + "x=" + x_str)
print("my fav number is" + x_str + "." + "x=" + x_str)
```


## Input
Prints whatever is in the quotes
User types something and hits enter
Binds that value to a variable
```python
text = input("Type anything... ")
print(5*text)
```
As `input()` gives a string, it must be type cast if working with number
```python
num = int(input("Type a number... "))
print(5*num)
```

---

## Control Flow - Branching
```python
if <condition>:
	<expression>
	<expression>
	...
```
The condition is checked, it's evaluated to *True* or *False*. If the condition is *True* it'll execute the extra set of expressions. If *False* it won't execute these expressions. Everything that is indented is part of the expression that are executed.

```python
if <condition>:
	<expression>
	<expression>
	...
else:
	<expression>
	<expression>
	...
```
This will do one set of instructions, never both. After either one is executed, it continues with regular execution of the code.

```python
if <condition>:
	<expression>
	<expression>
	...
elif <condition>:
	<expression>
	<expression>
	...
else:
	<expression>
	<expression>
	...
```
If first condition is not *True*, it'll check the next elif. If that is not *True* it'll catch all and it'll execute the last set of expressions. You'll never enter more than one codeblock.

For example
```python
x = float(input("Enter a number for x: "))
y = float(input("Enter a number for y: "))
if x == y:
    print("x and y are equal")
    if y != 0:
        print("therefore, x / y is", x/y)
elif x < y:
    print("x is smaller")
elif x > y:
    print("y is smaller")
print("thanks!")
```

We can use a shortcut for if with the ternary operator so we don't have to do this.
```python
if y == 5:
	x = 10
else:
	x = 11
```
or we can do this
```python
x = 10 if y==5 else 11
```


## While Loops
As long as the condition is true, the loop is executed. 
```python
while <condition>:
	<expression>
	<expression>
	...
```

The condition evaluates to a Boolean, if *True* do all the steps inside the while code bock. Then check the condition again, repeat until the condition is *False*.

For example
```python
n = input("You're in the Lost Forest. Go left or right? ")
while n == "right":
    n = input("You're in the Lost Forest. Go left or right? ")
print("You got out of the Lost Forest!")
```

Iterate through numbers in a sequence
```python
n = 0			# initialize the loop counter
while n < 5:
    print(n)
    n = n+1		# increment the loop counter
```

## For Loops
```python
for <variable> in range(<some_num>):
	<expression>
	<expression>
	...	
```
Each time through the loop, variable takes a value starting with the smallest value, then previous value + 1 until the list of values are exhausted.
`range(start, stop, step)`
If you only give it one parameter, this is the `stop`.
`range(3)`
If you give it two parameters, this is `start` and `stop`.
`range(7,10)` 
If you give it three parameters, this is the `start`, `stop`, and `step`.
`range(2,20,2)`
You always go until the value `stop` - 1.

```python
for n in range(5):	# range(5) creates a sequence of numbers 0 to 4
    print(n)
```

 For loops iterate through only one string.
We can use the enumerate() to build an iterable tuple list.
```python
>>> list(enumerate(cool))
[(0, 'Grey'), (1, 'green'), (2, 'Blue')]
>>> list(cool)
['Grey', 'green', 'Blue']
```

```python
for index, value in enumerate(cool):
	print("{} is in position {}".format(value, index))
# Grey is in position 0
# green is in position 1
# Blue is in position 2
```

### Example XORing Data and Keys
```python
>>> def xor_strings(str1, str2):
...     results = ''
...     for index, a_char in enumerate(str2):
...         results += chr(ord(str1[index]) ^ ord(a_char))
...     return results
... 
>>> xor_strings("THISSTRING","THISONE")
'\x00\x00\x00\x00\x1c\x1a\x17'
```

## Break Statement
Immediately exits whaterver loop it is in, it also skips remaining expressions in code block. Exits only the most innermost loop.
```python
while <condition_1>:
	while <condition_2>:
		<expression_a>
		break			# we will exit out of the innermost loop (2)
		<expression_b>	# this will not be evaluated
	<expression_c>		# this will be evaluated as it is part of the outer while loop
```

*for* loops 
- know number of iterations
- can end early via *break*
- uses a counter
- can rewrite a *for* loop using a *while* loop

*while* loops
- unbounded number of iterations
- can end early via *break*
- can use a counter but must initialize before loop and increment it inside loop
- may not be able to rewrite a *while* loop using a *for* loop

## Case/Switch Control Structures
We can use a dictionary of functions to perform case/switch statements.
This example executes function `a()` when the variable `i` is even and function `b()` when it is odd.
```python
def a():
    print("A",end=" ")

def b():
    print("B",end=" ")

case={0:a,1:b}

for i in range(20):
    case[i%2]()
```

case `{0: <function a at 0x7f2c6a385c80>, 1: <function b at 0x7f2c69cfa840>}`

## Interactive Prompt
We can use the `_` to bound the return value of the previously executed statement in the interactive prompt.
```python
>>> True
True
>>> yes=_
>>> yes
True
```

## Python2 to Python3
2to3.py will upgrade the program.