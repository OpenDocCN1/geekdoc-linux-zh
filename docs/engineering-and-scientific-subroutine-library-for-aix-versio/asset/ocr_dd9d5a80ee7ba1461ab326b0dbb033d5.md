Otherwise, it is a storage work area used by this subroutine, which is available for use by the calling program between calls to this subroutine. Its size is specified by *aux1*.

Specified as: an area of *storage*, containing long-precision real numbers.

*nau* x 1* is the size of the work area specified by *aux1*—that is, the number of elements in *aux1*.

Specified as: a fullword integer, where:

If *nau* x 1* = 0 and error 2015 is unrecoverable, DSMGCG dynamically allocates the work area used by this subroutine. The work area is deallocated before control is returned to the calling program.

Otherwise, it must have at least the following value, where:

+   - If IPARM(2) = 0, use *nau* x 1* ≥ 7m. - If IPARM(2) > 0, use *nau* x 1* ≥ (k+2)m+k(k+4)+1, where *k* = IPARM(2).

*aux* 2* is the storage work area used by this subroutine. If IPARM(3) = −10, *aux* 2* must contain the incomplete LU factorization of matrix *A*, computed in an earlier call to DSMGCG. The size of *aux* 2* is specified by *nau* x 2*.

Specified as: an area of *storage*, containing long-precision real numbers.

*nau* x 2* is the size of the work area specified by *aux* 2*—that is, the number of elements in *aux* 2*.

Specified as: a fullword integer. When IPARM(3) = 10, *nau* x 2* must have at least the following value: *nau* x 2* ≥ 3+2m+1.5m2(m).

# **On Return:**

*x* is the vector *x* of length *m*, containing the solution of the system *Ax* = *b*. Returned as: a one-dimensional array of (at least) length *m*, containing long-precision real numbers.

*iparm* is an array of parameters, IPARM(*i*), where:

+   - IPARM(1) is unchanged. - IPARM(2) is unchanged. - IPARM(3) is unchanged. - IPARM(4) contains the number of iterations performed by this subroutine. Returned as: a one-dimensional array of length 4, containing fullword integers.

*rparam* is an array of parameters, RPARAM(*i*), where:

+   - RPARAM(1) is unchanged. - RPARAM(2) is reserved. - RPARAM(3) contains the estimate of the error of the solution. If the process converged, RPARAM(3) ≤ RPARAM(1) Returned as: a one-dimensional array of length 3, containing long-precision real numbers.

*aux* 2* is the storage work area used by this subroutine. If IPARM(3) = 10, *aux* 2* contains the incomplete LU factorization of matrix *A*.