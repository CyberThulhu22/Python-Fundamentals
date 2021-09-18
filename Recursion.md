Algorithmically: It's the idea of dividing a conquering. Taking a problem you want to solve, reducing it to a simpler version of the same problem and doing it again. 
Semantically: A programming technique where a function will call itself inside its body.
- Goal is NOT to have infinite recursion
- Must have 1 or more base cases that are easy to solve (base case is a way of stopping the unwinding of the problems)
- Must solve the same problem or some other input with the goal of simplifying the larger problem input

### Multiplication - Iterative Solution
Multiplying *a* * *b* is the same as adding *a* to itself *b* times.
We can capture state by an iteration number (*I*) which starts at b
	i <- b
	i <- i - 1 and stops at b (each time through the loop)
A current value of computation (*result*)
	result <- result + a
```python
def mult_iter(a, b):
	result = 0
	while b > 0:				# iteration
		result += a				# current value of computation, running sum
		b -= 1					# current value of iteration variable
	return result
```

### Multiplication - Recursive Solution
- Recursive step, think of how to reduce problem to a simpler/smaller version of the same problem

a * b = a + a + a + a + ... + a 
						 b times
		= a + (a + a + a + ... + a)
					b - 1 times
		= a + a * (b - 1)
		
- Base case, keep reducing the problem until reaching a simple case that can be solved directly
- when b = 1, a * b = a

```python
def mult(a, b):
	if b == 1:
		return a
	else:
		return a + mult(a, b-1)
```
			

### Factorial - Recursion
Our base case
n = 1			--> if n = 1:	
						 	return 1
n! = n * (n - 1) * (n - 2) * (n-3) * ... * 1

How to reduce the problem? Rewrite in terms of something simpler in order to reach the base case.
n*(n-1)!		--> else:
						   	  return n * factorial(n-1)
							  # this is the recursive step

```python
def fact(n):
	if n == 1:
		return 1
	else:
		return n*fact(n-1)
```
Recurses until base case, then returns so if fact(4) we'll get to base case then return 1, who asked for that? fact(2) then fact(3), returing the value for the recursed. 

Each recursive call to a function creates its own scope (enviroment).
Bindings of variables in a scope are not changed by recursive call.
**Flow of control passes back to previous call once function call returns value (hits base case then all the way back out)**

To do factorial iteratively we'd do something like this
```python
def factorial_iter(n):
	prod = 1
	for i in range(1,n+1):
		prod *= i
	return prod
```

Recursion may be simpler, more intuitive, and more efficient from programmer POV.
However, it may not be efficient from computer POV.

### Inductive Reasoning
We ask, how do we know that our recursive code will work?
```python
def mult_iter(a, b):
	result = 0
	while b > 0:				# iteration
		result += a				# current value of computation, running sum
		b -= 1					# current value of iteration variable
	return result
```
We know mult_iter() will terminate as b is positive, and decreases by 1 each time around loop, so it must eventually become less than 1.

```python
def mult(a, b):
	if b == 1:
		return a
	else:
		return a + mult(a, b-1)
```
mult() called with b = 1, will not recurse and it will stop.
mult() called with b > 1, makes a recursive call with a smaller version of b, it must eventually reach the call with b = 1.

If I want to prove a statement that runs over integers, and prove its true for all values of those integers, we prove it is true for the smallest value of n (0, 1) then we need to prove it's true for n+1. 
For example
0 + 1 + 2 + 3 + .. + n = (n(n+1))/2
We do the case n = 0 
	0 = 0 so it's true
Assume true for some k, we then need to show it is true for 
0 + 1 + 2 + .. + k + (k+1) = ((k+1)(k+2))/2
LHS is k(k+1)/2 + (k+1). 
This is equal to ((k+1)(k+2))/2

## Towers of Hanoi
I want to move a tower n, so i take a stack n -1, move the bottom one over, then I move the bottom one over. How do I move the smaller stack, recursively! Just unwind it.
```python
def printMove(fr, to):
    print('move from ' + str(fr) + ' to ' + str(to))

def Towers(n, fr, to, spare):
    if n == 1:
        printMove(fr, to)
    else:
        Towers(n-1, fr, spare, to)
        Towers(1, fr, to, spare)
        Towers(n-1, spare, to, fr)

print(Towers(4, 'P1', 'P2', 'P3'))
```

## Fibonacci
```python
def fib(x):
    """assumes x an int >= 0
       returns Fibonacci of x"""
    if x == 0 or x == 1:
        return 1
    else:
        return fib(x-1) + fib(x-2)
```

However, this is inefficient.
We can first do a look in case we have already calculated the value.
Modify dictionary as progress through function calls.
```python
def fib_efficient(n, d):
	# checks to see if it is in the dictionary
    if n in d:
        return d[n]
    else:
		# adds computed values to dictionary so they do not need to be done again
        ans = fib_efficient(n-1, d)+fib_efficient(n-2, d)
        d[n] = ans
        return ans
        
d = {1:1, 2:2}
```


## Palindromes
Base case: a string of length 0 or 1 is a palindrome.
Recursive case:
If first character matches last character, then is a palindrome if middle section is a palindrome.
```python
def isPalindrome(s):

    def toChars(s):
        s = s.lower()
        ans = ''
        for c in s:
            if c in 'abcdefghijklmnopqrstuvwxyz':
                ans = ans + c
        return ans

    def isPal(s):
        if len(s) <= 1:
            return True
        else:
			# check first and last element are the same
			# and slice the string ignoring the last and first element
			# and ask if that isPal()
            return s[0] == s[-1] and isPal(s[1:-1])

    return isPal(toChars(s))
```



