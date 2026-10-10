
## DGSS

Specified as: a fullword integer; $naux \ge 10n + 100$.

### On Return:

ia is the transformed array, referred to as IA, which can be used as input in subsequent calls to this subroutine. This may result in a performance increase.

Specified as: an array of length lna, containing fullword integers.

bx is the solution vector x of length n, containing the results of the computation.

Specified as: a one-dimensional array, containing long-precision real numbers.

### Notes

1. The input arguments n, lna, and naux, must be the same as those specified for DGSF. Whereas, the input arguments a, ia, ja, and aux must be those produced on output by DGSF. Otherwise, results are unpredictable.
2. You have the option of having the minimum required value for naux dynamically returned to your program. For details, see "Using Auxiliary Storage in ESSL" on page 32.

### Function

The system $\mathbf{A}\mathbf{x}=\mathbf{b}$ is solved for $\mathbf{x}$, where $\mathbf{A}$ is a sparse matrix and $\mathbf{x}$ and $\mathbf{b}$ are vectors. Depending on the value specified for the jopt argument, DGSS can also solve the system $\mathbf{A}^{\mathrm{T}}\mathbf{x}=\mathbf{b}$, where $\mathbf{A}^{\mathrm{T}}$ is the transpose of sparse matrix $\mathbf{A}$.

If the value specified for the jopt argument is 0 or 10, the following equation is solved:

$\mathbf{A}\mathbf{x}=\mathbf{b}$

If the value specified for the jopt argument is 1 or 11, the following equation is solved:

$\mathbf{A}^{\mathrm{T}}\mathbf{x}=\mathbf{b}$

DGSS uses the results of the factorization of matrix $\mathbf{A}$, produced by a preceding call to DGSF. The transformed matrix $\mathbf{A}$ consists of the upper triangular matrix $\mathbf{U}$ and the lower triangular matrix $\mathbf{L}$.

See references [12], [49], and [96].

### Error Conditions

Computational Errors: None

Input-Argument Errors:
1. jopt $\ne 0$, 1, 10, or 11
2. n $< 0$
3. lna $\le 0$
4. naux is too small—that is, less than the minimum required value. Return code 1 is returned if error 015 is recoverable.

### Example 1

This example shows how to solve the system $\mathbf{A}\mathbf{x}=\mathbf{b}$, where matrix $\mathbf{A}$ is a 5 by 5 sparse matrix. The right-hand side is not sparse.

**Note:** The input for this subroutine is the same as the output from DGSF, except for *BX*.

Matrix A is:

$$
\begin{pmatrix} 
2.0 & 0.0 & 4.0 & 0.0 & 0.0 \\ 
1.0 & 1.0 & 0.0 & 0.0 & 3.0 \\ 
0.0 & 0.0 & 3.0 & 4.0 & 0.0 \\ 
2.0 & 2.0 & 0.0 & 1.0 & 5.0 \\ 
0.0 & 0.0 & 1.0 & 1.0 & 0.0 
\end{pmatrix}
$$

#### Call Statement and Input:

```fortran
            JOPT    N    A    IA   JA    LNA    BX   AUX    NAUX

CALL DGSS( 0 ,  5 , A , IA , JA , 27 ,  BX , AUX , 150 )
```

```fortran
A   =  (0.5, . , 0.3, 1.0, . , 1.0, . , 3.0, . , . , . , 1.0, 
        1.0, . , . , . , . , . , . , . , -1.7, -0.5, -1.0, -1.0, 
        4.0, -3.0, -4.0) 
IA  =  (0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, . , . , . , . , . , . , . , . ) , 
JA  =  (1, 0, 5, 2, 0, 4, 0, 2, 0, 0, 0, 3, 4, . , . , . , . , . , 
        1, . , . , . , 4, 2, 4, 4, 1, 3, 1)
BX  =  (1.0, 1.0, 1.0, 1.0, 1.0)
```

#### Output:

```fortran
IA  =  (0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, . , . , . , . , . , . , . , . ) , 
BX  =  ( . , . , . , . , 2, 1, 1, 3, 3, 5, 5)
      =  (-5.500000, 9.500000, 3.000000, -2.000000, -1.000000)
```

**Note:** On input, a " " . " " means that you do not have to store a value in that position in the array. However, the storage position is required and may be overwritten during the computation. On output, a " " . " " means that the value in that position in the array is not significant.

### Example 2

This example shows how to solve the system $A^T x = b$, using the same matrix $A$ used in Example 1. The input is also the same as in Example 1, except for the *jopt* argument. The right-hand side is not sparse.

#### Call Statement and Input:

```fortran
            JOPT    N    A    IA   JA    LNA    BX   AUX    NAUX

CALL DGSS( 1 ,  5 , A , IA , JA , 27 ,  BX , AUX , 150 )
```

```fortran
BX  =  (1.0, 1.0, 1.0, 1.0, 1.0)
```

#### Output:

```fortran
IA  =  (0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, . , . , . , . , . , . , . , . ) , 
BX  =  ( . , . , . , . , 2, 1, 1, 3, 3, 5, 5)
      = (0.000000, -3.000000, -2.000000, 2.000000, 7.000000)
```

**Note:** On input, a " " . " " means that you do not have to store a value in that position in the array. However, the storage position is required and may be overwritten during the computation. On output, a " " . " " means that the value in that position in the array is not significant.

### Example 3

This example shows how to solve the system $Ax = b$, using the same matrix $A$ as in Examples 1 and 2. The input is also the same as in Examples 1 and 2, except for the *jopt* and *bx* arguments. The right-hand side is sparse.

#### Call Statement and Input:

```fortran
JOPT N A IA JA LNA BX AUX NAUX
|
| |
| |
| |
| |
| |
CALL DGSS( 10 , 5 , A , IA , JA , 27 , BX , AUX , 150 )
```

BX = (0.0, 0.0, 0.0, 0.0, 1.0, 0.0)

#### Output:

IA = (1, 4, 2, 5, 3, 5, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 2, 1, 1, 3, 3, 5, 5)

BX = (0.000000, 3.000000, 0.000000, 0.000000, -1.000000)

**Note:** On input, a " " . " " means that you do not have to store a value in that position in the array. However, the storage position is required and may be overwritten during the computation. On output, a " " . " " means that the value in that position in the array is not significant.

### Example 4

This example shows how to solve the system $ATx = b$, using the same matrix $A$ as in Examples 1, 2, and 3. The input is also the same as in Examples 1, 2, and 3, except for the *jopt* argument. The right-hand side is sparse.

#### Call Statement and Input:

```fortran
JOPT N A IA JA LNA BX AUX NAUX
|
| |
| |
| |
| |
CALL DGSS( 11 , 5 , A , IA , JA , 27 , BX , AUX , 150 )
```

BX = (0.0, 0.0, 0.0, 1.0, 0.0)

#### Output:

IA = (1, 4, 2, 5, 3, 5, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 2, 1, 1, 3, 3, 5, 5)

BX = (0.000000, 0.000000, 1.000000, 0.000000, -3.000000)

**Note:** On input, a " " . " " means that you do not have to store a value in that position in the array. However, the storage position is required and may be overwritten during the computation. On output, a " " . " " means that the value in that position in the array is not significant.

## DGKFS—General Sparse Matrix or Its Transpose Factorization, Determinant, and Solve Using Skyline Storage Mode

This subroutine can perform either or both of the following functions for general sparse matrix A, stored in skyline storage mode, and for vectors x and b:

- Factor A and, optionally, compute the determinant of A.
- Solve the system $Ax = b$ or $A^{T}x = b$ using the results of the factorization of matrix A, produced on this call or a preceding call to this subroutine.

You also have the choice of using profile-in or diagonal-out skyline storage mode for A on input or output.

Note: The input to the solve performed by this subroutine must be the output from the factorization performed by this subroutine.

### Syntax

| Language | Code |
| :------- | :--- |
| Fortran | `CALL DGKFS (n, au, nu, iau, al, nl, idl, iparm, rparm, aux, naux, bx, ldx, mbx)` |
| C and C++ | `dgkfs (n, au, nu, iau, al, nl, idl, iparm, rparm, aux, naux, bx, ldx, mbx);` |

### On Entry:

n is the order of general sparse matrix A. Specified as: a fullword integer; $n \geq 0$.

au is the array, referred to as AU, containing one of three forms of the upper triangular part of general sparse matrix A, depending on the type of computation performed, where:

- If you are doing a **factor and solve** or a **factor only**, and if IPARM(3) = 0, then AU contains the unfactored upper triangle of general sparse matrix A.
- If you are doing a **factor only**, and if IPARM(3) > 0, then AU contains the partially factored upper triangle of general sparse matrix A. The first IPARM(3) columns in the upper triangle of A are already factored. The remaining columns are factored in this computation.
- If you are doing a **solve only**, then AU contains the factored upper triangle of general sparse matrix A, produced by a preceding call to this subroutine.

In each case:

- If IPARM(4) = 0, diagonal-out skyline storage mode is used for A.
- If IPARM(4) = 1, profile-in skyline storage mode is used for A.

Specified as: a one-dimensional array of (at least) length nu, containing long-precision real numbers.

nu is the length of array AU.

Specified as: a fullword integer; $nu = 0$ and $nu \geq (IDU(n+1)-1)$.

idu is the array, referred to as IDU, containing the relative positions of the diagonal elements of matrix A (in one of its three forms) in array AU.

Specified as: a one-dimensional array of (at least) length n+1, containing fullword integers.
