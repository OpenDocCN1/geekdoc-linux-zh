
## Convolutions and Correlations by Fourier Methods

The convolution and correlation subroutines that use the Fourier methods determine a sequence length $n$, whose Fourier transform is computed using ESSL subroutines. In the simple case where $iy0 = 0$ for convolution or $iy0 = -nh+1$ for correlation, $n$ is chosen as a value greater than or equal to the following, which is also acceptable to the Fourier transform subroutines:

- $nt = min(nh+nx-1, ny)$ for convolution and correlation
- $nt = min(nx+nx-1, ny)$ for autocorrelation

which is also acceptable to the Fourier subroutines.

## Related Computation Considerations

This section describes some key points about using the related-computation subroutines.

## Accuracy Considerations

- Many of the subroutines performing short-precision computations provide increased accuracy by accumulating results in long precision. This is noted in the functional description for each subroutine.
- There are ESSL-specific rules that apply to the results of computations on the workstation processors using the ANSI/IEEE standards. For details, see “What Data Type Standards Are Used by ESSL, and What Exceptions Should You Know About?” on page 44.

## Fourier Transform Subroutines

This section contains the Fourier transform subroutine descriptions.

## SCFT and DCFT—Complex Fourier Transform

These subroutines compute a set of $m$ complex discrete $n$-point Fourier transforms of complex data.

Table 138. Data Types

| X, Y | scale | Subroutine |
| :--- | :--- | :--- |
| Short-precision complex | Short-precision real | SCFT |
| Long-precision complex | Long-precision real | DCFT |

Note: Two invocations of this subroutine are necessary: one to prepare the working storage for the subroutine, and the other to perform the computations.

### Syntax

| | |
| :--- | :--- |
| Fortran | CALL SCFT \| DCFT (init, x, inc1x, inc2x, y, inc1y, inc2y, n, m, isign, scale, aux1, naux1, aux2, naux2) |
| C and C++ | scft \| dcft (init, x, inc1x, inc2x, y, inc1y, inc2y, n, m, isign, scale, aux1, naux1, aux2, naux2); |

### On Entry:

- **init**
  - is a flag, where:
  - If $init \neq 0$, trigonometric functions and other parameters, depending on arguments other than $x$, are computed and saved in **aux1**. The contents of $x$ and $y$ are not used or changed.
  - If $init = 0$, the discrete Fourier transforms of the given sequences are computed. The only arguments that may change after initialization are $x, y$, and **aux2**. All scalar arguments must be the same as when the subroutine was called for initialization with $init \neq 0$.
  - Specified as: a fullword integer. It can have any value.

- **x**
  - is the array $\mathbf{X}$, consisting of $m$ sequences of length $n$.
  - Specified as: an array of (at least) length $1 + (n-1)inc1x + (n-1)inc2x$, containing numbers of the data type indicated in Table 138.

- **inc1x**
  - is the stride between the elements within each sequence in array **X**.
  - Specified as: a fullword integer; $inc1x > 0$.

- **inc2x**
  - is the stride between the first elements of the sequences in array **X**. (If $m = 1$, this argument is ignored.) Specified as: a fullword integer; $inc2x > 0$.

- **y**
  - See “On Return” on page 752.

- **inc1y**
  - is the stride between the elements within each sequence in array **Y**.
  - Specified as: a fullword integer; $inc1y > 0$.

- **inc2y**
  - is the stride between the first elements of each sequence in array **Y**. (If $m = 1$, this argument is ignored.) Specified as: a fullword integer; $inc2y > 0$.

- **n**
  - is the length of each sequence to be transformed.
  - Specified as: a fullword integer; $n \leqslant 37748736$ and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. all other values specified less than 37748736, you have the option of having the next larger acceptable value returned in this argument, as well as in the optionally-recoverable error 2030. For details, see “Providing a Correct Transform Length to ESSL” on page 38.

- **m**
  - is the number of sequences to be transformed.
  - Specified as: a fullword integer; $m > 0$.

- **isign**
  - controls the direction of the transform, determining the sign $lsign$ of the exponent of $W_n$, where:
  - If $isign$ = positive value, $lsign$ = + (transforming time to frequency).
  - If $isign$ = negative value, $lsign$ = – (transforming frequency to time).
  - Specified as: a fullword integer; $isign > 0$ or $isign < 0$.

- **scale**
  - is the scaling constant $scale$. See “Function” on page 754 for its usage.
  - Specified as: a number of the data type indicated in Table 138 on page 751, where $scale > 0.0$ or $scale < 0.0$

- **aux1**
  - is the working storage for this subroutine, where:
  - If $init \neq 0$, the working storage is computed.
  - If $init = 0$, the working storage is used in the computation of the Fourier transforms.
  - Specified as: an area of storage, containing $naux1$ long-precision real numbers.

- **naux1**
  - is the number of doublewords in the working storage specified in $aux1$.
  - Specified as: a fullword integer; $naux1 > 7$ and $naux1 \geq$ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For values between 7 and the minimum value, you have the option of having the minimum value returned in this argument. For details, see “Using Auxiliary Storage in ESSL” on page 32.

- **aux2**
  - has the following meaning:
  - If $naux2 = 0$ and error 2015 is unrecoverable, $aux2$ is ignored.
  - Otherwise, it is the working storage used by this subroutine, which is available for use by the calling program between calls to this subroutine.
  - Specified as: an area of storage, containing $naux2$ long-precision real numbers. On output, the contents are overwritten.

- **naux2**
  - is the number of doublewords in the working storage specified in $aux2$.
  - Specified as: a fullword integer, where:
  - If $naux2 = 0$ and error 2015 is unrecoverable, SCFT and DCFT dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.
  - Otherwise, $naux2 \geq$ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For all other values specified less than the minimum value, you have the option of having the minimum value returned in this argument. For details, see “Using Auxiliary Storage in ESSL” on page 32.

### On Return:

- **y**
  - has the following meaning, where:
  - If $init \neq 0$, this argument is not used, and its contents remain unchanged.
  - If $init = 0$, this is array $Y$, consisting of the results of the $m$ discrete Fourier transforms, each of length $n$.
  - Returned as: an array of (at least) length $1+(n-1)incIy+(m-1)inc2y$, containing numbers of the data type indicated in Table 138 on page 751. This array must be aligned on a doubleword boundary.
  - $aux1$ is the working storage for this subroutine, where:
  - If $init \neq 0$, it contains information ready to be passed in a subsequent invocation of this subroutine.
  - If $init = 0$, its contents are unchanged.
  - Returned as: the contents are not relevant.

### Notes

1. $aux1$ should not be used by the calling program between calls to this subroutine with $init \neq 0$ and $init = 0$. However, it can be reused after intervening calls to this subroutine with different arguments.
2. When using the ESSL SMP library, for optimal performance, the number of threads specified should be the same for $init \neq 0$ and $init = 0$.
3. For optimal performance, the preferred value for $incIx$ and $incIy$ is 1. This implies that the sequences are stored with stride 1. The preferred value for $inc2x$ and $inc2y$ is $n$. This implies that sequences are stored one after another without any gap.

It is possible to specify sequences in the transposed form—that is, as rows of a two-dimensional array. In this case, $inc2x$ (or $inc2y$) = 1 and $incIx$ (or $incIy$) is equal to the leading dimension of the array. One can specify either input, output, or both in the transposed form by specifying appropriate values for the stride parameters. For selecting optimal values of $incIx$ and $incIy$ for _CFT, you should use “STRIDE—Determine the Stride Value for Optimal Performance in Specified Fourier Transform Subroutines” on page 963. Example 1 in the STRIDE subroutine description explains how it is used for _CFT.

If you specify the same array for X and Y, then $incIx$ and $incIy$ must be equal, and $inc2x$ and $inc2y$ must be equal. In this case, output overwrites input. If $m = 1$, the $inc2x$ and $inc2y$ values are not used by the subroutine. If you specify different arrays for X and Y, they must have no common elements; otherwise, results are unpredictable. See “Concepts” on page 55.

### Processor-Independent Formulas for SCFT for NAUX1 and NAUX2

**NAUX1 Formulas:**
If $n \leq 8192$, use $naux1 = 20000$.
If $n > 8192$, use $naux1 = 20000+1.14n$.

**NAUX2 Formulas:**
If $n \leq 8192$, use $naux2 = 20000$.
If $n > 8192$, use $naux2 = 20000+1.14n$.
For the transposed case, where $inc2x = 1$ or $inc2y = 1$, and where $n \geq 252$, add the following to the above storage requirements:
$(n+256)(\min(64, m))$.
