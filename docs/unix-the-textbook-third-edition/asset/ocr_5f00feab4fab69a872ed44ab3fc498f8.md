you want to do Python in! If you do not know, given the particular shell you are using (we use the C shell, with the % prompt), what your path of execution is set to, go back to Section 2.8 and examine your path and set it properly. For example, in the C shell, you can see your path of execution by typing echo $path at the shell prompt. On our base UNIX system, PC-BSD, Python is installed by default in /usr/local/bin.

+   3. You are doing Python in a console or terminal window without an integrated development environment (IDE). Therefore, the basic procedure is as follows: you edit Python scripts in your favorite text editor, save them to the current working directory, and execute Python in that current working directory. You execute Python interactively by typing commands into its "interpreter" shell window. When you become more familiar with Python, you may wish to make your work with the language more efficient by using an IDE.

+   4. In general, whenever we want you to type something on the Python command line, we will indicate what is to be typed in bold text.

Computer programs execute and accomplish their objectives in a particular order, from start to finish. They may "branch" within that order, perhaps to only execute some of their instructions, based on certain logical tests or conditions. They may also repeat segments of their operation, either for some predetermined number of times, or indeterminately, based on changing conditions. Python conforms to this model, and operates using the following scheme of levels:

+   1. Everything in Python programs, or scripts, is composed of modular components.
+   2. These modular components contain syntactically correct Python statements.
+   3. These statements contain expressions.
+   4. The expressions create and manipulate objects.

# 16.1.6 Running Python

The following subsection illustrates the three ways that we use to run Python.

# 16.1.6.1 Way 1 (Interactive Mode)

In a console or terminal window, you type python. The program executes, and you are presented with the Python command prompt, >>>. Then, you type single or multiple lines of Python code on the Python command line, and see the results immediately. A good reason to use this mode is that you can test small fragments of Python code one line at a time this way directly in the interpreter. A simple example of this would be as follows:

# Example 16.0.a

```
>>>print "How about some more?"
How about some more?
>>>
```