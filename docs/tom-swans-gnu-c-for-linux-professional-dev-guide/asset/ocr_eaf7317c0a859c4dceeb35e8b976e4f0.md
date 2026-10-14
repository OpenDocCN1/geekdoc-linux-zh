Note
Operators +, -, *, and & may be overloaded for binary and unary expressions. Operators not in the table—such as the comma operator, scope resolution operator ::, and the ?: conditional expression operator—may not be overloaded.

The hypothetical ZZ class declares operator functions for the first four operators in the table. Each function has the following general form:

```
friend ZZ operator+(ZZ a, ZZ b);
```

The function is declared as a friend of the class to give the function access to the class's private and protected members (the sample class here has no such data, however). The function returns type ZZ so that its result may be assigned to another ZZ object. (However, the function might return a different type.) Most important, the function's name operator+() identifies the function as the method by which expressions that use the plus operator can handle objects of this class. For example, the program can construct three ZZ objects and use the following statement to add two of them and assign the results to the third:

```
ZZ a, b, c;
...
c = a + b;
```

Note
In most cases, classes that overload operators must provide operator=() functions and copy constructors. See Chapter 13, "Creating and Destroying Objects," for help in writing these functions.

When overloading operators, keep in mind that the compiler does not enforce mathematical concepts for class objects. It's a good idea to write functions such as operator+() that perform addition-like actions. Similarly, the code for operator*() should perform an operation that at least resembles mathematical multiplication. The actions of overloaded operators are up to you, but if you sidestep tradition—for example, defining a plus sign that multiplies instead of adds—the results are likely to be confusing at best.

# EXAMPLE OF OVERLOADED OPERATORS

A working example of overloaded operators helps illustrate the preceding concepts. Listing 19.1, strops.cpp, shows the beginnings of a class that can store integer values in string form. By using overloaded operators, the program evaluates mathematical expressions for string objects—not something that C++ ordinarily can do.

# LISTING 19.1 STROPS.CPP

```
#include <iostream.h>
#include <stdlib.h>   // Need atol()
#include <string>     // Need string class

class TStrop {
private:
```