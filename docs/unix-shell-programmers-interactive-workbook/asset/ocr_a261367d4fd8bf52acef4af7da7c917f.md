# 260 Lab 6.1: Typed Variables and Scope

g) Doeset affect the value of an integer, or just how it is displayed?

Now run the following commands:

```
typeset -F3 x=1.23456
print x=$x
typeset -F2 x
print x=$x
typeset -F9 x
print x=$x
```

h) What does the digit after the F do to the value, and how it is dis-played?

There is one more point to make here. Run the following commands:

```
typeset -i x
typeset -F x
print x=$x
```

i) What effect does changing a variable from type float to type integer and back have on its value?

The fourth type of variable is called a name reference. You won't see any examples that really need name references in this book, but there is no reason that you can't learn how they work now. The idea of a name reference is that you can use it to set up two different names for the same variable.

You declare a variable to be a name reference with typeset -n.