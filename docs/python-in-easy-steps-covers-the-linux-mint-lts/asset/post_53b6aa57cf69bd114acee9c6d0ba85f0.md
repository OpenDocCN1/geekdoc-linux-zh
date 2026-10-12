
4. Then, add indented statements to display an appropriate message describing whether the attempt succeeded

```
if is_valid: print('Valid Address:', is_valid.group()) else: print('Invalid Address! Please Retry...\n')
```

5. Finally, add a statement to call the defined function

```
get_address()
```

6. Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see that only a complete email address will validate

![](img/d06b1f1cf83677f6647237f0c7827141_144_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_144_1.png)

You can discover more about Regular Expressions in the Library Reference section of the Python documentation at docs.python.org/3/ library/re.html

## Summary

- Functions can be stored in modules that are named as the file name without the “.py” file extension
- An **import** statement makes module functions available in a program by dot-suffixing their name after the module name.
- A **from import** statement makes module functions available in a program without the need to dot-suffix their name.
- The **sys** module has attributes that contain the Python version number, interpreter location, and path to search for modules.
- The **keyword** module has a **kwlist** attribute that contains a list of all current Python keywords.
- The **math** module provides methods to perform mathematical procedures such as *math.ceil()* and *math.floor()*.
- The **random** module provides a *random()* method that produces pseudo random numbers and a *sample()* method that produces a list of elements selected at random from a sequence.
- The **decimal** module provides a *Decimal()* object with which floating-point numbers can be accurately represented to calculate monetary values.
- The **datetime** module provides a *datetime* object with *year, month, day, hour, minute, second, microsecond* attributes that can be referenced by dot-suffixing or with the *getattr()* method.
- A *datetime* object has a *strftime()* method that can specify a directive to return a formatted part of the object.
- The **time** module provides a *time()* method that returns the current elapsed time in seconds since the Epoch.
- The *gmtime()* and *localtime()* methods return a *struct_time* object that has attributes containing date and time components.
- The `re` module provides a `compile()` method to create a Regular Expression pattern and a `match()` method to compare a pattern to a specified string.

# 6

# Managing strings

This chapter demonstrates how to work with string data values and text files in Python programs.

- Manipulating strings
- Formatting strings
- Modifying strings
- Converting strings
- Accessing files
- Reading and writing files
- Updating file strings
- Pickling data
- Summary

## Manipulating strings

String values can be manipulated in a Python program using the various operators listed in the table below:

| Operator | Description | Example |
| :--- | :--- | :--- |
| `+` | **Concatenate** - join strings together | 'Hello' + 'Mike' |
| `*` | **Repeat** - multiply the string | 'Hello' * 2 |
| `[ ]` | **Slice** - select a character at a specified index position | 'Hello' [0] |
| `[ : ]` | **Range Slice** - select characters in a specified index range | 'Hello' [ 0 : 4 ] |
| `in` | **Membership Inclusive** - return True if character exists in the string | 'H' in 'Hello' |
| `not in` | **Membership Exclusive** - return True if character doesn't exist in string | 'h' not in 'Hello' |
| `r/R` | **Raw String** - suppress meaning of escape characters | print(r'\n') |
| `""" """` | **Docstring** - describe a module, function, class, or method | def sum( a,b ) :""" Add Args """ |

The `[ ]` slice operator and `[ : ]` range slice operator recognize that a string is simply a list containing an individual character within each list element, which can be referenced by their index number.

![](img/d06b1f1cf83677f6647237f0c7827141_148_0.png)

The membership operators perform a case-sensitive match, so 'A' in 'abc' will fail. Similarly, the in and not in membership operators iterate through each element seeking to match the specified character.

The raw string operator r (or uppercase R) must be placed immediately before the opening quote mark to suppress escape characters in the string, and is useful when the string contains the backslash character.

A “docstring” is a descriptive string literal that occurs as the first statement in a module, a function, a class, or a method definition. This should be enclosed within triple single quote marks. Uniquely, the docstring becomes the `__doc__` special attribute of that object, so can be referenced using its name and dot-suffixing. All modules should normally have docstrings, and all functions and classes exported by a module should also have docstrings.

![](img/d06b1f1cf83677f6647237f0c7827141_149_0.png)

The Range Slice returns the string up to, but not including, the final specified index position.

![](img/d06b1f1cf83677f6647237f0c7827141_149_1.png)

- Start a new Python script by defining a simple function that includes a docstring description
- `def display(s):` `“Display an argument value.”` `print(s)`
- Next, add a statement to display the function description
- `display(display.__doc__)`
- Now, add a statement to display a raw string value that contains the backslash character
- `display(r'C:\Program Files')`
- Then, add a statement to display a concatenation of two string values that include an escape character and a space
- `display('\nHello'+'Python')`

5. Next, add a statement to display a slice of a specified string within a range of element index numbers
   ```python
   display( 'Python In Easy Steps'[7:1] )
   ```

6. Finally, display the results of seeking characters within a specified string
   ```python
   display( 'P' in 'Python')
   ```

7. Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see manipulated strings get displayed

![](img/d06b1f1cf83677f6647237f0c7827141_150_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_150_1.png)

The **doc** keyword is preceded by TWO **_underscore** characters and followed by TWO **_underscore** characters.

![](img/d06b1f1cf83677f6647237f0c7827141_150_2.png)

Remember that strings must be enclosed within either single quote marks or double quote marks.

![](img/d06b1f1cf83677f6647237f0c7827141_151_0.png)

With range slice, if the start index number is omitted, zero is assumed, and if the end index number is omitted, the string length is assumed.

## Formatting strings

The Python built-in `dir()` function can be useful to examine the names of functions and variables defined in a module by specifying the module name within its parentheses. Interactive mode can easily be used for this purpose by importing the module name then calling the `dir()` function. The example below examines the “dog” module created [here](#) in the previous chapter:

![](img/d06b1f1cf83677f6647237f0c7827141_152_0.png)

Those defined names that begin and end with a double underscore are Python objects, whereas the others are programmer-defined. The `__builtins__` module can also be examined using the `dir()` function, to examine the names of functions and variables defined by default, such as the `print()` function and a `str` object.

The `str` object defines several useful methods for string formatting, including an actual `format()` method that performs replacements. A string to be formatted by the `format()` method can contain both text and “replacement fields” marking places where text is to be inserted from an ordered comma-separated list of values. Each replacement field is denoted by `{}` braces, which may, optionally, contain the index number position of the replacement in the list.

Strings may also be formatted using the C-style `%s` substitution operator to mark places in a string where text is to be inserted from a comma-separated ordered list of values.
