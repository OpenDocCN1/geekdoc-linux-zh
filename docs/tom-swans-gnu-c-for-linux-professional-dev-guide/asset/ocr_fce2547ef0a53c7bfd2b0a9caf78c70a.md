The exception class's Report() function displays the values of the object's b and e double variables, and also writes an additional message held in what_str. The TPowExcept class not only contains all values that fully describe a problem with the power() function, but also the means for displaying an error message.

Function power() uses the TPowExcept class to report errors. For example, if you attempt to raise a negative value to a fractional exponent, the program throws the following exception:

```
throw TPowExcept(b, e, "Result is a complex number");
```

This is all that power() needs to do to report this type of error. In throwing the exception, the function passes the faulty base and exponent values and a string message to the TPowExcept() constructor.

> Note
> The last statement in the power() function is unreachable—it should never execute. I included it, however, to demonstrate how you can insert internal error-reporting code that might be useful during debugging. To see how this works, comment-out the return 0; statement. I sometimes like to use similar programming to make sure that I've covered all the bases, especially in a function that uses nested if-else statements. However, some C++ compilers complain about the final throw statement—if that happens on your system, you can delete that line.

Listing 16.3, tpower.cpp, tests the power module and demonstrates how to use try and catch statements to trap a function's exceptions.

# LISTING 16.3 TPOWER.CPP

```
#include <iostream.h>
#include "power.h"  // Need TPowExcept, power()

int main()
{
    double base, exponent, result;  // Input and result variables
    try {
        cout << "base? ";
        cin >> base;
        cout << "exponent? ";
        cin >> exponent;
        result = power(base, exponent);  // Exception possible here
        cout << "result = " << result << endl;
    }
    catch (TPowExcept &except) {
        except.Report();  // Display error message
        return 1;         // Exit with error
    }
    return 0;  // Exit with no error
}
```

Compile the power.cpp module and the test program with the following commands:

```
$ g++ -c power.cpp
$ g++ tpower.cpp power.o
```