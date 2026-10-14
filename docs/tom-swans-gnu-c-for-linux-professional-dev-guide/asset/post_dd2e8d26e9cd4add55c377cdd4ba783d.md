
Figure 21.1 shows the relationship between a class that, through reference counting, keeps track of its owners. Objects A through F own data objects Data1, Data2, and Data3. Those objects track their ownership counts, shown in parentheses.

## Figure 21.1
Using reference counting, a data object keeps track of the number of its owners.

![](img/6eab91cc30158075ed10d0cabbac9029_495_0.png)

Data objects such as Data1, Data2, and Data3 in Figure 21.1 provide a function that returns a copy of themselves. Instead of constructing an entirely new object, however, the function merely increments its object's ownership counter and returns that same object. For example, from Figure 21.1, if a new object G is constructed using Data3, that object's function increments Data3's ownership counter to indicate that three objects own that data. In this way, only one copy of the unique data exists in memory.

Deleting objects also takes special handling. Again, using Figure 21.1, if the program deletes object B, it must not also delete Data2 because two other objects, C and D, still own that data. To handle the deletion of B, Data2's destructor simply decrements its ownership count, changing 3 to 2. Likewise, if object D is deleted, Data2's ownership counter is again decremented from 2 to 1, indicating that only one object owns it. If C is then deleted, Data2 is also disposed of because its ownership counter now equals 1, signaling that this is the only copy of the data, and it therefore may be safely deleted.

## COPY-ON-WRITE METHOD

Reference counting alone is only half the game in providing for safe, efficient, object copying. Another required piece of the puzzle is what happens when a change is made to a duplicated object. For example, from Figure 21.1, if the program assigns new data to object D, the program must take three actions:

- 1. Make a copy of Data2 and assign it to D.
- 2. Decrement Data2's ownership count.
- 3. Change the original data.

Those are the essential steps in the copy-on-write method—an object is copied only when its data changes. Figure 21.2 shows the resulting organization among objects. The original Data2's ownership counter indicates that it is now owned by two objects, B and C. The modified Data2 value, labeled Data2.1, is uniquely addressed by object D.

## Figure 21.2
In the copy-on-write method, objects are copied only when their data changes.

![](img/6eab91cc30158075ed10d0cabbac9029_495_1.png)

To program reference counting and the copy-on-write method takes some careful thought. Following are three listings that provide a shell you can use to add these features to your own classes. File cow.h (that’s "cow" for copy-on-write) declares two classes, TData and TContain, that create objects as illustrated in Figures 21.1 and 21.2. Listing 21.1 shows the first class in the cow.h header file.

## LISTING 21.1 COW.H (PARTIAL)

```
#include <string.h>  // Need strcmp(), strcpy(), strlen()

// A class that manages a pointer to data and keeps track
// of the number of owners of this object. This class is
// implemented entirely inline.

class TData {

    friend class TContain;  // Only this class may use TData

private:        // All members are private!

    char *cp;   // Pointer to string
    int owners; // Number of owners of this TData object

    // Parameterized constructor
    //
    TData(const char *cp_arg): cp(0), owners(1)
    {
        if (cp_arg) {
            cp = new char[strlen(cp_arg) + 1];
            strcpy(cp, cp_arg);
        }
    }

    // Destructor
    //
    ~TData()
    {
        delete[] cp;
    }

    // Return pointer to this object as a copy
    // and increment ownership counter
    //
    TData *GetCopy()
    {
        owners++;
        return this;
    }

    // Put new data into object (copy on write)
    //
    TData *PutData(const char *s)
    {
        /*
```

## LISTING 21.1 CONTINUED

```
if this is the only copy
delete old data
insert new data
return this object
else
decrease ownership count
return new object
*/

if (owners <= 1) {
    delete[] cp;
    cp = NULL;
    if (s) {
        cp = new char[strlen(s) + 1];
        strcpy(cp, s);
    }
    return this;
} else {
    owners--;
    return new TData(s);
}

// Delete this copy of a TData object
//
int DeleteCopy()
{
    return owners--;
}

// Return pointer to object data
//
const char *GetString() const
{
    return cp;
}

// Return number of owners
// For testing only; can be deleted
//
int NumberOfOwners()
{
    return owners;
}
};
```

The TData class provides the basis for objects that are copied only when their data changes. Duplicate copies of TData objects are counted by the objects themselves. The class, which is implemented here entirely inline, differs significantly in two ways from most classes in this book:

- TData declares another class as a friend.
- All TData members are private to the class.
