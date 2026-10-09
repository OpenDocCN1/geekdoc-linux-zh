The final example shows nested list comprehensions. It nests **for** loops and uses `x + y` to concatenate the elements of both lists in all combinations.

```
```python
>>> A = ['a', 'b', 'c']
>>> B = ['1', '2', '3']
>>> all = [x + y for x in A for y in B]
>>> print(all)
['a1', 'a2', 'a3', 'b1', 'b2', 'b3', 'c1', 'c2', 'c3']
```
```

# # CHAPTER SUMMARY

Python is an interpreted language: It translates code into bytecode at runtime and executes the bytecode within the Python virtual machine. You can run a Python program from the Python interactive shell or from a file. The Python interactive shell is handy for development because you can use it to debug and execute code one line at a time and see the results immediately. Within the Python interactive shell, Python displays output from any command line that does not have an action. From this shell you can give the command `help()` to use the Python **help** feature or you can give the command `help('object')` to display help on *object*.

Functions help improve code readability, efficiency, and expandability. Many functions are available when you first call Python (built-in functions) and many more are found in libraries that you can download and/or import. Methods are similar to functions except they work on objects whereas functions stand on their own. Python allows you to define both normal functions and nameless functions called Lambda functions.

Python enables you to read from and write to files in many ways. The `open()` function opens a file and returns a file object called a file handle. Once the file is opened, you direct input and output using the file handle. When you are finished working with a file, it is good practice to close it. The `pickle` module allows you to store an object in a file in a standard format for later use by the same or a different program.

A Python list is an object that comprises one or more elements; it is similar to an array in C or Java. An important feature of lists is that they are *iterable*, meaning a control structure such as **for** can loop (iterate) through each item in a list. A Python dictionary holds unordered key–value pairs in which the keys are unique. Like lists, dictionaries are iterable.

Python implements many control structures, including **if...else**, **if...elif...else**, **while**, and **for**. Unlike most languages, Python requires SPACES (or TABs) at the beginning of lines in a control structure. The indented code marks a *logical block*, or section of code, that is part of the control structure.

Python regular expressions are implemented by the *python re* (regular expression) module. You must give the command `import re` before you can use the **re** methods.