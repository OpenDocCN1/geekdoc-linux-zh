# **SPOTRF, DPOTRF, CPOTRF, ZPOTRF, SPOF, DPOF, CPOF, ZPOF, SPptrf, DPptrf, SPpf, and Dppf—Positive Definite Real Symmetric or Complex Hermitian Matrix Factorization**

These subroutines factor matrix *A* as explained below:

**SPOTRE, DPOTRE, CPOTRE, ZPOTRE, SPOE, DPOE, CPOE, and ZPOF**

The SPOTRE, DPOTRE, CPOTRE, ZPOTRE, SPOE, DPOE, CPOE, and ZPOF subroutines factor matrix *A* stored in upper or lower storage mode, where:

+   - For SPOTRE, DPOTRE, SPOF, and DPOF, *A* is a positive definite real symmetric matrix.
+   *   For CPOTRE, ZPOTRE, CPOF, and ZPOF, *A* is a positive definite complex Hermitian matrix.

Matrix *A* is factored using Cholesky factorization.

To solve the system of equations with one or more right-hand sides, follow the call to SPOTRE, DPOTRE, CPOTRE, ZPOTRE, SPOE, DPOE, CPOE, or ZPOF with a call to SPOTRS, DPOTRS, CPOTRS, ZPOTRS, SPOSM, DPOSM, CPOSM, or ZPOSM, respectively.

To find the inverse of matrix *A*, follow the call to SPOTRE, DPOTRE, CPOTRE, ZPOTRE, SPOE, or DPOE with a call to SPOTRI, DPOTRI, CPOTRI, ZPOTRI, SPOICD, or DPOICD, respectively.

**SPptrf and DPptrf**

The SPptrf and DPptrf subroutines factor positive definite real symmetric matrix *A*, stored in upper-packed or lower-packed storage mode, using Cholesky factorization. To solve the system of equations with one or more right-hand sides, follow the call to SPptrf or DPptrf with a call to SPptrs or DPptrs, respectively.

**SPpf and Dppf**

The SPpf and Dppf subroutines factor positive definite real symmetric matrix *A*, stored in lower-packed storage mode, using Gaussian elimination (*LL* $L^{\mathrm{T}}$) or Cholesky factorization. To solve a system of equations with one or more right-hand sides, follow the call to these subroutines with one or more calls to SPPS or DPPS, respectively. To find the inverse of matrix *A*, follow the call to these subroutines, performing Cholesky factorization, with a call to SPpICD or DPpICD, respectively.

| Table 100. Data Types | | | |
|---|---|---|---|
| | | *A* | Subroutine |
| | Short-precision real | SPOTRF$^{\triangle}$, SPPTRE$^{\triangle}$, SPPE, and SPOF |
| | Long-precision real | DPOTRE$^{\triangle}$, DPPTRE$^{\triangle}$, DPPE, and DPOF |
| | Short-precision complex | CPOTRF$^{\triangle}$ and CPOF |
| | Long-precision complex | ZPOTRE$^{\triangle}$ and ZPOF |

**Note:** The output from each of these subroutines should be used only as input for specific other subroutines, as shown in the table below.