
## LISTING 23.1 CONTINUED

```cpp
iarray[20] = 50;
int* ip = find(iarray, iarray + SIZE, 50);
if (ip == iarray + SIZE)
    cout << "50 not found in array" << endl;
else
    cout << *ip << " found in array" << endl;
return 0;
}
```

After including the headers for I/O streams and STL algorithms (notice that algorithm lacks the usual .h suffix), the sample program tells the compiler to use the std namespace. This is optional, and you may delete this line because name conflicts are unlikely in such a small program.

To provide a data structure, the program defines a global array of integers using constant SIZE. Because it's a global variable, the array is automatically initialized to all zero values at runtime. The following statement uses the STL find() algorithm to search for the value 50, inserted at index 20:

```cpp
iarray[20] = 50;
int* ip = find(iarray, iarray + SIZE, 50);
```

To find(), the program passes three arguments of values typical in many STL algorithms. The first two arguments are iterators that define the range of values to search. Because C and C++ arrays are equivalent to pointers, the expression iarray points to the first value in the array. Likewise, the second argument, iarray + SIZE, equals the past-the-end value—in this case, one element beyond the last object in the array. The third argument is the value to locate, 50 in this example. The find() algorithm returns an iterator of the same type as its first two arguments, in this case an integer pointer assigned in the test program to ip.

### Tip

> Keep in mind that the STL uses templates. As such, STL algorithms automatically mold themselves according to the types of data they use.

To determine whether find() is successful, the sample program tests ip against the past-the-end value using the following statement: `if (ip == iarray + SIZE) ...`

If the expression is true, then the iterator equals the past-the-end value. Because that value addresses no valid object, this means that the search argument is not in the specified range. But if ip does not equal the past-the-end value, then it addresses a valid object, and it is safe to dereference the pointer using the expression *ip as shown in the output statement: `cout << *ip << " found in array" << endl;`

Remember always that it is not correct to test whether an algorithm's returned iterator equals NULL. Do not use code such as this:

```cpp
int* ip = find(iarray, iarray + SIZE, 50);
if (ip != NULL) ... // ??? incorrect
```

When using STL algorithms, it is necessary only to test whether `ip` equals the past-the-end value, whatever that happens to be for a particular container. Although in this case a C++ pointer, its use must conform to the rules for STL iterators. Other simple listings in this and the next two chapters show concrete examples that illustrate the proper ways to use many different types of iterators.

## CONTAINER ITERATORS

Although, as the preceding section demonstrates, C++ pointers are iterators, it is more common to use iterators exported by a container class. These types of iterators are used in exactly the same way as in `iterdemo.cpp`, but instead of declaring iterators as pointer variables, you can call a container function to obtain an iterator object for use with algorithms such as `find()`. Two typical container functions are `begin()` and `end()`. They represent the full range of objects in most types of containers. Some containers also provide reverse iterators by way of functions `rbegin()` and `rend()` for specifying a range of objects in reverse order.

To demonstrate container iterators, Listing 23.2, vectdemo.cpp, creates a `vector`—the STL's equivalent of a C++ array—and uses an iterator to search for a value in the container. The program is the STL equivalent of the conventional C++ iterdemo.cpp program in the preceding section.

```cpp
#include <iostream.h>
#include <algorithm>
#include <vector>

using namespace std;

vector<int> intVector(100);

void main()
{
    intVector[20] = 50;
    vector<int>::iterator intIter =
        find(intVector.begin(), intVector.end(), 50);
    if (intIter != intVector.end())
        cout << "Vector contains value " << intIter << endl;
    else
        cout << "Vector does not contain 50" << endl;
}
```

The program defines a vector of 100 int values using the standard vector container class template. This statement instantiates the vector template for data elements of type int:

`vector<int> intVector(100);`

The statement also calls the vector class’s constructor to reserve space for 100 objects of the indicated type. (Chapter 24, “Building Standard Containers,” explains in detail methods for constructing container objects.)
