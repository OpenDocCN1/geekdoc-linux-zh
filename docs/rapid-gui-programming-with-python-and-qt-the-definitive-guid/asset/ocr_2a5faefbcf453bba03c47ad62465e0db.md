# Table 1.9 Selected Math-Related Built-ins

| Syntax | Description |
| :--- | :--- |
| abs(n) | Returns the absolute value of number n |
| divmod(i, j) | Returns a tuple containing the quotient and remainder that result from dividing i by j |
| hex(i) | Returns a hexadecimal string representing number i |
| oct(i) | Returns an octal string representing number i |
| float(x) | Returns x converted to a float; x may be a string or a number |
| int(x) | Returns x converted to an int; x may be a string or a number |
| long(x) | Returns x converted to a long; x may be a string or a number |
| pow(x, y) | Returns x raised to the power y; can accept a third modulo argument—the two-argument form is the same as using operator ** |
| round(x, n) | Returns float value x rounded to n digits after the decimal place |

The range() function is covered in Chapter 2 when we look at looping, and the open() function is covered in Chapter 6 when we look at reading and writing files. The hasattr() and instance() functions are covered in Chapter 3.

For the sequence-related functions, max() and min() work on sequences that contain strings as well as those that contain numbers, but may give suprising results:

```
>>> x = "Zebra\u2019s don\u2019t sail"    
>>> max(x), min(x)    
('t', ' ')    
```

The ordering is based on the byte values for str strings and on code points for unicode strings. For example, ord("Z") is 90, whereas ord("t") is 116.

Some of Python\u2019s built-in mathematical functions are shown in Table 1.9. Python is also supplied with a mathematics library that has all the standard functions we would expect. We can discover what they are by importing the math module, and using dir():

```
>>> import math    
>>> dir(math)    
['__doc__', '__file__', '__name__', 'acos', 'asin', 'atan', 'atan2',    
'ceil', 'cos', 'cosh', 'degrees', 'e', 'exp', 'fabs', 'floor', 'fmod',    
'frexp', 'hypot', 'ldexp', 'log', 'log10', 'modf', 'pi', 'pow',    
'radians', 'sin', 'sinh', 'sqrt', 'tan', 'tanh']
```