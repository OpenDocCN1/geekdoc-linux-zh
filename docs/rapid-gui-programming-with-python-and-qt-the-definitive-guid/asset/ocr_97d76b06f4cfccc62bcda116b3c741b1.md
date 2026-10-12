evaluates to. Lambda functions can be closures, a topic covered later. In this example, we have assigned the lambda function to the variable cube, which we can now use, for example: cube(3) which will return 27.

Some Python programmers dislike lambda; certainly it is not needed since def can be used to create any function we want. However, when we start on GUI programming we will see one context where lambda can be useful, although we will also show alternatives that don't use it.

# Dynamic Function Creation

The Python interpreter starts reading from the top of the .py or .pyw file. When the interpreter encounters a def statement it executes the statement, thereby creating the function and binding the name following the def to it. Any code that is not inside a def statement (or inside a class statement, as we will see in the next chapter) is executed directly.

Python cannot call functions or use objects that have not been defined. So Python programs that occupy a single file tend to have a Pascal-like structure with lots of function definitions from the top down, and at the end a call to one of them to start the processing off.

Unlike C++ and Java, Python programs do not have a fixed entry point, and the name “main” is not special. The Python interpreter simply executes the code it encounters from the first line down. For example, here is a complete Python program:

```
#!/usr/bin/env python

def hello():
    print "Hello"

def world():
    print "World"

def main():
    hello()
    world()

main()
```

The interpreter executes def hello(), that is, it creates the hello() function, then creates the world() function, and then creates the main() function. Finally, the interpreter reaches a function call, to main() (in this case, so the interpreter executes the function call, at which point what we normally think of as program execution commences.

Python programmers usually put only one statement at the top level, a call to the first function they want to execute. They usually call this function main(), and call their other functions from it, resulting in a structure similar to that used by C++ and Java.