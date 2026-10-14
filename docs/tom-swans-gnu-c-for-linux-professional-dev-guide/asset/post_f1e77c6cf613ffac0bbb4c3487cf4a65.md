
An explicit destructor call is unusual and should be employed only when it isn’t possible to delete an object. Older compilers may require you to specify the class name as follows (this also works with newer GNU C++ releases). Use this form for the best portability:

p->TPersist::~TPersist();

## NESTED CLASS DECLARATIONS

By nesting certain kinds of declarations in classes, you can provide a class with data types that are determined solely by the class. A class can nest a typedef symbol, a struct, or even another class. Such declarations are sometimes useful for providing items that are intimately tied to the class’s internal design. For example, using a nested typedef declaration, you can create a class that keeps track of how many objects of its type exist at any one time in a program—a device that might be useful for debugging.

Listing 21.13, objcount.cpp, demonstrates how to create an automatic object counter by exporting a data type from the class.

```cpp
#include <iostream.h>

class TAnyClass {
private:
    typedef int CLASS_COUNTER;
    static CLASS_COUNTER classCount;
    static int GetCount() { return classCount; }
public:
    TAnyClass() { ClassCount++; }  // Constructor
    ~TAnyClass() { ClassCount--; } // Destructor
    static void ShowCount();
};

// Define static member
//
TAnyClass::CLASS_COUNTER TAnyClass::ClassCount;

TAnyClass globalObject;

int main()
{
    cout << "On entry to program" << endl;
    TAnyClass::ShowCount();

    TAnyClass localObject;
    cout << "After constructing one object" << endl;
    TAnyClass::ShowCount();

    TAnyClass objectA, objectB, objectC;
    cout << "After constructing three objects" << endl;
    TAnyClass::ShowCount();

    TAnyClass * pointer = new TAnyClass;
    cout << "After creating a dynamic object" << endl;
```

```
TAnyClass::ShowCount();
delete pointer;
cout << "After deleting the dynamic object" << endl;
TAnyClass::ShowCount();

}

void TAnyClass::ShowCount()
{
    cout << "Number of objects == " << TAnyClass::GetCount();
    cout << endl;
}
```

The sample program uses static members to store a count of the objects of type TAnyClass in existence at any one time. To keep track of this count, the class constructor increments the static ClassCount variable. The class destructor decreases this value. To export the counter's type, the class nests the typedef declaration:

```
typedef int CLASS_COUNTER;
static CLASS_COUNTER ClassCount;
```

In this way, the class itself determines the type of the static ClassCounter variable. Although this is a simple example, it might be used to change the type from int to long—or even to a class object—without requiring any changes except to the preceding declaration. Because the ClassCounter is static, it must be defined somewhere in the program. The test program defines the variable like this:

```
TAnyClass::CLASS_COUNTER TAnyClass::ClassCount;
```

The importance of this programming is that ClassCount's type is hidden inside TAnyClass. Thus, this variable can be declared without the program having any specific knowledge of its type. When you compile and run the program, the rest of the test statements show how many TAnyClass objects exist at various stages.

Complex nested declarations are also possible. A class can declare an inner struct like this:

```
class TAnyClass {
public:
    struct ClassStruct {
        int x, y;
    };
};
```

The struct is exported by the class and must therefore be used in reference to the class. For example, the program could define an object of type ClassStruct by using a statement such as

```
TAnyClass::ClassStruct structure;
```

Statements as follows refer to the struct's x and y members:

```
structure.x = 1;
cout << "y = " << structure.y << endl;
```

It's common to use this technique to provide the design of an object from inside a class. Listing 21.14, nest.cpp, demonstrates the basic technique of a class that exports the type of another class for use in the program.

## LISTING 21.14 NEST.CPP

```
#include <iostream.h>

class TAnyClass {
public:
class TOtherClass {
private:
int x, y;
public:
TOtherClass(int x_arg, int y_arg): x(x_arg), y(y_arg) { }
int Getx() { return x; }
int Gety() { return y; }
};
};

int main()
{
TAnyClass::TOtherClass object(10, 20);
cout << "x == " << object.Getx() << endl;
cout << "y == " << object.Gety() << endl;
return 0;
}
```

The sample program declares TAnyClass with only a single member—an exported class of type TOtherClass. (In practice, TAnyClass would probably declare its own constructors, destructor, data members, and member functions.) The nested TOtherClass has two private integer variables, a constructor that initializes those data members, and two member functions that return the private data values.

The nested class is a public member of TAnyClass so that statements in the program can refer to both classes. It's also possible to nest classes in protected and private sections, and, in fact, this is useful in complex class hierarchies that export class declarations for use only in that class and in derived classes.

To create an object of type TOtherClass, the program uses the following statement:

```
TAnyClass::TOtherClass object(10, 20);
```

The object is of type TOtherClass, not TAnyClass. Although it's possible to construct an object of the outer class as follows, it's important to realize that this does not create an object of TOtherClass:

```
TAnyClass value;
```

TAnyClass exports the TOtherClass class declaration; it does not contain an object of that type. Although the preceding statement compiles, there's nothing in this case to do with the resulting object because TAnyClass declares no other members.
