If IPARM(2) = 1, 11, 101, or 111, then $0 \leq \text{IPARM}(3) \leq n$  
IPARM(4), IPARM(5) = 0 or 1

If IPARM(2) = 0, 1, 10, or 11, then:

+   * IPARM(10) = 0 or 1
+   * IPARM(11), IPARM(12) = −1, 0, or 1
+   * IPARM(13) = −1 or 1
+   * IPARM(14), IPARM(15) = −1, 0, or 1

If IPARM(2) = 100, 101, 110, or 111, then:

+   * IPARM(10) = 0 or 1
+   * IPARM(11), IPARM(12), IPARM(13) = −1 or 1
+   * IPARM(14), IPARM(15) = −1, 0, or 1

*rparm* is an array of parameters, RPARM(*i*), where:

+   * RPARM(1) through RPARM(9) are reserved.

+   * RPARM(10) has the following meaning, where:
+       * If you are doing a **factor and solve** or a **factor only**, RPARM(10) is the tolerance value for small pivots. This sets the bounds for the pivot regions, where pivots are processed according to the options you specify for the five regions in IPARM(11) through IPARM(15), respectively. The suggested value is $10^{-15} \leq \text{RPARM}(10) \leq 1$.
+       * If you are doing a **solve only**, this argument is not used.

+   * RPARM(11) through RPARM(15) have the following meaning, where:
+       * If you are doing a **factor and solve** or a **factor only**, RPARM(11) through RPARM(15) are the fix-up values to use for the pivots in regions 1 through 5, respectively. For each RPARM(10+*i*) for $i = 1, 5$, where the pivot occurs in region *i*:
+           * If IPARM(10+*i*) = 1, the pivot is replaced with RPARM(10+*i*), where |RPARM(10+*i*)| should be a sufficiently large nonzero value to avoid overflow when calculating the reciprocal of the pivot. For Gaussian elimination, the suggested value is $10^{-15} \leq |\text{RPARM}(10+i)| \leq 1$. For Cholesky decomposition, the value must be RPARM(10+*i*) > 0.
+           * If IPARM(10+*i*) ≠ 1, RPARM(10+*i*) is not used.

+   * If you are doing a **solve only**, these arguments are not used.

+   * RPARM(16) through RPARM(25), see “On Return” on page 624.

Specified as: a one-dimensional array of (at least) length 25, containing long-precision real numbers, where if IPARM(2) = 0, 1, 10, 11, 100, 101, 110, or 111, then:

+   * RPARM(10) ≥ 0
+   * If IPARM(2) = 0, 1, 10, or 11, then RPARM(11) through RPARM(15) ≠ 0.0
+   * If IPARM(2) = 100, 101, 110, or 111, then RPARM(11) through RPARM(15) > 0.0

*aux* has the following meaning:

If *aux* = 0 and error 2015 is unrecoverable, *aux* is ignored.

Otherwise, it is the storage work area used by this subroutine. Its size is specified by *naux*.

Specified as: an area of storage, containing long-precision real numbers.

*naux* is the size of the work area specified by *aux*—that is, the number of elements in *aux*.

Specified as: a fullword integer, where: