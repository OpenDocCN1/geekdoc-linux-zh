Each object such as `birthday_paul` and `birthday_susan` has its own separate instances of the `TDate` class data members `dt_month`, `dt_day`, and `dt_year`. In each case, the class constructor initializes the objects by copying the specified arguments to the objects’ data members.

> **Warning**
> 
> When writing constructors, be careful not to create any objects of the class type in the constructor implementation. If you do, the constructor might end up calling itself over and over in an endless recursion—endless, that is, until the program runs out of memory and aborts with a core dump!

# MEMBER FUNCTIONS

A common misconception is that objects contain functions such as `Display()`. They don’t. Objects contain only data. Constructors and member functions belong to their classes, and only one copy of each member function and constructor exists in the compiled program.

A member function’s implementation is similar to that of a conventional function’s. For example, the `newdate.cpp` program implements the `TDate` class’s `Display()` member function like this:

```
void TDate::Display()
{
    cout << dt_month << "/" << dt_day << "/" << dt_year << endl;
}
```

The function return type, `void` in this example, comes first. Second is the name of the class that declares the function prototype. The C++ scope resolution operator `::` comes next, followed by the function name and any parameters (there are none in this example). Finally, a pair of braces delimits the function’s statement block inside of which are the statements that perform the function’s job.

Except for the class name and scope resolution operator, the member function’s implementation is the same as a conventional function’s. The class name and operator uniquely identify this function as belonging to its class. Together, the expression `TDate::Display()` fully identifies the member function. Consequently, another class may have a `Display()` member function without causing any name conflicts.

> **Note**
> 
> To identify a class member function in this book, I use the form `TDate::Display()` only when the name of the function alone is ambiguous.

There’s another less obvious difference between a member function and a conventional one. Because member functions are called in conjunction with an object of the class, they can operate on that class’s data members without any further qualification. In the `Display()` member function, for instance, this statement displays the object’s three integer members:

```
cout << dt_month << "/" << dt_day << "/" << dt_year << endl;
```