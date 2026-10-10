
## Table 21. *List of Numerical Quadrature Subroutines*

| Descriptive Name | Short- Precision Subroutine | Long- Precision Subroutine | Page |
| :--- | :--- | :--- | :--- |
| Numerical Quadrature Performed on a Set of Points | SPTNQ | DFTNQ | 917 |
| Numerical Quadrature Performed on a Function Using Gauss-Legendre Quadrature | SGLNQ† | DGLNQ† | 920 |
| Numerical Quadrature Performed on a Function Over a Rectangle Using Two-Dimensional Gauss-Legendre Quadrature | SGLNQ2† | DGLNQ2† | 922 |
| Numerical Quadrature Performed on a Function Using Gauss-Laguerre Quadrature | SGLGQ† | DGLGQ† | 928 |
| Numerical Quadrature Performed on a Function Using Gauss-Rational Quadrature | SGRAQ† | DGRAQ† | 931 |
| Numerical Quadrature Performed on a Function Using Gauss-Hermite Quadrature | SGHMQ† | DGHMQ† | 935 |

† This subprogram is invoked as a function in a Fortran program.

## Random Number Generation

Random number generation subroutines generate uniformly distributed random numbers or normally distributed random numbers (Table 22).

## Table 22. *List of Random Number Generation Subroutines*

| Descriptive Name | Short- Precision Subroutine | Long- Precision Subroutine | Page |
| :--- | :--- | :--- | :--- |
| Generate a Vector of Uniformly Distributed Random Numbers | SURAND | DURAND | 941 |
| Generate a Vector of Normally Distributed Random Numbers | SNRAND | DNRAND | 944 |
| Generate a Vector of Long Period Uniformly Distributed Random Numbers | SURXOR | DURXOR | 947 |

## Utilities

The utility subroutines perform general service functions that support ESSL, rather than mathematical computations (Table 23).

## Table 23. *List of Utility Subroutines*

| Descriptive Name | Subroutine | Page |
| :--- | :--- | :--- |
| ESSL Error Information-Handler Subroutine | EINFO | 954 |
| ESSL ERRSAV Subroutine for ESSL | ERRSAV | 957 |
| ESSL ERRSET Subroutine for ESSL | ERRSET | 958 |
| ESSL ERRSTR Subroutine for ESSL | ERRSTR | 960 |
| Set the Vector Section Size (VSS) for the ESSL/370 Scalar Library | IVSSET§ | |
| Set the Extended Vector Operations Indicator for the ESSL/370 Scalar Library | IEVOPS§ | |
| Determine the Level of ESSL Installed | IESSL | 961 |
| Determine the Stride Value for Optimal Performance in Specified Fourier Transform Subroutines | STRIDE | 963 |
| Convert a Sparse Matrix from Storage-by-Rows to Compressed-Matrix Storage Mode | DSRSM | 972 |
| For a General Sparse Matrix, Convert Between Diagonal-Out and Profile-In Skyline Storage Mode | DGKTRN | 976 |
| For a Symmetric Sparse Matrix, Convert Between Diagonal-Out and Profile-In Skyline Storage Mode | DSKTRN | 981 |

# Chapter 2. Planning Your Program

This chapter provides information about ESSL that you need when planning your program. Its purpose is to help you in performing the following tasks:

- Selecting an ESSL subroutine
- Avoiding conflicts with internal ESSL routine names that are exported
- Setting up your data
- Setting up your ESSL calling sequences
- Using auxiliary storage in ESSL
- Providing a correct transform length to ESSL
- Getting the best accuracy
- Getting the best performance
- Dealing with errors when using ESSL

## Selecting an ESSL Subroutine

Your choice of which ESSL subroutine to use is based mainly on the functional needs of your program. However, you have a choice of several variations of many of the subroutines. In addition, there are instances where certain subroutines cannot be used. This section describes these variations and limitations. See the answers to each question below that applies to you.

## Which ESSL Library Do You Want to Use?

ESSL provides two run-time libraries:

- The **ESSL SMP Library** provides thread-safe versions of the ESSL subroutines for use on all SMP processors. In addition, a subset of these subroutines are also multithreaded versions; that is, they support the shared memory parallel processing programming model. For a list of the multithreaded subroutines in the ESSL SMP Library, see Table 24 on page 26.
- The **ESSL Serial Library** provides thread-safe versions of the ESSL subroutines for use on all processors. You may choose to use this library if you decide to develop your own multithreaded programs that call the thread-safe ESSL subroutines.

The number of threads you choose to use depends on the problem size, the specific subroutine being called, and the number of physical processors you are running on. To achieve optimal performance, experimentation is necessary; however, picking the number of threads equal to the number of online processors generally provides good performance in most cases. In a few cases, performance may increase if you choose the number of threads to be less than the number of online processors. For more information about thread concepts, see AIX *General Programming Concepts: Writing and Debugging Programs* and reference [86].

The **ESSL SERIAL Library** and the **ESSL SMP Library** support both 32-bit environment and 64-bit environment applications. For details see Chapter 4, "Coding Your Program," on page 107 and Chapter 5, "Processing Your Program," on page 157.

## Table 24. Multithreaded ESSL SMP Subroutines

| Subroutine Names |
| :--- |
| **Vector-Scalar Linear Algebra Subprograms:**<br>SASUM, DASUM, SCASUM, DZASUM<br>SAXPY, DAXPY, CAXPY, ZAXPY<br>SCOPY, DCOPY, CCOPY, ZCOPY<br>SDOT, DDOT, CDOTU, ZDOTU, CDOTC, ZDOTC<br>SNDDOT, DNDDOT<br>SNORM2, DNORM2, CNORM2, ZNORM2<br>SROT, DROT, CROT, ZROT, CSROT, ZDROT<br>SCAL, DSCAL, CSCAL, ZSCAL, CSSCAL, ZDSCAL<br>SSWAP, DSWAP, CSWAP, ZSWAP<br>SVEA, DVEA, CVEA, ZVEA<br>SVES, DVES, CVES, ZVES<br>SVEM, DVEM, CVEM, ZVEM<br>SAX, DYAX, CYAX, ZYAX, CSYAX, ZDYAX<br>SZAXPY, DZAXPY, CZAXPY, ZZAXPY |
| **Matrix-Vector Linear Algebra Subprograms:**<br>SGEMV, DGEMV, CGEMV, ZGEMV<br>SGER, DGER, CGERU, ZGERU, CGERC, ZGERC<br>SSPMV, DSPMV, CHPMV, ZHPMV<br>SSYMV, DSYMV, CHEMV, ZHEMV<br>SSPR, DSPR, CHPR, ZHPR<br>SSYR, DSYR, CHER, ZHER<br>SSPR2, DSPR2, CHPR2, ZHPR2<br>SSYR2, DSYR2, CHER2, ZHER2<br>SGBMV*, DGBMV*<br>CGBMV*, ZGBMV*<br>SSBMV*, DSBMV*<br>CHBMV*, ZHBMV*<br>STRMV, DTRMV, CTRMV, ZTRMV<br>STPMV, DTPMV, CTPMV, ZTPMV<br>STBMV*, DTBMV*<br>CTBMV*, ZTBMV* |
| **Matrix Operations:**<br>SGEADD, DGEADD, CGEADD, ZGEADD<br>SGESUB, DGESUB, CGESUB, ZGESUB<br>SGEMUL, DGEMUL, CGEMUL, ZGEMUL<br>SGEMM, DGEMM, CGEMM, ZGEMM<br>SSYMM, DSYMM, CSYMM, ZSYMM, CHEMM, ZHEMM<br>STRMM, DTRMM, CTRMM, ZTRMM<br>SSYRK, DSYRK, CSYRK, ZSYRK, CHERK, ZHERK<br>SSYR2K, DSYR2K, CSYR2K, ZSYR2K, CHER2K, ZHER2K<br>SGETMI, DGETMI, CGETMI, ZGETMI<br>SGETMO, DGETMO, CGETMO, ZGETMO |
| **Dense Linear Algebraic Equations:**<br>SGESV, DGESV, CGESV, ZGESV<br>SGEE, DGEF, CGEE, ZGEE<br>SGES, DGES, CGES, ZGES<br>SGE2RE, DGE2RE, CGE2RE, ZGE2RE<br>SGE2RS, DGE2RS, CGE2RS, ZGE2RS<br>SP2SV, DP2SV<br>SP2F, DP2F, SP2TF, DP2TF, DP2OF, DP2TTF<br>SP2TRS, DP2TRS<br>SP2SV, DP2SV, CP2SV, ZP2SV<br>SP2SM, DP2SM, CP2SM, ZP2SM<br>SP2PCD, DP2PCD, CP2PCD, ZP2PCD<br>STR2SV, DTR2SV, CTR2SV, ZTR2SV<br>STR2PSV, DTR2PSV, CTR2PSV, ZTR2PSV<br>STR2SM, DTR2SM, CTR2SM, ZTR2SM<br>STR2I, DTR2I, CTR2I, ZTR2I |
| **Sparse Linear Algebraic Equations:**<br>DSRI<sup>a</sup> |

Many of the dense linear algebraic equations and eigensystem analysis subroutines make one or more calls to the multithreaded versions of the matrix-vector linear algebra and matrix operation subroutines shown in this table. SCOSF, DCOSF, SSINF, and DSINF make one or more calls to the multithreaded versions of the Fourier Transform subroutines shown in this table. These subroutines benefit from the increased performance of the multithreaded versions of the ESSL SMP subroutines.

Your performance may be improved by setting the Environment variables:

- **ESSL for AIX** | `export MALLOCMULTIHEAP=true`
- —and—
- `export XLSMPOPTS="spins=0; yields=0"`
- **ESSL for Linux** | `export XLSMPOPTS="spins=0; yields=0"`

For additional information, see the AIX Performance Management Guide and the XLF Manuals.

- \* DSRIS only uses multiple threads when 1PARM(4) = 1 or 2.
- \* The Level 2 Banded BLAS use multiple threads only when the bandwidth is sufficiently large.
- \* Multiple threads are used for the factor or inverse computation.

## What Type of Data Are You Processing in Your Program?

The version of the ESSL subroutine you select should agree with the data you are using. ESSL provides a short- and long-precision version of most of its subroutines processing short- and long-precision data, respectively. In a few cases, it also provides an integer version processing integer data or returning just integer data. The subroutine names are distinguished by a one- or two-letter prefix based on the following letters:

- S for short-precision real
- D for long-precision real
- C for short-precision complex
- Z for long-precision complex
- I for integer

The precision of your data affects the accuracy of your results. This is discussed in “Getting the Best Accuracy” on page 43. For a description of these data types, see “How Do You Set Up Your Scalar Data?” on page 29.

## How Is Your Data Structured? And What Storage Technique Are You Using?

Some subroutines process specific data structures, such as sparse vectors and matrices or dense and banded matrices. In addition, these data structures can be stored using various storage techniques. You should select the proper subroutine on the basis of the type of data structure you have and the storage technique you want to use. If possible, you should use a storage technique that conserves storage and potentially improves performance. For more about storage techniques, see “Setting Up Your Data” on page 29.
