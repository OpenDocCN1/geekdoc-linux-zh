Using standard algorithms, you can sort, merge, search, copy, and perform other magic on objects in STL containers. The standard algorithms work with all types of data structures, and they simplify common programming tasks. For example, the sort() algorithm can operate on a list or a vector regardless of the type of data the container holds. Also, because standard algorithms are not object-oriented, they carry out their duties equally well in OOP and in conventional applications.

The Standard Template Library (STL) provides every algorithm as a generalized template function that defines the algorithm’s name, a return type or void, and any parameters. Extensive use of inline code keeps algorithms running fast without sacrificing versatility. To use most algorithms, you simply define any required data types and provide one or more iterators that define a range of objects or values on which to operate. Using this information, GNU C++ constructs a function that performs the required task.

> **Tip**
> 
> Remember to compile using at least one level of optimization (for example, -O1) to enable inline function expansion.

# INTRODUCING STANDARD ALGORITHMS

In GNU C++, the algo.h and algobase.h header files define all standard algorithm template functions. To use one or more standard algorithms from these files, include the standard algorithm header using the following directive:

```
#include <algorithm>
```

Don't include algo.h or algobase.h—they might be named something else in another ANSI C++ compiler system, or their declarations might be combined into one file. Always include algorithm as shown here to ensure portability. Also include any other STL headers such as vector, deque, and list, that define the container you want to use. You may use standard algorithms with simple C++ arrays and other structures of your own making; you can even invent your own containers if you want. In most cases, however, you will use a standard container along with a standard algorithm described in this chapter.

The following sections explain how to use most STL algorithms in categories sorted alphabetically. Because of space limitations, in some cases topics are mentioned before they are introduced, so you might need to read this chapter a couple of times to fully understand all the algorithms. Also read Chapter 23, “Using the Standard Template Library (STL),” and Chapter 24, “Building Standard Containers,” for information on using the STL and standard container class templates.