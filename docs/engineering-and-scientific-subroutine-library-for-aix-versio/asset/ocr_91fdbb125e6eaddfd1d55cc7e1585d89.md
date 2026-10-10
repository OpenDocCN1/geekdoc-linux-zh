# SIZC and DIZC—1-th Zero Crossing

These subroutines find the position of the *i*-th zero crossing in vector *x*. This is the *i*-th transition between positive and negative or negative and positive, where 0 is considered a positive value. It returns the position of the element in vector *x* where the *i*-th zero crossing is detected. The direction of the scan is either from the first element to the last or from the last element to the first, depending on the value you specify for the scan direction argument.

Table 151. *Data Types*
| *x* | Subroutine |
| :--- | :--- |
| Short-precision real | SIZC |
| Long-precision real | DIZC |

# Syntax

| Fortran | CALL SIZC \| DIZC (*x*, *idrx*, *n*, *i*, *ky*) |
| :--- | :--- |
| C and C++ | *sizc* \| *dizc* (*x*, *idrx*, *n*, *i*, *ky*); |

# On Entry:

*x* is the target vector **x** of length *n*. Specified as: a one-dimensional array of (at least) length *n*, containing numbers of the data type indicated in Table 151.

*idrx* indicates the scan direction. If it is positive or 0, *x* is scanned from the first element to the last (1, *n*). If it is negative, *x* is scanned from the last element to the first (*n*, 1). Specified as: a fullword integer. It can have any value.

*n* is the number of elements in vector *x*. Specified as: a fullword integer; *n* > 1.

*i* is the number of the zero crossing to be identified. Specified as: a fullword integer; *i* > 0.

*ky* See "On Return."

# On Return:

*ky* is the integer vector **ky** of length 2, containing elements *ky*$_{1}$ and *ky*$_{2}$, where: If the *i*-th zero crossing is found:

*   *ky*$_{1}$ = *j*, where *j* is the position of the element *x*_j at the point that the *i*-th zero crossing is found. The position is always relative to the beginning of the vector regardless of the scan direction.
*   *ky*$_{2}$ = *i*

If the *i*-th zero crossing is not found:

*   *ky*$_{1}$ = 0
*   *ky*$_{2}$ = the total number of zero crossings encountered in the scan. Returned as: an array of (at least) length 2, containing fullword integers.