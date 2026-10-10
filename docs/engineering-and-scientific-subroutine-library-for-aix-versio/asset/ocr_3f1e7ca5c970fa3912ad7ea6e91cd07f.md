z See "On Return."

$ldz$ has the following meaning, where:

If $i opt = 0$, it is not used in the computation.

If $i opt = 1$, it is the leading dimension of the output array specified for $z$.

Specified as: a fullword integer. It must have the following value, where:

If $i opt = 0, \quad l d z>0$.

If $i opt = 1, \quad l d z>0$ and $l d z \geq n$.

$n$ is the order of matrices $A$ and $B$.

Specified as: a fullword integer; $n \geq 0$.

aux has the following meaning:

If $n a u x=0$ and error 2015 is unrecoverable, aux is ignored.

Otherwise, it is a storage work area used by this subroutine. Its size is specified by $n a u x$.

Specified as: an area of storage, containing numbers of the data type indicated in Table 134 on page 736. On output, the contents are overwritten.

$n a u x$ is the size of the work area specified by aux—that is, the number of elements in aux.

Specified as: a fullword integer, where:

If $n a u x=0$ and error 2015 is unrecoverable, SSYGV and DSYGV dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.

Otherwise, It must have the following value, where:

If $i opt = 0, \quad n a u x \geq n$.

If $i opt = 1, \quad n a u x \geq 2 n$.

# On Return:

$w$ is the vector $w$ of length $n$, containing the eigenvalues of the generalized real symmetric eigen-system $A \mathbf{z}=w B \mathbf{z}$ in ascending order. Returned as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 134 on page 736.

$z$ has the following meaning, where:

If $i opt = 0$, it is not used in the computation.

If $i opt = 1$, it is the matrix Z of order $n$, containing the eigenvectors of the generalized real symmetric eigen-system, $A \mathbf{z}=w B \mathbf{z}$. The eigenvectors are normalized so that $\mathbf{Z}^{T} B \mathbf{Z}=I$. The eigenvector in column $i$ of matrix $\mathbf{Z}$ corresponds to the eigenvalue $w_{i}$.

Returned as: an $l d z$ by (at least) $n$ array, containing numbers of the data type indicated in Table 134 on page 736.

# Notes

+   1. When you specify $i opt = 0$, you must specify:
+      * A positive value for $l d z$
+      * A dummy argument for $z$ (see "Example 1" on page 739)