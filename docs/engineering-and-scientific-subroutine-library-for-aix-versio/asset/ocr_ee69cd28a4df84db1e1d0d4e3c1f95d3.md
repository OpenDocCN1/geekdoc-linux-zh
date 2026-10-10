# **IBSRCH, SBSRCH, and DBSRCH**

# # IBSRCH, SBSRCH, and DBSRCH—Binary Search for Elements of a Sequence X in a Sorted Sequence Y

These subroutines perform a binary search for the locations of the elements of sequence *x* in another sequence *y*, where *y* has been sorted into ascending order. The first occurrence of each element is found. When an exact match is not found, the position of the next larger element in *y* is indicated. The locations are returned in the indices array INDX, and, optionally, return codes indicating whether the exact elements were found are returned in array RC.

# *Table 159. Data Types*

| *x*, *y* | Subroutine |
| :--- | :--- |
| Integer | IBSRCH |
| Short-precision real | SBSRCH |
| Long-precision real | DBSRCH |

# ## Syntax

| Fortran | CALL IBSRCH \| SBSRCH \| DBSRCH (*x, incx, n, y, incy, m, idx, rc, iopt*) |
| :--- | :--- |
| C and C++ | *ibsrch* \| *sbsrch* \| *dbsrch* (*x, incx, n, y, incy, m, idx, rc, iopt*); |

**On Entry:**

+   *   **x**
+       is the sequence *x* of length *n*, containing the elements for which sequence *y* is searched.
+       Specified as: a one-dimensional array, containing numbers of the data type indicated in Table 159. It must have at least 1 + (n − 1)|*incx*| elements.

+   *   ***incx***
+       is the stride for sequence *x*.
+       Specified as: a fullword integer. It can have any value.

+   *   ***n***
+       is the number of elements in sequence *x* and arrays INDX and RC.
+       Specified as: a fullword integer; *n* ≥ 0.

+   *   ***y***
+       is the sequence *y* of length *m*, to be searched, where *y* must be sorted into ascending order.

**Note:** Be careful in specifying the stride for sequence *y*. A negative stride reverses the direction of the search, because the order of the sequence elements is reversed in the array.

+       Specified as: a one-dimensional array of (at least) length 1 + (m − 1)|*incy*|, containing numbers of the data type indicated in Table 159.

+   *   ***incy***
+       is the stride for sequence *y*.
+       Specified as: a fullword integer. It can have any value.

+   *   ***m***
+       is the number of elements in sequence *y*. Specified as: a fullword integer; *m* ≥ 0.

+   *   ***indx***
+       See “On Return” on page 888.

+   *   ***rc***
+       See “On Return” on page 888.

+   *   ***iopt***
+       has the following meaning, where: