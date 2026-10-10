# Table 1. Summary of ESSL Subroutines

| ESSL Area of Computation | Integer<br>Subroutines | Short-Precision<br>Subroutines | Long-Precision<br>Subroutines |
| :--- | :---: | :---: | :---: |
| **Linear Algebra Subprograms:** |  |  |  |
| Vector-scalar | 0 | 41 | 41 |
| Sparse vector-scalar | 0 | 11 | 11 |
| Matrix-vector | 1 | 32 | 32 |
| Sparse matrix-vector | 0 | 0 | 3 |
| **Matrix Operations:** |  |  |  |
| Addition, subtraction, multiplications, rank-k updates, rank-2k updates, and matrix transposes | 0 | 25 | 26 |
| **Linear Algebraic Equations:** |  |  |  |
| Dense linear algebraic equations | 3 | 49 | 54 |
| Banded linear algebraic equations | 0 | 18 | 18 |
| Sparse linear algebraic equations | 0 | 0 | 11 |
| Linear least squares | 0 | 3 | 5 |
| **Eigensystem Analysis:** |  |  |  |
| Solutions to the algebraic eigensystem analysis problem and the generalized eigensystem analysis problem | 0 | 8 | 8 |
| **Signal Processing Computations:** |  |  |  |
| Fourier transforms | 0 | 15 | 11 |
| Convolutions and correlations | 0 | 10 | 2 |
| Related computations | 0 | 6 | 6 |
| **Sorting and Searching:** |  |  |  |
| Sorting, sorting with index, and binary and sequential searching | 5 | 5 | 5 |
| **Interpolation:** |  |  |  |
| Polynomial and cubic spline interpolation | 0 | 4 | 4 |
| **Numerical Quadrature:** |  |  |  |
| Numerical quadrature on a set of points or on a function | 0 | 6 | 6 |
| **Random Number Generation:** |  |  |  |
| Generating vectors of uniformly distributed and normally distributed random numbers | 0 | 3 | 3 |
| **Utilities:** |  |  |  |
| General service operations | 8 | 0 | 3 |
| **Total ESSL Subroutines** | 13 | 236 | 249 |


# ESSL—Processing Capabilities

ESSL provides two run-time libraries, the ESSL SMP Library and the ESSL Serial Library. These libraries are designed to provide high levels of performance for numerically intensive computing jobs on the IBM @server pSeries and RS/6000 processors.