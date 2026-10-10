# SCOSF and DCOSF—Cosine Transform

These subroutines compute a set of *n* real even discrete *n*-point Fourier transforms of cosine sequences of real even data.

# Table 141. Data Types

| X, Y, scale | Subroutine |
| :--- | :--- |
| Short-precision real | SCOSF |
| Long-precision real | DCOSF |

**Note:** Two invocations of this subroutine are necessary: one to prepare the working storage for the subroutine, and the other to perform the computations.

# Syntax

| Fortran | CALL.SCOSF \| DCOSF (*init, x, inc1x, inc2x, y, inc1y, inc2y, n, m, scale, aux1, naux1, aux2, naux2*) |
| :--- | :--- |
| C and C++ | scosf \| dcosf (*init, x, inc1x, inc2x, y, inc1y, inc2y, n, m, scale, aux1, naux1, aux2, naux2*); |

# On Entry:

+   *init*
+   is a flag, where:
+   
+   If *init* ≠ 0, trigonometric functions and other parameters, depending on arguments other than *x*, are computed and saved in *aux1*. The contents of *x* and *y* are not used or changed.
+   
+   If *init* = 0, the discrete Fourier transforms of the given sequences are computed. The only arguments that may change after initialization are *x*, *y*, and *aux2*. All scalar arguments must be the same as when the subroutine was called for initialization with *init* ≠ 0.

+   *x*
+   is the array X, consisting of *m* sequences of length *n*/2+1.
+   
+   Specified as: an array of (at least) length 1+(n/2)*inc1x*+(n−1)*inc2x*, containing numbers of the data type indicated in Table 141.

+   *inc1x*
+   is the stride between the elements within each sequence in array X.
+   
+   Specified as: a fullword integer; *inc1x* > 0.

+   *inc2x*
+   is the stride between the first elements of the sequences in array X. (If *m* = 1, this argument is ignored.) Specified as: a fullword integer; *inc2x* > 0.

+   *y*
+   See “On Return” on page 774.

+   *inc1y*
+   is the stride between the elements within each sequence in array Y.
+   
+   Specified as: a fullword integer; *inc1y* > 0.

+   *inc2y*
+   is the stride between the first elements of the sequences in array Y. (If *m* = 1, this argument is ignored.) Specified as: a fullword integer; *inc2y* > 0.

+   *n*
+   is the transform length. However, due to symmetry, only the first *n*/2+1 values are given in the input and output.