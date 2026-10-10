
AC is the m by n general sparse matrix A or symmetric matrix A of order n stored in compressed-matrix storage mode in an array, referred to as AC. Returned as: an lda by at least (input argument) nz array, containing long-precision real numbers, where only the first (output argument) nz columns are used to store the matrix.

KA is the array referred to as KA, containing the column numbers of the matrix A elements that are stored in the corresponding positions in array AC. Returned as: an lda by at least (input argument) nz array, containing fullword integers, where only the first (output argument) nz columns are used to store the column numbers.

## Notes

1. In your C program, argument nz must be passed by reference.
2. The value specified for input argument nz should be greater than or equal to the number of nonzero elements you estimate to be in each row of sparse matrix A. The value returned in output argument nz corresponds to the nz value defined for compressed-matrix storage mode. This value is less than or equal to the value specified for input argument nz.
3. For a description of the storage modes for sparse matrices, see "Compressed-Matrix Storage Mode" on page 90 and "Storage-by-Rows" on page 95.

## Function

A sparse matrix A is converted from storage-by-rows (using arrays AR, JA, and IA) to compressed-matrix storage mode (using arrays AC and KA). The argument iopt indicates whether the input matrix A is stored by rows using the storage variation for general sparse matrices or for symmetric sparse matrices. See reference [75].

This subroutine is meant for existing programs that need to convert their sparse matrices to a storage mode compatible with some of the ESSL sparse matrix subroutines, such as DSMMX.

## Error Conditions

Computational Errors: None

Input-Argument Errors:

1. iopt \neq 0 or 1
2. m < 0
3. lda < 1
4. lda < m
5. nz \leq 0
6. IA(m+1) < 1
7. IA(i+1)-IA(i) < 0, for any i = 1, m
8. nz is too small to store matrix A in array AC, where:
    - If iopt = 0, AC and KA are not modified.
    - If iopt = 1, AC and KA are modified.

## Example 1

This example shows a general sparse matrix A, which is stored by rows and converted to compressed-matrix storage mode, where sparse matrix A is:

![](img/5b0f44f3be6048723819b26aed7f6f03_996_0.png)

Because there is a maximum of only two nonzero elements in each row of *A*, and argument *nz* is specified as 5, columns 3 through 5 of arrays AC and KA are not used.

### Call Statement and Input:

```fortran
IOPT   AR    JA   IA   M   NZ   AC   KA   LDA
   |    |     |    |    |    |    |    |    |
CALL DSRSM( 0 , AR , JA , IA , 4 , 5 , AC , KA , 4 )

AR       = (11.0, 14.0, 22.0, 24.0, 33.0, 34.0, 44.0)
JA       = (1, 4, 2, 4, 3, 4, 4)
IA       = (1, 3, 5, 7, 8)
```

### Output:

NZ = 2

```text
AC = [ 11.0  14.0 . . .
      22.0  24.0 . . .
      33.0  34.0 . . .
      44.0   0.0 . . .
]

KA = [ 1  4 . . .
      2  4 . . .
      3  4 . . .
      4  4 . . .
]
```

### Example 2

This example shows a symmetric sparse matrix *A*, which is stored by rows and converted to compressed-matrix storage mode, where sparse matrix *A* is:

```text
[ 11.0  0.0  0.0  14.0]
[ 0.0  22.0  0.0  24.0]
[ 0.0  0.0  33.0  34.0]
[ 14.0  24.0  34.0  44.0]
```

Because there is a maximum of only four nonzero elements in each row of *A*, and argument *nz* is specified as 6, columns 5 and 6 of arrays AC and KA are not used.

### Call Statement and Input:

```fortran
IOPT   AR    JA   IA   M   NZ   AC   KA   LDA
   |    |     |    |    |    |    |    |    |
CALL DSRSM( 1 , AR , JA , IA , 4 , 6 , AC , KA , 4 )

AR       = (11.0, 14.0, 22.0, 24.0, 33.0, 34.0, 44.0)
JA       = (1, 4, 2, 4, 3, 4, 4)
IA       = (1, 3, 5, 7, 8)
```

### Output:

NZ = 4

```text
AC = [ 11.0  14.0  0.0  0.0 . .
      22.0  24.0  0.0  0.0 . .
      33.0  34.0  0.0  0.0 . .
      44.0  24.0  34.0 14.0 . .
]

KA = [ 1  4  4  4 . .
      2  4  4  4 . .
      3  4  4  4 . .
      4  2  3  1 . .
]
```

## DGKTRN—For a General Sparse Matrix, Convert Between Diagonal-Out and Profile-In Skyline Storage Mode

This subroutine converts general sparse matrix A of order n from one skyline storage mode to another—that is, between the following:

- Diagonal-out skyline storage mode
- Profile-in skyline storage mode

## Syntax

| | |
| :--- | :--- |
| **Fortran** | `CALL DGKTRN (n, au, nu, idu, al, nl, idl, itran, aux, naux)` |
| **C and C++** | `dgktrn (n, au, nu, idu, al, nl, idl, itran, aux, naux);` |

**On Entry:**

- **n**
  is the order of general sparse matrix A. Specified as: a fullword integer;
  n ≥ 0.

- **au**
  is the array, referred to as AU, containing the upper triangular part of general sparse matrix A, stored as follows, where:
  - If ITRAN(1) = 0, A is stored in diagonal-out skyline storage mode.
  - If ITRAN(1) = 1, A is stored in profile-in skyline storage mode.
  Specified as: a one-dimensional array of (at least) length nu, containing long-precision real numbers.

- **nu**
  is the length of array AU.
  Specified as: a fullword integer; nu ≥ 0 and nu ≥ (IDU(n+1)−1).

- **idu**
  is the array, referred to as IDU, containing the relative positions of the diagonal elements of matrix A in input array AU.
  Specified as: a one-dimensional array of (at least) length n+1, containing fullword integers.

- **al**
  is the array, referred to as AL, containing the lower triangular part of general sparse matrix A, stored as follows, where:
  - If ITRAN(1) = 0, A is stored in diagonal-out skyline storage mode.
  - If ITRAN(1) = 1, A is stored in profile-in skyline storage mode.
  **Note:** Entries in AL for diagonal elements of A are assumed not to have meaningful values.
  Specified as: a one-dimensional array of (at least) length nl, containing long-precision real numbers.

- **nl**
  is the length of array AL.
  Specified as: a fullword integer; nl ≥ 0 and nl ≥ (IDL(n+1)−1).

- **idl**
  is the array, referred to as IDL, containing the relative positions of the diagonal elements of matrix A in input array AL.
  Specified as: a one-dimensional array of (at least) length n+1, containing fullword integers.

- **itran**
  is an array of parameters, ITRAN(i), where:
  - **ITRAN(1)** indicates the input storage mode used for matrix *A*. This determines the arrangement of data in arrays *AU*, *IDU*, *AL*, and *IDL* on input, where:
    - If ITRAN(1) = 0, diagonal-out skyline storage mode is used.
    - If ITRAN(1) = 1, profile-in skyline storage mode is used.
  - **ITRAN(2)** indicates the output storage mode used for matrix *A*. This determines the arrangement of data in arrays *AU*, *IDU*, *AL*, and *IDL* on output, where:
    - If ITRAN(2) = 0, diagonal-out skyline storage mode is used.
    - If ITRAN(2) = 1, profile-in skyline storage mode is used.
  - **ITRAN(3)** indicates the direction of sweep that ESSL uses through the matrix *A*, allowing you to optimize performance (see “Notes” on page 978), where:
    - If ITRAN(3) = 1, matrix *A* is transformed in the positive direction, starting in row or column 1 and ending in row or column *n*.
    - If ITRAN(3) = −1, matrix *A* is transformed in the negative direction, starting in row or column *n* and ending in row or column 1.
  Specified as: a one-dimensional array of (at least) length 3, containing fullword integers, where:
  ITRAN(1) = 0 or 1
  ITRAN(2) = 0 or 1
  ITRAN(3) = −1 or 1

- **aux**
  has the following meaning:
  - If *naux* = 0 and error 2015 is unrecoverable, *aux* is ignored.
  - Otherwise, it is the storage work area used by this subroutine. Its size is specified by *naux*.
  Specified as: an area of *storage*, containing *naux* long-precision real numbers.

- **naux**
  is the size of the work area specified by *aux*—that is, the number of elements in *aux*.
  Specified as: a fullword integer, where:
  - If *naux* = 0 and error 2015 is unrecoverable, DGKTRN dynamically allocates the work area used by this subroutine. The work area is deallocated before control is returned to the calling program.
  - Otherwise, *naux* ≥ 2*n*.

## On Return:

- **au** is the array, referred to as *AU*, containing the upper triangular part of general sparse matrix *A*, stored as follows, where:
  - If ITRAN(2) = 0, *A* is stored in diagonal-out skyline storage mode.
  - If ITRAN(2) = 1, *A* is stored in profile-in skyline storage mode.
  Returned as: a one-dimensional array of (at least) length *nu*, containing long-precision real numbers.

- **idu** is the array, referred to as *IDU*, containing the relative positions of the diagonal elements of matrix *A* in output array *AU*.
  Returned as: a one-dimensional array of (at least) length *n*+1, containing fullword integers.
