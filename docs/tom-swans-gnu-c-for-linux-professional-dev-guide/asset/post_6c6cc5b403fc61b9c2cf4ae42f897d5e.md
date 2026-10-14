
## LISTING 19.9 CONTINUED

```
friend ostream & operator<<(ostream & os, const TAnyClass &t) {
    os << t.object;
    return os;
}

int main()
{
    TAnyClass t{100};

    cout << "t == " << t;
    cout << "; ++t == " << ++t << endl;
    cout << "t == " << t << ";";
    cout << "t++ == " << t++ << endl;
    cout << "t == " << t;
    cout << "; --t == " << --t << endl;
    cout << "t == " << t;
    cout << "; t-- == " << t-- << endl;

    return 0;
}
```

Running and compiling refinedec.cpp produces the same output as the original program. Enter the following commands to run the test:

```
$ g++ refinedec.cpp
$ ./a.out
t == 100; ++t == 101
t == 101; t++ == 101
t == 102; --t == 101
t == 101; t-- == 101
```

That's the same output as the original program, but because the output stream operator is overloaded for the class, main() can more simply write object t instead of calling the GetX() function.

Internally, the program's classes handle the expressions such as ++t and t++ differently. To represent the class of object requiring the overloaded operations, TObject provides two member functions:

```
void Increment();
void Decrement();
```

To use the method described here, your own class needs to provide only these two functions. It may provide others, and what happens when the functions are called is up to you. For the demonstration, the functions simply increment and decrement an integer value. Most important, however, is that there is no need to distinguish between prefix (++x) and postfix (x++) operations.

That job is handled by a second class, represented in Listing 19.9 as TAnyClass. The class declares two objects of type TObject:

```
private:
TObject object;
TObject temp;
```

The temp object makes it possible for the overloaded operators to return the correct prefix and postfix values regardless of the nature of the actual data. For example, the overloaded postfix operator++() function is implemented inline using this code:

```
const TObject & operator++(int) { // Postfix object++
    temp = object;
    object.increment();
    return temp;
}
```

It is necessary to assign the current object value to temp so that object can be incremented but still permit the function to return the unincremented value. There might be other ways to achieve this same result (pushing the original object onto a stack container, for example, and then popping it off as the return value). However, the method shown here should be adequate for most purposes. Simply replace TObject with your own class and provide Increment() and Decrement() member functions. If your class addresses any dynamic memory, be sure to provide a copy constructor and operator=() function as well (see Chapter 13, “Creating and Destroying Objects”).

## Other Operator Overloading Concerns

When overloading operators for your own classes, keep the following restrictions in mind:

- C++ does not “understand” the meaning of an overloaded operator. It’s your responsibility to define meaningful operations for specific operators.

- C++ is unable to derive complex operators from simple ones. For example, in a class with overloaded operator*() and operator=(), C++ cannot combine those functions to evaluate expressions in statements such as a *= b. To handle the shorthand operator, the class must additionally overload the operator*=() function.

- You cannot change the syntax of an overloaded operator. Binary operators must remain binary. Unary operators must remain unary. It is not possible to create a unary division operator because no such capability exists for C++.

- You cannot invent new operators. You may overload only the operators listed in Table 19.1.

- You cannot overload preprocessing symbols such as #define.

## Overloading and Memory Management

C programs use standard library functions such as malloc() and free() to allocate and deallocate memory. By contrast, C++ programs use operators new and delete. Below the hatch, many C++ compilers implement new and delete by calling malloc() and free(). It is a mistake, however, to conclude that no significant differences exist between C and C++ memory management.
