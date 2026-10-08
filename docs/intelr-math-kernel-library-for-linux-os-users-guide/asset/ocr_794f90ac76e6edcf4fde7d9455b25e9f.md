# 7 Intel® Math Kernel User's Guide

### Table 7-1 Interface Libraries and Modules (continued)

| File name | Contains |
|---||
| libmkl_blas95_lp64.a¹ | Fortran 95 wrappers for BLAS (BLAS95) supporting ILP64 interface. |
| libmkl_lapack95.a¹ | Fortran 95 wrappers for LAPACK (LAPACK95) for IA-32 architecture. |
| libmkl_lapack95_lp64.a¹ | Fortran 95 wrappers for LAPACK (LAPACK95) supporting LP64 interface. |
| libmkl_lapack95_lp64.a¹ | Fortran 95 wrappers for LAPACK (LAPACK95) supporting ILP64 interface. |
| libffftw2xc_intel.a¹ | Interfaces for FFTW version 2.x (C interface for Intel® compiler) to call Intel MKL FFTs. |
| libffftw2xc_gnu.a | Fortran 95 for FFTW version 2.x (C interface for GNU compiler) to call Intel MKL FFTs. |
| libffftw2xf_intel.a | Fortran 95 for FFTW version 2.x (C interface for Intel compiler) to call Intel MKL FFTs. |
| libffftw2xf_gnu.a | Fortran 95 for FFTW version 2.x (C interface for GNU compiler) to call Intel MKL FFTs. |
| libffftw3xc_intel.a² | Fortran 95 for FFTW version 3.x (C interface for Intel compiler) to call Intel MKL FFTs. |
| libffftw3xc_gnu.a | Fortran 95 for FFTW version 3.x (C interface for GNU compiler) to call Intel MKL FFTs. |
| libffftw3xf_intel.a² | Fortran 95 for FFTW version 3.x (C interface for Intel compiler) to call Intel MKL FFTs. |
| libffftw3xf_gnu.a | Fortran 95 for FFTW version 3.x (C interface for GNU compiler) to call Intel MKL FFTs. |
| libffftw2x_cdft_SINGLE.a | Single-precision interfaces for MPI FFTW version 2.x (c) to call Intel MKL cluster FFTs. |
| libffftw2x_cdft_DOUBLE.a | Double-precision interfaces for MPI FFTW version 2.x (c) to call Intel MKL cluster FFTs. |

**Modules, in architecture- and interface-specific subdirectories of the Intel MKL include directory**

+   * blas95.mod¹ Fortran 95 interface module for BLAS (BLAS95).
* lapack95.mod¹ Fortran 95 interface module for LAPACK (LAPACK95).
* f95_precision.mod¹ Fortran 95 definition of parameters for BLAS95 and LAPACK95.
* mk195_blas.mod¹ Fortran 95 interface module for BLAS (BLAS95), identical to blas95.mod. To be removed in one of the future releases.
* mk195_lapack.mod¹ Fortran 95 interface module for LAPACK (LAPACK95), identical to lapack95.mod. To be removed in one of the future releases.