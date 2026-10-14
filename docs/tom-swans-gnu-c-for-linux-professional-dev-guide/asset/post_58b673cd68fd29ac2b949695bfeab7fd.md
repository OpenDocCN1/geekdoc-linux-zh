
to the object's data is carefully controlled. Interestingly, the program has, in effect, added C++ exception handling to the common C-language array data structure!

## FUNCTION CALL OPERATOR

Overloading the function call operator—represented by a pair of parentheses ()—effectively makes a class object appear to be a callable function. The overloaded operator()() function may return a typed value, or void, and it may optionally declare parameters. It must be a nonstatic class member. Here's a sample class with an overloaded function call operator that returns an int value:

```
class TAnyClass {
private:
    int x;
public:
    TAnyClass(int arg): x(arg) { }
    int operator()();
};
```

This example of the overloaded operator()() function declares no parameters. Implement it separately using code such as this:

```
int TAnyClass::operator()()
{
    return x;
}
```

Or, you can more simply create an inline function directly in the class:

```
int operator()() { return x; }
```

Either way, a program can use an object of the class as though it were a callable function. Statements such as the following are possible:

```
TAnyClass object(100);
int q = object();  // Call object as a function
```

The second statement appears to call a function named object(), but it actually calls the operator()() function of TAnyClass for object. This technique might be useful to hide the fact that object() is not really a function, or more likely, to upgrade existing code that calls a function in need of extensive repairs. By converting the original function to a class, and providing it with an overloaded function-call operator()(), the existing programming can be compiled to take advantage of other features available only with object-oriented C++ classes.

## CLASS MEMBER ACCESS OPERATOR

Overloading the unary struct- and class member access operator, ->, provides pointer-like access to members. There may be few if any practical uses for this technique, but it might serve as a debugging device to trace member function calls. Listing 19.5, access.cpp, demonstrates the basic method.

### LISTING 19.5 ACCESS.CPP

```
#include <iostream.h>

class TAnyClass {
private:
    int x, y;
public:
    TAnyClass(int xarg, int yarg): x(xarg), y(yarg) {}
    TAnyClass * operator->();
    int Getx() const { return x; }
    int Gety() const { return y; }
};

int main()
{
    TAnyClass test(123, 456);
    cout << test->Getx() << endl;
    cout << test->Gety() << endl;
    return 0;
}

TAnyClass * TAnyClass::operator->()
{
    cout << "Accessing member: ";
    return this;
}
```

To overload the -> operator, insert a prototype such as the following into a class's public section:

```
TAnyClass * operator->();
```

This states that the operator->() function returns a pointer to an object of its class. Technically, it should be possible to return a reference or an object value, but GNU C++ seems to recognize only the pointer variety. (There's no real benefit in using the other forms, and no need for concern about this minor problem.)

Implement the overloaded operator as shown at the end of Listing 19.5. The function may perform any actions—here it displays a string that indicates when the function is called. The final statement should always be as shown. Returning this returns a pointer to the object for which the function is called.

To demonstrate how the overloaded operator works, the sample program constructs a test object of type TAnyClass and then executes two output statements:

```
TAnyClass test(123, 456);
cout << test->Getx() << endl;
cout << test->Gety() << endl;
```

Even though test is constructed as a local variable, because of the overloaded operator->() function, statements may use test as though it were a pointer to a TAnyClass object. When

```
```cpp
cout << "t = " << t.Get();
cout << "; t++ == " << t++ << endl;
cout << "t = " << t.Get();
cout << "; ++t == " << ++t << endl;
cout << "t = " << t.Get();
cout << "; t-- == " << t-- << endl;
cout << "t = " << t.Get();
cout << "; t-- == " << t-- << endl;

return 0;
}
```
```

The overloaded function operator++() defines a prefix increment operator for a class object—in this case, for TanyClass. To define a postfix increment operator, declare an int parameter in the function. Usually, you define both operators as follows:

```
```cpp
int operator++()     { return ++x; }  // Prefix ++
int operator++(int)  { return x++; }   // Postfix ++
```
```

The int parameter needs no name, and its value is unimportant. This merely takes advantage of the C++ overloading rule that states any function may be overloaded (have the same name) as long as such functions differ in at least one parameter type. This is how it's possible to define different ++ operators for the same class. Define decrement operators similarly:

```
```cpp
int operator--()     { return --x; }  // Prefix --
int operator--(int)  { return x--; }   // Postfix --
```
```

What the operators do is up to you. Here, they simply operate on the class's private integer variable. In another situation, they might advance or retard a pointer to objects linked together in a list, or move forward and back through a database. It's totally up to you what the operators do. However, be sure to respect the general nature of prefix and postfix operations. A prefix expression such as ++object should return object's value and then perform the increment. A postfix expression such as object++ should return the incremented value of object, whatever that means.

To demonstrate the overloaded operators, the program writes the current value of a test object and then applies each operator in turn. Compile and run the program with the following commands and see the results as printed here:

```
```text
$ g++ in​dec.cpp
$ ./a.out
t = 100; t++ == 101
t == 101; ++t == 101
t = 102; t-- == 101
t = 101; t-- == 101
```
```

Each operator expression such as ++t applies to the value shown at its left. Study each line to verify that prefix and postfix operations are evaluated correctly. For example, the value of t++ equals the value of t before its value is incremented.

In practice, writing operator++() and operator--() functions might not be as simple as the in​dec.cpp program in Listing 19.6 implies. Later in this chapter, Listing 19.9 shows a more
