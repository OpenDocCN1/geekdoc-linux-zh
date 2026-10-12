# # Using the doctest Module

Python has considerable support for testing, with the doctest and unittest modules for unit testing and the test module for regression testing. PyQt also provides unit-testing functionality with the QTest module.

When we create modules, such as the length and ordereddict modules we wrote earlier, they are designed to be imported and the objects they provide (e.g., the Length and OrderedDict classes), used by the importing application. But since .py files can also be executables, we can easily include unit-testing code: When the module is imported the unit-testing code is simply ignored; but when the module is run the unit tests are executed. This approach is supported by the doctest module.

The doctest module makes unit testing as simple and painless as possible. To use it all we need to do is add examples to our doctstrings, showing what we would type into the interactive Python interpreter (or IDLE) and what response we expect back. For example, here is the OrderedDict class's get() method in full:

```
```
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
```

The doctstring contains a brief description of the method's purpose, and then some examples written as though they were typed into the interpreter. We begin by creating an OrderedDict object; we don't need to import or qualify since we are inside the ordereddict module. We then write a call to the method we are testing and what the interpreter (or IDLE) is expected to respond. And then we do another call and response.

The doctest module uses this syntax because it is so familiar to Python programmers through their use of the interactive Python interpreter or of IDLE, or of any other Python IDE, such as Eric4, that embeds a Python interpreter. When the tests are run, the doctest module will import the module itself, then read every doctstring (using Python's introspection capabilities) and then execute each statement that begins with the >>> prompt. It then checks the result against the expected output (which may be nothing), and will report any failures.