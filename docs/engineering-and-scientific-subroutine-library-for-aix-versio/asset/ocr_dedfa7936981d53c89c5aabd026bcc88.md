RPARM(1) is unchanged.

RPARM(2) is unchanged if IPARM(2) = 0 or 2. If IPARM(2) = 1, RPARM(2) contains \(\lambda\), an estimate of the smallest eigenvalue of the iteration matrix.

RPARM(3) contains the estimate of the error of the solution. If the process converged, RPARM(3) \(\le \epsilon\).

Returned as: a one-dimensional array of length 3, containing long-precision real numbers; \(\lambda > 0\).

aux2 is the storage work area used by this subroutine.

If IPARM(3) = 10, aux2 contains the incomplete Cholesky factorization of matrix A.

If IPARM(3) = \(-10\), aux2 is unchanged.

See “Notes” for additional information on aux2. Returned as: an area of storage, containing long-precision real numbers.

# Notes

+   1. When IPARM(3) = \(-10\), this subroutine uses the incomplete Cholesky factorization in aux2, computed in an earlier call to this subroutine. When IPARM(3) = 10, this subroutine computes the incomplete Cholesky factorization and stores it in aux2.

+   2. If you solve the same sparse linear system of equations several times with different right-hand sides using the preconditioned algorithm, specify IPARM(3) = 10 on the first invocation. The incomplete factorization is stored in aux2. You may save computing time on subsequent calls by setting IPARM(3) = \(-10\). In this way, the algorithm reutilizes the incomplete factorization that was computed the first time. Therefore, you should not modify the contents of aux2 between calls.

+   3. Matrix A must have no common elements with vectors x and b; otherwise, results are unpredictable.

+   4. In the iterative solvers for sparse matrices, the relative accuracy \(\epsilon\) (RPARM(1)) must be specified “reasonably” \((10^{-4} \text{ to } 10^{-8})\). The algorithm computes a sequence of approximate solution vectors x that converge to the solution. The iterative procedure is stopped when the norm of the residual is sufficiently small—that is, when: \(\lVert b - A\mathbf{x}\rVert_2 / \lambda\lVert\mathbf{x}\rVert_2 < \epsilon\)

+   where \(\lambda\) is an estimate of the minimum eigenvalue of the iteration matrix, which is either estimated adaptively or given by the user. As a result, if you specify a larger \(\epsilon\), the algorithm takes fewer iterations to converge to a solution. If you specify a smaller \(\epsilon\), the algorithm requires more iterations and computer time, but converges to a more precise solution. If the value you specify is unreasonably small, the algorithm may fail to converge within the number of iterations it is allowed to perform.

+   5. For a description of how sparse matrices are stored in compressed-matrix storage mode, see “Compressed-Matrix Storage Mode” on page 90.

+   6. On output, array AC and vector b are not bitwise identical to what they were on input, because the matrix A and the right-hand side are scaled before starting the iterative process and are unscaled before returning control to the user. In addition, arrays AC and RA may be rearranged on output, but still contain a mathematically equivalent mapping of the elements in matrix A.