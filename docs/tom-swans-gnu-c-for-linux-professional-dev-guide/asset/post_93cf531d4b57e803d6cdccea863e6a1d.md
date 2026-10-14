
```cpp
catch (TOverflow except) {
    // handle overflow condition
}
catch (TUnderflow except) {
    // handle underflow condition
}
```

You can usually avoid such unwieldy programming by placing the calls to various functions inside another function, typically written inline to avoid an extra function call:

```cpp
inline void f()
{
    functionA();
    functionB();
}
```

This allows the program to use a single try block followed by catch statements to trap any exceptions thrown by functionA() or functionB():

```cpp
try {
    f();
}
catch (TOverflow except) {
    // handle overflow condition
}
catch (TUnderflow except) {
    // handle underflow condition
}
```

## Using try Blocks

Some additional examples help clarify what try blocks are and how to use them. A try block may execute multiple statements as in this code fragment:

```cpp
int x;
try {
    cout << "Here we go!" << endl;
    x = AnyFunction();
    cout << "x == " << x << endl;
}
catch (MyException except) {
    cout << except.what() << endl;
}
```

The sample try block first displays a message. This is unlikely to cause any exceptions to be thrown, and so it doesn't strictly need to be inside a try block—but there's no harm in placing it there. Next, the program calls AnyFunction(), assigning the function's return value to integer x. However, if AnyFunction() throws an exception, the try block immediately ends and no value is assigned to x. The output statement following AnyFunction() is also skipped. Because of the exception, the program jumps directly to the catch statement that lists the type of exception object.

A special value as an error indicator. Using standard error handling methods, AnyFunction() might return -1 to indicate a problem, detected conventionally with an if statement:

```cpp
int x = AnyFunction();
if (x == -1)
    ErrorHandler(x);
```

This technique has many problems. For one, the reserved value -1 contains no information about the problem. Also, it isn't always convenient to reserve a value as an error indicator. Furthermore, it's too easy for programmers to ignore an error value returned from a function. All these troubles are eliminated by using exceptions in C++.

## Programming with Exceptions

Now that you've met the basics of exception handling, examine the program in this section for a practical example of how to use exceptions for reporting errors. The program implements a function, power(), that raises a double floating point value to an exponent, which may be fractional. An illegal input value, such as a negative base raised to a fractional exponent (-4^1/3, for example), throws an exception. So that you can use the function in other programs, I wrote it as a separate module. Listing 16.1, power.h, declares the power() function and exception class used to report errors.

### Listing 16.1 POWER.H

```cpp
#include <exception>  // Need exception class
#include <string>      // Need string class

class TPowExcept: public exception {
    double b;          // Base value
    double e;          // Exponent value
    string what_str;   // Error description
public:
    TPowExcept(double b_arg, double e_arg,
               const string &what_arg)
        : b(b_arg), e(e_arg), what_str(what_arg) {}
    virtual const char *what() const {
        return what_str.c_str();
    }
    void Report();
};

double power(double b, double e) throw(TPowExcept);
```

Take a look first at the end of the header file where the power() function is prototyped. The declaration ends with throw(TPowExcept), an optional indicator of what kinds of exceptions this function might throw. This is called a declared exception. Even though it is optional to declare a function's exceptions, you should almost always do so. This makes perfectly clear the types of exceptions you need to trap in catch statements after calling the function in a try block.

Also in the power.h header file is the declaration for the TPowExcept class, derived from the standard exception class. Three private data members hold values that describe the nature of a problem. Doubles b and e are the input values to power() that were found to be illegal, and what_str further describes the problem. The TPowExcept constructor is written inline. It assigns its three arguments to the three private data members but performs no other chores. The virtual what() function returns the string value of the what_str private object. Function Report() is implemented in Listing 16.2, power.cpp.

### Listing 16.2 POWER.CPP

```cpp
#include <iostream.h>
#include <math.h>    // Need modf(), fmod()
#include "power.h"  // Need TPowExcept, power()

// Display error message in exception object
void TPowExcept::Report()
{
    cout << "Domain error: base == " << b
         << ", exponent == " << e << endl;
    cout << what() << endl;
}

// Subfunction called by power()
double fpower(double b, double e)
{
    return exp(e * log(b));
}

// Returns b raised to the e power
// Throws TPowExcept exception for illegal input values
double power(double b, double e) throw(TPowExcept)
{
    if (b > 0.0) return fpower(b, e);
    if (b < 0.0) {
        double ipart;
        double fpart = modf(e, &ipart);
        if (fpart == 0) {
            if (fmod(ipart, 2) != 0) // i.e. ipart is odd
                return -fpower(-b, e);
            else
                return fpower(-b, e);
        } else
            throw TPowExcept(b, e, "Result is a complex number");
    } else {
        if (e == 0.0) return 1.0;
        if (e < 1.0)
            throw TPowExcept(b, e, "Exponent must be zero or >= 1.0");
        return 0.0;
    }
    throw TPowExcept(0, 0, "Error in power() function");
}
```
