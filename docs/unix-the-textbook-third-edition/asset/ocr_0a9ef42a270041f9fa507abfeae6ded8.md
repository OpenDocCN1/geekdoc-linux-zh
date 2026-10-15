```
>>> (5 + 7>= 6 >= 78 - 9)/8
>>> (5 + 7>= 6 >= 78 - 9)/-8
```

# 16.3.2 Variables

An important feature of a high-level programming language like Python is providing for names that allow you to refer to computational objects. The name represents, or stands for in any particular computational environment of interest, the value or values which the object can take on; thus it is called a 'variable'.

Python variable names can contain both letters, numbers, and the underscore (_ ) character, but must begin with a letter. If you get an error message about the use of a variable name, it may be a reserved word, or keyword, in Python. Table 16.3 lists the 31 keywords that may not be used as variable names in a Python statement.

In Python 3.X, exec is no longer a keyword, but nonlocal is.

In the following simple example, we define some variables, and use them:

```
>>> pie=3.14159
>>> radius=10
>>> pie* (radius*radius)
314.159 >>> circumference=2*pie*radius
>>> circumference
62.8318
```

# 16.3.3 Functions

Python provides a programming construct called a function that allows you to define your own named procedures and lets you reuse those procedures in a modular fashion in your code. You can think of a function as a black box machine that takes named objects present before the function call or invocation as inputs, processes them inside the black box with names that are only seen inside the black box, and then spits them out as named objects available to the Python program via an assignment statement.

The general form of a function definition is:

```
def name (formal parameters):
    body of the function
    return (returned parameters)
```

TABLE 16.3 Python 2.7.X Keywords
| and | del | from | not | while |
| as | elif | global | or | with |
| assert | else | if | pass | yield |
| break | except | import | print | |
| class | exec | in | raise | |
| continue | finally | is | return | |
| def | for | lambda | try | |