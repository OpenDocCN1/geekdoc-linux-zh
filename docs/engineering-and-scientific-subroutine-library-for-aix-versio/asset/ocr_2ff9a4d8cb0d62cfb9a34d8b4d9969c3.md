# **SYPEV, DSPEV, CHPEV, and ZHPEV—Eigenvalues and, Optionally, the Eigenvectors of a Real Symmetric Matrix or a Complex Hermitian Matrix**

SSPEV and DSPEV compute the eigenvalues and, optionally, the eigenvectors of real symmetric matrix $A$, stored in lower- or upper-packed storage mode. CHPEV and ZHPEV compute the eigenvalues and, optionally, the eigenvectors of complex Hermitian matrix $A$, stored in lower- or upper-packed storage mode. Eigenvalues are returned in vector $w$, and eigenvectors are returned in matrix $Z$:

Az = wZ

where $A = A^{T}$ or $A = A^{H}$.

**Table 131. Data Types**

| $A, z$ | $w, aux$ | Subroutine |
|---|---|---|
| Short-precision real | Short-precision real | SSPEV${}^{a}$ |
| Long-precision real | Long-precision real | DSPEV${}^{a}$ |
| Short-precision complex | Short-precision real | CHPEV${}^{a}$ |
| Long-precision complex | Long-precision real | ZHPEV${}^{a}$ |

${}^{a}$Not LAPACK. Although this subroutine has the same name as an existing LAPACK subroutine, its calling-sequence arguments and functionality are different from that LAPACK subroutine.

Note: For compatibility with earlier releases of SSSL, you can use the names SSLEV, DSLEV, CHLEV, and ZHLEV for SSPEV, DSPEV, CHPEV, and ZHPEV, respectively.

# **Syntax**

| Fortran | `CALL SSPEV \| DSPEV \| CHPEV \| ZHPEV (i opt, ap, w, z, ldz, n, aux, naux)` |
| C and C++ | `sspev \| dspev \| chpev \| zhpev (i opt, ap, w, z, ldz, n, aux, naux);` |

# **On Entry:**

+   - $i opt$ indicates the type of computation to be performed, where:
+     - If $i opt = 0$ or 20, eigenvalues only are computed.
+     - If $i opt = 1$ or 21, eigenvalues and eigenvectors are computed.
+     - Specified as: a fullword integer; $i opt = 0, 1, 20$, or 21.

+   - $ap$ is the real symmetric or complex Hermitian matrix $A$ of order $n$, whose eigenvalues and, optionally, eigenvectors are computed. It is stored in an array, referred to as AP, where:
+     - If $i opt = 0$ or 1, it is stored in lower-packed storage mode.
+     - If $i opt = 20$ or 21, it is stored in upper-packed storage mode.
+     - Specified as: a one-dimensional array of (at least) length $n (n+1) / 2$, containing numbers of the data type indicated in Table 131. On output, for SSPEV and DSPEV if $i opt = 0$ or 20, and for CHPEV and ZHPEV, AP is overwritten; that is, the original input is not preserved.

+   - $w$ See “On Return” on page 717.
+   - $z$ See “On Return” on page 717.