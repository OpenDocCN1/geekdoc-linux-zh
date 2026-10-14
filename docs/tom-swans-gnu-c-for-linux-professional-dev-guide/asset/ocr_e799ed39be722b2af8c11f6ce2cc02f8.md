return tc_x;
}

int TCoordinate::GetY() const
{
    return tc_y;
}

There's nothing special about the implementation module, except again for the words const following GetX() and GetY(). The module implements the class's three member functions to set and get the values of the private data members tc_x and tc_y. To test the class, we need a host program. A sample is in Listing 14.3, tcoord.cpp (test TCoordinate).

# LISTING 14.3  TCOORD.CPP

```
#include <iostream.h>
#include "coordinate.h"

void display(const char *msg, TCoordinate &tc);
int main()
{
    TCoordinate t1;
    display("Default object", t1);
    TCoordinate t2(45, 218);
    display("Parameterized object", t2);
    t1.SetX(100, 200);
    display("After calling setxy()", t1);
    return 0;
}

void display(const char *msg, TCoordinate &tc)
{
    cout << msg << endl;

    cout << " x = " << tc.GetX() << "; y = " << tc.GetY();
    cout << endl;
}
```

Compile the program using the -c option for the coordinate module, and then link the host program to the module's object code with the following commands:

```
$ g++ -c coordinate.cpp
$ g++ tcoord.cpp coordinate.o
```

Run the program to display the results of three tests using two TCoordinate objects:

```
$ ./a.out
Default object
x = 0; y = 0
Parameterized object
x = 45; y = 218
After calling setxy()
x = 100; y = 200
```