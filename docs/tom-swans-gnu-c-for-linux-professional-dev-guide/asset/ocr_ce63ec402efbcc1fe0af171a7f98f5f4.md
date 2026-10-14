# INTEGER VARIABLES

There are seven numerical data types in C++: char, short, int, long, float, double, and long double. GNU C++ adds an eighth type, long long, but more on that in the section “Double Wide Integers” later in this chapter.

> Note
> Although the char type usually represents alphanumeric characters, it is internally just an integer value and can be used to represent byte values as well as characters.

Listing 6.1 shows how to declare variables of all seven C++ integer data types. The program also demonstrates how to determine the size of an object using the C++ sizeof operator.

# LISTING 6.1 INTEGERS.CPP

```
#include <iostream.h>

// Global variables

char c;
short s;
int i;
long l;
float f;
double d;
long double ld;

int main()
{
cout << "Sizeof char     == " << sizeof(c) << endl;
cout << "Sizeof short    == " << sizeof(s) << endl;
cout << "Sizeof int      == " << sizeof(i) << endl;
cout << "Sizeof long     == " << sizeof(l) << endl;
cout << "Sizeof float    == " << sizeof(f) << endl;
cout << "Sizeof double   == " << sizeof(d) << endl;
cout << "Sizeof long double == " << sizeof(ld) << endl;
return 0;
}
```

The integers.cpp program declares seven global variables, one for each of the C++ numerical data types. They are called global variables because they are declared outside any function and are therefore available for use globally throughout the program. (Chapter 10, “Creating and Calling Functions,” in the section “Functions and Variables” explains how to create and use local variables inside functions. See also “Global and Local Variables” later in this chapter.) Global variables are initially zeroed—in other words, the bytes that compose the variables are set to zero at runtime. Compile and run the integers.cpp program with the following two commands:

```
$ g++ integers.cpp
$ ./a.out
Sizeof char     == 1
Sizeof short    == 2
```