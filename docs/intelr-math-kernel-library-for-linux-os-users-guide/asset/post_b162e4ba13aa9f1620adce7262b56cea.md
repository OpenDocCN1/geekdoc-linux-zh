
# Calling BLAS Functions that Return the Complex Values in C/C++ Code

You must be careful when handling a call from C to a BLAS function that returns complex values. The problem arises because BLAS comprises Fortran functions, and complex values they return are handled quite differently for C and Fortran. However, in addition to normal function calls, Fortran enables calling functions as though they were subroutines, which provides a mechanism for returning the complex value correctly when the function is called from C program. When a Fortran function is called as a subroutine, the return value is the first parameter in the calling sequence. This feature can be used by the C programmer.

The following example shows how this works.

Normal Fortran function call:
`result = cdotc( n, x, l, y, 1 )`

A call to the function as a subroutine:
`call cdotc( result, n, x, l, y, 1, )`

A call to the function from C (notice that the parameter gets exposed):
`cdotc(&result, &n, &one, y, &one )`

![](img/78e923baedeba397a89d376927830122_79_0.png)

> NOTE. Intel MKL has both upper-case and lower-case entry points in the Fortran-style (case-insensitive) BLAS, with or without the trailing underscore. so, all these names are equivalent and acceptable: cdotc, cdotc_, cdotc_

The above example shows one of the ways to call level 1 BLAS functions that return complex values from your C and C++ applications. An easier way is to use the CBLAS interface. For instance, you can call the same function using the CBLAS interface as:

```c
cblas_cdotu( n, x, l, y, l, &result )
```

![](img/78e923baedeba397a89d376927830122_79_1.png)

> NOTE. The complex value comes last as the argument list in this case.

The following examples show use of the Fortran-style BLAS interface from C and C++, as well as the CBLAS (C language) interface.

The example below illustrates a call from a C program to the complex BLAS Level 1 function zdotc(). This function computes the dot product of two double-precision vectors.

In this example, the complex dot product is returned in the structure c.

# Example 7-1 Calling a Complex BLAS 1 Function from C

```cpp
#include "mkl.h"

#define N 5
void main()
{
    MKL_int n = N, inc = 1, incb = 1, i;
    MKL_Complex16 a[N], b[N], c;
    for( i = 0; i < n; i++){
        a[i].re = (double)i; a[i].im = (double)i * 2.0;
        b[i].re = (double)(n - i); b[i].im = (double)i * 2.0;
    }

    zdotc(&c, &n, a, &inca, b, &incb);
    printf("The complex dot product is: %6.2f, %6.2f\n", c.re, c.im);
}
```

```cpp
#include <complex>
#include <iostream>
#define MKL_Complex16 std::complex<double>
#include "mkl.h"

#define N 5

int main()
{
    int n, incr = 1, incb = i;
    std::complex<double> a[N], b[N], c;
    n = N;
    for(i = 0; i < n; i++) {
        a[i] = std::complex<double>(i,i*2.0);
        b[i] = std::complex<double>(n-i,i*2.0);
    }
    zdotc(&c, &n, a, &incr, b, &incb);
    std::cout << "The complex dot product is: " << c << std::endl;
    return 0;
}
```

# Language-specific Usage Options 7

The example below uses CBLAS:

# Example 7-3 Using CBLAS Interface Instead of Calling BLAS Directly from C

# Support for Boost uBLAS Matrix-matrix Multiplication

If you are used to uBLAS, you can perform uBLAS matrix-matrix multiplication in C++ using Intel MKL substitution of Boost uBLAS functions. uBLAS pertains to the Boost C++ open-source libraries and provides BLAS functionality for dense, packed, and sparse matrices.

# 7 Intel® Math Kernel Library User's Guide

The library uses an expression template technique for passing expressions as function arguments, which enables evaluating vector and matrix expressions in one pass without temporary matrices. uBLAS provides two modes:

- Debug (safe) mode, default. 
  Type and conformance checking is performed.

- Release (fast) mode.
  Enabled by the NDEBUG preprocessor symbol.

The documentation for the Boost uBLAS is available at www.boost.org/.

Intel MKL provides overloaded prod() functions for substituting uBLAS dense-matrix multiplication with the Intel MKL gem calls. Though these breaks uBLAS dense-matrix multiplication with the Intel MKL gem calls, the advantage can be considerable for matrix sizes that are not small. To use Intel MKL, the following:

- Add the appropriate header to your code.
- Link with the libraries.
- Use the functions as described in the documentation.

