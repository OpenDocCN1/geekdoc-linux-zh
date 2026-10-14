
# EXCEPTIONS AND LOCAL OBJECTS

When a function throws an exception, C++ automatically destroys any local variables created in that function. Be sure that you understand this effect. It can cause unforeseen consequences when the local variables are themselves objects of classes.

> Note
> Some compilers have a special option to enable the destruction of local objects in the event their declaring block throws an exception. GNU does this by default.

A simple example, localecept.cpp in Listing 16.5, demonstrates how GNU C++ destroys objects in functions that throw exceptions. You might use the program as a test of how other C++ compilers deal with this critical situation.

## LISTING 16.5 LOCALEXCEPT.CPP

```
#include <iostream.h>
#include <exception>

class A {
public:
    A() { cout << "A constructor" << endl; }
    ~A() { cout << "A destructor" << endl; }
};

void f();

int main()
{
    try {
        f();
    }
    catch (const char *s) {
        cout << s << endl;
    }
    return 0;
}

void f()
{
    A a;  // Construct object of class A
    throw ("Error condition");
}
```

The program declares a class, A, with only two members: a constructor and a destructor. Each of these functions displays a message as a trace of when they are called. Function f() constructs an object of type A and then throws an exception using a string to keep things simple. When you compile and run the program, it shows that the object is properly destroyed before the catch statement in main() receives the thrown exception:

```
$ g++ localecept.cpp
$ ./a.out
```

A constructor
A destructor
Error condition

So far, so good. But if the function constructs an object dynamically addressed by a pointer, a very different effect results. Suppose, for example, that function f() constructs the object like this:

```
void f()
{
    A *p = new A;
    throw ("Error condition"); // ???
}
```

Because the dynamic object has global scope, as do all objects created with new, the object's destructor is not called when the function ends with an exception. Worse, the pointer p is destroyed, leaving the object floating in space and causing a memory leak. To avoid this problem, before throwing an exception, you must delete any dynamic objects. You might, for example, use a flag to indicate an error inside the function, and if the flag is set, delete any dynamic objects before throwing the exception:

```
bool error_flag;
...
if (error_flag) {
    delete p;
    throw ("Error condition");
}
```

This type of mistake can easily happen in functions that return pointers to objects constructed with new. Remember that, if the function throws an exception, it does not return a value as it does normally.

# EXCEPTIONS AND CONSTRUCTORS

Class constructors may throw exceptions to indicate that they cannot successfully construct an object. This is a relatively new specification in C++ that some older compilers might not recognize, but GNU C++ is up-to-date in this department. You already saw one example of the technique in this chapter's Error class. To throw an exception in a constructor, simply use a statement as in the following class:

```
class AnyClass {
public:
    AnyClass() {
        if (condition) throw Error();
    }
    ~AnyClass(); // Destructor
};
```

The key concept here is that if a constructor throws an exception—causing the constructor to end abnormally—the object is not constructed, and, most important, any class destructor is not called. Only fully constructed objects are destroyed by calling their destructors, a fact that has especially important consequences in classes that own objects of other classes.

Consider this version of AnyClass:

```
class AnyClass {
    OtherClass x;
public:
    AnyClass(): x() {
        if (condition) throw Error(); }
    ~AnyClass(); // Destructor
};
```

Object x of type OtherClass (not shown) is initialized by AnyClass's constructor using the expression x(). If the OtherClass object's constructor throws an exception, then the AnyClass object's constructor is aborted and the destructor is not called. This effect can be even more crucial in classes that own multiple class objects:

```
class AnyClass {
    OtherClass a, b, c;
public:
    AnyClass(): a(), b(), c() {}
    ~AnyClass(); // Destructor
};
```

If object b's constructor throws an exception, object c is not constructed, and neither is the AnyClass object. However, object a's destructor is called because that object was fully constructed before the construction of b caused a problem. In cases where objects have pointers to dynamic memory, it might take a little thought to be sure that, in the event of a constructor throwing an exception, all objects are properly disposed. In rare cases, it might be necessary to rearrange the initialization order of class-object data members (a, b, and c in the example) so that everything works as intended.

# CLASSES THAT THROW THEMSELVES AROUND

A class can also throw an exception object of its own class type. Usually, this is done in an exception class by a member function, often called Raise(). You might, for example, design the exception class like this:

```
class Error {
public:
    void Raise() { throw Error(); }
};
```

The class might also declare other functions, constructors, a destructor, and data members. If e is an object of type Error, the following statement throws another object of the Error class:

```
e.Raise();  // Throws fresh Error object
```

Depending on other services in the Error class, this might be a good way to throw an exception after it is initially handled. Doing this keeps the exception alive, causing C++ to continue searching upward in the function call chain for a matching exception handler. In many cases, you can do this simply by throwing the same object received by a catch statement:

```
catch (Error e) {
    // initially handle this type of error
    throw e; // rethrow exception to this function's caller
}
```
