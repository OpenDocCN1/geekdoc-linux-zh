
As a template, the find() algorithm refers to no specific type of data but uses placeholders to represent actual data types provided when the template is used. One of these placeholders is named InputIterator. This type of iterator could be any type of object that has certain capabilities, such as being comparable using the != operator and being incremented with ++. The other type of placeholder is named T. It represents the type of data in the container.

> Tip
> Don't go hunting for InputIterator's type declaration in the STL's source files. This is just an arbitrary name, not a defined type, that becomes a real type when the find() template function is instantiated.

The find() algorithm declares three parameters. First are two iterators of type InputIterator, named first and last. The third parameter is a constant reference to an object, named value here, of type T. The find() algorithm's statements show how, using template placeholders instead of real data types, a completely general search function is written with absolutely no knowledge of the type of data searched. Examine the algorithm's while statement closely:

```
while (first != last && *first != value) ++first;
```

The statement executes while the first iterator is not equal to the last, and while the value addressed by first does not equal the search argument. As long as this condition is false, the loop increments first. The algorithm is completely general, and it can search any type of container such as a list, a vector, or an array.

After the search, first either points to the object equal to the search argument, or first equals last, in which case the search has failed. The find() algorithm simply returns this value.

> Note
> In the preceding find() algorithm, notice that if the search argument is not located, incrementing first must eventually cause it to equal last. If first and last refer to values in different containers, this algorithm potentially never ends. Although the compiler does not prevent this situation, with reasonable care, this shouldn't cause any problems.

## OUTPUT ITERATORS

An output iterator is write-only by default and is typically used to copy data from one location to another. Because output iterators cannot be used to read objects, you never use them in search and other types of algorithms. For example, the copy() algorithm can transfer objects from one data structure to another using an output iterator to specify the destination. However, that iterator cannot be used to read the copied values. For that, another input iterator (or descendant) is needed.

To demonstrate how to use an output iterator, Listing 23.3, outiter.cpp, uses the copy() algorithm to transfer an array of double values to a vector container. You might use a similar technique to upgrade a conventional C program that uses arrays to one that uses STL container classes. (The demonstrated technique is also useful for initializing containers for test programs such as those in this and the next two chapters.)

### LISTING 23.3 OUTITER.CPP

```cpp
#include <iostream.h>
#include <algorithm>  // Need copy()
#include <vector>     // Need vector

using namespace std;

double darray[10] =
    {1.0, 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7, 1.8, 1.9};

vector<double> vdouble(10);

int main()
{
    vector<double>::iterator outputIterator = vdouble.begin();
    copy(darray, darray + 10, outputIterator);
    while (outputIterator != vdouble.end()) {
        cout << *outputIterator << endl;
        outputIterator++;
    }
    return 0;
}
```

Compile and run the program, which uses the copy() algorithm to display the resulting vector of double values:

```text
$ g++ outiter.cpp
$ ./a.out
1
1.1
...
1.9
```

The program defines a common array of 10 double values, initialized to 1.0, 1.1, ..., 1.9. It also defines a vector<double> container large enough to hold 10 values. The first statement in main() declares and initializes an iterator named outputIterator for the vector. So that it points to the container's first object, this statement assigns to outputIterator the result of the begin() function for the container vdouble. Passing the iterator to the copy() algorithm transfers the values from the common array to the vector container:

```
copy(darray, darray + 10, outputIterator);
```

The first two arguments define the range of source values to copy. In this case, the iterators are pointers to the global darray. The third argument is an output iterator that defines the beginning of the destination to which objects are to be transferred. You might wonder how this statement "knows" what types of objects are being copied, but this information is implicit in the types of iterators involved. A pointer such as darray and a pointer expression such as darray + 10 are not simply address values—they are typed pointers, in this case, to values of type double. Similarly, outputIterator "knows" the type of container to which it belongs.
