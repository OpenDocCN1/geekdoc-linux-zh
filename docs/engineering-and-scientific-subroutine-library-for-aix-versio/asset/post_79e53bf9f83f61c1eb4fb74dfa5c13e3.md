
## SRCFT3 and DRCFT3—Real-to-Complex Fourier Transform in Three Dimensions

These subroutines compute the three-dimensional discrete Fourier transform of real data in a three-dimensional array.

**Table 147. Data Types**

| $\chi$\_scale | y | Subroutine |
| :--- | :--- | :--- |
| Short-precision real | Short-precision complex | SRCFT3 |
| Long-precision real | Long-precision complex | DRCFT3 |

**Note:** For each use, only one invocation of this subroutine is necessary. The initialization phase, preparing the working storage, is a relatively small part of the total computation, so it is performed on each invocation.

### Syntax

| Fortran | `CALL SRCFT3 \| DRCFT3 (x, inc2x, inc3x, y, inc2y, inc3y, n1, n2, n3, isign, scale, aux, naux)` |
| :--- | :--- |
| **C and C++** | `sref3 \| dref3 (x, inc2x, inc3x, y, inc2y, inc3y, n1, n2, n3, isign, scale, aux, naux);` |

### On Entry:

- **$\chi$** is the array $\chi$, containing the three-dimensional data to be transformed, where each element $\chi_{j1,j2,j3}$, using zero-based indexing, is stored in $X([j1+2(inc2x)+3(inc3x)])$ for $j1 = 0, 1, \ldots, n1-1$, $j2 = 0, 1, \ldots, n2-1$, and $j3 = 0, 1, \ldots, n3-1$. The strides for the elements in the first, second, and third dimensions are assumed to be 1, $inc2x$ ($\geq n1$), and $inc3x$ ($\geq (n2)(inc2x)$), respectively.

  Specified as: an array, containing numbers of the data type indicated in Table 147. If the array is dimensioned X(LDA1, LDA2, LDA3), then LDA1 = $inc2x$, (LDA1)(LDA2) = $inc3x$, and LDA3 $\geq n3$. For information on how to set up this array, see "Setting Up Your Data" on page 746. For more details, see "Notes" on page 814.

- **$inc2x$** is the stride between the elements in array $\chi$ for the second dimension.

  Specified as: a fullword integer; $inc2x \geq n1$.

- **$inc3x$** is the stride between the elements in array $\chi$ for the third dimension.

  Specified as: a fullword integer; $inc3x \geq (n2)(inc2x)$.

- **$y$** See "On Return" on page 813.

- **$inc2y$** is the stride between the elements in array $y$ for the second dimension.

  Specified as: a fullword integer; $inc2y \geq n1/2+1$.

- **$inc3y$** is the stride between the elements in array $y$ for the third dimension.

  Specified as: a fullword integer; $inc3y \geq (n2)(inc2y)$.

- **$n1$** is the length of the first dimension of the three-dimensional data in the array to be transformed.

  Specified as: a fullword integer; $n1 \leq 37748736$ and must be one of the values listed in "Acceptable Lengths for the Transforms" on page 743. For all other values specified less than 37748736, you have the option of having the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to ESSL” on page 38.

- **$n2$** is the length of the second dimension of the three-dimensional data in the array to be transformed.

  Specified as: a fullword integer; *n2* ≤ 37748736 and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. For all other values specified less than 37748736, you have the option of having the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to ESSL” on page 38.

- **$n3$** is the length of the third dimension of the three-dimensional data in the array to be transformed.

  Specified as: a fullword integer; *n3* ≤ 37748736 and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. For all other values specified less than 37748736, you have the option of having the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to ESSL” on page 38.

- **isign** controls the direction of the transform, determining the sign *Isign* of the exponents of *Wn1*, *Wn2*, and *Wn3*, where:
  - If *isign* = positive value, *Isign* = +(transforming time to frequency).
  - If *isign* = negative value, *Isign* = −(transforming frequency to time).

  Specified as: a fullword integer; *isign* > 0 or *isign* < 0.

- **scale** is the scaling constant *scale*. See “Function” on page 815 for its usage.

  Specified as: a number of the data type indicated in Table 147 on page 812, where *scale* > 0.0 or *scale* < 0.0.

- **aux** has the following meaning:
  - If *naux* = 0 and error 2015 is unrecoverable, *aux* is ignored.
  - Otherwise, it is a storage work area used by this subroutine.

  Specified as: an area of storage, containing *naux* long-precision real numbers. On output, the contents are overwritten.

- **naux** is the number of doublewords in the working storage area specified in *aux*.

  Specified as: a fullword integer, where:
  - If *naux* = 0 and error 2015 is unrecoverable, SRCFT3 and DRCFT3 dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.
  - Otherwise, *naux* ≥ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For all other values specified less than the minimum value, you have the option of having the minimum value returned in this argument. For details, see “Using Auxiliary Storage in ESSL” on page 32.

### On Return:

- **y** is the array *Y*, containing the elements resulting from the three-dimensional discrete Fourier transform of the data in *X*. Each element *y* *k1k2k3*, using zero-based indexing, is stored in *Y*(*k1*+*k2*(*inc2*)+*k3*(*inc3*)). For *k1* = 0, 1, ..., *n1*/2, *k2* = 0, 1, ..., *n2*−1, and *k3* = 0, 1, ..., *n3*−1. Due to complex conjugate symmetry, the output consists of only the first *n1*/2+1 values along the first dimension of the array, for *k1* = 0, 1, ..., *n1*/2. The strides for the elements in the first, second, and third dimensions are assumed to be 1, $inc2y$ ($\ge n1/2+1$), and $inc3y$ ($\ge (n2)(inc2y)$), respectively.

  Returned as: an array, containing numbers of the data type indicated in Table 147 on page 812. This array must be aligned on a doubleword boundary. If the array is dimensioned $Y(LDA1,LDA2,LDA3)$, then $LDA1 = inc2y$, $LDA1(LDA2) = inc3y$, and $LDA3 = n3$. For information on how to set up this array, see “Setting Up Your Data” on page 746. For more details, see “Notes.”

### Notes

- If you specify the same array for $X$ and $Y$, then $inc2x$ must be greater than or equal to $2(inc2y)$, and $inc3x$ must be greater than or equal to $2(inc3y)$. In this case, output overwrites input. When using the ESSL SMP library in a multithreaded environment, if $inc2x > 2(inc2y)$ or $inc3x > 2(inc3y)$, these subroutines run on a single thread and issue an attention message.
- If you specify different arrays $X$ and $Y$, they must have no common elements; otherwise, results are unpredictable. See “Concepts” on page 55.
- To achieve the best performance, you should align array $X$ on a doubleword boundary, and $inc2x$ and $inc3x$ should be even numbers. The strides for your input array do not affect performance as long as they are even numbers. In addition, you should use “STRIDE—Determine the Stride Value for Optimal Performance in Specified Fourier Transform Subroutines” on page 963 to determine the optimal values for the strides $inc2y$ and $inc3y$ for your output array. Example 8 in the STRIDE subroutine description explains how it is used for these subroutines. For additional information on how to set up your data, see “Setting Up Your Data” on page 746.

### Processor-Independent Formulas for SRCFT3 for NAUX

Use the following formulas for calculating $n aux$:

1. If $\max(n2, n3) < 252$ and:
   - If $n1 \le 16384$, use $n aux = 65000$.
   - If $n1 > 16384$, use $n aux = 60000 + 1.39n1$.
2. If $n2 \ge 252$, $n3 < 252$, and:
   - If $n1 \le 16384$, use $n aux = 65000 + \lambda$.
   - If $n1 > 16384$, use $n aux = 60000 + 1.39n1 + \lambda$,
     where $\lambda = (n2+256)(s+2.28)$ and $s = \min(64, 1+n1/2)$.
3. If $n2 < 252$, $n3 \ge 252$, and:
   - If $n1 \le 16384$, use $n aux = 65000 + \psi$.
   - If $n1 > 16384$, use $n aux = 60000 + 1.39n1 + \psi$,
     where $\psi = (n3+256)(s+2.28)$ and $s = \min(64, (n2)(1+n1/2))$.
4. If $n2 \ge 252$ and $n3 \ge 252$, use the larger of the values calculated for cases 2 and 3 above.

If $inc2x$ or $inc3x$ is an odd number, or if array $X$ is not aligned on a doubleword boundary, you should add the following amount to all the formulas given above: $n2(1+n1/2)$

### Processor-Independent Formulas for DRCT3 for NAUX

Use the following formulas for calculating $n aux$:

1. If $\max(n2, n3) < 252$ and:
   - If $n1 \le 4096$, use $n aux = 62000$.
   - If $n1 > 4096$, use $n aux = 60000 + 2.78n1$.
2. If $n2 \ge 252$, $n3 < 252$, and:
   - If $n1 \le 4096$, use $n aux = 62000 + \lambda$.
