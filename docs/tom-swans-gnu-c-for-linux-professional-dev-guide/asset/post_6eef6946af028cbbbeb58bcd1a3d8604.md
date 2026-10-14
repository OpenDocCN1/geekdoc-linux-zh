
The new bofstream and bifstream classes are similar to the ones listed earlier but are designed using templates to accommodate any C++ data type, including your own classes. In fact, the only significant differences in the two classes are the declarations and implementations of the overloaded input and output operators as templates. To understand the programming, examine the declaration for the bofstream class’s overloaded output operator:

```
template <class T>
bofstream & operator<<( const T & data);
```

This states that T is a placeholder type to be defined later. The overloaded operator<<() function returns a reference to a bofstream object (the same one for which it is called), and it accepts a parameter of type const T &—in other words, a constant reference to an object of an unspecified type. The template’s implementation writes the object using these statements:

```
writeBytes(&data, sizeof(data));
return *this;
```

These are the same statements you examined earlier—but because the type of data is not yet known, they now appear in the header file. No code is generated until C++ instantiates the template.

The overloaded input operator for the bifstream class is written similarly as a template. Listing 20.8, bstream.cpp, implements the bofstream and bifstream class member functions, writeBytes() and readBytes(). Again, these are the same functions presented earlier.

## LISTING 20.8 BSTREAM.CPP

```
#include "bstream.h"

void bofstream::writeBytes(const void *p, int len)
{
    if (!p) return;
    if (len <= 0) return;
    write((char *)p, len);
}

void bifstream::readBytes(void *p, int len)
{
    if (!p) return;
    if (len <= 0) return;
    read((char *)p, len);
}
```

We now have two general-purpose classes, bofstream and bifstream, with overloaded operators that, through the use of templates, can adapt to any data type. To use the classes, compile the module using the command

```
$ g++ -c bstream.cpp
```

That creates object code file bstream.o in the current directory. The next section lists a test program that includes bstream.h header file to read and write binary values in a file.

## READING AND WRITING BINARY VALUES

Listing 20.9 demonstrates how to use the `bofstream` and `bifstream` classes to read and write values of type `double` in a file.

```
```cpp
#include <iostream>
#include <cstdlib.h>      // Need exit()
#include <fstream.h>

#define FILENAME "tbdouble.dat"

int main()
{
    // Construct binary output file
    bofstream bofs(FILENAME);
    if (!bofs) {
        cerr << "Error: unable to write to " << FILENAME << endl;
        exit(1);
    }

    // Write values and close file
    double d = 3.14159;
    bofs << d << d << d << d;
    bofs.close();

    // Construct binary input file
    bifstream bifs(FILENAME);
    if (!bifs) {
        cerr << "Error: unable to open " << FILENAME << endl;
        exit(2);
    }

    // Read and display values from file
    int count = 0;
    cout.precision(8);
    bifs >> d;
    while (!bifs.eof()) {
        cout << ++count << ": " << d << endl;
        bifs >> d;
    }

    return 0;
}
```
```

Compile and run the sample program with the following commands (skip the first command if you already compiled bstream.cpp):

```
```shell
$ g++ -c bstream.cpp
$ g++ -o tbdouble tbdouble.cpp bstream.o
$ ./tbdouble
1: 3.14159
2: 9.8695877
3: 31.006198
```
```

To construct a binary output file, the program creates an object of type bofstream using the statement

```
bofstream bofs(FILENAME);
```

If this succeeds, the program simply writes values to disk using statements such as

```
bofs << d << d * d << d * d * d;
```

```
bofs.close();
```

The last statement closes the file. Although the program doesn't show it, you may write any type of data to the bofs object. However, it's your responsibility to read that data in the same order as written. The objects in the file are simply binary values with no indicators of their types.

To read the values just written, the program constructs an object of the other bstream.cpp class, bifstream:

```
bifstream bifs(FILENAME);
```

It then uses input stream statements such as the following along with a while loop to read and display all values previously stored on disk:

```
bifs >> d;
```

## READING AND WRITING BINARY CLASS OBJECTS

The preceding demonstration only hints at the power of the bofstream and bifstream classes. For example, you can also use these classes to read and write class objects in binary. First, we need a sample class with some private data members to represent any kind of object data. Listing 20.10, tanyclass.h, declares the test class.

## LISTING 20.10 TANYCLASS.H

```
#include <iostream.h>

class TAnyClass {
private:
    int x;  // Private class data members
    int y;
public:
    friend ostream & operator<< (ostream &, const TAnyClass &);
    friend istream & operator>> (istream &, TAnyClass &);
public:
    TAnyClass() : x(0), y(0) {}
    TAnyClass(int X, int Y) : x(X), y(Y) {}
};
```

The test class, TAnyClass, declares two private integer values. A public section declares two friend functions that overload the I/O stream operators << and >>. These functions must be friends of the class because we don't want them to receive a this pointer, but rather, a
