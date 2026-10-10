# SCSIN2 and DCSIN2—Two-Dimensional Cubic Spline Interpolation

These subroutines compute the interpolation values at a specified set of points, using data defined on a rectangular mesh in the $x$-$y$ plane.

Table 165. *Data Types*

| | $x, y, \textbf{Z}, t, \boldsymbol{u}$, aux, $S$ | Subroutine |
|---|---|---|
| | Short-precision real | SCSIN2 |
| | Long-precision real | DCSIN2 |

# **Syntax**

| Fortran | `CALL SCSIN2 \| DCSIN2` (x, y, z, n1, n2, ldz, t, u, m1, m2, s, lds, aux, naux) |
| C and C++ | scsin2 \| dcsin2 (x, y, z, n1, n2, ldz, t, u, m1, m2, s, lds, aux, naux); |

+   **On Entry:**
+   
+   $x$
+   is the vector $\mathbf{x}$ of length $n1$, containing the $x$-coordinates of the data points that define the spline. The elements of $\mathbf{x}$ must be distinct and sorted into ascending order.
+   
+   Specified as: a one-dimensional array of (at least) length $n1$, containing numbers of the data type indicated in Table 165.
+   
+   $y$
+   is the vector $\mathbf{y}$ of length $n2$, containing the $y$-coordinates of the data points that define the spline. The elements of $\mathbf{y}$ must be distinct and sorted into ascending order.
+   
+   Specified as: a one-dimensional array of (at least) length $n2$, containing numbers of the data type indicated in Table 165.
+   
+   $z$
+   is the matrix $\mathbf{Z}$, containing the data at $(x_i, y_j)$ for $i = 1, n1$ and $j = 1, n2$ that defines the spline.
+   
+   Specified as: an $ldz$ by (at least) $n2$ array, containing numbers of the data type indicated in Table 165.
+   
+   $n1$
+   is the number of elements in vector $\mathbf{x}$ and the number of rows in matrix $\mathbf{Z}$—that is, the number of $x$-coordinates at which the spline is defined.
+   
+   Specified as: a fullword integer; $n1 \geq 0$.
+   
+   $n2$
+   is the number of elements in vector $\mathbf{y}$ and the number of columns in matrix $\mathbf{Z}$—that is, the number of $y$-coordinates at which the spline is defined.
+   
+   Specified as: a fullword integer; $n2 \geq 0$.
+   
+   $ldz$
+   is the leading dimension of the array specified for $z$.
+   
+   Specified as: a fullword integer; $ldz > 0$ and $ldz \geq n1$.
+   
+   $t$
+   is the vector $\mathbf{t}$ of length $m1$, containing the $x$-coordinates at which the spline is evaluated.
+   
+   Specified as: a one-dimensional array of (at least) length $m1$, containing numbers of the data type indicated in Table 165.
+   
+   $u$
+   is the vector $\mathbf{u}$ of length $m2$, containing the $y$-coordinates at which the spline is evaluated.