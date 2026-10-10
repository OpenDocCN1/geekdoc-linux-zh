# Notes

+   1. This subroutine accepts lowercase letters for the *uplo* argument.
+   2. In your C program, argument *nsinfo* must be passed by reference.
+   3. In the input array specified for $ap$, the first $n(n+1)/2$ elements are matrix elements. The additional locations, required in the array, are used for working storage.
+   4. The array specified for $ap$ should not be altered between calls to the factorization and solve subroutines; otherwise, unpredictable results may occur.
+   5. On return, if *nsinfo* $\geq 0$ and $n > nco$, $ap$ contains additional information in $AP(1)$ that can be used to obtain the minimal required *nsinfo*. This information can be accessed using the following code fragment:
+   
+      ```fortran
+      REAL*8 AP(NSINFO)
+      INTEGER API(2)
+      EQUIVALENCE(API, AP)
+      ...
+      NSINFOMIN = API(2)
+      ```
+   
+   6. For a description of how a symmetric matrix is stored in upper- or lower-packed storage mode in an array, see "Symmetric Matrix" on page 64.

# Function

A real symmetric indefinite matrix $\boldsymbol{A}$, stored in upper- or lower-packed storage mode, is factored using the Bunch-Kaufman diagonal pivoting method, where $\boldsymbol{A}$ is expressed as:

```
$\quad \quad \boldsymbol{A} = \boldsymbol{UDU}^t$ or
$\quad \quad \boldsymbol{A} = \boldsymbol{LDL}^t$
```

where:

+   $\boldsymbol{U}$ is a product of permutation and unit upper triangular matrices.
+   $\boldsymbol{L}$ is a product of permutation and unit lower triangular matrices.
+   $\boldsymbol{D}$ is a symmetric block diagonal matrix, consisting of $1 \times 1$ and $2 \times 2$ diagonal blocks.

If $n = 0$, no computation is performed and the subroutine returns after doing some parameter checking.

See references [8] and [67].

# Error Conditions

**Resource Errors:** None.

**Computational Errors:** Matrix $\boldsymbol{A}$ is singular.

+   * The factorization completed but the block diagonal matrix $\boldsymbol{D}$ is exactly singular.
+     * *nsinfo* is set to $i$, where $d_{ii}$ is exactly zero. This diagonal element is identified in the computational error message.
+   * The computational error message may occur multiple times with processing continuing after each error, because the default for the number of allowable errors for error code 2147 is set to be unlimited in the ESSl error option table. For details, see "What Can You Do about ESSl Computational Errors?" on page 47.

**Input-Argument Errors:**

   1. *uplo* $\ne$ 'U' or 'L'
   2. $n < 0$