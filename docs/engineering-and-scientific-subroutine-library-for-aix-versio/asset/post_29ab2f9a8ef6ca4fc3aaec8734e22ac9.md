
# DSKTRN

Specified as: a one-dimensional array of (at least) length 3, containing fullword integers, where:
```
ITRAN(1) = 0 or 1
ITRAN(2) = 0 or 1
ITRAN(3) = -1 or 1
```

*aux* has the following meaning:
If *naux* = 0 and error 2015 is unrecoverable, *aux* is ignored.
Otherwise, it is the storage work area used by this subroutine. Its size is specified by *naux*.

*naux* is the size of the work area specified by *aux*—that is, the number of elements in *aux*.
Specified as: a fullword integer, where:
If *naux* = 0 and error 2015 is unrecoverable, DSKTRN dynamically allocates the work area used by this subroutine. The work area is deallocated before control is returned to the calling program.
Otherwise, *naux* ≥ *n*.

## On Return

*A* is the array, referred to as *A*, containing the upper triangular part of symmetric sparse matrix *A*, stored as follows, where:
If ITRAN(2) = 0, *A* is stored in diagonal-out skyline storage mode.
If ITRAN(2) = 1, *A* is stored in profile-in skyline storage mode.
Returned as: a one-dimensional array of (at least) length *na*, containing long-precision real numbers.

*idiag* is the array, referred to as IDIAG, containing the relative positions of the diagonal elements of matrix *A* in output array *A*. Returned as: a one-dimensional array of (at least) length *n*+1, containing fullword integers.

## Notes

- 1. Your various arrays must have no common elements; otherwise, results are unpredictable.
- 2. The ITRAN(3) argument allows you to specify the direction of travel through matrix *A* that ESSL takes during the transformation. By properly specifying ITRAN(3), you can optimize the performance of the transformation, which is especially beneficial when transforming large matrices.
  The direction specified by ITRAN(3) should be opposite the most recent direction of access through the matrix performed by the DSKFS or DSKFSP subroutine, as indicated in the following table:

| Most Recent Computation Performed by DSKFS/DSKFSP | Direction Used by DSKFS/DSKFSP | Direction to Specify in ITRAN(3) |
|:---|:---|:---|
| **Factor and Solve** | Negative | Positive (ITRAN(3) = 1) |
| **Factor Only** | Positive | Negative (ITRAN(3) = -1) |
| **Solve Only** | Negative | Positive (ITRAN(3) = 1) |

- 3. For a description of how sparse matrices are stored in skyline storage mode, see “Profile-In Skyline Storage Mode” on page 99 and “Diagonal-Out Skyline Storage Mode” on page 97.

- 4. You have the option of having the minimum required value for $n\_aux$ dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSL” on page 32.

# Function

A symmetric sparse matrix $A$ stored in diagonal-out or profile-in skyline storage mode is converted to either of these same two storage modes. (Generally, you convert from one to the other, but the capability exists to specify the same storage mode for input and output.) The argument ITRAN(3) indicates the direction in which you want the transformation performed on matrix $A$, allowing you to optimize your performance in this subroutine. This is especially beneficial for large matrices.

This subroutine is meant to be used in conjunction with DSKFS and DSKFSP, which process matrices stored in these skyline storage modes.

# Error Conditions

**Resource Errors:** Error 2015 is unrecoverable, $n\_aux = 0$, and unable to allocate work area.

**Computational Errors:** None

**Input-Argument Errors:**

- 1. $n < 0$
- 2. $na < 0$
- 3. IDIAG($n+1$) $> na+1$
- 4. IDIAG($i+1$) $\leq$ IDIAG($i$) for $i = 1, n$
- 5. IDIAG($i+1$) $>$ IDIAG($i-1$)+$i$ and ITRAN(1) $= 0$ for $i = 1, n$
- 6. IDIAG($i$) $>$ IDIAG($i-1$)+$i$ and ITRAN(1) $= 1$ for $i = 2, n$
- 7. ITRAN(1) $\neq$ 0 or 1
- 8. ITRAN(2) $\neq$ 0 or 1
- 9. ITRAN(3) $\neq$ –1 or 1
- 10. $n\_aux$ Error 2015 is recoverable or $n\_aux \neq$0, and is too small—that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.

# Example 1

This example shows how to convert a 9 by 9 symmetric sparse matrix $A$ from diagonal-out skyline storage mode to profile-in skyline storage mode. Matrix $A$ is:

[11.0 12.0 13.0 14.0 0.0 0.0 0.0 0.0 0.0]
[12.0 22.0 23.0 24.0 25.0 26.0 0.0 0.0 0.0]
[13.0 23.0 33.0 34.0 35.0 36.0 0.0 38.0 0.0]
[14.0 24.0 34.0 44.0 45.0 46.0 0.0 48.0 0.0]
[0.0 25.0 35.0 45.0 55.0 56.0 57.0 58.0 0.0]
[0.0 26.0 36.0 46.0 56.0 66.0 67.0 68.0 69.0]
[0.0 0.0 0.0 0.0 57.0 67.0 77.0 78.0 79.0]
[0.0 28.0 38.0 48.0 58.0 68.0 78.0 88.0 89.0]
[0.0 0.0 0.0 0.0 0.0 69.0 79.0 89.0 99.0]

Assuming that DSKFS last performed a factorization on matrix $A$, the direction of the transformation is negative; that is, ITRAN(3) is –1. This provides the best performance here.

Call Statement and Input:

```
                  N  A  NA    IDIAG  ITRAN   AUX    NAUX
                  |  |  |      |      |       |       |
   CALL DSKTRN( 9 , A , 33 , IDIAG , ITRAN , AUX , 9  )

   A          = (11.0, 22.0, 12.0, 33.0, 23.0, 13.0, 44.0, 34.0, 24.0,
                 14.0, 55.0, 45.0, 35.0, 25.0, 66.0, 56.0, 46.0, 36.0,
                 26.0, 77.0, 67.0, 57.0, 47.0, 88.0, 78.0, 68.0, 58.0, 48.0,
                 38.0, 28.0, 99.0, 89.0, 79.0, 69.0)
   IDIAG      = (1,  2,  4,  7,  11,  15,  20,  23, 30, 34)
   ITRAN      = (0, 1, -1)
```

Output:

```
   A          = (11.0, 12.0, 22.0, 13.0, 23.0, 33.0, 14.0, 24.0, 34.0,
                 44.0, 25.0, 35.0, 45.0, 55.0, 26.0, 36.0, 46.0, 56.0,
                 66.0, 57.0, 67.0, 77.0, 28.0, 38.0, 48.0, 58.0, 68.0,
                 78.0, 88.0, 69.0, 79.0, 89.0, 99.0)
   IDIAG      = (1,  3,  6, 10, 14, 19, 22, 29, 33, 34)
```

# Example 2

This example shows how to convert the same 9 by 9 symmetric sparse matrix $A$ in Example 1 from profile-in skyline storage mode to diagonal-out skyline storage mode.

Assuming that DSKFS last performed a solve on matrix $A$, the direction of the transformation is positive; that is, ITRAN(3) is 1. This provides the best performance here.

Call Statement and Input:

```
                  N  A  NA    IDIAG  ITRAN   AUX    NAUX
                  |  |  |      |      |       |       |
   CALL DSKTRN( 9 , A , 33 , IDIAG , ITRAN , AUX , 9  )

   A          =(same as output A in Example 1)
   IDIAG      =(same as output IDIAG in Example 1)
   ITRAN      = (1,  0,  1)
```

Output:

```
   A          =(same as input A in Example 1)
   IDIAG      =(same as input IDIAG in Example 1)
```

# Part 3. Appendixes

# Appendix A. Basic Linear Algebra Subprograms (BLAS)

This appendix lists the ESSL subprograms corresponding to a subprogram in the standard set of BLAS.

## Level 1 BLAS

Table 180. Level 1 BLAS Included in ESSL

## Level 2 BLAS

Table 181. Level 2 BLAS Included in ESSL

| Descriptive Name | Short- Precision Subprogram | Long- Precision Subprogram |
|---|---|---|
| Rank-One Update of a Real Symmetric or Complex Hermitian Matrix | SSPR CHPR SSYR CHER | DSPPR ZHPPR DSYR ZHER |
| Rank-Two Update of a Real Symmetric or Complex Hermitian Matrix | SSPR2 CHPR2 SSYR2 CHER2 | DSPPR2 ZHPPR2 DSYR2 ZHER2 |
| Matrix-Vector Product for a General Band Matrix, Its Transpose, or Its Conjugate Transpose | SGBMV CGBMV | DGBMV ZGBMV |
| Matrix-Vector Product for a Real Symmetric or Complex Hermitian Band Matrix | SSBMV CHBMV | DSBMV ZHBMV |
| Matrix-Vector Product for a Triangular Matrix, Its Transpose, or Its Conjugate Transpose | STPMV CTPMV STRMV CTRMV | DTPMV ZTPMV DTRMV ZTRMV |
| Solution of a Triangular System of Equations with a Single Right-Hand Side | STPSV CTPSV STRSV CTRSV | DTPSV ZTPSV DTRSV ZTRSV |
| Matrix-Vector Product for a Triangular Band Matrix, Its Transpose, or Its Conjugate Transpose | STBMV CTBMV | DTBMV ZTBMV |
| Triangular Band Equation Solve | STBSV CTBSV | DTBSV ZTBSV |

## Level 3 BLAS

Table 182. Level 3 BLAS Included in ESSL.

| Descriptive Name | Short- Precision Subprogram | Long- Precision Subprogram |
|---|---|---|
| Combined Matrix Multiplication and Addition for General Matrices, Their Transposes, or Conjugate Transposes | SGEMM CGEMM | DGEMM ZGEMM |
| Matrix-Matrix Product Where One Matrix is Real or Complex Symmetric or Complex Hermitian | SSYMM CSYMM CHEMM | DSYMM ZSYMM ZHEMM |
| Triangular Matrix-Matrix Product | STRMM CTRMM | DTRMM ZTRMM |
| Rank-K Update of a Real or Complex Symmetric or a Complex Hermitian Matrix | SSYRK CSYRK CHERK | DSYRK ZSYRK ZHERK |
| Rank-2K Update of a Real or Complex Symmetric or a Complex Hermitian Matrix | SSYR2K CSYR2K CHER2K | DSYR2K ZSYR2K ZHER2K |
| Solution of Triangular Systems of Equations with Multiple Right-Hand Sides | STRSM CTRSM | DTRSM ZTRSM |
