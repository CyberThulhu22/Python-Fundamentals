## Perfect Cube 
Given a problem, find the cube root of a number, you can guess the cube root of a number. 
Guess another value systematically, or exhaust all the possible values. 
Perfect Cube Example
```python3
cube = 27
#cube = 8120601
for guess in range(cube+1):
    if guess**3 == cube:
        print("Cube root of", cube, "is", guess)
        # loops keeps going even after found the cube root
```

## Guess and Check
```python
cube = 27
#cube = 8120601
for guess in range(abs(cube)+1):
    # passed all potential cube roots
    if guess**3 >= abs(cube):
        # no need to keep searching as greater than cube
        break
if guess**3 != abs(cube):
    print(cube, 'is not a perfect cube')
else:
    if cube < 0:
        guess = -guess
    print('Cube root of ' + str(cube) + ' is ' + str(guess))
```

Sometimes we do not care if it is not a perfect cube, so we want an approximate solution. So we will start with a guess and increment until we find a good enough solution. 

Keep guessing if
`|guess³ - cube| >= epsilon`
Decrementing increment size --> slower program
Increasing epsilon	--> less acurate answer
Approximate cube root
```python
cube = 27 
epsilon = 0.01
guess = 0.0
increment = 0.0001
num_guesses = 0
while abs(guess**3 - cube) >= epsilon and guess <= cube: 
	guess += increment					# keep on guessing
	num_guesses += 1
print("num_guesses =", num_guesses)
if abs(guess**3 - cube) >= epsilon:
	print("Failed on cube root of", cube)
else:
	print(guess, "is close to the cube root of", cube)
```

## Bisection Cube Root
With bisection search we eliminate half the search space. The larger the space we need to search, the btter it is to use bisection search.
1. Half interval each iteration
2. New guess is halfway in between
3. Higher or lower

```python
cube = 27
#cube = 8120601
# won't work with x < 1 because initial upper bound is less than ans
#cube = 0.25
epsilon = 0.01
num_guesses = 0
low = 0
high = cube
guess = (high + low)/2.0
while abs(guess**3 - cube) >= epsilon:
    if guess**3 < cube:
        # look only in upper half search space
        low = guess
    else:
        # look only in lower half search space
        high = guess
    # next guess is halfway in search space
    guess = (high + low)/2.0
    num_guesses += 1
print('num_guesses =', num_guesses)
print(guess, 'is close to the cube root of', cube)
```
If the guess it too low, set the guess to be low as we don't care about the other numbers. We create new boundaries and make another guess between these new boundaries. We keep on doing this until we get out number. 

### Convergence
Search space:
- first guess: N/2
- second guess: N/4
- kth guess: N/2ᵏ
2ᵏ=N
k=log2N

The guess converges on the order of log2N steps. So where N is  76 log2N would be 6 and this is the number of guesses we would at least need.

This only works where N is greater than 1 however as the cube root of numbers less than one is greater than them, and with our code this is out of bounds.

