deleting a NULL pointer does no harm. It's important to set p to NULL in case copy.p is NULL, in which case both objects address no data. This step is also frequently forgotten. Finally, if the copy object's p pointer is not NULL, the function performs whatever action is necessary to copy the data addressed by copy.p to the target object's p pointer. Again, as with the copy constructor, both objects now address unique memory allocations, avoiding the problems caused by duplicated pointers.

# CALLING operator=() FROM A COPY CONSTRUCTOR

You can usually avoid wasteful duplications in a copy constructor and overloaded operator=() function by combining their programming. The technique, however, might seem magical until you understand how it works. Inside the copy constructor, instead of statements that copy data, use code such as the following:

```
TAnyClass::TAnyClass(const TAnyClass &copy):
    p(NULL)
{
    *this = copy;  // !!!
}
```

As before, the constructor carries out its initialization responsibility of setting p to NULL. After that, the single assignment statement copies the copy parameter to *this. Because this points to the object being constructed, the statement calls the class's overloaded operator=() function to carry out the actual copying.

> Tip
> Be sure that the copy constructor initializes all class data members before executing the assignment statement shown here.

# REFERENCE COUNT OWNERSHIP

The preceding methods have the distinct disadvantage of leading to multiple copies of the same data in memory. For example, if TData addresses a string using a pointer, copying one TData object to another results in two identical strings in memory. Although we have prevented segmentation memory errors by not duplicating pointers, the result is highly inefficient. In cases where the program stores large strings, database records, and buffers, needlessly copying those objects might use up available memory. Also, if two objects address duplicate copies of the same data, if that data needs to be changed, how can the other object know to make the same change to its data?

One answer to these dilemmas is to design a class that keeps track of how many owners it has. This is called reference counting. Many programmers attempt to write this code by creating a class that somehow keeps track of duplicate objects. But the object-oriented approach attacks the problem from the other side of the fence—it makes the data object itself responsible for counting how many other objects own it.