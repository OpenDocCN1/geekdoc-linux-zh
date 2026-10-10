# SSPSV, DPSV, CHPSV, and ZHPSV

+   • For $i opt = 1, 11, 21,$ or $31$, the eigenvalues and eigenvectors are computed as follows:
+   1. Reduce the real symmetric matrix $\boldsymbol{A}$ (for SPSV and DPSV) or complex Hermitian matrix $\boldsymbol{A}$ (for CHPSV and ZHPSV) to a real symmetric tridiagonal matrix using orthogonal similarity transformations (for SPSV and DPSV) or unitary similarity transforms (for CHPSV and ZHPSV).
+   2. Compute the $m$ smallest eigenvalues or $m$ largest eigenvalues of the real symmetric tridiagonal matrix using a rational variant of the QR method with Newton corrections.
+   3. Compute the corresponding eigenvectors of the real symmetric tridiagonal matrix using inverse iteration.
+   4. Back transform the eigenvectors of the real symmetric tridiagonal matrix to those of the original matrix.
+   5. The eigenvalues are returned in vector $\boldsymbol{w}$ in the first $m$ positions, where the $m$ smallest are placed in ascending order, or the $m$ largest are placed in descending order. The corresponding eigenvectors are returned in matrix $\boldsymbol{Z}.$

# Error Conditions

**Resource Errors**: Error 2015 is unrecoverable, $nau x = 0$, and unable to allocate work area.

**Computational Errors**:

+   1. Eigenvale $(i)$ failed to converge after $(xxx)$ iterations. (The computational error message may occur multiple times with processing continuing after each error, because the number of allowable errors for error code 2114 is set to be unlimuted in the ESSSL error option table.)
+   * The eigenvalue, $w_{j}$, is the best estimate obtained. Any eigenvalues for which this message has not been issued are correct.
+   * $ap$ is modified.
+   * The return code is set to $1$.
+   * $i$ and $xxx$ can be determined at run time by use of the ESSSL error-handling facilities. To obtain this information, you must use ERRSET to change the number of allowable errors for error 2199 in the ESSSL error option table. See "What Can You Do about ESSL Computational Errors?" on page 47.
+   2. Eigenvector $(i)$ failed to converge after $(xxx)$ iterations. (The computational error message may occur multiple times with processing continuing after each error, because the number of allowable errors for error code 2102 is set to be unlimuted in the ESSSL error option table.)
+   * All eigenvalues are correct.
+   * The eigenvector that failed to converge is set to zero; however, any selected eigenvectors for which this message is not issued are correct.
+   * $ap$ is modified.
+   * The return code is set to 2.
+   * $i$ and $xxx$ can be determined at run time by use of the ESSSL error-handling facilities. To obtain this information, you must use ERRSET to change the number of allowable errors for error 2199 in the ESSSL error option table. See "What Can You Do about ESSL Computational Errors?" on page 47.

**Input-Argument Errors**:

+   1. $i opt \ne 0$, 1, 10, 11, 20, 21, 30, or 31
+   2. $n < 0$
+   3. $m < 0$
+   4. $m > n$
+   5. $ldz \le 0$ and $i opt = 1, 11, 21,$ or 31
+   6. $n > ldz$ and $i opt = 1, 11, 21,$ or 31