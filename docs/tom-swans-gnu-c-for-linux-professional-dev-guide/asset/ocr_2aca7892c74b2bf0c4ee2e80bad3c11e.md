**Note**

Because of the large number of sample programs in this chapter, many of which contain duplicate statements, the following sections do not list the sample programs in full. Of course, all files mentioned in this chapter are on the CD-ROM in the `src/c25` directory. Each section begins with references to the algorithms discussed and to the relevant source file. To compile the sample programs, use the following commands where `name-ex.cpp` is the name of the program’s source code file:

```text
$ g++ name-ex.cpp
$ ./a.out
```

# Accumulation Algorithm

*Algorithm:*

`accumulate()`

*Sample program:*

`accum-ex.cpp`

An accumulation is an arbitrary operation that combines a collection of objects in some specified fashion. For example, a simple accumulation sums a list or an array of integers, or calculates a combined product or factorial. The accumulate algorithm is defined as follows:

```
DataType accumulate(
    InputIterator first, InputIterator last,
    DataType initial {, BinaryFunction } )
```

**Note**

In this and other algorithm definitions, bracketed items such as `BinaryFunction` are optional. I also changed a few identifiers for clarity—replacing `T` with `DataType` for instance.

Two iterators, first and last, define a range of data objects in a container. The initial argument provides a starting value for the type of data objects. This value should be 0 for addition operations, and 1 for multiplication. By default, `accumulate()` sums the specified range of data objects. To perform a different operation, you can optionally specify a binary function object such as `multiplies`.

To demonstrate how to use `accumulate()`, the sample program defines a container with a few floating point values:

```
double data[5] = { 1.2, 3.4, 5.6, 7.8, 9.10 };
vector<double> array(data, data + 5);
```

To sum the values in the array, the program calls `accumulate()` with three arguments:

```
double sum = accumulate(
    array.begin(), array.end(), 0.0);
```