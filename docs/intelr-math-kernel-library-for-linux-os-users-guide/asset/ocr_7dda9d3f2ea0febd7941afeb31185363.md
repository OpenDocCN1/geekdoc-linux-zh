# A Intel Math Kernel Library User's Guide

Table A-1 Language Interfaces Support (continued)

| Function Domain | FORTRAN 77 interface | Fortran 90/95 interface | C/C++ interface |
|---|---|---|--|
| Trigonometric Transform routines | | Yes | Yes |
| Fast Poisson, Laplace, and Helmholtz Solver (Poisson Library) routines | | Yes | Yes |
| Optimization (Trust-Region) Solver routines | Yes | Yes | Yes |
| GMP* arithmetic functions | | | Yes |
| Service routines (including memory allocation) | | | Yes |

† Supported using a mixed language programming call. See Table A-2 for the respective header file.

Table A-2 lists available header files for all Intel MKL function domains.

# Table A-2 Include Files

| Function domain | Fortran | C or C++ |
|---|---|--|
| All function domains | mkl.fi | mkl.h |
| BLAS Routines | blas.f90 | mkl_blas.h |
| | mkl_blas.fi | |
| BLAS-like Extension Transposition Routines | mkl_trans.fi | mkl_trans.h |
| CBLAS Interface to BLAS | mkl_cblas.fi | mkl_cblas.h |
| Sparse BLAS Routines | mkl_spblas.fi | mkl_spblas.h |
| LAPACK Routines | lapack.f90 | mkl_lapack.h |
| | mkl_lapack.fi | |
| ScalAPACK Routines | | mkl_scalapack.h |
| All Sparse Solver Routines | mkl_solver.f90 | mkl_solver.h |
| | mkl_pardiso.f77 | mkl_pardiso.h |
| | mkl_pardiso.f90 | |
| DSS Interface | mkl_dss.fi | mkl_dss.h |
| | mkl_dss.f90 | |
| RCI Iterative Solvers | mkl_rci.fi | mkl_rci.h |
| ILU Factorization | | |
| Optimization Solver Routines | mkl_rci.fi | mkl_rci.h |
| Vector Mathematical Functions | mkl_vml.f77 | mkl_vml.h |
| | mkl_vml.fi | |