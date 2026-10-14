
## OVERLOADED INPUT STREAMS

Overloading the input stream operator >> effectively teaches C++ how to input objects of a class. Listing 19.8, pointin.cpp, is similar to pointout.cpp, but adds both input and output operators for TCoordinate objects.

```cpp
#include <iostream.h>

class TCoordinate {
private:
    int tc_x, tc_y;
public:
    TCoordinate(): tc_x(0), tc_y(0) { }
    TCoordinate(int x, int y): tc_x(x), tc_y(y) { }
    void Setxy(int x, int y);
    int Getx() const;
    int Gety() const;
    friend ostream &
        operator<<(ostream & os, const TCoordinate &t);
    friend istream &
        operator>>(istream & is, TCoordinate &t);
};

int main()
{
    TCoordinate p;

    cout << "Before: " << p << endl;
    cout << "Enter x and y values (ex. 10 20): ";
    cin >> p;
    if (cin.good())
        cout << "Input error" << endl;
    else
        cout << "After: " << p << endl;

    return 0;
}

// Implement the overloaded << operator friend function
//
ostream &
operator<<(ostream & os, const TCoordinate &t)
{
    os << "x = " << t.tc_x << "; y = " << t.tc_y;
    return os;
}

// Implement the overloaded >> operator friend function
//
istream &
operator>>(istream & is, TCoordinate &t)
{
    is >> t.tc_x >> t.tc_y;
    return is;
}
```

The overloaded input stream operator >> function is declared similarly to the output function as a friend of the following class:

```
friend istream &
operator>>(istream & is, TCoordinate &t);
```

The operator>>() function returns a reference to an istream (input stream) object so that it can be used in cascaded input statements. It declares two parameters: an istream reference named is and a reference to a TCoordinate object. In this case, the input object cannot be constant because the input operator presumably changes its value in some way. In this case, the function's implementation simply reads from the input stream parameter is into the TCoordinate object's tc_x and tc_y private data members using the following statement:

```
is >> t.tc_x >> t.tc_y;
```

Following this, the function returns the same input stream reference (is). All operator>>() functions should end the same.

The main() program demonstrates how to use the TCoordinate class's new input capability. The program first constructs a default object and then prompts you to enter values into it:

```
TCoordinate p;
 cin >> p;
```

To try this, enter the following commands to compile and run the program, and then type two integer values separated by a blank as shown here:

```
$ g++ pointin.cpp
$ ./a.out
Before: x == 0; y == 0
Enter x and y values (ex. 10 20): 45 62
After: x == 45; y == 62
```

> Note
> Chapter 20, "Customizing I/O Streams," explains more about overloading input and output stream operators, and shows how to use them to read and write objects in disk files.

## INCREMENT AND DECREMENT OPERATORS REVISITED

As mentioned, successfully overloading the operator++() and operator--() functions is not as simple as demonstrated earlier in this chapter in the incdec.cpp program (refer to Listing 19.6). This is so primarily because, to distinguish between prefix and postfix operations, often requires special care.

For example, in a container class that stores class objects instead of integer values, careful programming is needed to correctly implement prefix and postfix increment and decrement operations. For readers who are struggling with this, Listing 19.9, refin dec.cpp, shows how to use temporary objects to provide these operators for two hypothetical classes.

### LISTING 19.9 REFINCDEC.CPP (PARTIAL)

```
#include <iostream.h>

// Sample class for object upon which increment and
// decrement operations are defined. Can be anything
// that defines public Increment() and Decrement()
// functions. The output stream operator is just for
// this demonstration and is not required.
//
class TObject {
private:
    int x;
public:
    TObject(int arg): x(arg) {}
    // int Getx() const { return x; }
    // int Putx(int arg) { x = arg; }
    void Increment() { x += 1; }
    void Decrement() { x -= 1; }
    friend ostream & operator<<(ostream & os, const TObject &t) {
        os << t.x;
        return os;
    }
};

// Represents the class that overloads ++ and -- operators
// for an object of type TObject. Only that class name needs
// to be changed to use this class. The overloaded output
// stream operator is for this demonstration only.
//
class TAnyClass {
private:
    TObject object;
    TObject temp;
public:
    TAnyClass(int arg): object(arg), temp(arg) {}
    const TObject & operator++() {    // Prefix ++object
        object.Increment();
        return object;
    }
    const TObject & operator++(int) { // Postfix object++
        temp = object;
        object.Increment();
        return temp;
    }
    const TObject & operator--() {    // Prefix --object
        object.Decrement();
        return object;
    }
    const TObject & operator--(int) { // Postfix object--
        temp = object;
        object.Decrement();
        return temp;
    }
};
```
