
## Table 7-1 Interface Libraries and Modules (continued)

| File name | Contains |
|---|---|
| mkl95_precision.mod¹ | Fortran 95 definition of precision parameters for BLAS95 and LAPACK95, identical to f95_precision.mod. To be removed in one of the future releases. |

- 1. Prebuilt for the Intel® Fortran compiler
- 2. FFTW3 interfaces are integrated with Intel MKL. Look into <mkl directory>/interfaces/fftw3x*/makefile for options defining how to build and where to place the standalone library with the wrappers.

See Fortran 95 Interfaces to LAPACK and BLAS, which shows how to generate these libraries and modules.

See Appendix G in the Intel MKL Reference Manual for details of FFTW to Intel MKL wrappers.

## Fortran 95 Interfaces to LAPACK and BLAS

Fortran 95 interfaces are compiler-dependent. Intel MKL provides the interface libraries and modules precompiled with the Intel® compiler. Additionally, the Fortran 95 interfaces and wrappers are delivered as sources. (For more information, see Compiler-dependent Functions and Fortran 90 Modules). If you are using a different compiler, build the appropriate library and modules with your compiler and link the library as a user's library:

- 1. Go to the respective directory <mkl_directory>/interfaces/blas95 or <mkl_directory>/interfaces/lapack95
- 2. Type one of the following commands:

```
make libem32t [interface=lp64|ilp64]          for the IA-32 architecture.
INSTALL_DIR=<user_dir>                       for the Intel® 64 architecture.
make lib64 [interface=lp64|ilp64]             for the IA-64 architecture.
INSTALL_DIR=<user_dir>
```

> NOTE. Parameter INSTALL_DIR is required.

As a result, the resulting library will be built and installed in the <user dir>/lib/<arch> directory, and the .mod files will be built and installed in the <user dir>/include/<arch>/{lp64 | ilp64}] directory, where <arch> is one of {32, em64, 64}.

By default, the ifort compiler is assumed. You may change the compiler command name with an additional parameter of make: FC=<compiler>.

## 7 Intel® Math Kernel Library User's Guide

For example, command

```
libem64t FC=pgf95_DIR=<user_pgf95_dir> interface=lp64
```

builds the required library .mod files and installs them in subdirectories of <user_pgf95_dir>.

There is also a way to use the interfaces when building the libraries.

To delete the library from the building directory, use the following commands:

```
make clean32 INSTALL_DIR=<user_dir>           for the IA-32 architecture.
make clean64t INSTALL_DIR=<user_dir>     for the Intel® 64 architecture.
make clean64 INSTALL_DIR=<user_dir>      for the IA-64 architecture.
make clean INSTALL_DIR=<user_dir>        for all the architectures.
```

![](img/78e923baedeba397a89d376927830122_75_0.png)

> NOTE. Setting INSTALL_DIR=../ or INSTALL_DIR=<mki_directory> in a build or clean command will replace or delete the Intel MKL prebuilt Fortran 95 library and modules. This is only possible if you have administrative rights, you are strongly discouraged from doing this.

## Compiler-dependent functions and Fortran 90 Modules

Compiler-dependent functions occur whenever the compiler places functions into the object code function calls that are resolved in its run-time library (RTL). Linking of code without the appropriate RTL will result in undefined symbols. Intel MKL has been designed to minimize RTL dependencies.

Where dependencies occur, a supporting RTL is shipped with Intel MKL. The examples of RTLs, except those relevant to the Intel MKL cluster software, are libomp and libguide, which are the libraries for the OpenMP® code compiled with an Intel® compiler. Both libomp and libguide support the threaded code in Intel MKL.

In other cases RTL dependencies might arise, the functions are delivered as source code and you need to compile the code with whatever compiler you are using for your application.

In particular, Fortran 90 modules result in the compiler-specific code generation requiring RTL support, so, Intel MKL delivers these modules as source code.

## Mixed-language Programming with Intel® MKL

Appendix A lists the programming languages supported for each Intel MKL function domain. However, you can call Intel MKL routines from different language environments. This section explains how to do this using mixed-language programming.

## Calling LAPACK, BLAS, and CBLAS Routines from C Language Environments

Not Intel MKL function domains support both C and Fortran environments. To use Intel MKL Fortran-style functions in C/C++ environments, you should observe conventions, which are discussed for LAPACK and BLAS in the subsections below.

> WARNING. Avoid calling BLAS95/LAPACK95 from C/C++. Such calls require skills in manipulating the descriptor of a deferred-shape array, which is the Fortran 90 type. Moreover, BLAS95/LAPACK95 routines contain links to a Fortran RTL.

## LAPACK

Because LAPACK routines are Fortran-style, when calling them from C, you must follow the following:

- * Pass variables by address instead of by value.
- * Store data in column-major order rather than row-major.

## 7 Intel® Math Kernel Library User's Guide

Figure 7-1 Column-major versus Row-major

| | Column-major | Row-major |
|---|---|---|
| 1 | A(1,1) | A(1,1) |
| 2 | A(2,1) | A(1,2) |
| 3 | A(3,1) | A(1,3) |
| 4 | A(1,2) | A(2,1) |
| 5 | A(2,2) | A(2,2) |
| 6 | A(3,2) | A(2,3) |
| 7 | A(1,3) | A(3,1) |
| 8 | A(2,3) | A(3,2) |
| 9 | A(3,3) | A(3,3) |

When calling LAPACK from C, be aware that because the Fortran language is case-insensitive, the routine names can be both upper-case and lower-case, with or without the underscore. For example, these names are equivalent: getrf, GETRF_.

## BLAS

BLAS routines are Fortran-style. If calling them from C, you must follow the following:

- * Pass variables by address instead of by value.
- * Store data in column-major order rather than row-major.

Refer to the LAPACK section for details of these conventions. See Example 7-2 for BLAS.

## CBLAS

Instead of calling BLAS routines from C-language, you can use the CBLAS interface.

BLAS is a C-style interface to the BLAS routines. You can call CBLAS routines using regular C-style. When using the CBLAS interface, the header file mkl.h will simplify the program development because it features enumerated values as well as prototypes of all the functions. The header determines if the program is compiled with a C++ compiler, and if it is, the included file will be correct for C++.

Example 7-3

 Using Complex Types in C/C++

As described in the Building Applications document for the Intel® Fortran Compiler, C/C++ does not directly implement the Fortran types COMPLEX(4) and COMPLEX(8). However, you can write equivalent structures.

Intel MK provides complex types MKL_Complex8 and MKL_Complex16, which are structures equivalent to the Fortran types COMPLEX(4) and COMPLEX(8), respectively. These types are defined in the mkl_types.h header file. You can also define the types with your own types before including the mkl_types.h header file. The only requirement is that the types must be compatible with the Fortran layout, as the complex type must be a pair of real numbers and imaginary parts.
