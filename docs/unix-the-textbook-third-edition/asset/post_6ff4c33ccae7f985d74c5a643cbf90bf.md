
With that said, an exception, or unexpected end to a program, is a Python object that represents an error. To terminate the flow of execution of a program because of some exception the interpreter has found, Python has two kinds of exception-handling structure that can end the program. These structures are

- 1. Exception handling that uses for example try:...except:...else: as shown in Example 16.15, and the standard exceptions—for example, StopIteration, as shown in Example 16.13.
- 2. Assertions, for example using the assert statement.

The general form of try:...except:...else: is:

```
try:
    Some operations...
    ...
except ExceptionI:
    If there is an Exception, do this...
else:
    If there is no Exception then, do this...
```

The following is a simple exception test example, which opens a new file in the current working directory, writes some content to the file, and then exits normally.

## Example 16.20

```
>>> try:
...     handler = open("datafile", "w")
...     handler.write("This is a data file for testing
... exception handling!!")
... except IOError:
...     print "Error: Can't find file or write data"
... else:
...     print "File write successful"
...     handler.close()
...
File write successful
>>>
```

## EXERCISE 16.10

- 1. List five other standard exceptions, what general class of exception they signal, and what source you used to obtain their names.
- 2. Modify the code of Example 16.18 so that it writes the integers 1,2,3,4,5,6,7,8,9, and 10 as a string list to the file named datafile.

## 16.3.16 Modules, Global and Local Scope in Functions

At a certain level of abstraction, everything in Python is a module, even Python itself. A Python module is a container or package which holds all the hierarchical objects, statements, expressions, and other modular components we spoke about in the introduction to this chapter that are necessary to accomplish an intended task or subtask. Modules may contain function definitions, class operations, and variable assignments. Basically, there are only two types of Python module: a module written by you, or a module from some external library, like the Python standard library. The standard library that is built in contains over 200 modules, and there are many other module resources available online that a programmer can use so that she does not have to “reinvent the wheel,” so to speak.

A schematic diagram of the modular construction of a possible Python program is as follows.

```
Python shell ---> First Module.py ---> Second Module.py, etc. --->
Standard Library
>> commands   <---objects   <---objects   <---objects
results
```

The following example, taken from the code in Example 16.1, shows the composition and use of a module, which happens to be a function, that you create:

If you have not already done so, type the code from Example 16.1 into a file named arith1.py using your favorite text editor (or rename math1.py as arith1.py). Then type the following lines of Python code at the Python command line:

## Example 16.21

```
>>> import arith1
>>> A = arith1.add(3.5,4.2)
>>> B = A + arith1.subtract(16.78,20.45)
>>> C = arith1.multiply(B,5.0)
>>> D = arith1.divide(A,C)
>>> D
0.13487133984028396
>>>
```

Notice what is different about Example 16.1’s code and the code in Example 16.19:

- 1. You use import rather than from...import.
- 2. The functions in arith1 are addressed or touched by referencing arith1.function_name.

## EXERCISE 16.11

- 1. After doing Example 16.21, what result do you get if you type b on the Python command line, and why?

2. After doing Example 16.21, type del arith1 on the Python command line. Then type D = arith1.divide(A,C) and press <Enter> on the keyboard. What result do you get, and why?

3. Edit the file arith1.py, and comment out all of the return statements in the functions. Then, redo the commands shown in Example 16.21. What is D equal to, and why?

A simple example of a library module from the standard library that you can import and use to execute UNIX operating system commands is given next. Type in the commands shown on the Python command line (the output results given in the example may differ from what you see on your screen, depending on the specifics of your system):

## Example 16.22a

```
>>> import os
>>> File = os.popen('pwd')
>>> File.read(50)
'/usr/home/bob/n'
>>> for line in os.popen('ls -la f*'): print(line.rstrip())
#Press Enter twice!
...
-rw-r--r-- 1 bob bob 42 Feb 14 23:07 func1.py
-rw-r--r-- 1 bob bob 222 Feb 14 23:08 func1.pyc
-rw-r--r-- 1 bob bob 27 Feb 14 21:54 func2.py
-rw-r--r-- 1 bob bob 207 Feb 14 21:47 func2.pyc
```

## 16.4 PRACTICAL EXAMPLES

To begin this section, it would be helpful for you to read and try to understand the following two references in the Python online documentation for the release of Python you are using to get a better "top-down" overview of how Python is structured:

- 1. Python Language Reference: Release 2.7.X by Guido van Rossum and Fred L. Drake, Jr.
- 2. Python standard library, particularly the sys and os modules.

In the previous sections of this chapter, we provided an overview of the Python language and its syntax via the writing and execution of small (1–25 line) script files and functions.

In this section, we will detail some of Python's practical applications in real-world computer programming with larger (25–50 line) user-written modules, functions, and scripts.

As mentioned in Section 16.1, Python can be used to accomplish tasks revolving around shell scripting, systems programming, network and Internet scripting, database programming, systems administration scripting, GUI scripting, scientific and math programming, and data mining.

We will begin by writing script files in Python that accomplish what UNIX shell scripts accomplish, with the goal of familiarizing you with Python.
