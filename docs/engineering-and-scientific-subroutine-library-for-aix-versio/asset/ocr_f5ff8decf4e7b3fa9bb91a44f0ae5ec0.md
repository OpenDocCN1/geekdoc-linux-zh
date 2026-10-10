indefinite matrices and triangular matrices. Some of these subroutines correspond to the Level 2 BLAS, Level 3 BLAS, and LAPACK routines described in references [34], [36] and [8].

# *Table 11. List of Dense Linear Algebraic Equation Subroutines*

| Descriptive Name | Short-Precision Subroutine | Long-Precision Subroutine | Page |
|---|---|---|---|
| General Matrix Factorization and Multiple Right-Hand Side Solve | SGE$^{\triangle}$<br>CGES$^{\triangle}$ | DGES$^{\triangle}$<br>ZGES$^{\triangle}$ | 440 |
| General Matrix Factorization | SGET$^{\dagger}$<br>CGET$^{\dagger}$ | DGET$^{\dagger}$<br>ZGET$^{\dagger}$ | 444 |
| | SGES<br>CGES | DGES<br>ZGES | 452 |
| | DGEF<br>ZGEF<br>DGEFF${}^{a}$ | | |
| General Matrix, Its Transpose, or Its Conjugate Transpose<br>Multiple Right-Hand Side Solve | SGES$^{\triangle}$<br>CGES$^{\triangle}$ | DGES$^{\triangle}$<br>ZGES$^{\triangle}$ | 448 |
| | SGESM<br>CGESM | DGESM<br>ZGESM | 459 |
| General Matrix, Its Transpose, or Its Conjugate Transpose Solve | SGES<br>CGES | DGES<br>ZGES | 455 |
| General Matrix Factorization, Condition Number Reciprocal, and Determinant | SGEFCD | DGEFCD | 464 |
| Positive Definite Real Symmetric Matrix Factorization and<br>Multiple Right-Hand Side Solve | SPPSV$^{\triangle}$ | DPYSV$^{\triangle}$ | 468 |
| Positive Definite Real Symmetric or Complex Hermitian Matrix<br>Factorization and Multiple Right-Hand Side Solve | SPOSV$^{\triangle}$<br>CPOSV$^{\triangle}$ | DPOSV$^{\triangle}$<br>ZPOSV$^{\triangle}$ | 472 |
| Positive Definite Real Symmetric or Complex Hermitian Matrix<br>Factorization | SPOT$^{\dagger}$<br>CPOT$^{\dagger}$<br>SPOF<br>CPPTRF$^{\triangle}$<br>SPPF | DPOF$^{\dagger}$<br>ZPOF$^{\dagger}$<br>DPOF<br>ZPOF<br>DPPTRF$^{\triangle}$<br>DPFF<br>DPPFP${}^{a}$ | 477 |
| Positive Definite Real Symmetric or Complex Hermitian Matrix<br>Multiple Right-Hand Side Solve | SPOTS${}^{\triangle}$<br>CPOSS${}^{\triangle}$<br>SPOSM<br>CPOSM<br>SPPTRS${}^{\triangle}$ | DPOTS${}^{\triangle}$<br>ZPOTS${}^{\triangle}$<br>DPOSM<br>ZPOSM<br>DPPTRS${}^{\triangle}$ | 488 |
| Positive Definite Real Symmetric Matrix Solve | SPPS | DPPS | 495 |
| Positive Definite Real Symmetric Matrix Factorization, Condition<br>Number Reciprocal, and Determinant | SPPFCD<br>SPOFCD | DPPFCD<br>DPOFCD | 498 |
| Symmetric Indefinite Matrix Factorization and Multiple<br>Right-Hand Side Solve | | DBSSV | 504 |
| Symmetric Indefinite Matrix Factorization | | DBSTRF | 510 |
| Symmetric Indefinite Matrix Multiple Right-Hand Side Solve | | DBSTRS | 515 |
| General Matrix Inverse, Condition Number Reciprocal, and<br>Determinant | SGET$^{\dagger}$<br>CGET$^{\dagger}$<br>SQEIC | DGET$^{\dagger}$<br>ZGET$^{\dagger}$<br>DGEICD | 519 |
| Positive Definite Real Symmetric or Complex Hermitian Matrix<br>Inverse, Condition Number Reciprocal, and Determinant | SPOT$^{\dagger}$<br>CPO$^{\dagger}$<br>SPPICD<br>SPOICD | DPOT$^{\dagger}$<br>ZPO$^{\dagger}$<br>DPPICD<br>DPOICD | 526 |