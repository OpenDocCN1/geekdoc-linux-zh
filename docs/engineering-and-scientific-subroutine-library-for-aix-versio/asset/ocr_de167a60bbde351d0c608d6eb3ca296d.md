# # SRCFT2 and DRCFT2—Real-to-Complex Fourier Transform in Two Dimensions

These subroutines compute the two-dimensional discrete Fourier transform of real data in a two-dimensional array.

| Table 144. Data Types|
|---|
| $x$, scale | Y | Subroutine |
| Short-precision real | Short-precision complex | SRCFT2 |
| Long-precision real | Long-precision complex | DRCFT2 |

**Note:** Two invocations of this subroutine are necessary: one to prepare the working storage for the subroutine, and the other to perform the computations.

# ## Syntax

| Fortran | CALL SRCFT2 (init, x, inc2x, y, inc2y, n1, n2, isign, scale, aux1, auxx1, aux2, naux2, aux3, naux3)
CALL DRCFT2 (init, x, inc2x, y, inc2y, n1, n2, isign, scale, aux1, naux1, aux2, naux2) |
|---|
| C and C++ | srcf2 (init, x, inc2x, y, inc2y, n1, n2, isign, scale, aux1, naux1, aux2, naux2, aux3, naux3);
drcf2 (init, x, inc2x, y, inc2y, n1, n2, isign, scale, aux1, naux1, aux2, naux2); |

# ## On Entry:

init is a flag, where:

+      - If init \u2260 0, trigonometric functions and other parameters, depending on arguments other than x, are computed and saved in aux1. The contents of x and y are not used or changed.
+      - If init = 0, the discrete Fourier transform of the given array is computed.
+   The only arguments that may change after initialization are x, y, and aux2. All scalar arguments must be the same as when the subroutine was called for initialization with init \u2260 0.
+      - Specified as: a fullword integer. It can have any value.

x is the array X, containing n1 rows and n2 columns of data to be transformed. The data in each column is stored with stride 1. Specified as: an inc2x by (at least) n2 array, containing numbers of the data type indicated in Table 144. See “Notes” on page 795 for more details.

inc2x is the leading dimension (stride between columns) of array X. Specified as: a fullword integer; inc2x \u2265 n1.

y See “On Return” on page 795.

inc2y is the leading dimension (stride between columns) of array Y. Specified as: a fullword integer; inc2y \u2265 ((n1)/2)+1.

n1 is the number of rows of data—that is, the length of the columns in array X involved in the computation. The length of the columns in array Y are (n1)/2+1.
Specified as: a fullword integer; n1 \u2264 37748736 and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. For all other values specified less than 37748736, you have the option of having