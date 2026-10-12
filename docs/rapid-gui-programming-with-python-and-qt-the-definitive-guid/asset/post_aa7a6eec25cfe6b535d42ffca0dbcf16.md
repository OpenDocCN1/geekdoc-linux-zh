
```python
raise NotImplementedError, "Dimension.volume()"
```

This defines the Dimension interface as having the two methods we want. If we multiply-inherit Dimension and forget to reimplement the methods, we will get a NotImplemented exception if we try to use them. Here is a new version of the Painting class that makes use of the interface:

```python
class Painting(Item, Dimension):
    def __init__(self, artist, title, year=None, width=None,
                 height=None):
        super(Painting, self).__init__(artist, title, year)
        self._width = width
        self._height = height
```

To calculate a painting's area we need its width and height, so we add these to the constructor, and assign them to suitable attributes:

```python
def area(self):
    if self._width is None or self._height is None:
        return None

    return self._width * self._height

def volume(self):
    return None
```

We must implement `area()` and `volume()`. Although the `volume()` method does not make sense for a painting, we must provide an implementation anyway (since the interface requires one), so we do so and return `None`. An alternative would have been to have raised an exception—for example, `ValueError`.

It would be natural to rework the Sculpture class to accept width, height, and depth arguments, and to provide a `volume()` implementation. But an `area()` implementation may or may not make sense for a sculpture. We might mean the overall area of the total volume, or the area of a face from a particular viewpoint. Since there is ambiguity, we could either pass an additional argument to disambiguate, or give up and either return `None` or raise an exception.

Multiply inheriting just involves listing two or more base classes in the class statement. The order in which the base classes appear does not matter in our example, but can matter in more complex hierarchies.

Python's object-oriented functionality goes beyond what we have covered in this chapter. For instances that need to store a fixed set of attributes as compactly as possible, it is possible to use the `__slots__` class attribute. We mention this only to highlight the fact that this is completely different from the PyQt slots (which are functions and more commonly methods) that we will encounter in the GUI chapters. It is also possible to create meta-classes, but again this is beyond the scope of what we need for GUI programming, so we do not need to cover the topic here.

## Modules and Multi-file Applications

Object-oriented programming allows us to package up functionality (e.g., methods and data attributes), into classes. Python modules allow us to package up functionality at a higher level—for example, entire sets of classes, functions, and instance variables. A module is simply a file with a `.py` extension. Modules may have code that is executed when they are imported, but more commonly they simply provide functions and classes which are instantiated when they are imported. We have already seen examples of this: The `Length` class is in a file called `length.py`, and is therefore accessible as the `length` module. When importing a module, we specify the name of the module file without the extension. For example:

```python
import length
a = length.Length("4.5 yd")
```

Only modules that are in the current directory, or in Python's `sys.path` list, can be imported. If we need access to modules that are elsewhere in the filesystem, we can add additional paths to `sys.path`. In addition to a file, a module can be an entire directory of files. In these cases, the directory must contain a file called `__init__.py`. This file can be (and often is) empty; it is simply used as a marker to tell Python that the directory contains `.py` files and that the directory name is the top-level module name. For example, we might create a directory called `mylibrary` and put `length.py`, `ordereddict.py`, and an empty `__init__.py` in it. As long as we add the directory that contains the `mylibrary` directory to Python's path, we could do this:

```python
import mylibrary.length
a = mylibrary.length.Length("14.3 km")
```

In practice, we might prefer to alias `mylibrary.length` to something shorter. For example:

```python
import mylibrary.length as length
a = length.Length("948mm")
```

Python's module handling is a lot more sophisticated than we have shown, but what we have covered is sufficient for the GUI programming which is our main concern. Python and PyQt applications can be written in a single file or can be spread over multiple files. We will show both approaches in the coming chapters.

> *The module import semantics are due to change in Python 2.7, with imports becoming absolute rather than relative. See http://www.python.org/dev/peps/pep-0328 for details.*

## Using the doctest Module

Python has considerable support for testing, with the `doctest` and `unittest` modules for unit testing and the `test` module for regression testing. PyQt also provides unit-testing functionality with the `QTest` module.

When we create modules, such as the `length` and `ordereddict` modules we wrote earlier, they are designed to be imported and the objects they provide (e.g., the `Length` and `OrderedDict` classes), used by the importing application. But since `.py` files can also be executables, we can easily include unit-testing code: When the module is imported the unit-testing code is simply ignored; but when the module is run the unit tests are executed. This approach is supported by the `doctest` module.

The `doctest` module makes unit testing as simple and painless as possible. To use it all we need to do is add examples to our docstrings, showing what we would type into the interactive Python interpreter (or IDLE) and what response we expect back. For example, here is the `OrderedDict` class's `get()` method in full:

```python
def get(self, key, value=None):
    """Returns the value associated with key or value if key isn't
    in the dictionary

    >>> d = OrderedDict(dict(s=1, a=2, n=3, i=4, t=5, y=6))
    >>> d.get("X", 21)
    21
    >>> d.get("i")
    4
    """
    return self._dict.get(key, value)
```

The docstring contains a brief description of the method's purpose, and then some examples written as though they were typed into the interpreter. We begin by creating an `OrderedDict` object; we don't need to import or qualify since we are inside the `ordereddict` module. We then write a call to the method we are testing and what the interpreter (or IDLE) is expected to respond. And then we do another call and response.

The `doctest` module uses this syntax because it is so familiar to Python programmers through their use of the interactive Python interpreter or of IDLE, or of any other Python IDE, such as Eric4, that embeds a Python interpreter. When the tests are run, the `doctest` module will import the module itself, then read every docstring (using Python's introspection capabilities) and then execute each statement that begins with the `>>>` prompt. It then checks the result against the expected output (which may be nothing), and will report any failures.

To make a module able to use `doctest` like this we just need to add three lines at the end of the module:

```python
if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

Whether a module is imported by being the subject of an import statement, or is invoked on the command line, all the module's code is executed. This causes the module's functions and classes to be created ready for use.

We can tell whether a module was imported because in this case its `__name__` attribute is set to the module's name. On the other hand, if a module is invoked its `__name__` attribute is set to `__main__`.

As shown earlier, we can use an `if` statement to see whether the module was imported, in which case we do nothing else. But if the module was invoked on the command line, we import the `doctest` module and execute the `testmod()` function which performs all our tests.

We can perform a test run from inside a console window. For example:

```bash
C:\>cd C:\pygt\chap03
C:\pygt\chap03>ordereddict.py
```

If there are no test failures, the module will run silently. If there are any errors, these will be output to the console. We can force the `doctest` module to be more verbose by using the `-v` flag:

```bash
C:\pygt\chap03>ordereddict.py -v
```

This shows every single test that is performed, and a summary at the end.

It is also possible to test for expected failures, for example, out-cases where we expect an exception to be raised. For these we just write the first and last lines of the expected output (because the traceback in the middle may vary) and use an ellipsis, `...`, to indicate the traceback. For example, here is the `OrderedDict` class's `setAt()` method in full:

```python
def setAt(self, index, value):
    """Sets the index-th item's value to the given value

    >>> d = OrderedDict(dict(s=1, a=2, n=3, i=4, t=5, y=6))
    >>> d.getAt(5)
    6
    >>> d.setAt(5, 99)
    >>> d.getAt(5)
    99
    >>> d.setAt(19, 42)
    Traceback (most recent call last):
    ...
```
