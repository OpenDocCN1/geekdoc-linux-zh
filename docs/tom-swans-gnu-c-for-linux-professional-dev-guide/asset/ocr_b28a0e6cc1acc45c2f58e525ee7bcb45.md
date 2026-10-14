realistic example of how to program these operators for objects other than simple integer values. See "Increment and Decrement Operators Revisited" for more on this topic.

Note

Listing 19.6, incdec.cpp, demonstrates a subtle bug in GNU C++ that I discovered also in Borland C++ 4.5 (fixed in 5.0). The output stream statements are written as shown in the listing to force the correct evaluation order of statements such as t.Getx() and ++t. If these are written in a single cascaded output statement:

cout << "t == " << t.Getx() << "; ++t == " << ++t << endl;

the statement ++t is incorrectly evaluated before t.Getx(), and the results are very different. This unintended side effect in output statements is a serious matter. Until it is fixed, beware of this bug—it is easily missed. Both forms of output statements are in the incdec.cpp file on the CD-ROM.

# OVERLOADED OUTPUT STREAMS

The default output stream operator << recognizes all native C and C++ data types such as int, double, char, and char *. By overloading the output stream operator, you can add your own class data types that output statements can write. Instead of writing a Display() or similar output function, by overloading the << operator, your program can use code such as the following to write the values of any type of object:

```
TYourClass object;
...
cout << "object == " << object << endl;
```

Listing 19.7, pointout.cpp, demonstrates how to overload the << operator for a version of the TCoordinate class from Chapter 14, "Investing in Inheritance."

# LISTING 19.7 POINT OUT.CPP

```
#include <iostream.h>

class TCoordinate {
private:
    int tc_x, tc_y;
public:
    TCoordinate(): tc_x(0), tc_y(0) {}
    TCoordinate(int x, int y): tc_x(x), tc_y(y) {}
    void Setxy(int x, int y);
    int Getx() const;
    int Gety() const;
    friend ostream &
    operator<<(ostream & os, const TCoordinate &t);
};

int main()
{
    TCoordinate p(10, 20);
```