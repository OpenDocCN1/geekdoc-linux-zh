# SNDOT and DNDOT—Compute Special Dot Products N Times

These subprograms compute one of the following special dot products *n* times:

+   * $s_i \leftarrow x_i^* \cdot y_i$	Store positive dot product
+   * $s_i \leftarrow -x_i^* \cdot y_i$	Store negative dot product
+   * $s_i \leftarrow s_i + x_i^* \cdot y_i$	Accumulate positive dot product
+   * $s_i \leftarrow s_i - x_i^* \cdot y_i$	Accumulate negative dot product
+   * \quad for $i = 1, n$ 

where each $s_i$ is an element in vector $s$, and each $x_i$ and $y_i$ are vectors contained in vectors (or matrices) $x$ and $y$, respectively.

Table 49. Data Types

| $s$, $x$, $y$ | Subprogram |
| Short-precision real | SNDOT |
| Long-precision real | DNDOT |

# Syntax

| Fortran | CALL SNDOT \| DNDOT (*n*, *m*, *s*, *isu*, *x*, *incx*, *y*, *incy*, *isu*) |
| C and C++ | sndot \| dndot (*n*, *m*, *s*, *isu*, *x*, *incx*, *y*, *incy*, *isu*); |

# On Entry:

*n*	 is the number of dot product computations to be performed and the number of elements in the vector *n*.
Specified as: a fullword integer; *n* ≥ 0.

*m*	 is the number of elements in vectors $x_i$ and $y_i$ for each dot product computation.
Specified as: a fullword integer; *m* ≥ 0.

*s*	 is the vector *s*, containing the *n* scalar values $s_i$, where: If *isu* = 1 or 2, *s* is not used in the computation (no input value specified.)
If *isu* = 3 or 4, $s_i$ is used in the computation (input value specified.)
Specified as: a one-dimensional array of (at least) length $1+(n-1)\, \mathrm{incs}$, containing numbers of the data type indicated in Table 49.

*incs*	 is the stride for vector *s*.
Specified as: a fullword integer; *incs* > 0 or *incs* < 0.

*isu*	 indicates the type of computation to perform, depending on the value specified:

	If *isu* = 1, 	 $s_i \leftarrow x_i^* \cdot y_i$
	If *isu* = 2, 	 $s_i \leftarrow -x_i^* \cdot y_i$
	If *isu* = 3, 	 $s_i \leftarrow s_i + x_i^* \cdot y_i$
	If *isu* = 4, 	 $s_i \leftarrow s_i - x_i^* \cdot y_i$
	 where $i = 1, n$

Specified as: a fullword integer. Its value must be 1, 2, 3, or 4.

*x*	 is the vector (or matrix) *x*, containing the $x_i$ vectors of length *m*, used in the