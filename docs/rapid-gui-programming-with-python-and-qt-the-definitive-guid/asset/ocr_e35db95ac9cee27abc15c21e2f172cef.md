## Built-in Functions

39

**Table 1.8** *Some Useful Built-ins*

| Syntax | Description |
|:------- |:---------- |
| chr(i) | Returns a one-character str whose ASCII value is given by int i |
| unichr(i) | Returns a one-character unicode string whose Unicode code point is given by int i |
| ord(c) | Returns the int that is the byte value (0–255) if c is a one-character str string, or the int for the Unicode code point if c is a one-character unicode string |
| dir(x) | Returns a list of most of object x’s attributes, including all its method names |
| help(x) | In IDLE, prints a brief description of object x’s type and a list of its attributes including all its methods |
| hasattr(x, a) | Returns True if the object x has the attribute called a |
| id(x) | Returns the unique ID of the object that object reference x refers to |
| isinstance(x, C) | Returns True if x is an instance of class C or a subclass of class C |
| type(x) | Returns the type of x; isinstance() is offered since it accounts for inheritance; type() is most often used for debugging |
| eval(s) | Returns the result of evaluating the string s which can contain an arbitrary Python expression |
| open(f, m) | Opens the file named in string f using mode m, and returns the file handle; covered in Chapter 6 |
| range(i) | Returns a list of int i ints numbered from 0 to i – 1; additional arguments specify start, end, and step values |

This will display all the str class’s methods with a brief explanation of each. Quite a lot of information is provided, so we often have to scroll up using the PageUp key or using the scrollbar.

```text
>>> help()

With no arguments the help() function takes us into the interactive help system. Type quit to return to normal IDLE interaction.

Once we are familiar with Python’s classes and we need just a quick reminder, we can use dir() to get a bare list of a class’s methods, for example:

```
>>> dir(str)
```

range() examples

≡ 50