# SGEMMS, DGEMMS, CGEMMS, and ZGEMMS

equivalence rules when you want to transpose or conjugate transpose the result of the multiplication computation. When coding the calling sequences for these cases, be careful to code your matrix arguments and dimension arguments in the order indicated by the rule. Also, be careful that you output array, receiving C$^{t}$ or C$^{H}$, has dimensions large enough to hold the resulting transposed or conjugate transposed matrix. See “Example 2” on page 381 and “Example 4” on page 383.

# Error Conditions

+   - **Resource Errors:** Error 2015 is unrecoverable, naux = 0, and unable to allocate work area.
+   - **Computational Errors:** None

+   - **Input-Argument Errors:**
+       1. lda, ldb, ldc ≤ 0
+       2. l, m, n < 0
+       3. l > ldc
+       4. transa, transb ≠ ‘N’ or ‘T’ for SGEMMS and DGEMMS
+       5. transa, transb ≠ ‘N’, ‘T’, or ‘C’ for CGEMMS and ZGEMMS
+       6. transa = ‘N’ and l > lda
+       7. transa = ‘T’ or ‘C’ and m > lda
+       8. transb = ‘N’ and m > ldb
+       9. transb = ‘T’ or ‘C’ and n > ldb
+       10. Error 2015 is recoverable or naux≠0, and naux is too small—that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.

# Example 1

This example shows the computation C=AB, where A, B, and C are contained in larger arrays A, B, and C, respectively. It shows how to code the calling sequence for SGEMMS, but does not use the Strassen algorithm for doing the computation. The calling sequence is shown below. The input and output, other than auxiliary storage, is the same as in “Example 1” on page 381 for SGEMUL.

# Call Statement and Input:

```
A LDA TRANS B LDB TRANS C LDC L M N AUX Naux
CALL SGEMMS ( A, 8, ‘N’, B, 6, ‘N’, C, 7, 6, 5, 4, AUX, 0 )
```

# Example 2

This example shows the computation C=AB$^{H}$, where A and C are contained in larger arrays A and C, respectively, and B is the same size as the array B in which it is contained. The arrays contain complex data. This example shows how to code the calling sequence for CGEMMS, but does not use the Strassen algorithm for doing the computation. The calling sequence is shown below. The input and output, other than auxiliary storage, is the same as in “Example 8” on page 385 for CGEMUL.

# Call Statement and Input:

```
A LDA TRANS B LDB TRANS C LDC L M N AUX Naux
CALL CGEMMS ( A, 4, ‘N’, B, 3, ‘C’, C, 4, 3, 2, 3, AUX, 0 )
```