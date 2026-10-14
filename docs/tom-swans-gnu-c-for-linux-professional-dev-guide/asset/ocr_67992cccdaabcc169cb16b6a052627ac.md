That statement constructs an object of the Overflow class, and it throws that object back to the function’s caller. In that function, the program can trap the exception with code such as

```
catch (Overflow) {
    cout << "Overflow detected" << endl;
}
```

# The Standard exception Class

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