
# SSPEV, DSPeV, CHPEV, and ZHPEV

$$
\begin{bmatrix}
\{1.0, & 0.0\} & \{0.0, & -1.0\} \\
\{0.0, & 1.0\} & \{1.0, & 0.0\}
\end{bmatrix}
$$

where:

- **NAUX** is equal to 4N.
- **AUX** contains 4N elements.
- On output, AP has been overwritten.

**Note:** This matrix is used in Example 6.1 in referenced text [65].

**Call Statement and Input:**

```
IOPT AP W Z LDZ N AUX NAUX
|
|  |
|  |  |  |  |  |  |
CALL ZHPEV( 1 , AP , W , Z , 2 , 2 , AUX , 8  )

AP = ((1.0,  . ), (0.0,  1.0), (1.0,  . ))
```

**Output:**

$$
\mathrm{W} = \left[ \begin{array}{r} 0.000000 \\ 2.000000 \end{array} \right]
$$

$$
\mathrm{Z} = \left[ \begin{array}{rr} \{0.000000, & -0.707107\} & \{0.000000, & -0.707107\} \\ \{-0.707107, & 0.000000\} & \{0.707107, & 0.000000\} \end{array} \right]
$$

## Example 6

This example shows how to find the eigenvalues only of a complex Hermitian matrix $A$ of order 4, stored in upper-packed storage mode. Matrix $A$ is:

$$
\left[ \begin{array}{rrrr} \{3.0, & 0.0\} & \{1.0, & 0.0\} & \{0.0, & 0.0\} & \{0.0, & 2.0\} \\ \{1.0, & 0.0\} & \{3.0, & 0.0\} & \{0.0, & -2.0\} & \{0.0, & 0.0\} \\ \{0.0, & 0.0\} & \{0.0, & 2.0\} & \{1.0, & 0.0\} & \{1.0, & 0.0\} \\ \{0.0, & -2.0\} & \{0.0, & 0.0\} & \{1.0, & 0.0\} & \{1.0, & 0.0\} \end{array} \right]
$$

where:

- **NAUX** is equal to 3N.
- **AUX** contains 3N elements.
- **LDZ** is set to 1 to avoid an error condition.
- **DUMMY** is used as a placeholder for argument $Z$, which is not used in the computation.
- On output, AP has been overwritten.

**Note:** This matrix is used in Example 6.6 in referenced text [65].

**Call Statement and Input:**

```
IOPT AP W Z LDZ N AUX NAUX
| | | | | | | | | |
CALL ZHPEV( 20 , AP , W , DUMMY , 1 , 4 , AUX , 12 )

AP = ((3.0,  . ), (1.0, & 0.0), (3.0,  . ), (0.0, & 0.0),
      (0.0, -2.0), (1.0,  . ), (0.0, & 2.0), (0.0, & 0.0),
      (1.0,  0.0), (1.0,  . ))
```

**Output:**

$$
\begin{array}{l}
w
\end{array}
=
\left[
\begin{array}{l}
-0.828427\\
0.000000\\
4.000000\\
4.828427
\end{array}
\right]
$$

## Example 7

This example shows how to find the eigenvalues and eigenvectors of a complex Hermitian matrix $A$ of order 2, stored in lower-packed storage mode. Matrix $A$ is:

![](img/5b0f44f3be6048723819b26aed7f6f03_746_0.png)

where:

- NAUX is equal to $4N$.
- AUX contains $4N$ elements.
- On output, AP has been overwritten.

**Note:** This matrix is used in Example 6.2 in referenced text [65].

### Call Statement and Input:

```
            IOPT    AP     W      Z      LDZ     N      AUX     NAUX
CALL ZHPEV( I ,  AP ,  W ,  Z ,  2 ,  AUX ,  8  )
AP          = ((1.0, . ) , (1.0, 1.0) , (1.0, . ) )
```

### Output:

```
w          = [ -0.414214 ]
              [ 2.414214 ]
```

![](img/5b0f44f3be6048723819b26aed7f6f03_746_1.png)

# SSPSV, DPSV, CHPSV, and ZHPSV—Extreme Eigenvalues and, Optionally, the Eigenvectors of a Real Symmetric Matrix or a Complex Hermitian Matrix

SSPSV and DPSV compute the extreme eigenvalues and, optionally, the eigenvectors of real symmetric matrix A, stored in lower- or upper-packed storage mode. CHPSV and ZHPSV compute the extreme eigenvalues and, optionally, the eigenvectors of complex Hermitian matrix A, stored in lower- or upper-packed storage mode. The extreme eigenvalues are returned in vector w, and the corresponding eigenvectors are returned in matrix Z:

$Az = wZ$

where $A = A^T$ or $A = A^H$.

**Table 132. Data Types**

| A, z | w, aux | Subroutine |
|---|---|---|
| Short-precision real | Short-precision real | SSPV† |
| Long-precision real | Long-precision real | DPSV† |
| Short-precision complex | Short-precision real | CHPSV† |
| Long-precision complex | Long-precision real | ZHPSV† |

†Not LAPACK. Although this subroutine has the same name as an existing LAPACK subroutine, its calling-sequence arguments and functionality are different from that LAPACK subroutine.

> **Note:** If you want to compute 10% or fewer eigenvalues only, or you want to compute 30% or fewer eigenvalues and eigenvectors, you get better performance if you use _SSPSV_ and _HPSV_ instead of _SPEV_ and _HPEV_, respectively. For all other uses, you should use _SPEV_ and _HPEV_.

## Syntax

| Fortran | CALL SSPSV \| DPSV \| CHPSV \| ZHPSV (*i*opt, *ap*, *w*, *z*, *ldz*, *n*, *m*, *aux*, *naux*) |
|---|---|
| C and C++ | sspsv \| dpspv \| chpsv \| zhpsv (*i*opt, *ap*, *w*, *z*, *ldz*, *n*, *m*, *aux*, *naux*); |

On Entry:

- ***i*opt** indicates the type of computation to be performed, where:
  - If *i*opt = 0 or 20, the *m* smallest eigenvalues only are computed.
  - If *i*opt = 1 or 21, the *m* smallest eigenvalues and the eigenvectors are computed.
  - If *i*opt = 10 or 30, the *m* largest eigenvalues only are computed.
  - If *i*opt = 11 or 31, the *m* largest eigenvalues and the eigenvectors are computed.
  - Specified as: a fullword integer; *i*opt = 0, 1, 10, 11, 20, 21, 30, or 31.

- ***ap*** is the real symmetric or complex Hermitian matrix A of order n, whose m smallest or largest eigenvalues and, optionally, the corresponding eigenvectors are computed. It is stored in an array, referred to as AP, where:
  - If *i*opt = 0, 1, 10, or 11, it is stored in lower-packed storage mode.
  - If *i*opt = 20, 21, 30, or 31, it is stored in upper-packed storage mode.

Specified as: a one-dimensional array of (at least) length $n(n+1)/2$, containing numbers of the data type indicated in Table 132 on page 724. On output, $\text{AP}$ is overwritten; that is, the original input is not preserved.

- $w$: See “On Return.”
- $z$: See “On Return.”
- $ldz$: has the following meaning, where:
  - If $i\text{opt} = 0, 10, 20$, or $30$, it is not used in the computation.
  - If $i\text{opt} = 1, 11, 21$, or $31$, it is the leading dimension of the output array specified for $z$.
  - Specified as: a fullword integer. It must have the following value, where:
    - If $i\text{opt} = 0, 10, 20$, or $30$, $ldz > 0$.
    - If $i\text{opt} = 1, 11, 21$, or $31$, $ldz > 0$ and $ldz \ge n$.

- $n$: is the order of matrix $\text{A}$.
  - Specified as: a fullword integer; $n \ge 0$.

- $m$: is the number of eigenvalues and, optionally, eigenvectors to be computed.
  - Specified as: a fullword integer; $0 \le m \le n$.

- $aux$: has the following meaning:
  - If $n\text{aux} = 0$ and error 2015 is unrecoverable, $aux$ is ignored.
  - Otherwise, it is a storage work area used by this subroutine. Its size is specified by $n\text{aux}$.
  - Specified as: an area of storage, containing numbers of the data type indicated in Table 132 on page 724. On output, the contents are overwritten.

- $n\text{aux}$: is the size of the work area specified by $aux$—that is, the number of elements in $aux$.
  - Specified as: a fullword integer, where:
    - If $n\text{aux} = 0$ and error 2015 is unrecoverable, SSPSV, DPSV, CHPSV, and ZHPSV dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.
    - Otherwise, It must have the following value, where:
      - For SSPSV and DPSV:
        - If $i\text{opt} = 0, 10, 20$, or $30$, $n\text{aux} \ge 3n$.
        - If $i\text{opt} = 1, 11, 21$, or $31$, $n\text{aux} \ge 9n$.
      - For CHPSV and ZHPSV:
        - If $i\text{opt} = 0, 10, 20$, or $30$, $n\text{aux} \ge 5n$.
        - If $i\text{opt} = 1, 11, 21$, or $31$, $n\text{aux} \ge 11n$.

## On Return:

- $w$: is the vector $w$ of length $n$, containing in the first $m$ positions of either the $m$ smallest eigenvalues of $\text{A}$ in ascending order or the $m$ largest eigenvalues of $\text{A}$ in descending order.
  - Returned as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 132 on page 724.

- $z$: has the following meaning, where:
  - If *iOpt* = 0, 10, 20, or 30, it is not used in the computation.
  - If *iOpt* = 1, 11, 21, or 31, it is the *n* by *n* matrix *Z*, containing *m* orthonormal eigenvectors of matrix *A*. The eigenvector in column *i* of matrix *Z* corresponds to the eigenvalue *w_i*.
  - Returned as: an *ldz* by (at least) *m* array, containing numbers of the data type indicated in Table 132 on page 724.

## Notes

1. When you specify *iOpt* = 0, 10, 20, or 30, you must specify:
   - A positive value for *ldz*
   - A dummy argument for *z* (see “Example 4” on page 729)
2. The following items must have no common elements: matrix *A*, matrix *Z*, vector *w*, and the data area specified for *aux*; otherwise, results are unpredictable. See “Concepts” on page 55.
3. On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix *A* are assumed to be zero, so you do not have to set these values.
4. For a description of how real symmetric matrices are stored in lower- or upper-packed storage mode, see “Lower-Packed Storage Mode” on page 65 or “Upper-Packed Storage Mode” on page 66, respectively.
   - For a description of how complex Hermitian matrices are stored in lower- or upper-packed storage mode, see “Complex Hermitian Matrix” on page 69.
5. You have the option of having the minimum required value for *nAux* dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSL” on page 32.

## Function

The methods used to compute the extreme eigenvalues and, optionally, the eigenvectors for either a real symmetric matrix or a complex Hermitian matrix are described in the steps below. For more information on these methods, see references [41], [45], [65], [90], [100], and [102]. If *n* or *m* is 0, no computation is performed. The results of the computations using *short*- and *long*-precision data can vary in accuracy. Eigenvalues computed using equivalent *iOpt* values are mathematically equivalent, but are not guaranteed to be bitwise identical. For example, the results computed using *iOpt* = 0 and *iOpt* = 20 are mathematically equivalent, but are not necessarily bitwise identical.

These algorithms have a tendency to generate underflows that may hurt overall performance. The system default is to mask underflow, which improves the performance of these subroutines.

The extreme eigenvalues and, optionally, the eigenvectors of a real symmetric matrix *A* or complex Hermitian matrix *A* are computed as follows:

- For *iOpt* = 0, 10, 20, or 30, the eigenvalues are computed as follows:
  1. Reduce the real symmetric matrix *A* (for SSPSV and DSPSV) or complex Hermitian matrix *A* (for CHPSV and ZHPSV) to a real symmetric tridiagonal matrix using orthogonal similarity transformations (for SSPSV and DSPSV) or unitary similarity transforms (for CHPSV and ZHPSV).
  2. Compute the *m* smallest eigenvalues or *m* largest eigenvalues of the real symmetric tridiagonal matrix using a rational variant of the QR method with Newton corrections.
  3. The eigenvalues are returned in vector *w* in the first *m* positions, where the *m* smallest are placed in ascending order, or the *m* largest are placed in descending order.
