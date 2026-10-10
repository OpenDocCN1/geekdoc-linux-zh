If naux = 0 and error 1015 is unrecoverable, DSKFS dynamically allocates the work area used by this subroutine. The work area is deallocated before control is returned to the calling program.

Otherwise, If you are doing a factor only, you can use naux ≥ n; however, for optimal performance, use naux ≥ 3n.

If you are doing a factor and solve or a solve only, use naux ≥ 3n+4mbx. For further details on error handling and the special factor-only case, see “Notes” on page 626.

bx has the following meaning, where:

If you are doing a factor and solve or a solve only, bx is the array, containing the mbx right-hand side vectors b of the system Ax = b. Each vector b is length n and is stored in the corresponding column of the array.

If you are doing a factor only, this argument is not used in the computation.

Specified as: an ldbx by (at least) mbx array, containing long-precision real numbers.

ldbx has the following meaning, where:

If you are doing a factor and solve or a solve only, ldbx is the leading dimension of the array specified for bx.

If you are doing a factor only, this argument is not used in the computation.

Specified as: a fullword integer; ldbx ≥ n and: If mbx ≠ 0, then ldbx > 0. If mbx = 0, then ldbx ≥ 0.

mbx has the following meaning, where:

If you are doing a factor and solve or a solve only, mbx is the number of right-hand side vectors, b, in the array specified for bx.

If you are doing a factor only, this argument is not used in the computation.

Specified as: a fullword integer; mbx ≥ 0.

# On Return:

a is the array, referred to as h, containing the upper triangular part of symmetric sparse matrix A in LDL^T or R^TR factored form, where: If IPARM(5) = 0, diagonal-out skyline storage mode is used for A. If IPARM(5) = 1, profile-in skyline storage mode is used for A.

(If mbx = 0 and you are doing a solve only, then a is unchanged on output.) Returned as: a one-dimensional array of (at least) length na, containing long-precision real numbers.

idiag is the array, referred to as IDIAG, containing the relative positions of the diagonal elements of the factored output matrix A in array h. (If mbx = 0 and you are doing a solve only, then idiag is unchanged on output.) Returned as: a one-dimensional array of (at least) length n+1, containing fullword integers.