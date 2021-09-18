Strings are sequences of characters. They're also objects so we can use many operations to manipulate the strings. We can compare strings. Strings are immutable so we cannot change substrings within the string.

They're denoted by quotes. 
`'our string'`
`'''our string'''`
`"our string"`
`'''our string'''`

To include quots as part of the string we can alternate the type of quote (single/double) or escape with a backslash. **Quotes indicate an assignment of a literal string.**
`"This is a 'test'"`
`"This is a \"test\""`

To see all methods for a string create a string variable and `dir()` it.
`a="Example sring"`
`dir(a)`
If a function has `__` in it's name don't mess with it! It's internal for the Python program itself.
## Useful String Methods
var = "hello world!"
Uppercase: var.upper() "HELLO WORLD!"
Lowercase: var.lower() "hello world!"
Title Case: var.title() "Hello World!"
Replace Substring: var.replace('world','noob') "hello noob!"
Is substring in var: "world" in var	True
Convert to list: var.split() `['hello', 'world!']`
Count substrings: var.count('o') 2

You can chain methods together if they return a string.
## len
`len()` is a fucntion that retrieves the length of the string the parentheses
```python
s = "abc"
len(s)		# This evaluates to 3
```
It tells us how many characters in the strings.

To find the middle of a string
`len(string) // 2`

## Formatting Strings
We can build strings dynamically and plug in values and variables into the string.
```python
num = 3
astr = "First {} Second {} Third {}".format('X',2,num)
print(astr)
# First X Second 2 Third 3
```

If we place numbers inside the brackets we can use the corresponding argument in the format() method.
```python
astr = "First {2} Second {0} Third {1}".format('X',2,num)
print(astr)
# First 3 Second X Third 2
astr = "First {item1} Second {item2}".format(item1='X',item2=2)
print(astr)
# First X Second 2
```

### Format Specifiers
We can contain more than argument numbers.
`{ARG#:<fill><alignment><length><type>`
`{<#>:<F><A><L><T>}` For example `{0:X^20s}`
`#` = Argument Number: Identify corresponding argument in the format method
`F` = Fill Character to fill any empty string space when aligning
`A` = Align: "<" = Left, "^" = Center, ">" = Right
`L` = Lenght of the string when aligned
T = Type as a letter indicating variable type.
x: hex
X: Uppercase Hex
b: Binary
d: Decimal
f: Float
s: String
%: Percent sign
e: Exponetnial Notation
o: Octal
c: Integers to char
```python
>>> "Center 20 wide [{0: ^20}]".format("centered") 
'Center 20 wide [      centered      ]'
>>> "Left 20 wide [{0:X<20}]".format("LEFT")
'Left 20 wide [LEFTXXXXXXXXXXXXXXXX]'
>>> "Floats with precision {0:0>6.2f}".format(3.14)
'Floats with precision 003.14'
>>> "Formatted HEX {0:0>10x}".format(255)
'Formatted HEX 00000000ff'
>>> "Formatted binary {0:0>8b}".format(85)
'Formatted binary 01010101'
```

In python3.5> we can use a lowercase "f" ourtside the quotes and use the variable names instead of positions.
```python
>>> name = "noob"
>>> rating = "massive noob"
>>> f"{name} is a {rating:*^20}"
'noob is a ****massive noob****'
```

C style Format Strings
```python
>>> "Centered String [%10s]" % ("HI".center(10))
'Centered String [    HI    ]'
```

## Raw Strings
"r" outside of the string makes a string *raw* telling it not to interpret any of the characters.
```python
>>> print("python \"stinks\"\b\b\b\b\b\b\b\b \"rock")
python  "rocks"
>>> print(r"python \"stinks\"\b\b\b\b\b\b\b\b \"rock")
python \"stinks\"\b\b\b\b\b\b\b\b \"rock
```

## Indexing
Square brackets are used for indexing and tells python that we want to know what character is at a certain position inside a string.
```python
s = "abc"

s[0]	# Evaluates to "a"
s[2]	# Evaluates to "c"
s[3]	# Evaluates to OOB, error
s[-1]	# Evaluates to "c"
s[-3]	# Evaluates to "a"
```
Indexing always starts at 0.
`string_variable[index]` is the general syntax for indexing.

### Slicing
We can slice strings also with square brackets []
`[start:stop:step]`
If we give two numbers `[start:stop]` step=1 by default.
We can also omit numbers and just leave colons. 
We stop at `stop-1`
```python
s = "abcdefgh"
s[3:6] = "def"			# same as s[3:6:1]
s[3:6:2] = "df"
s[::] = "abcdefgh"		# same as s[0:len(s):1]
s[::-1] = "hgfedcba"	# same as s[-1:-(len(s)+1):-1]
s[4:1:-2] = "ec"	
```

Strings are immutable, so they cannot be modified.
```python
s = "hello"
s[0] = 'y'		# This would give an error
s = 'y' + s[1:len(s)]
```
The string object does not support item assignment.
For example we create `s = "hello"`. `"hello"` is in memory and binded to `s`. When we do `s = 'y' + s[1:len(s)]` python breaks it bond with `"hello"` in memory and binds the string variable `s` to the new object. 

We can use bytearrays() as they are a mutable data structure.
```python
>>> x = bytearray(b"HellO")
>>> x[0:4] = b"Byee"
>>> x
bytearray(b'ByeeO')
>>> x.decode()
'ByeeO'
```


## Byte Strings
"b" means the string is byte values between 0 and 255
```python
>>> b"decode will convert these bytes to a string".decode()
'decode will convert these bytes to a string'
```

### Converting between bytes() and str()
```python
>>> b"\x41\x42\x43"
b'ABC'
>>> bytes([0x41,0x42,0x43])
b'ABC'
>>> bytes([0x41,0x42,0x43]).decode()
'ABC' # Returns a string
>>> 'ABC'.encode()
b'ABC' # Returns bytes
```

Encoding a single byte "\x80" (over 127) turns it into 2 bytes. 
First byte is C2 or binary 11000010 (110 indicates 2 bytes, 00010 is the first 5 bits of the value being stores (0x80)).
To turn binary data into a string, always encode with LATIN-1, which has 255 values.
```python
>>> '\x7e'.encode("utf-8")
b'~'
>>> '\x7f'.encode("utf-8")
b'\x7f'
>>> '\x80'.encode("utf-8")
b'\xc2\x80'
>>> bin(0xc2)
'0b11000010'
>>> bin(0x80)
'0b10000000'
>>> '\x7e'.encode("latin-1")
b'~'
>>> '\x80'.encode("latin-1")
b'\x80'
```

### Encoding characters in a String
`\x` followed by 2 hex digits encodes a single byte character
`\u` followed by 4 hex digits encodes a 2-byte character
`\U` followed by 8 hex digits encodes a 4-byte character
`\U`  needs to be followed by 8 hex digits so when we try store this path it'll throw an errror if we don't use "r" to signify raw bytes.
```python
>>> windows_path = r"c:\Users"
>>> windows_path
'c:\\Users'
```

### Encoding and Decoding Integers
`chr()` converts an `int()` into a character
```python
>>> chr(65)
'A'
>>> chr(128013)
'🐍'
```
`ord()` is the opposite and converts a `chr()` into an `int()`.
## for Loops
*for*  loops have a loop variable that iterates over a set of values. 
```python
for var in range(4):		# var iterates over values 0-3
	<expressions>			# expressions inside executed with each value of var
```

`range` is a way to iterate over numbers, a *for* loop variable can iterate over any set of values, not just numbers.

`for` loops can be iterated over strings.
```python
s = "abcdefgh"
for index in range(len(s)):
	if s[index] == 'i' or s[index] == 'u':
		print("There is an i or u")

# This is a lot more pythonic way of doing it, cleaner
for char in s:
	if char = 'i' or char == 'u':
		print("There is an i or u")
```

If *while* loops are iterating through a string and are using indexing, use a *for* loop.
```python
an_letters = "aefhilmnorsxAEFHILMNORSX"
word = input("I will cheer for you! Enter a word: ")
times = int(input("Enthusiasm level (1-10): "))

#i = 0
#while i < len(word):
#    char = word[i]
#    i += 1
#print("What does that spell?")
for char in word:
    if char in an_letters:
        print("Give me an " + char + "! " + char)
    else:
        print("Give me a  " + char + "! " + char)

for i in range(times):
    print(word, "!!!")
```


```python
#i = 0
#while i < len(word):
#    char = word[i]
#    i += 1
```
Don't do this.
Do this.
```python
for char in word:
    if char in an_letters:
```
Iterate over the word.

## String Encoders and Decoders
We can use the codecs module to encode and decode bytes
```python
>>> import codecs
>>> codecs.encode("Hello World","rot-13")
'Uryyb Jbeyq'
>>> codecs.encode(b"Hello World","HEX")
b'48656c6c6f20576f726c64'
>>> codecs.encode("Hello World","utf-16le")
b'H\x00e\x00l\x00l\x00o\x00 \x00W\x00o\x00r\x00l\x00d\x00'
>>> codecs.encode(b"Hello World","base64")
b'SGVsbG8gV29ybGQ=\n'
```

## Shortcut Processing
OR = Return first if it True otherwise it returns second
- Get first thing that is true.
`True or False` returns True
`0 or False` returns false
AND = Return first if is False otherwise returns second
- Get first thing that is False
`False and 0` returns False
`0 and False` returns 0 