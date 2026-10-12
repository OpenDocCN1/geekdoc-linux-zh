# **Functions, Methods, and Operators Terminology**

The term function is used to refer to a subroutine that can be executed independently, and the term method is used to refer to a function that can only be executed when bound to an object, that is, called on an instance of a particular class.

An operator may be independent or it may be bound to an object, but unlike functions and methods, operators do not use parentheses. Operators that are represented by symbols such as +, *, and < are rather obviously called operators, but operators that have names such as del and print are often called statements.

Python functions do not have to be pure in the mathematical sense: They do not have to return a value and they can modify their arguments. Python functions are like C and C++ functions, or like Pascal functions that take var parameters. Python methods are like C++ or Java member functions.

Python has two ways of comparing objects: by "identity" and by "value". An object's identity is effectively its address in memory, and this is what an object reference holds. If we use comparison operators, such as == and <, we get value comparison. For example, two strings are equal using == if they both contain the same text. If we use is we get identity comparison, which is fast because we are just comparing two addresses and don't have to look at the objects themselves. An object's identity can be obtained by calling id() on an object reference.

Python has a special object called None. This can be assigned to any variable and it means that the variable has no value. There is only ever one instance of the None object, so we can always use the fast is and is not comparisons when testing for it.

Notice that we wrote x on its own at the >>> prompt. If we write an expression or variable in IDLE, its value is automatically printed. In a program, we must use an explicit print statement to print an expression. For example:

```
print x
```

Python's print statement is an operator, not a function, and for this reason it is invoked without using parentheses (just as we use + and other operators without them).

Earlier we said that Python uses dynamic typing. There are two factors involved in this. First, we can assign any object to any variable; for example, we could write:

```
x = 47
x = "Heron"
```