# **ISMIN and IDMIN—Position of the First or Last Occurrence of the Vector Element Having Minimum Value**

These subprograms find the position *i* of the first or last occurrence of a vector element having the minimum value.

You get the position of the first or last occurrence of an element by specifying positive or negative stride, respectively, for vector *x*. Regardless of the stride, the position *i* is always relative to the location specified in the calling sequence for vector *x* (in argument *x*).

*Table 43. Data Types*

| x | Subprogram |
| :--- | :---: |
| Short-precision real | ISMIN |
| Long-precision real | IDMIN |

# Syntax

| Fortran | ISMIN \| IDMIN (*n*, *x*, *incx*) |
| :--- | :--- |
| **C and C++** | ismin \| idmin (*n*, *x*, *incx*); |

**On Entry:**

*n* is the number of elements in vector *x*. Specified as: a fullword integer; *n* ≥ 0.

*x* is the vector *x* of length *n*. Specified as: a one-dimensional array of (at least) length 1+(n−1)*|incx*|, containing numbers of the data type indicated in Table 43.

*incx* is the stride for vector *x*.

Specified as: a fullword integer. It can have any value.

**On Return:**

*Function value*

is the position *i* of the element in the array, where:

If *incx* ≥ 0, *i* is the position of the first occurrence.

If *incx* < 0, *i* is the position of the last occurrence.

Returned as: a fullword integer; 0 ≤ *i* ≤ *n*.

**Note**
Declare the ISMIN and IDMIN functions in your program as returning a fullword integer value.

**Function**
These subprograms find the first element *x*_{*k*}, where *k* is defined as the smallest index *k*, such that:

*x*_{*k*} = min{*x*_{*j*} for *j* = 1, *n*}

By specifying a positive or negative stride for vector *x*, the first or last occurrence, respectively, is found in the array. The position *i*, returned as the value of the