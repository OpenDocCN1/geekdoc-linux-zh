tc_x to the value of x, and tc_y to the value of y. The statement block is empty because the constructor has no other tasks to perform, but it may execute other statements if needed. The equivalent constructor could be written using the more familiar programming:

```
TCoordinate(int x, int y)
{
    tc_x = x;
    tc_y = y;
}
```

In simple classes like TCoordinate, either method is perfectly acceptable, and both techniques produce the same end results. You may use initializing expressions or statements to initialize data member values. However, consider again our hypothetical class that declares a data member as a TDate object:

```
class TAnyClass {
private:
    TDate the_date;    // Class object data member
public:
    TAnyClass();       // Default constructor
};
```

The question is, how can the class initialize the date? As you know, all objects must be initialized by calling a class constructor. But, when you try to implement the TAnyClass constructor, you run head-on into a brick wall:

```
public:
    TAnyClass() { the_date //...???
```

To initialize the_date requires calling a TDate class constructor, but it’s not possible to call constructors as common functions, and the programmer is stuck. The solution, as you might already suspect, is to use an initializing expression to construct the_date. The completed class follows:

```
class TAnyClass {
private:
    TDate the_date;    // A class object data member
public:
    TAnyClass() : the_date(2, 1, 2001) { }
};
```

The initializing expression (notice the colon) constructs the_date, in this case, by calling the TDate() parameterized constructor. This is, in fact, the only way you can initialize data members in a class that are themselves objects of classes.

> **Tip**  You may use initializing expressions for data members of any type; they are required, however, only for initializing data members that are themselves objects of C++ classes.

You may use initializing expressions also when implementing constructors separately from their prototypes. Declare the preceding class as follows:

```
class TAnyClass {
private:
```