
## Built-in modules

### 19. Executing functions at the time of Python interpreter termination

You can use 'atexit' module to execute functions at the time of Python interpreter termination.

# Example:

```
def sum():
    print(4+5)
def message():
    print("Executing Now")
import atexit
atexit.register(sum)
atexit.register(message)
```

# Output:

Executing Now
9

### 20. Converting from integer to binary, hexadecimal and octal

Python provides easy-to-use functions – bin(), hex() and oct() – to convert from integer to binary, decimal and octal format respectively.

# Example:

```
>>> bin(24)
'0b11000'
>>> hex(24)
'0x18'
>>> oct(24)
'0o30'
```

### 21. Converting any charset to UTF-8

You can use the following function to convert any charset to UTF-8.

```
data.decode("input_charset_here").encode('utf-8')
```

### 22. Removing duplicates from lists

If you want to remove duplicates from a list, just put every element into a dict as a key (for example with 'none' as value) and then check dict.keys().

```
from operator import setitem
def distinct(l):
    d = {}
    map(setitem, (d,)*len(l), l, [])
    return d.keys()
```

### 23. Do-while loops

Since Python has no do-while or do-until loop constructs (yet), you can use the following method to achieve similar results:

```
while True:
    do_something()
    if condition():
        break
```

### 24. Detecting system platform

To execute platform-specific functions, it is very useful to detect the platform on which the Python interpreter is running. You can use 'sys.platform' to find out the current platform.

# Example:

```
On Ubuntu Linux
>>> import sys
>>> sys.platform
'linux2'
On Mac OS X Snow Leopard
>>> import sys
>>> sys.platform
'darwin'
```

### 25. Disabling and enabling garbage collection

Sometimes you may want to enable or disable the garbage collector at runtime. You can use the 'gc' module to enable or disable the garbage collection.

```
>>> import gc
>>> gc.enable()
<built-in function enable>
>>> gc.disable()
<built-in function disable>
```

### 26. Using C-based modules for better performance

Many Python modules ship with counterpart C modules. Using these C modules will give a significant performance boost in complex applications.

# Example:

cPickle instead of Pickle, cStringIO instead of StringIO

### 27. Calculating maximum, minimum and sum out of any list or iterable

You can use the following built-in functions:

max: Returns the largest element in the list.
min: Returns the smallest element in the list.
sum: This function returns the sum of all elements in the list. It accepts an optional second argument: the value to start with when summing (defaults to 0).

### 28. Representing fractional numbers

Fraction instance can be created using the following constructor:

```
Fraction([numerator [, denominator]])
```

### 29. Performing math operations

The 'math' module provides a plethora of mathematical functions. These work on integer and float numbers, except complex numbers. For complex numbers, a separate module is used, called 'cmath'.

# For example:

```
math.acos(x): Return arc cosine of x.
math.cos(x): Returns cosine of x.
math.factorial(x): Returns x factorial.
```

### 30. Working with arrays

The 'array' module provides an efficient way to use arrays in your programs. The 'array' module defines the following type:

```
array[typecode [, initializer]]
```

Once you have created an array object, say myarray, you can apply a bunch of methods to it. Here are a few important ones:

myarray.count(x): Returns the number of occurrences of x in a.
myarray.extend(x): Appends x at the end of the array.
myarray.reverse(): Reverse the order of the array.

### 31. Sorting items

The 'bisect' module makes it very easy to keep lists in any possible order. You can use the following functions to order lists.

```
bisect.insort(list, item [, low [, high]])
```

Inserts item into list in sorted order. If item is already in the list, the new entry is inserted to the right of any existing entries.

```
bisect.insort_left(list, item [, low [, high]])
```

Inserts item into list in sorted order. If item is already in the list, the new entry is inserted to the left of any existing entries.
