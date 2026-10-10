# # SRCFT and DRCFT—Real-to-Complex Fourier Transform

These subroutines compute a set of $n$ complex discrete $n$-point Fourier transforms of real data.

**Table 139. Data Types**

| $X$, scale | $Y$ | Subroutine |
| :--- | :--- | :--- |
| Short-precision real | Short-precision complex | SRCFT |
| Long-precision real | Long-precision complex | DRCFT |

> Note: Two invocations of this subroutine are necessary: one to prepare the working storage for the subroutine, and the other to perform the computations.

# ## Syntax

| Fortran | CALL SRCFT (init, x, inc2x, y, inc2y, n, m, isign, scale, aux1, auxx1, aux2, naux2, aux3, naux3)<br>CALL DRCFT (init, x, inc2x, y, inc2y, n, m, isign, scale, aux1, auxx1, aux2, naux2) |
| :--- | :--- |
| C and C++ | srcft (init, x, inc2x, y, inc2y, n, m, isgn, scale, aux1, naux1, aux2, naux2, aux3, naux3);<br>drctf (init, x, inc2x, y, inc2y, n, m, isgn, scale, aux1, naux1, aux2, naux2); |

# ## On Entry:

*init* is a flag, where:

If $init \neq 0$, trigonometric functions and other parameters, depending on arguments other than $X$, are computed and saved in $aux1$. The contents of $X$ and $Y$ are not used or changed.

If $init = 0$, the discrete Fourier transforms of the given sequences are computed. The only arguments that may change after initialization are $X$, $Y$, and $aux2$. All scalar arguments must be the same as when the subroutine was called for initialization with $init \neq 0$.

$X$ is the array $X$, consisting of $n$ sequences of length $n$, which are to be transformed. The sequences are assumed to be stored with stride 1.

*inc2x* is the stride between the first elements of the sequences in array $X$. (If $m = 1$, this argument is ignored.) Specified as: a fullword integer; inc2x $\ge n$.

$Y$ See “On Return” on page 761.

*inc2y* is the stride between the first elements of the sequences in array $Y$. (If $m = 1$, this argument is ignored.) Specified as: a fullword integer; inc2y $\ge (n/2)+1$.

$n$ is the length of each sequence to be transformed.

Specified as: a fullword integer; $n \le 37748736$ and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. For all other values specified less than 37748736, you have the option of having