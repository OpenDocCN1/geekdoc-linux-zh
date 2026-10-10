
# LISTING 34.3 Example Conditional Statement

```python
#! /usr/bin/env python

mylist = [2, 'cows', 'running', ['slowly', 'quickly']]
from types import *
for x in mylist:
    if type(x) is IntType:
        print 'Integer:', x
    elif type(x) is StringType:
        print 'String:', x
    elif type(x) is ListType:
        print 'List:'
        for y in x:
            print y
    else:
        print 'Uh oh!'
```

This script will output the following text:
Integer: 2
String: cows
String: running
List: slowly quickly

First, we define a list that consists of an integer, two strings, and a list of two strings. It's perfectly legal (even encouraged!) to nest lists and tuples to your heart's content. We determine the appropriate way of outputting `x`, depending on its type. Let's look at the `if` statement. It can have any number of `elif` sequences, which stand for else if, and an optional `else` at the end. Also note that `if` statements are so compact that there is no `case` statement, as in `C`. The same thing can be accomplished compactly with an `if` statement and a number of `elif` statements and an `else`.

> **Tip**
> If you are having a hard time getting the interpreter to accept your `if` statement, make sure that you are putting a colon immediately after the `if`, `elif`, and `else` statements. It's a common mistake for those unfamiliar with the language. The same thing goes for `while` and `for` statements, which should also end with a colon.

## Looping Constructs

A simple way of performing looping in Python is to use a `while` statement. The key to proper `while` loops is to get your indentation right. Here's a more complicated example:

```python
x=1
y=0
while x < 10:
    print x,
    x=x+1
    y=x
    while y > 0:
        print "!"",
        y=y-1
        
    print
```

This above code snippet contains two `while` loops: one is an outer loop, and the other is an inner loop. This means that the inner loop executes repeatedly because it appears in the body of the outer loop. Based on this information, use your mental prowess to figure out what this code does, and then type it into the interpreter, watch it run, and see if you were right!

### range()

The important thing to remember about `for` statements is that they iterate through items in a list, rather than simply incrementing a number. For times where you would like to cycle through a range of numbers, use the `range()` function to dynamically create a list of sequential numbers:

```python
>>> range(0,10)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> range(1,5)
[1, 2, 3, 4]
>>>
for x in range(1,10):
```

The second to last line is equivalent to `for x in [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]`, and the last two lines will cause the numbers zero through nine to be printed on separate lines.

## Two Types of Loops

In the following code, we see that we often have two options in how to perform `for` loops. The first method is the most efficient:

```python
mylist=['Here','is','another','one','of','those','lists!']
# this prints each item in the list on a separate line
# the variable x is set to each item in the list, one at a time
for x in mylist:
    print x
```

```python
# this does too, but uses a different method
# the variable x is set to each list index in the list (zero through six)

for x in range(0,len(mylist)):
    print mylist[x]
```

But the second method is handy when you want to access a numerical list index from within the loop:

```python
for x in range(0,len(mylist)):
    print x, mylist[x]
```

Play around with these different methods of iterating through lists in the interpreter or in a shell script.

## Loop Control Statements

For all looping constructs, there are three statements that you should know about: break, continue, and pass.

The pass statement does absolutely nothing, but it takes up space. Sometimes this is necessary when code is syntactically required, but you want nothing to happen. It can come in handy when creating empty while loops. The continue statement allows you to jump immediately to the next iteration of the loop, without executing any additional code. The break statement immediately aborts the innermost loop and is useful for things like this:

```python
f=open("/etc/fstab","r")
while 1:
    a=f.readline()
    if not a:
        break
    else:
        print a
```

The preceding code prints out the contents of your /etc/fstab file, line by line.

# Functions and Namespaces

Functions (like their C counterpart) allow you to create logical "bunches" of code that can be passed optional arguments and that can return an optional value. Here's a sample function.

## Function Descriptions

```python
>>> def foo():
...     "foo prints bar"
...     print "bar"
...
>>> foo()
bar
>>>
```

It's simple but boring. The only thing to mention here is that it is proper Python etiquette to include a one-line *string literal* as the first line of the function body, to serve as a description, which does not get printed. Let's consider a more complex example.

## Default Arguments

```python
def greeting(person='Bob',city='Albuquerque',nickname='Bosster'):
    'My cute little form letter'
    print 'Dear,',person+':'
    print
    print 'Hey,',nickname+'!','How are things in',city+'?'
    print
    print 'Sincerely,'
    print
    print 'Your friend.'
```

The preceding function has default values that will be assumed if not all arguments are specified. This means that all the following function calls are legal:

```python
greeting()
greeting('Anthony','Jersey','Big Tony')
greeting(nickname='Robsterino')
greeting('Robert')
```

## Return Values

Functions also allow us to return objects, by using the *return* statement. Using the *return* statement, we can pass back one object as a result. If more than one object needs to be passed back, we can group them into a list or tuple and pass that back to the caller:

```python
def squares(mynum):
    if mynum<0:
        # not legal!
        return None
    else:
        myval=[]
        for x in range(0,mynum):
            myval.append(x**2)
        return (myval,'morethings','squirrels',('chicken','pot','pie'))
```

The following statements are legal:

```python
print squares(8)
mysquares=squares(100)

for x in squares(10):
    print x
```

![](img/df365d352a104b50fea29e59a052de4d_866_0.png)

# Introduction to Namespaces

Python differs from most languages in how it deals with functions that want to access and/or modify global objects. But to understand how this works, we first need to become familiar with namespaces. Practically speaking, a namespace allows Python to find objects by name. Technically speaking, a namespace is a mapping from a name to an object and can be represented as a dictionary.

When a function is called in Python, the interpreter creates a completely new namespace for the function body, called the local namespace. When you refer to an object inside the function, Python searches this local namespace first before looking outside:

```python
>>> x=10
>>> def printx():
...     print x
...
>>> printx()
10
```

In the preceding example, when we called printx(), it first searched the local namespace, and after not finding the name x, it searched the global namespace. It then found the object and printed it. No surprises here; this is what you probably expected.

## Namespace Confusion—global to the Rescue

Here comes the interesting part. In Python, creating and modifying global objects from inside a function is done a bit differently. From the following example, we can see how not to try to modify a global object:

```python
>>> x=10
>>> def setx():
...     x=99999999
...
>>> setx()
>>> x
10
```

What happened? When we created the new object x inside the setx() function, Python created a new object in the local namespace. As a rule, when you create a new object or perform an assignment in a code block, Python modifies the local namespace only, unless we explicitly tell Python to modify the global namespace. We'll look at an example of how to do this soon, but for now, let's reflect a bit on the ramifications of this design decision. What it means for the programmer is that we can “read” global objects if there is no local object defined with the same name, but we cannot “write” to a global object. From a programming standpoint, this is ideal because it eliminates the possibility of creating unwanted side effects in your code, where global objects are accidentally
