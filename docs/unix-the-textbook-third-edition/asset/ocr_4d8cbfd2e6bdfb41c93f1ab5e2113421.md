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

# Example 16.4

```
limit = [1, 2, 3, 4, 5]
for number in limit:
    print "number of repeats %d" % number
```