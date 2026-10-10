
# SGEGV and DGEGV

If `opt` = 1, it is the leading dimension of the output array specified for `z`.
Specified as: a fullword integer. It must have the following value, where:
- If `opt` = 0, `ldz` > 0.
- If `opt` = 1, `ldz` ≥ 0 and `ldz` ≥ `n`.

- **n** is the order of matrices **A** and **B**.
  Specified as: a fullword integer; `n` ≥ 0.
- **aux** has the following meaning:
  - If `naux` = 0 and error 2015 is unrecoverable, `aux` is ignored.
  - Otherwise, it is a storage work area used by this subroutine. Its size is specified by `naux`.
  Specified as: an area of storage, containing numbers of the data type indicated in Table 133 on page 731. On output, the contents are overwritten.
- **naux** is the size of the work area specified by `aux`—that is, the number of elements in `aux`.
  Specified as: a fullword integer, where:
  - If `naux` = 0 and error 2015 is unrecoverable, SGEGV and DGEGV dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.
  - Otherwise, `naux` ≥ 3*n*.

### On Return:

- **alpha** is the vector **α** of length `n`, containing the numerators of the eigenvalues of the generalized real eigensystem **Az** = **wBz**. Returned as: a one-dimensional array of (at least) length `n`, containing numbers of the data type indicated in Table 133 on page 731.
- **beta** is the vector **β** of length `n`, containing the denominators of the eigenvalues of the generalized real eigensystem **Az** = **wBz**. Returned as: a one-dimensional array of (at least) length `n`, containing numbers of the data type indicated in Table 133 on page 731.
- **z** has the following meaning, where:
  - If `opt` = 0, it is not used in the computation.
  - If `opt` = 1, it is the matrix **Z** of order `n`, containing the eigenvectors of the generalized real eigensystem **Az** = **wBz**. The eigenvector in column `i` of matrix **Z** corresponds to the eigenvalue $w_i$, computed using the $\alpha_i$ and $\beta_i$ values. Each eigenvector is normalized so that the modulus of its largest element is 1.
  Returned as: an `ldz` by (at least) `n` array, containing numbers of the data type indicated in Table 133 on page 731.

## Notes

1. When you specify `opt` = 0, you must specify:
   - A positive value for `ldz`
   - A dummy argument for `z` (see “Example 1” on page 734)
2. Matrices **A**, **B**, and **Z**, vectors **α** and **β**, and the work area specified for **naux** must have no common elements; otherwise, results are unpredictable. See “Concepts” on page 55.
3. You have the option of having the minimum required value for `naux` dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSL” on page 32.

## Function

The following steps describe the methods used to compute the eigenvalues and, optionally, the eigenvectors of a generalized real eigensystem, **Az** = **wBz**, where **A** and **B** are real general matrices. The methods are based upon Moler and Stewart’s QZ algorithm. You must calculate the resulting eigenvalues **w** based on the two parts returned in vectors **α** and **β**. Each eigenvalue is calculated as follows: $w_i = \alpha_i/\beta_i$ for $\beta_i \neq 0$ and $w_i = *$ for $\beta_i = 0$. Eigenvalues are unordered, except that complex conjugate pairs appear consecutively with the eigenvalue having the positive imaginary part first.

For `iopt` = 0, the eigenvalues are computed as follows:

1. Simultaneously reduce **A** to upper Hessenberg form and **B** to upper triangular form using orthogonal transformations.
2. Reduce **A** from upper Hessenberg form to quasi-upper triangular form while maintaining the upper triangular form of **B** using orthogonal transformations.
3. Compute the eigenvalues of the generalized real eigensystem with **A** in quasi-upper triangular form and **B** in upper triangular form using orthogonal transformations.
4. The numerators and denominators of the eigenvalues are returned in vectors **α** and **β**, respectively.

For `iopt` = 1, the eigenvalues and eigenvectors are computed as follows:

1. Simultaneously reduce **A** to upper Hessenberg form and **B** to upper triangular form using and accumulating orthogonal transformations.
2. Reduce **A** from upper Hessenberg form to quasi-upper triangular form while maintaining the upper triangular form of **B** using and accumulating orthogonal transformations.
3. Compute the eigenvalues of the generalized real eigensystem with **A** in quasi-upper triangular form and **B** in upper triangular form using and accumulating orthogonal transformations.
4. Compute the eigenvectors of the generalized real eigensystem with **A** in quasi-upper triangular form and **B** in upper triangular form using back substitution.
5. The numerators and denominators of the eigenvalues are returned in vectors **α** and **β**, respectively, and the eigenvectors are returned in matrix **Z**.

For more information on these methods, see references [41], [45], [60], [85], [65], [64], [90], [100], and [102]. If `n` is 0, no computation is performed. The results of the computations using short- and long-precision data can vary in accuracy.

These algorithms have a tendency to generate underflows that may hurt overall performance. The system default is to mask underflow, which improves the performance of these subroutines.

## Error Conditions

**Resource Errors:** Error 2015 is unrecoverable, `naux` = 0, and unable to allocate work area.

**Computational Errors:** Eigenvalue (i) failed to converge after (xxx) iterations:

- The eigenvalues $w_j$ ($j = i+1, i+2, \dots, n$) are correct.
- If `iopt` = 1, then **Z** is modified, but no eigenvectors are correct.
- **A** and **B** have been modified.
- The return code is set to 1.
- $i$ and $xxx$ can be determined at run time by use of the ESSL error-handling facilities. To obtain this information, you must use **ERRSET** to change the number of allowable errors for error code 2101 in the ESSL error option table; otherwise, the default value causes your program to terminate when this error occurs. See “What Can You Do about ESSL Computational Errors?” on page 47.

**Input-Argument Errors:**

1. `iopt` $\not=$ 0 or 1
2. $n < 0$
3. $lda \leq 0$
4. $n > lda$
5. $ldb \leq 0$
6. $n > ldb$
7. $ldz \leq 0$ and `iopt` = 1
8. $n > ldz$ and `iopt` = 1
9. Error 2015 is recoverable or $naux=0$, and **naux** is too small—that is, less than the minimum required value. Return code 2 is returned if error 2015 is recoverable.

## Example 1

This example shows how to find the eigenvalues only of a real generalized eigensystem problem, **AZ = wBZ**, where:

- **NAUX** is equal to 3N.
- **AUX** contains 3N elements.
- **LDZ** is set to 1 to avoid an error condition.
- **DUMMY** is used as a placeholder for argument $z$, which is not used in the computation.
- On output, matrices **A** and **B** are overwritten.

**Note:** These matrices are from page 257 in referenced text [64].

**Call Statement and Input:**

```
IOPT     A      LDA    B      LDB    ALPHA    BETA     Z      LDZ    N      AUX      NAUX

CALL DGEGV( 0 , A , 3 , B , 3 , ALPHA , BETA , DUMMY , 1 , 3 , AUX , 9 )
```

$A = \left[ \begin{array}{ccc} 10.0 & 1.0 & 2.0 \\ 1.0 & 3.0 & -1.0 \\ 1.0 & 1.0 & 2.0 \end{array} \right]$

$B = \left[ \begin{array}{ccc} 1.0 & 2.0 & 3.0 \\ 4.0 & 5.0 & 6.0 \\ 7.0 & 8.0 & 9.0 \end{array} \right]$

**Output:**

**ALPHA =** $\left[ \begin{array}{c} (4.778424,\ 0.000000) \\ (-4.760580,\ 0.000000) \\ (2.769466,\ 0.000000) \end{array} \right]$
