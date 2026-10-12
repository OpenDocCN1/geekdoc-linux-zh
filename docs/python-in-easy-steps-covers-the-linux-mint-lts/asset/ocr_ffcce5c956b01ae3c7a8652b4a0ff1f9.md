# # Formatting strings

The Python built-in `dir()` function can be useful to examine the names of functions and variables defined in a module by specifying the module name within its parentheses. Interactive mode can easily be used for this purpose by importing the module name then calling the `dir()` function. The example below examines the “dog” module created [here](#) in the previous chapter:

![](bbox=[0.2, 0.31, 0.77, 0.56])

Those defined names that begin and end with a double underscore are Python objects, whereas the others are programmer-defined. The `__builtins__` module can also be examined using the `dir()` function, to examine the names of functions and variables defined by default, such as the `print()` function and a `str` object.

The `str` object defines several useful methods for string formatting, including an actual `format()` method that performs replacements. A string to be formatted by the `format()` method can contain both text and “replacement fields” marking places where text is to be inserted from an ordered comma-separated list of values. Each replacement field is denoted by `{}` braces, which may, optionally, contain the index number position of the replacement in the list.

Strings may also be formatted using the C-style `%s` substitution operator to mark places in a string where text is to be inserted from a comma-separated ordered list of values.