
That statement constructs an object of the Overflow class, and it throws that object back to the function’s caller. In that function, the program can trap the exception with code such as

```
catch (Overflow) {
    cout << "Overflow detected" << endl;
}
```

## The Standard exception Class

Usually, exception classes derive from a base class that provides information about a problem. So that your exception handling is compatible with the C++ default handlers, for best results, base your own exception handlers on the standard C++ exception class, declared as

```
class exception {
public:
    exception() { }
    virtual ~exception() { }
    virtual const char* what() const;
};
```

To make the class available in your program, include the standard exception header file, which in this case, does not end in .h. Also include the standard string header for use in storing descriptive messages in exception objects:

```
#include <exception>
#include <string>
```

The exception class declares three public members: a do-nothing default constructor, a virtual destructor, and a virtual function what() that returns type const char *, and because of the const suffix, states that calling the function makes no changes to the object. To use the exception class, derive another class, something like this:

```
class TMyException: public exception {
private:
    string what_str;
public:
    TMyException(const string &what_arg):
        what_str(what_arg) { }
    virtual const char* what() const {
        return what_str.c_str();
    }
};
```

The derived class publicly inherits the standard exception class, adding a private string object named what_str. The new class’s constructor specifies a reference parameter to a C++ string object, and it uses an initializing expression to assign what_arg to what_str. The constructor has no other duties to perform, so its statement block is empty. The virtual what() function returns a const char * to a C-style string by calling the what_str object’s c_str() function. Function what() is traditional in exception objects for obtaining a description of the problem that caused the exception to be thrown.

To use the derived class, a function statement throws an object of the derived class with a string description as an argument. The function might be written something like this:

```
int AnyFunction()
{
    if (errorCondition)
        throw TMyException("Underflow");
    else
        return aValue;
}
```

If an error condition is detected, the function throws an object of the TMyException class; otherwise, it returns a value normally.

> **Note**
> 
> For more information on C++ string objects, see Chapter 22, “Mastering the Standard String Class.”

## INTRODUCING try BLOCKS

Now it’s time to toss in another wrinkle—try blocks, which seem to confuse everybody the first time they use them. To prepare for trapping an exception in a catch statement, using the TMyException class and sample AnyFunction() from the preceding section, a program enables exception handling with code such as this:

```
int x;
try {
    x = AnyFunction();  // Might throw an exception
    cout << "x = " << x << endl;  // May not execute
}
catch (TMyException except) {
    cout << except.what() << endl;
    exit(1);
}
```

A try block executes one or more statements, some of which might throw an exception. In this case, sample AnyFunction() throws an exception of type TMyException if it detects an error. If that happens, no assignment is made to x, and the output statement does not execute. Instead, the program hops immediately to the first catch statement that matches the exception’s type. In this case, the sample catch statement traps the exception object, displays its message by calling what(), and then ends the program by calling exit().

One or more catch statements must follow a try block. You cannot have a try block in one place and its catch statements in another. That would be like having a ball game’s pitcher on the mound and the catcher in the parking lot. In all cases, you must follow a try block with one or more catch statements that catch any exceptions thrown by the tried statements.
