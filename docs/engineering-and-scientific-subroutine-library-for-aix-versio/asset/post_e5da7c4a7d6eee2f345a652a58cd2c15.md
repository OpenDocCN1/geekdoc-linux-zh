
## SSPEV, DSPEV, CHPEV, and ZHPEV

1. A dummy argument for $z$ (see “Example 1” on page 719).
2. The following items must have no common elements: matrix $A$, matrix $Z$, vector $\boldsymbol{w}$, and the data area specified for aux; otherwise, results are unpredictable. See “Concepts” on page 55.
3. On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix $A$ are assumed to be zero, so you do not have to set these values.
4. For a description of how real symmetric matrices are stored in lower- or upper-packed storage mode, see “Lower-Packed Storage Mode” on page 65 or “Upper-Packed Storage Mode” on page 66, respectively. For a description of how complex Hermitian matrices are stored in lower- or upper-packed storage mode, see “Complex Hermitian Matrix” on page 69.
5. You have the option of having the minimum required value for naux dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSL” on page 32.

### Function

The next two sections describe the methods used to compute the eigenvalues and, optionally, the eigenvectors for either a real symmetric matrix or a complex Hermitian matrix. For more information on these methods, see references [41], [45], [65], [90], [100], and [102]. If $n$ is 0, no computation is performed. The results of the computations using short- and long-precision data can vary in accuracy. See “Example 3” on page 720 and “Example 4” on page 721 for an illustration of the difference in results. Eigenvalues computed using equivalent iopt values are mathematically equivalent, but are not guaranteed to be bitwise identical. For example, the results computed using $iopt=0$ and $iopt=20$ are mathematically equivalent, but are not necessarily bitwise identical.

These algorithms have a tendency to generate underflows that may hurt overall performance. The system default is to mask underflow, which improves the performance of these subroutines.

### Real Symmetric Matrix

The eigenvalues and, optionally, the eigenvectors of a real symmetric matrix $A$ are computed as follows:

- For $iopt=0$ or 20, the eigenvalues are computed as follows:
  1. Reduce the real symmetric matrix $A$ to a real symmetric tridiagonal matrix using orthogonal similarity transformations.
  2. Compute the eigenvalues of the real symmetric tridiagonal matrix using the implicit QL algorithm.
  3. The eigenvalues are ordered and returned in vector $\boldsymbol{w}$.

- For $iopt=1$ or 21, the eigenvalues and eigenvectors are computed as follows:
  1. Reduce the real symmetric matrix $A$ to a real symmetric tridiagonal matrix using and accumulating orthogonal similarity transformations.
  2. Compute the eigenvalues of the real symmetric tridiagonal matrix and the eigenvectors of the real symmetric matrix using the implicit QL algorithm.
  3. The eigenvalues are ordered and returned in vector $\boldsymbol{w}$, and the corresponding eigenvectors are returned in matrix $Z$.

### Complex Hermitian Matrix

The eigenvalues and, optionally, the eigenvectors of a complex Hermitian matrix $A$ are computed as follows:

- For $iopt=0$ or 20, the eigenvalues are computed as follows:
  1. Reduce the complex Hermitian matrix $A$ to a real symmetric tridiagonal matrix using unitary similarity transformations.
  2. Compute the eigenvalues of the real symmetric tridiagonal matrix using the implicit QL algorithm.
  3. The eigenvalues are ordered and returned in vector $\boldsymbol{w}$.

- For $iopt=1$ or 21, the eigenvalues and eigenvectors are computed as follows:
  1. Reduce the complex Hermitian matrix $A$ to a real symmetric tridiagonal matrix using unitary similarity transformations.
  2. Compute the eigenvalues and eigenvectors of the real symmetric tridiagonal matrix using the implicit QL algorithm.
  3. Back transform the eigenvectors of the real symmetric tridiagonal matrix to those of the original complex Hermitian matrix.
  4. The eigenvalues are ordered and returned in vector $\boldsymbol{w}$, and the corresponding eigenvectors are returned in matrix $Z$.

### Error Conditions

**Resource Errors:** Error 2015 is unrecoverable, $n_{aux} = 0$, and unable to allocate work area.

**Computational Errors:** Eigenvalue ($i$) failed to converge after ($xxx$) iterations:

- The eigenvalues ($w_j$, $j = 1, 2, \dots, i-1$) are correct, but are unordered.
- If $iopt = 1$ or 21, then $Z$ is modified, but no eigenvectors are correct.
- If $iopt = 0$ or 20 for SSPEV and DSPEV, $AP$ is modified.
- For CHP EV and ZHP EV, $AP$ is modified.
- The return code is set to 1.
- $i$ and $xxx$ can be determined at run time by use of the ESSL error-handling facilities. To obtain this information, you must use ERRSET to change the number of allowable errors for error code 2101 in the ESSL error option table; otherwise, the default value causes your program to terminate when this error occurs. See “What Can You Do about ESSL Computational Errors?” on page 47.

**Input-Argument Errors:**

1. $iopt \neq 0, 1, 20$, or 21
2. $n < 0$
3. $ldz \leq 0$ and $iopt = 1$ or 21
4. $n > ldz$ and $iopt = 1$ or 21
5. Error 2015 is recoverable or $n_{aux} \neq 0$, and $n_{aux}$ is too small—that is, less than the minimum required value. Return code 2 is returned if error 2015 is recoverable.

### Example 1

This example shows how to find the eigenvalues only of a real short-precision symmetric matrix $A$ of order 3, stored in lower-packed storage mode. Matrix $A$ is:

![](img/5b0f44f3be6048723819b26aed7f6f03_742_0.png)

where:

- NAUX is equal to N.
- AUX contains N elements.
- LDZ is set to 1 to avoid an error condition.
- DUMMY is used as a placeholder for argument $Z$, which is not used in the computation.
- On output, $AP$ has been overwritten.

**Call Statement and Input:**

```fortran
CALL SSPEV(0, AP, W, DUMMY, 1, 3, AUX, 3)
AP = (1.0, -1.0, 0.0, 2.0, -1.0, 1.0)
```

**Output:**

```text
W = [
  0.000000
  1.000000
  3.000000
]
```

### Example 2

This example shows how to find the eigenvalues and eigenvectors of a real short-precision symmetric matrix $A$ of order 4, stored in upper-packed storage mode. Matrix $A$ is:

```text
5.0  4.0  1.0  1.0
4.0  5.0  1.0  1.0
1.0  1.0  4.0  2.0
1.0  1.0  2.0  4.0
```

where:

- NAUX is equal to $2N$.
- AUX contains $2N$ elements.

**Note:** This matrix is used in Example 4.1 in referenced text [65].

**Call Statement and Input:**

```fortran
CALL SSPEV(21, AP, W, Z, 4, 4, AUX, 8)
AP = (5.0, 4.0, 5.0, 1.0, 1.0, 4.0, 1.0, 1.0, 2.0, 4.0)
```

**Output:**

```text
W = [
  1.000000
  2.000000
  5.000000
  9.999999
]

Z = [
  0.707107  0.000000  0.316227  0.632455
 -0.707107  0.000000  0.316228  0.632455
  0.000000 -0.707106 -0.632455  0.316227
  0.000000  0.707107 -0.632455  0.316228
]
```

### Example 3

This example shows how to find the eigenvalues and eigenvectors of a real short-precision symmetric matrix $A$, stored in lower-packed storage mode, which has an eigenvalue of multiplicity 2. Matrix $A$ is:

```text
6.0  4.0  4.0  1.0
4.0  6.0  1.0  4.0
4.0  1.0  6.0  4.0
1.0  4.0  4.0  6.0
```

where:

- NAUX is equal to $2N$.
- AUX contains $2N$ elements.

**Note:** This matrix is used in Example 4.2 in referenced text [65].

**Call Statement and Input:**

```fortran
CALL SSPEV(1, AP, W, Z, 4, 4, AUX, 8)
AP = (6.0, 4.0, 4.0, 1.0, 6.0, 1.0, 4.0, 6.0, 4.0, 6.0)
```

**Output:**

```text
W = [-1.000000, 4.999999, 5.000000, 15.000000]
Z = [ -0.500000  0.000000  0.707107  0.500000
      0.500000 -0.707107  0.000000  0.500000
      0.500000 -0.707107  0.000000  0.500000
     -0.500000  0.000000 -0.707107  0.500000 ]
```

### Example 4

This example shows how the results of Example 3 differ if matrix $A$ is a real long-precision symmetric matrix.

**Call Statement and Input:**

```fortran
CALL DSPEV(1, AP, W, Z, 4, 4, AUX, 8)
```

**Output:**

```text
W = [-1.000000, 5.000000, 5.000000, 15.000000]
Z = [ -0.500000 -0.216773 -0.673060  0.500000
      0.500000  0.673060 -0.216773  0.500000
      0.500000 -0.673060  0.216773  0.500000
     -0.500000  0.216773  0.673060  0.500000 ]
```

### Example 5

This example shows how to find the eigenvalues and eigenvectors of a complex Hermitian matrix $A$ of order 2, stored in lower-packed storage mode. Matrix $A$ is:
