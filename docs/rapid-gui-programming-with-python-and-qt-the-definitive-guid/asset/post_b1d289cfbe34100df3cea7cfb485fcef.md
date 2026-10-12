
# Part I

# Python Programming

## 1. Data Types and Data Structures

- Executing Python Code
- Variables and Objects
- Numbers and Strings
- Collections
- Built-in Functions

In this chapter, we begin a Python conversion course that shows non-Python programmers how to program with Python. We introduce some fundamental data types and data structures, as well as some of Python's procedural syntax. The approach taken throughout is to emphasize realistic code like that used in practice, rather than giving the formal definitions and explanations that are already available in the documentation that is supplied with Python and available online at `http://www.python.org`.

![](img/9bfe0a027fcc8793bb087287001100dd_23_0.png)

If you have not already installed Python and PyQt, it would be a good idea to do so: That way you will be able to try out the examples that accompany this book (downloadable from `http://www.qtrac.eu/pyqbook.html`). See Appendix A for installation details. One advantage of installing the software is that the IDLE integrated development environment is installed along with Python.

### The IDLE Development Environment

The full installation of Python includes IDLE, a basic but very useful integrated development environment. When IDLE is launched (click Start→All Programs→Python 2.x→IDLE on Windows, or click Finder→Applications→MacPython 2.x→IDLE on Mac OS X, or run idle in a console on Linux), it presents its Python Shell window.

As the screenshot in Figure 1.1 shows, IDLE has a rather retro Windows 95 look. This is because it is written in Tkinter rather than in PyQt. We've chosen to use IDLE because IDLE comes as standard with Python and is very simple to learn and use. If you want to use a much more powerful and modern-looking IDE, you might prefer *Erica* which is written in PyQt, or one of the other Python IDEs that are available. However, if you are new to Python, we recommend that you start out with the simpler IDLE, and once you are more experienced with Python, then try the other IDEs to see if you prefer one of them. And of course, you could simply use a plain text editor and debug using print statements and not use an IDE at all.

IDLE provides three key facilities: the ability to enter Python expressions and code and to see the results directly in the Python Shell; a code editor that provides Python-specific color syntax highlighting; and a debugger that can be used to step through code to help identify and kill bugs. The Python Shell is especially useful for trying out simple algorithms, snippets of code, and regular expressions, and can also be used as a very powerful and flexible calculator.

### Executing Python Code

Before we can really explore the Python language we need to know how to execute Python code. We will show this by reviewing a tiny example program that is just one line long.

We must use a plain text editor for working with Python files.¹ On Windows it is possible to use Notepad, but IDLE includes a suitable Python editor designed specifically for editing Python code: Simply start IDLE and then click File→New Window.

We will type the following line into a file, called `hello.py`:

```python
print "Hello World"
```

Note that no semicolon is necessary: In Python newline acts as a statement separator. Also, we do not need a newline, `\n`, in the string, since `print` automatically adds a newline unless we suppress it with a trailing comma.

Assuming that we have saved the code in the file `hello.py` (in the directory `C:\pygt\chap01` if using Windows), we can start up a console (click **Start**→**All Programs**→**Accessories**→**Console** on Windows XP—sometimes Console is called **Command Prompt**, or run **Terminal.app** on **Applications/utilities** on Mac OS X), change to that directory, and execute the program like this:

```
C:\>cd C:\pygt\chap01
C:\pygt\chap01>hello.py
```

As long as Python is correctly installed, Windows will recognize the `.py` file extension and give the file to `python.exe` to execute. The program will print "Hello World" on the console as we would expect.²

On Mac OS X and Linux we must explicitly run the interpreter by typing its name and the file’s name at the console’s prompt, like this:

```
% python hello.py
```

This will work providing that Python is installed and in your **PATH**. Alternatively, for Linux and Mac OS X, we can add an additional “shebang” (shell execute) comment line which tells the operating system to use a Python interpreter, making the `hello.py` file two lines long:

```
#!/usr/bin/env python
print "Hello World"
```

For this to work on Mac OS X and Linux, the file’s permissions must be set correctly. For example, at the console prompt in the same directory as the file, enter `chmod +x hello.py` to make the file executable.

Python comments start with “#” and continue until the end of the line. This means that it is perfectly safe to add the “shebang” line to all Python programs, since the comment is ignored on Windows but on Linux it tells the operating system to execute the file using a Python interpreter. Appendix A shows how to associate the Python interpreter with `.py` and `.pyw` files on Mac OS X.

When we speak of executing a Python program, what happens behind the scenes is that Python reads the `.py` (or `.pyw`) file into memory, and parses it, to get a bytecode program that it then goes on to execute. For each module that is imported by the program, Python first checks to see whether there is a precompiled bytecode version (in a `.pyo` or `.pyc` file) that has a timestamp which corresponds to its `.py` file. If there is, Python uses the bytecode version; otherwise, it parses the module’s `.py` file, saves it into a `.pyc` file, and uses the bytecode it just generated. So, unlike Java, we don’t have to explicitly bytecode-compile any modules, whether they are supplied with Python or are ones we have written ourselves. And in most Python installations, the supplied modules are compiled as part of the installation process so as to avoid having to compile them whenever a Python application that uses them is run.

¹ Mac OS X users note that whenever we refer to a console, this is the same as a Mac *Terminal*.

### Variables and Objects

In most programming languages, including C++ and Java, we must declare each variable, specifying its type, before it can be used. This is called *static typing*, because the compiler knows at compile time what type each variable is. Python, like most very high level languages, uses a different approach: Variables have no type restrictions (dynamic typing), and they don't need to be declared.

We could learn about Python's variables and identifiers by creating and executing a file, as we did with hello.py in the preceding section. But for trying out small code snippets we don't need to create a file at all. We can just enter the lines directly in the IDLE Python Shell window at the >>> prompt:

```python
>>> x = 71
>>> y = "Dove"
```

The whitespace around the assignment operator = is optional but is included because it makes the code easier to read. As a matter of style we will always put one space before and after binary operators. On the other hand, it is important that each statement occupies its own line and has no extraneous leading whitespace. This is because Python uses indentation and line breaks to signify its block structure, rather than the braces and semicolons used by many other programming languages.

Now we are ready to review what the two lines actually do. The first line creates an object of type int and binds the name x to it.³ The second line creates an object of type str (an 8-bit string type) and binds the name y to it.

Some Python programmers refer to names (such as the x and y used earlier), as *object references* since they refer to objects rather than being objects in their own right. For basic data types like int and str it makes no difference whether we see their variables as "objects" or as "object references"; they behave in the same way as they do in other programming languages:

```python
>>> x = 82
>>> x += 7
>>> x
89
```

Later on we will see cases where the fact that Python variables are object references makes a difference.

³ This is similar to the Java assignment, Integer x = new Integer(71); for C++ a near-equivalent would be int xd = 71; int x = xd;.
