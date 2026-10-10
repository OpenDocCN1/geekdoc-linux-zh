# SSPSV, DPSV, CHPSV, and ZHPSV—Extreme Eigenvalues and, Optionally, the Eigenvectors of a Real Symmetric Matrix or a Complex Hermitian Matrix

SSPSV and DPSV compute the extreme eigenvalues and, optionally, the eigenvectors of real symmetric matrix A, stored in lower- or upper-packed storage mode. CHPSV and ZHPSV compute the extreme eigenvalues and, optionally, the eigenvectors of complex Hermitian matrix A, stored in lower- or upper-packed storage mode. The extreme eigenvalues are returned in vector w, and the corresponding eigenvectors are returned in matrix Z:

Az = wZ

where A = A<sup>T</sup> or A = A<sup>H</sup>.

**Table 132. Data Types**

| A, z | w, aux | Subroutine |
|---|---|---|
| Short-precision real | Short-precision real | SSPV<sup>†</sup> |
| Long-precision real | Long-precision real | DPSV<sup>†</sup> |
| Short-precision complex | Short-precision real | CHPSV<sup>†</sup> |
| Long-precision complex | Long-precision real | ZHPSV<sup>†</sup> |

<sup>†</sup>Not LAPACK. Although this subroutine has the same name as an existing LAPACK subroutine, its calling-sequence arguments and functionality are different from that LAPACK subroutine.

> > **Note:** If you want to compute 10% or fewer eigenvalues only, or you want to compute 30% or fewer eigenvalues and eigenvectors, you get better performance if you use _SSPSV_ and _HPSV_ instead of _SPEV_ and _HPEV_, respectively. For all other uses, you should use _SPEV_ and _HPEV_.

# Syntax

| Fortran | CALL SSPSV \| DPSV \| CHPSV \| ZHPSV (*i*opt, *ap*, *w*, *z*, *ldz*, *n*, *m*, *aux*, *naux*) |
|---|---|
| C and C++ | sspsv \| dpspv \| chpsv \| zhpsv (*i*opt, *ap*, *w*, *z*, *ldz*, *n*, *m*, *aux*, *naux*); |

On Entry:

+   - ***i*opt**  indicates the type of computation to be performed, where:
+   
+         - If *i*opt = 0 or 20, the *m* smallest eigenvalues only are computed.
+         - If *i*opt = 1 or 21, the *m* smallest eigenvalues and the eigenvectors are computed.
+         - If *i*opt = 10 or 30, the *m* largest eigenvalues only are computed.
+         - If *i*opt = 11 or 31, the *m* largest eigenvalues and the eigenvectors are computed.
+   
+         Specified as: a fullword integer; *i*opt = 0, 1, 10, 11, 20, 21, 30, or 31.

+   - ***ap***  is the real symmetric or complex Hermitian matrix A of order n, whose m smallest or largest eigenvalues and, optionally, the corresponding eigenvectors are computed. It is stored in an array, referred to as AP, where:
+   
+         - If *i*opt = 0, 1, 10, or 11, it is stored in lower-packed storage mode.
+         - If *i*opt = 20, 21, 30, or 31, it is stored in upper-packed storage mode.