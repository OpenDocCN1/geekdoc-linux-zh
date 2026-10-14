The first two arguments are iterators that define the range of objects on which to operate (double values in this case). The third argument is the starting value for the accumulation, set to 0.0 here. To keep a running total—summing multiple containers, for example—define a variable of the appropriate type and pass it to accumulate()’s third parameter. By default, accumulate() applies the plus operator (+) to the starting value and all others in the defined range, one after the other. The function returns the resulting value, assigned here to the double variable, sum.

To perform a different type of accumulation, specify a function object as the fourth argument. For example, the following statement multiplies all values in the container:

```
double product = accumulate(
    array.begin(), array.end(), 1.0, multiplies<double>());
```

The multiplies function object is declared in the functional header file. Specify a data type (such as double) to the template and append an empty pair of parentheses to indicate that the program is to call the object as a function—an operation performed by calling operator()() for this function object. Because the operation is a multiplication, the starting value passed to accumulate()’s third parameter is 1.0.

> Note
> Some C++ compilers name the multiplies function template times.

# COPYING ALGORITHMS

+   Algorithms:
+   - copy()
+   - copy_backward()
+   Sample program:
+   - copy-ex.cpp

There are two copy() algorithms. The first, copy(), copies a range of data objects from an input source container to a destination, in a forward direction. The algorithm is declared as follows:

```
OutputIterator copy(
    InputIterator first, InputIterator last,
    OutputIterator result)
```

> Note
> The OutputIterator and InputIterator identifiers are template placeholders, not defined types. The actual types of iterators are defined when you use the function—for example, when operating on a container of double values, the OutputIterator type becomes double*, and the InputIterator is const double*.