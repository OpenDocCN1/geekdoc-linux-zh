# SGEMV, DGEMV, CGEMV, ZGEMV, SGEMX, DGEMX, SGEMTX, and DGEMTX

Specified as: a one-dimensional array, containing numbers of the data type indicated in *Table 66 on page 287*, where:

+   For SGEMV, DGEMV, CGEMV, and ZGEMV:
+   
+   - If *transa* = 'N', it must have at least $1 + (n-1)|incx|$ elements.
+   - If *transa* = 'T' or 'C', it must have at least $1 + (m-1)|incx|$ elements.

For SGEMX and DGEMX, it must have at least $1 + (n-1)|incx|$ elements.

For SGEMTX and DGEMTX, it must have at least $1 + (m-1)|incx|$ elements.

+   *incx*
+   
+   is the stride for vector *x*.

Specified as: a fullword integer; It can have any value.

+   *beta*
+   
+   is the scaling constant *β*.

Specified as: a number of the data type indicated in *Table 66 on page 287*.

+   *y*
+   
+   is the vector *y*, where:

+   For SGEMV, DGEMV, CGEMV, and ZGEMV:
+   
+   - If *transa* = 'N', it has length *m*.
+   - If *transa* = 'T' or 'C', it has length *n*.

For SGEMX and DGEMX, it has length *m*.

For SGEMTX and DGEMTX, it has length *n*.

Specified as: a one-dimensional array, containing numbers of the data type indicated in *Table 66 on page 287*, where:

+   For SGEMV, DGEMV, CGEMV, and ZGEMV:
+   
+   - If *transa* = 'N', it must have at least $1 + (n-1)|incy|$ elements.
+   - If *transa* = 'T' or 'C', it must have at least $1 + (n-1)|incy|$ elements.

For SGEMX and DGEMX, it must have at least $1 + (m-1)|incy|$ elements.

For SGEMTX and DGEMTX, it must have at least $1 + (n-1)|incy|$ elements.

+   *incy*
+   
+   is the stride for vector *y*.

Specified as: a fullword integer; *incy* > 0 or *incy* < 0.

# On Return:

+   *y*
+   
+   is the vector *y*, containing the result of the computation, where:

+   For SGEMV, DGEMV, CGEMV, and ZGEMV:
+   
+   - If *transa* = 'N', it has length *m*.
+   - If *transa* = 'T' or 'C', it has length *n*.

For SGEMX and DGEMX, it has length *m*.

For SGEMTX and DGEMTX, it has length *n*.

Returned as: a one-dimensional array, containing numbers of the data type indicated in *Table 66 on page 287*.