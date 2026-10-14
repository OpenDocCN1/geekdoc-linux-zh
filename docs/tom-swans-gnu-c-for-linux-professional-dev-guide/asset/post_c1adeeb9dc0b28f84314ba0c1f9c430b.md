
## LISTING 21.5 IMPLICIT.CPP

```
#include <iostream.h>
#include <stdlib.h>    // Need atoi()

class TAnyClass {
private:
    int value;
public:
    TAnyClass(int n) { value = n; }
    TAnyClass(const char *ns) { value = atoi(ns); }
    int GetValue() { return value; }
};

int main()
{
    TAnyClass v1 = 123;
    TAnyClass v2 = "96";
    cout << "v1 == " << v1.GetValue() << endl;
    cout << "v2 == " << v2.GetValue() << endl;
    return 0;
}
```

TAnyClass declares two constructors, one that requires an int argument and another that requires a char pointer to a NULL-terminated string. Each constructor assigns its parameter to the private value data member. (For simplicity, the class is implemented entirely inline.) The alternate constructor calls the standard atoi() function declared in stdlib.h to convert its string parameter to an integer. The main program declares two variables of type TAnyClass and then displays their values by calling the class's GetValue() member function.

In the two statements in main() that construct variables v1 and v2, the values 123 and "96" are implicitly converted into objects of their class types so that the assignment statements compile. To explicitly state that such values must only be class objects, and thus prevent the implicit conversions, preface the constructors with the reserved word explicit. Listing 21.6, explicit.cpp, shows the revised class and gives examples of allowable declarations of TAnyClass objects.

## LISTING 21.6 EXPLICIT.CPP

```
#include <iostream.h>
#include <stdlib.h>    // Need atoi()

class TAnyClass {
private:
    int value;
public:
    TAnyClass(int n) { value = n; }
    explicit TAnyClass(const char *ns) { value = atoi(ns); }
    int GetValue() { return value; }
};
```

### LISTING 21.6 CONTINUED

```
int main()
{
    TAnyClass v1 = TAnyClass(123);
    TAnyClass v2 = TAnyClass("987");
    TAnyClass v3(456);
    TAnyClass v4('654');
    cout << "v1 == " << v1.GetValue() << endl;
    cout << "v2 == " << v2.GetValue() << endl;
    cout << "v3 == " << v3.GetValue() << endl;
    cout << "v4 == " << v4.GetValue() << endl;
    return 0;
}
```

Using the revised class, because of the explicit constructors, any attempts you make to create objects using statements such as these (taken from Listing 21.5, implicit.cpp) now produce errors:

```
TAnyClass v1 = 123;  // ???
TAnyClass v2 = "96";  // ???
```

Compiling the program with statements such as those causes GNU C++ to issue these error messages:

```
explicit.cpp: In function `int main()':
explicit.cpp:25: conversion from `int' to
  non-scalar type `TAnyClass' requested
explicit.cpp:26: conversion from `char[3]'
  to non-scalar type `TAnyClass' requested
```

Because the TAnyClass constructors are explicit, C++ no longer allows values such as 123 and "96" to be implicitly converted to TAnyClass objects for assigning to other TAnyClass objects or for use in constructing new objects.

> Tip
> In practice, classes with explicit constructors such as those in this section probably also need copy constructors and operator=() functions.

## MUTABLE DATA MEMBERS

To prevent a class member function from modifying the value of a data member in that class (or one inherited from an ancestor class), declare the function const like this:

```
class TAnyClass {
    ...
    int x;
    int GetValue() const { return x; }
};
```

If any statement in GetValue() attempts to change x, the compiler issues an error message. However, the const designation makes all data members in the class unchangeable. This can be troublesome in designing functions that need to change some data but designate other values as hands off. Listing 21.7, constant.cpp, demonstrates the basic problem.

## LISTING 21.7 CONSTANT.CPP

```
#include <iostream.h>

class TAnyClass {
private:
    int value;
    long counter;
public:
    TAnyClass(int arg): value(arg), counter(0) { }
    int GetValue() /*const*/ {
        counter++; // ???
        return value;
    }
    int GetCounter() const { return counter; }
};

int main()
{
    TAnyClass v1(123);
    cout << "v1 value == " << v1.GetValue() << endl;
    cout << "v1 counter == " << v1.GetCounter() << endl;
    return 0;
}
```

Class TAnyClass declares two data members, an integer value, and a long counter. We want member function GetValue() to return the integer and guarantee that its value isn't changed by calling that function. However, to keep track of how many times GetValue() is called, we want the function also to increment counter. If you remove the comment delimiters from const in the GetValue() declaration, compiling the program causes GNU C++ to complain with the following error message:

```
$ g++ constant.cpp constant.cpp
In method 'int TAnyClass::GetValue() const':
constant.cpp:21: increment of read-only member 'TAnyClass::counter'
```

Listing 21.8, mutable.cpp, makes counter mutable to allow changes to it even in const functions such as GetValue().

## LISTING 21.8 MUTABLE.CPP

```
#include <iostream.h>

class TAnyClass {
private:
    int value;
    mutable long counter;
public:
    TAnyClass(int arg): value(arg), counter(0) { }
    int GetValue() const {
        counter++;
        return value;
```
