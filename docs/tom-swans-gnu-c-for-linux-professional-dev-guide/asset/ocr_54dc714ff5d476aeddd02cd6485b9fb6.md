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
T AnyClass::CLASS_COUNTER TAnyClass::ClassCount;
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
T AnyClass::ClassStruct structure;
```

Statements as follows refer to the struct's x and y members:

```
structure.x = 1;
cout << "y = " << structure.y << endl;
```