searching algorithms use random access iterators, which also have the capability of being compared using relational operators.

The random_shuffle() algorithm demonstrates random access iterators. The algorithm specifies two for these iterators that define a range of values in a sequence to be shuffled—to prepare test data for a program, for instance, or as part of an encryption method. The random_shuffle() algorithm is declared as follows:

```
template <class RandomAccessIterator>
void random_shuffle (RandomAccessIterator first,
                    RandomAccessIterator last);
```

Using the vdouble vector from outiter.cpp (refer to Listing 23.3), the following statement scrambles all values in the container:

```
random_shuffle(vdouble.begin(), vdouble.end());
```

# ITERATOR TECHNIQUES

Learning to use iterators along with STL containers and algorithms requires learning a few new techniques described in the following sections.

# IOSTREAMS AND ITERATORS

Many of this book's sample programs use I/O stream statements to read and write values. For example, the following statements prompt for, read, and display a value entered by the program's user:

```
int value;
cout << "Enter value: ";
cin >> value;
cout << "You entered " << value << endl;
```

With iterators, there's another way to use streams and standard algorithms. The key to understanding the method, which can help you write functions adaptable to different types of objects, is that an input or output stream can be accessed using iterators as though the stream were a container. In this way, any algorithm that can accept an iterator argument (most do) can work with streams in the same way as they do with other data structures. Listing 23.4, outstrm.cpp, demonstrates the technique by using an output stream iterator and the copy() algorithm to display a container's objects.

# LISTING 23.4 OUTSTRM.CPP

```
#include <iostream.h>
#include <stdlib.h>    // Need random(), srandom()
#include <time.h>      // Need time()
#include <algorithm>   // Need sort(), copy()
#include <vector>      // Need vector
using namespace std;
```