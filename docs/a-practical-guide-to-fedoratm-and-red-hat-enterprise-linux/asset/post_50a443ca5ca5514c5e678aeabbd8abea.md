
## group()

The `group()` method allows you to access the match a `MatchObject` holds.

```python
>>> a.group(0)
'hit'
```

## type()

When no match exists, `search()` returns a `NoneType` object (as shown by the `type()` function), which evaluates to `None` or in a Boolean expression evaluates to `False`.

```python
>>> a = re.search('xx.', 'bye hit him hex')
>>> type(a)
<type 'NoneType'>
>>> print a
None
>>> bool(a)
False
```

Because a `re` method in a Boolean context evaluates to true or false, you can use a `re` method as the expression an `if` statement evaluates. The next example uses `search()` as the expression in an `if` statement; because there is a match, `search()` evaluates as true, and Python executes the `print` statement.

```python
>>> name = 'sam'
>>> if(re.search(name,'zach max sam helen')):
...     print 'The list includes ' + name
... 
The list includes sam
```

## match()

The `match()` method of the `re` object uses the same syntax as `search()`, but looks only at the beginning of string for a match to regex.

```python
>>> name = 'zach'
>>> if(re.match(name,'zach max sam helen')):
...     print 'The list includes ' + name
... 
The list includes zach
```

# DEFINING A FUNCTION

A Python function definition must be evaluated before the function is called, so it generally appears in the code before the call to the function. The contents of the function, as with other Python logical blocks, must be indented. The syntax of a function definition is

```python
def my_function(args):
... 
```

Python passes lists and other data structures to a function by reference (page 1089), meaning that when a function modifies a data structure that was passed to it as an argument, it modifies the original data structure. The following example demonstrates this fact:

```python
>>> def add_ab(my_list):
...
...     my_list.append('a')
...     my_list.append('b')
...
>>> a = [1,2,3]
>>> add_ab(a)
>>> a
[1, 2, 3, 'a', 'b']
```

You can pass arguments to a function in three ways. Assume the function `place_stuff` is defined as follows. The values assigned to the arguments in the function definition are defaults.

```python
>>> def place_stuff(x = 10, y = 20, z = 30):
...     return x, y, z
```

If you call the function and specify arguments, the function uses those arguments:

```python
>>> place_stuff(1,2,3)
(1, 2, 3)
```

If you do not specify arguments, the function uses the defaults:

```python
>>> place_stuff()
(10, 20, 30)
```

Alternatively, you can specify values for some or all of the arguments:

```python
>>> place_stuff(z=100)
(10, 20, 100)
```

# USING LIBRARIES

This section discusses the Python standard library, nonstandard libraries, and Python namespace, as well as how to import and use a function.

## STANDARD LIBRARY

The Python standard library, which is usually included in packages installed with Python, provides a wide range of facilities, including functions, constants, string services, data types, file and directory access, cryptographic services, and file formats. Visit docs.python.org/library/index.html for a list of the contents of the standard library.

## NONSTANDARD LIBRARIES

In some cases a module you want might be part of a library that is not included with Python. You can usually find what you need in the Python Package Index (PyPI, pypi.python.org), a repository of more than 22,000 Python packages.

You can find lists of modules for the distribution you are using by searching the Web for **distro package database**, where *distro* is the name of the Linux distribution you are using, and then searching one of the databases for **python**.

### SciPy and NumPy Libraries

Two popular libraries are SciPy and NumPy. The SciPy (“Sigh Pie” ; scipy.org) library holds Python modules for mathematics, science, and engineering. It depends on NumPy (numpy.scipy.org), a library of Python modules for scientific computing.

You must download and install the package that holds NumPy before you can use any of its modules. Under Debian/Ubuntu/Mint and openSuSE, the package is named **python-numpy**; under Fedora/RH/EL, it is named **numpy**. See page 534 for instructions on downloading and installing packages. Alternatively, you can obtain the libraries from scipy.org or pypi.python.org. Once you import SciPy (`import scipy`), `help(scipy)` will list the functions you can import individually.

### Namespace

A *namespace* comprises a set of names (identifiers) in which all names are unique. For example, the namespace for a program might include an object named **planets**. You might instantiate **planets** as an integer:

```python
>>>  planets = 5
>>>  type(planets)
<type 'int'>
```

Although it is not good programming practice, later on in the program you could assign **planets** a string value. It would then be an object of type string.

```python
>>>  planets = 'solar_system'
>>>  type(planets)
<type 'str'>
```

You could make **planets** a function, a list, or another type of object. Regardless, there would always be only one object named **planets** (identifiers in a namespace must be unique).

When you import a module (including a function), Python can merge the namespace of the module with the namespace of your program, creating a conflict. For example, if you import the function named **sample** from the library named **random** and then define a function with the same name, you will no longer be able to access the original function:

```python
>>>  from random import sample
>>>  sample(range(10), 10)
[6, 9, 0, 7, 3, 5, 2, 4, 1, 8]
>>>  def sample(a, b):
...          print 'Problem?'
...
>>> sample(range(10), 10)
Problem?
```

The next section discusses different ways you can import objects from a library and steps you can take to avoid the preceding problem.

## Importing a Module

You can import a module in one of several ways. How you import the module determines whether Python merges the namespace of the module with that of your program.

The simplest thing to do is to import the whole module. In this case Python does not merge the namespaces but allows you to refer to an object from the module by prefixing its name with the name of the module. The following code imports the **random** module. Using this syntax, the function named **sample** is not defined: You must call it as **random.sample**.

```python
>>> import random
>>> sample(range(10), 10)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'sample' is not defined

>>> random.sample(range(10), 10)
[1, 0, 6, 9, 8, 3, 2, 7, 5, 4]
```

This setup allows you to define your own function named **sample**. Because Python has not merged the namespaces from your program and the module named **random**, the two functions can coexist.

```python
>>> def sample(a, b):
...     print 'Not a problem.'
...
>>> sample(1, 2)
Not a problem.
>>> random.sample(range(10), 10)
[2, 9, 6, 5, 1, 3, 4, 0, 7, 8]
```

Another way to import a module is to specify the module and the object.

```python
>>> from random import sample
```

When you import an object using this syntax, you import only the function named **sample**; no other objects from that module will be available. This technique is very efficient. However, Python merges the namespaces from your program and from the object, which can give rise to the type of problem illustrated in the previous section.

You can also use `from module import *`. This syntax imports all names from `module` into the namespace of your program; it is generally not a good idea to use this technique.

## EXAMPLE OF IMPORTING A FUNCTION

The `my_max.py` program on page 1090 finds the largest element in a predefined list. The following program works the same way, except at runtime it fills a list with random numbers.

The following command imports the `sample()` function from the standard library module named **random**. You can install an object from a nonstandard library, such as NumPy, the same way.

```python
from random import sample
```

After importing this function, the command `help(sample)` displays information about `sample()`. The `sample()` function has the following syntax:

`sample(list, number)`

where `list` is a list holding the population, or values `sample()` can return, and `number` is the number of random numbers in the list `sample()` returns.

```python
>>> sample([0, 1, 2, 3, 4, 5, 6, 7, 8, 9], 4)
[7, 1, 2, 5]
>>> sample([0, 1, 2, 3, 4, 5, 6, 7, 8, 9], 6)
[0, 5, 4, 1, 3, 7]
```

The following program uses the `range()` function (page 1096), which returns a list holding the numbers from 0 through 1 less than its argument:

```python
>>> range(8)
[0, 1, 2, 3, 4, 5, 6, 7]
>>> range(16)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
```

When you combine the two functions, `range()` provides a list of values and `sample()` selects values randomly from that list.

```python
>>> sample(range(100),10)
[5, 32, 70, 93, 74, 29, 90, 7, 30, 11]
```

In the following program, `sample` generates a list of random numbers and `for` iterates through them.

```python
$ cat my_max2.py
#!/usr/bin/python
from random import sample
my_rand_list = sample(range(100), 10)
print 'Random list of numbers:', my_rand_list
largest = -1
for item in my_rand_list:
    if (item > largest):
        largest = item
        print largest

print
print 'largest number is ', largest
```
