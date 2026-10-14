
Then use statements such as the following to construct vector containers for specific types of data:

```cpp
vector<int> vint;
vector<string> vstring(10);
vector<double> vdouble(100);
```

The first statement constructs an empty vector that can hold values of type `int`. However, it's rarely useful to construct empty vectors, and you'll normally specify an initial size as the other two statements demonstrate. The first of these constructs a vector container, `vstring`, big enough to hold 10 `string` objects. The second statement constructs a vector named `vdouble` big enough for 100 values.

> **Warning**
> Attempting to insert an object into an empty vector may cause a memory segmentation fault. To prevent this unhappy event, always specify a size for vector containers.

Because the containers are vectors, the most common way to insert data into them is to use array index expressions such as the following:

```cpp
vstring[1] = "Value == ";
vdouble[2] = 3.14159;
```

You can also access elements in a vector, for example, to display their values in an output statement:

```cpp
cout << vstring[1] << vdouble[2] << endl;
```

You may store other types of data in vector containers. However, any structures, including class objects, require the following elements:

- A default constructor
- A copy constructor
- A destructor
- An overloaded operator&() (address of) function
- An overloaded operator=() (assignment) function

You need to implement those elements only if C++ cannot generate them automatically. For example, if your class declares any pointers to allocated memory, the class must have an explicit copy constructor and `operator=()` function to prevent memory leaks.

## LISTING 24.1 TCOORDINATE.H (CLASS MEMBERS)

```cpp
class TCoordinate {
private:
    int tc_x, tc_y;
public:
    TCoordinate();
    TCoordinate(int x, int y);
    TCoordinate(const TCoordinate& arg);
    ~TCoordinate();
    void operator=(const TCoordinate& copy);
    bool operator==(const TCoordinate& arg) const;
    bool operator<(const TCoordinate& arg) const;
    inline friend ostream &
        operator<<(ostream & os, const TCoordinate& q);
    inline friend istream &
        operator>>(istream & is, TCoordinate& q);
    void SetX(int x);
    void SetY(int y);
    int GetX() const;
    int GetY() const;
};
```

Given the `TCoordinate` class, you can create a vector of class objects and a pointer to those objects using statements such as these:

```cpp
vector<TCoordinate> vobject(10);
vector<TCoordinate *> vpointer(10);
```

The first statement constructs a vector of 10 `TCoordinate` objects. The second statement constructs a similar vector but stores pointers to `TCoordinate` objects. To insert a class object into a vector, construct it and assign the result using an array index expression:

```cpp
vobject[0] = TCoordinate(10, 20);
vpointer[0] = new TCoordinate(30, 40);
```

Because `TCoordinate` provides overloaded `<<` and `>>` operators, you can display the object values with output statements such as the following:

```cpp
cout << "vobject[0] : " << vobject[0] << endl;
cout << "vpointer[0] : " << *vpointer[0] << endl;
```

As mentioned, when storing pointers in containers, it is your responsibility to delete any objects created using `new`:

```cpp
delete vpointer[0];
```

You may also construct a vector using iterators. For example, these statements copy an array of `int` values into a vector:

```cpp
int iarray[24];
vector<int> v1(iarray, iarray + 24);
```

This statement copies the values from vector `v1` to a new vector `v2`:

```cpp
vector<int> v2(v1.begin(), v1.end());
```

In addition to these methods for constructing vector containers, a second argument passed to the constructor is supposed to initialize the values in a container:

```cpp
vector<int> vinit(32, -1); // ???
```

That should set all 32 elements in `vinit` to -1, but at this writing, the statement does not compile. Work around this problem by passing a variable instead of a literal initial value:

```cpp
int x = -1;
vector<int> vinit(32, x);
```

## USING VECTORS

The size of a vector container equals how many elements it stores. If `vdouble` is a vector of 100 `double` values, the following statement displays 100:

```cpp
cout << "Size of vdouble = " << vdouble.size() << endl;
```

A vector's capacity indicates how large the vector may become before a memory allocation is needed for holding more objects:

```cpp
cout << "Capacity = " << vdouble.capacity() << endl;
```

A vector's size may be the same or less than its capacity. A vector's maximum size returns the upper limit on how many objects a vector can hold:

```cpp
cout << "Max size = " << vdouble.max_size() << endl;
```

The maximum size does not, however, indicate how much memory is available to the vector. You can alter a vector's capacity without affecting its current size by calling the `reserve()` function. This is a memory-efficient way to avoid frequent allocations in cases where you can determine in advance how many values the program ultimately stores in the container. For example, the following statement changes the `vdouble` container's capacity to 250, but its size remains at 100:

```cpp
vdouble.reserve(250);
```

## BOOLEAN VECTORS

The STL treats a Boolean vector container as a special superset of the `vector` class template. Define a Boolean vector using the C++ `bool` data type like this:

```cpp
vector<bool> vbool(16);
```

That creates a vector named `vbool` of 16 `true` and `false` values. Use subscript expressions to assign values to vector elements:

```cpp
vbool[0] = true;
vbool[1] = false;
```

You can also specify an initial value. For example, this constructs an eight-element Boolean vector with all values initialized to `true`:

```cpp
vector<bool> vbin(8, true);
```
