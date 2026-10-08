# Language-specific Usage Options

The Intel® Math Kernel Library (Intel® MKL) provides broad support for Fortran and C/C++ programming. However, not all functions support both Fortran and C interfaces (see Table A-1 in Appendix A). For example, LAPACK has no C interface. You can call functions comprising such domains from C using mixed-language programming.

If you want to use LAPACK or BLAS, which support the Fortran 95 environment, additional effort may be initially required to build compiler-specific interface libraries and modules from the source code provided with Intel MKL.

This chapter focuses on mixed-language programming and the use of language-specific interfaces. It expands upon the use of Intel MKL in C language environments for function domains that provide as as explains usage of language-specific interfaces, specifically the Fortran 95 interfaces to LAPACK and BLAS. The chapter also discusses compiler-dependent functions to explain why Fortran 90 modules are supplied as sources. A separate section guides you through the process of running examples to invoke Intel MKL functions from Java-

# Using Language-Specific Interfaces with Intel® MKL

You can create the following interface libraries and modules using the respective interfaces located in the interfaces directory.

| Table 7-1 Interface Libraries and Modules |
| File name | Contains |
| Libraries, in Intel MKL architecture-specific directories | |
| libmkl_blas95.a¹ | Fortran 95 wrappers for BLAS (BLAS95) for IA-32 architecture. |
| libmkl_blas95_ilp64.a¹ | Fortran 95 wrappers for BLAS (BLAS95) supporting LP64 interface. |