# Importing Objects

Python has a large and comprehensive library of modules that provides a huge amount of predefined functionality. We can use this functionality by importing the constants, variables, functions, and classes that we want. The general syntax for importing is:

```
```python
import moduleName
```
```

We can then access objects inside the module using the dot operator. For example, the random module provides the randint() function, which can be imported and used like this:

```
```python
import random
x = random.randint(1, 10)
```
```

Note that it is common to put import statements at the beginning of .py files, but they can be put elsewhere—for example, inside a function definition.

One benefit of Python’s module system is that each module acts as a namespace, so we avoid name collisions effortlessly. For example, we may have defined our own randint() function, but there is no name conflict because the imported one in the example is accessed using the fully qualified name random.randint(). And as we will see in Chapter 3, we can create our own modules and import our own objects.

Modules themselves can contain other modules, and for very large modules, it is more convenient to import objects directly into the current namespace. Python provides a syntax for this. For example:

```
```python
from PyQt4.QtCore import *
x = Qstring()
y = Qdate()
```
```

Here we have imported every object, that is, all the classes from the PyQt4 module’s QtCore module, and this allows us to use their unqualified names. Using this syntax is frowned on by some developers, but since we know that almost all of the PyQt objects begin with a capital “Q”, providing we don’t create any of our own objects with names beginning with “Q”, we will not get any name collisions and can type far less. However, for those who prefer to use fully qualified names in all cases, the plain import syntax can be used:

```
```python
import PyQt4
x = PyQt4.QtCore.Qstring()
y = PyQt4.QtCore.Qdate()
```
```

For the sake of brevity we will use the from … import syntax for the PyQt4 modules, although we will use the plain import syntax for everything else.