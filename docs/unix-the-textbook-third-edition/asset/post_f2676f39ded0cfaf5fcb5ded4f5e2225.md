
cond2 is a test condition whose truth value determines whether the additional statement(s) block gets executed
else is the default which executes final statement(s)

A simple example of the use of this structure using Way 1 (Interactive mode) in Python is as follows (remember to press <Enter> on the keyboard after each line you type in).

## Example 16.2

```
>>> x = 1
>>> if x == 0: # the == is a logical, or Boolean operator
    print "x equal 0"
    elif x == 1: #one or more of these optional blocks are
    # allowed
        print "x equal 1"
    else:        #optional block
        print "x is something else"
x equal 1
>>>
```

## EXERCISE 16.3

- 1. If you leave out the elif block in Example 16.2, what prints out?
- 2. If you change the first line to read x = 3, and leave out the else line in Example 16.2, what prints out?
- 3. If you change the first line to read x = 1.8 in Example 16.2, what prints out?

It is also possible to nest conditional execution blocks inside of one another. For example:

## Example 16.3

```
>>> w = 36
>>> y = 13
>>> z = 20
>>> if w < 37:
...     print "w is less than 37"
...     if y > 13:
...         print "y is greater than 13"
...     elif y == 13:
...         print "y is equal to 13"
...     else:
...         print "y is less than 13"
...     if z > 21:
...         print "z is greater than 21"
...     elif z == 21:
...     print "z is equal to 21"
...     else:
...         print "z is less than 21"
... else:
...     print "w is greater than or equal to 37"
...
w is less than 37
y is equal to 13
z is less than 21
>>>
```

## 16.3.5 Determinate and Indeterminate Repetition Structures and Recursion

Python can repeat segments of program or script file structure in two basic ways: via determinate repetition structures or indeterminate repetition structures. Traditionally, a determinate repetition structure is called counting repetition, and an indeterminate repetition structure is called logical repetition. These two methods are implemented with the for procedural statement and the while procedural statement. Generally, if you know ahead of time (at the time you are writing the code) how many repetitions of a block of code you want to execute, you use the for statement, and if you do not (when, for example, you allow the user to input the number of repetitions as the script file is run), you use the while statement.

Of course, it is possible to implement the same two ways of repetition by not using a specific structured programming approach; for example, by using conditional execution and unstructured switching to obtain the same results. But, we choose to show the structured approach in Python.

Make sure that in the body of statements included in the indeterminate repetition block that while is executing, the test condition for continued execution becomes false. Otherwise, this will result in infinite repetition! To halt infinite repetition in an executing script file, hold down the <Ctrl> and C keys on the keyboard.

Proceeding from Guido van Rossum's definition of Pythonic in the Python language reference, a common technique in Python is to loop over all elements of an iterable object using a for statement. Many other languages do not have this type of construct, so people unfamiliar with Python sometimes use a numerical counter instead:

```
>>>for i in range(len(money)):
...     print money[i]
```

The Pythonic way is:

```
>>>for bills in money:
...     print bills
```

The Pythonic way can be characterized as iteration, whereas the traditional language construct can be characterized as counting.

The for structure can repeat a block of operations on any iterable sequence, such as strings, lists, tuples, or user-defined iterable objects in classes.

The general form of the for statement structure is:

```
for a certain number of times
    repeat these statements
```

The while structure can repeat a block of operations as long as a test condition is true.

The general form of the while statement structure is:

```
while a certain condition is true
    repeat these statements
```

An object, K, is iterable if it can be successfully run with the following code. This code also shows that a counting form of iteration such as the traditional for loop structure can be implemented with a while structure (be careful of indentation, and press <Enter> after the last ellipsis ...):

```
>>>K = [22,33,44,55]                #Lists are iterable.
>>>c = K.__iter__()                #c is the counter
>>>while 1:
...     #execute while true
...     try:
...         item = c.next()            #get the next one
...         print item                 # Do some operations on each item
...                                     # as you count through it
...     except StopIteration:          #Nothing left
...         break
...
22
33
44
55
>>>
```

Following are two simple examples of both forms of repetition. We use Way 2 (Script mode) to run them:

Save the following three lines of Python in a file named for1.py in the current working directory (notice that the keywords in the Python script file are in bold type):

## Example 16.4

```
limit = [1, 2, 3, 4, 5]
for number in limit:
    print "number of repeats %d" % number
```
