# LISTING 19.7 CONTINUED

```
cout << p << endl;
return 0;
}

// Implement the overloaded << operator friend function
//
ostream &
operator<<(ostream & os, const TCoordinate &t)
{
    os << "x == " << t.tc_x << "; y == " << t.tc_y;
    return os;
}
```

In the sample program, the operator<<( ) function is declared as a friend of its class so that it can access the private data members tc_x and tc_y. The function returns type ostream &—a reference to an ostream object. The function also declares two parameters: an ostream reference object os and a const reference to an object of the class for which the operator is being overloaded (TCoordinate in this example). The TCoordinate reference parameter must be const in GNU C++ (some other compilers do not require this), which is just as well because writing an object in an output stream statement certainly should not change its value.

Because the overloaded operator function returns an ostream reference, objects of the class may be used in cascaded output statements. For instance, if p1 and p2 are TCoordinate objects, this simple statement displays their values:

cout << p1 << endl;
    << p2 << endl;

You can provide the same output capabilities for any class. In the operator<<( ) function's implementation, write whatever you want to the os parameter, as the sample program does in the following statement:

os << "x == " << t.tc_x << "; y == " << t.tc_y;

The target of the output statement is os, not cout, as you might assume. By writing to the ostream reference object os passed to the overloaded function, TCoordinate objects can be written to any destination such as a disk file. More on that, however, in Chapter 20, "Customizing I/O Streams."

Listing 19.7 demonstrates how the overloaded output operator works. The program constructs a TCoordinate object and writes it to cout with these statements:

TCoordinate p(10, 20);
cout << p << endl;

Compile and run the program using the following commands to see the text that the second statement produces:

$ g++ pointout.cpp
$ ./a.out
x == 10; y == 20