```
$ ./my_max2.py
random list of numbers: [67, 40, 1, 29, 9, 49, 99, 95, 77, 51]
67 99
largest number is 99
$ ./my_max2.py
random list of numbers: [53, 33, 76, 35, 71, 13, 75, 58, 74, 50]
53 76
largest number is 76
```

**max()** The algorithm used in this example is not the most efficient way of finding the maximum value in a list. It is more efficient to use the **max()** builtin function.

```
>>> from random import sample
>>> max(sample(range(100), 10))
96
```

# **optional**
# LAMBDA FUNCTIONS

Python supports *Lambda* functions—functions that might not be bound to a name. You might also see them referred to as *anonymous* functions. Lambda functions are more restrictive than other functions because they can hold only a single expression. In its most basic form, Lambda is another syntax for defining a function. In the following example, the object named **a** is a Lambda function and performs the same task as the function named **add_one**:

```
>>> def add_one(x):
...     return x + 1
...
>>> type (add_one)
<type 'function'>

>>> add_one(2)
3

>>> a = lambda x: x + 1
>>> type(a)
<type 'function'>

>>> a(2)
3
```

**map()** You can use the Lambda syntax to define a function inline as an argument to a function such as **map()** that expects another function as an argument. The syntax of the **map()** function is

```
map(func, seq1[, seq2, ...])
```

where *func* is a function that is applied to the sequence of arguments represented by *seq1* (and *seq2* ...). Typically the sequences that are arguments to **map()** and the