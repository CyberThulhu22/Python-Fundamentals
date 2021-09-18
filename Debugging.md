 ## Testing
 Testing is as simple as, coming up with inputs, figuring out what outputs you expect, and then running your program. Does the output of the program match what you expect, if it does great, if not it leads to debugging.
 
 1.	You start testing after you make sure your program runs.
 	Eliminate syntax and semantic errors. 
 2. Come up with test cases.

### Understanding Tracebacks
Read tracebacks from the bottom to top. Bottom line is most relevant.
 
 ### Classes of Tests
 Unit Testing
 - Validate that each piece of program
 - Testing each function separately

Regression Testing
- Add test for bugs as you find them
- Catch reintroducted errors that were previsouly fixed

Integration testing
- Does the overall program work?
- Tend to rush to do this

### Testing Approaches
Intuition about natural boundaries to the problem.
If no natural partitions, might do random testing?
- probability that code is correct increases with more tests.

Black box testing
- explore paths through specification
- look at the docstring

 Glass box testing
 - explore paths through code
- when you have access to code itself
Use the code directly to guide design of test cases.
*path-complete* if every potential path through code is tested at least once
However, some drawbacks are
- can go through loops arbitrarily many times
- missing paths

Some guidelines for glass box testing of loops
branches
- exercise all parts of a conditional

for loops 
- loop not entered,
- body of loop executed exactly once
- body of loop executed more than once

while loops
- same as for loops
- cases that catch all ways to exit loop

 ## Debugging
 Study events which lead up to an error. 
 Why is it not working?
How can I fix my program?

print() is very important for debugging.
They're good ways to test hypotheses.
 
 Put a print statement half way through to identify if the first half is buggy if it works, then you know the first half is not buggy so you eliminate it as possible buggy code. Then repeat for the remaining halves.
 The steps are 
 - Study program code
	 - don't ask what is wrong (this is what your test cases figured out)
	 - ask how did i get this unexpected result
	 - is it part of a family
 - scientific method
	 - study the available data
	 - form a hypothesis
	 - repeatable experiments
	 - pick simplest input to test with

Syntax errors are the easy errors. Logic errors are the harder ones. 
**Rubber ducky debugging**

## Error Messages
Error messages are called exceptions, it's an exception to what the program expected.

### Dealing with Exceptions
If you know a piece of code might give you an exception, Python can provide handlers for these exceptions.
```python
try:
    a = int(input("Tell me one number: "))
    b = int(input("Tell me another number: "))
    print("a/b = ", a/b)
except:
    print("Bug in user input.")
```
You can put any lines of code which you think might give an error inside a try block. For example, if someone puts strings in where integers are expected, an exception will be raised. Any exception raised in a body of *try* are handled by the *except* statement and execution continues within the body of the *except* statement. 

We can be more specific with our errors and have separate *except* clauses to deal with a particular type of exception.
```python
try:
    a = int(input("Tell me one number: "))
    b = int(input("Tell me another number: "))
    print("a/b = ", a/b)
    print("a+b = ", a+b)
except ValueError:
    print("Could not convert to a number.")
except ZeroDivisionError:
    print("Can't divide by zero")
except:
    print("Something went very wrong.")
```

We could have an *else:* block if the body of our *try* completed with no exceptions.
*finally:* is **always** executed after *try*, *else* and *except* clauses, regardless of if they raised another error or executed a *break*, *continue*, *return*.
	- This is useful for clean-up code that should be run no matter what else happened(e.g. close a file)
	
What to do with exceptions?
1. Fail silently (default values/continue) bad idea
2. return an error value e.g. return -1 or a value which represents the error (bad idea complicates code, requires check)
3. Stop execution, signal error condition
	`raise Exception("descriptive string")`

Exceptions can be used as control flow. Don't return special values when an error occurs, and then check whether 'error value' was returned.
Instead, raise an exception when unable to produce a result consistent with function's specifications.
`raise <exceptionName>(<arguments>)`
`raise ValueError("something is wrong")`

### Assertions
assert statements are used to make sure that the assumptions on computations are exactly what the function expects it to be.
```python
    assert len(grades) != 0, 'warning: no grades data'
	# assert <what the function expects>, <what to print if assertion does not hold>
	# we expect that the len(grades) !=0
```
If the assert is false, it does not continue, it stops. Assertions help to ensure pre and post conditions on functions are exactly as you expect. As soon as an assert is false, the function immediately terminates. It'll prevent the program from propagating bad values. 

Where to use assertions?
Spot bugs as soon as introduced and make it clear where they happened.
Use as a supplement to testing.
Raise exceptions if user supplies bad data input.
Use assertions to:
- check types of arguments or values
- check that invariants on data structures are met
- check constraints on return values
- check for violations of constraints on procedure (e.g. no duplicates)

### Python Debugger (PDB)
Add `import pdb; pdb.set_trace()` at the point you want to pause execution in the program.
You can view contents of variables and see what's going on.

`python -m pdb <script.py>` will run the entire script in the debugger from line 1.

`python -i <script.py>` launch an interactive shell after it crashes
`import pdb; pdb.pm()` once it crashes, use this.

Debugger commands  
```
h (help) [command] print help about commandn (next) execute current line of code, go to next line  
c (continue) continue executing the program until next  
breakpoint, exception, or end of the programs (step into) execute current line of code; if a function is  
called, follow execution inside the function  
l (list) print code around the current linew (where) show a trace of the function call that led to the  
current line  
p (print) print the value of a variableq (quit) leave the debugger  
b (break) [lineno | function[, condition]]  
set a breakpoint at a given line number orfunction, stop execution there if condition is  
fulfilledcl (clear) clear a breakpoint  
disable [breakpoint]
clear [breakpoint]
ignore [breakpoint] [# times]
! (execute) execute a python command<enter> repeat last command
n (next) executes until the 'next' line of code, stepping over functions
s (step) executes a single line of code, stepping into functions
```
 