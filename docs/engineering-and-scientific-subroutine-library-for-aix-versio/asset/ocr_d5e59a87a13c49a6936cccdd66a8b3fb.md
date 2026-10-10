# # SRCFT3 and DRCFT3—Real-to-Complex Fourier Transform in Three Dimensions

These subroutines compute the three-dimensional discrete Fourier transform of real data in a three-dimensional array.

**Table 147. Data Types**

| $\chi$\_scale | y | Subroutine |
| :--- | :--- | :--- |
| Short-precision real | Short-precision complex | SRCFT3 |
| Long-precision real | Long-precision complex | DRCFT3 |

**Note:** For each use, only one invocation of this subroutine is necessary. The initialization phase, preparing the working storage, is a relatively small part of the total computation, so it is performed on each invocation.

# ## Syntax

| Fortran | CALL SRCFT3 \| DRCFT3 (x, inc2x, inc3x, y, inc2y, inc3y, n1, n2, n3, isign, scale, aux, naux) |
| :--- | :--- |
| **C and C++** | sref3 \| dref3 (x, inc2x, inc3x, y, inc2y, inc3y, n1, n2, n3, isign, scale, aux, naux); |

# ## On Entry:

**$\chi$** is the array $\chi$, containing the three-dimensional data to be transformed, where each element $\chi_{j1,j2,j3}$, using zero-based indexing, is stored in $X([j1+2(inc2x)+3(inc3x)])$ for $j1 = 0, 1, \ldots, n1-1$, $j2 = 0, 1, \ldots, n2-1$, and $j3 = 0, 1, \ldots, n3-1$. The strides for the elements in the first, second, and third dimensions are assumed to be 1, $inc2x$ ($\geq n1$), and $inc3x$ ($\geq (n2)(inc2x)$), respectively.

Specified as: an array, containing numbers of the data type indicated in Table 147. If the array is dimensioned X(LDA1, LDA2, LDA3), then LDA1 = $inc2x$, (LDA1)(LDA2) = $inc3x$, and LDA3 $\geq n3$. For information on how to set up this array, see "Setting Up Your Data" on page 746. For more details, see "Notes" on page 814.

**$inc2x$** is the stride between the elements in array $\chi$ for the second dimension.

Specified as: a fullword integer; $inc2x \geq n1$.

**$inc3x$** is the stride between the elements in array $\chi$ for the third dimension.

Specified as: a fullword integer; $inc3x \geq (n2)(inc2x)$.

**$y$** See "On Return" on page 813.

**$inc2y$** is the stride between the elements in array $y$ for the second dimension.

Specified as: a fullword integer; $inc2y \geq n1/2+1$.

**$inc3y$** is the stride between the elements in array $y$ for the third dimension.

Specified as: a fullword integer; $inc3y \geq (n2)(inc2y)$.

**$n1$** is the length of the first dimension of the three-dimensional data in the array to be transformed.

Specified as: a fullword integer; $n1 \leq 37748736$ and must be one of the values listed in "Acceptable Lengths for the Transforms" on page 743. For all other values specified less than 37748736, you have the option of having