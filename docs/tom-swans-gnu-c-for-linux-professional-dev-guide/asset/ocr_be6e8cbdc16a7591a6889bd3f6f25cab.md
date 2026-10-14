reference to the stream object—not the TAnyClass object—for which they are called. As described here, to write a TAnyClass object to the standard output, the program can use simple statements such as the following:

```
TAnyClass object(1, 2);
cout << object;
```

It can similarly read new values into a TAnyClass object by using an equally simple statement:

```
cin >> object;
```

In addition to its two friends, TAnyClass declares two constructors—a default that sets the two private variables to zero, and a parameterized version that accepts integer arguments to initialize x and y. Listing 20.11, tanyclass.cpp, implements the two friend functions:

```
LISTING 20.11  TANYCLASS.CPP

#include <iostream.h>
#include "tanyclass.h"

// Implements overloaded ostream output operator
ostream & operator<< (ostream &os, const TAnyClass &c)
{
    os << "x: TAnyClass object : " << endl;
    os << "x: " << c.x << endl;
    os << "y: " << c.y << endl;
    return os;
}

// Implements overloaded istream input operator
istream & operator>> (istream &is, TAnyClass &c)
{
    cout << "Enter value for x: ";
    is >> c.x;
    cout << "Enter value for y: ";
    is >> c.y;
    return is;
}
```

The sample listing has a suggestion. You can implement the overloaded operators using any method to read and write class objects. You can now compile the TAnyClass module with the following command:

```
$ g++ -c tanyclass.cpp
```

Listing 20.12, objio.cpp (test binary object) demonstrates how to use the binary file classes, fstream and ifstream, to read and write a TAnyClass object in a disk file.