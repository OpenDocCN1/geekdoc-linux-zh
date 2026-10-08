
# Listing Libraries on a Link Line

To link with Intel MKL libraries, specify paths and libraries on the link line as shown below.

![](img/78e923baedeba397a89d376927830122_43_0.png)

> **NOTE.** The syntax is for dynamic linking. For static linking, replace each library name preceded with "-l" with the path to the library file, for example, replace -imkl_core with $MKLPATH/libmkl_core.a, where $MKLPATH is the appropriate user-defined environment variable. See specific examples in the Linking Examples section.

```
files to link
-LMKL path -IMKL include
[-IMKL include/][32|em64c|[il64|ip64]|64/{il64|ip64}]
-lmkl_blas[95|95_ip64|95_ip64]
-lmkl_lapack[95|95_ip64|95_ip64]
<cluster components>
-lmkl_intel_ilp64|intel_ip64|intel_sp2dp[gf|gf_il64|gf_ip64]
-lmkl_{intel_thread|gnu_thread|pgi_thread|sequential]
-lmkl_solver,[ilp64|ip64]
-lmkl_lapack -lmkl_core
-lmomp5-lguide [-lpthread]-[-lm]
```

See Selecting Libraries to Link for details of this syntax usage and recommendations on which libraries to link depending on your Intel MKL usage scenario.
See Working with the Intel Math Kernel Library Cluster Software with linking libraries denoted as <cluster components>.

In case of static linking, include the cluster components, interface, threading, and computational libraries in grouping symbols (for example, -W1,--start-group $MKLPATH/libmkl_cdft.a $MKLPATH/libmkl_blacs_intpi_ilp64.a $MKLPATH/libmkl_intel_ilp64.a $MKLPATH/libmkl_intel_thread.a $MKLPATH/libmkl_core.a -W1,--end-group). See specific examples in the Linking Examples section.

The order of listing libraries on the link line is essential, for the libraries enclosed in the grouping symbols above.

# Selecting Libraries to Link

This recommends which libraries to link depending on your Intel MKL usage scenario and provides details of the linking in subsections:

- Linking for Fortran 95 Interface Libraries
- Linking with Threading Libraries
- Linking with Computational Libraries
- Linking with Compiler RTLs
- Linking with System Libraries
- Linking Examples

# Linking with Fortran 95 Interface Libraries

The libmkl_blas_95.a, libmkl_blas_95_ilp64.a, libmkl_blas_95_ilp64.a, libmkl_lapack_95.a, and libmkl_lapack_95_ilp64.a libraries contain Fortran 95 interfaces for BLAS and LAPACK, respectively, which are compiler-dependent. In the Intel MKL package, they are prebuilt for the Intel compiler. If you are using a different compiler, build these libraries before using the interface. (See Fortran 95 Interfaces to LAPACK and BLAS and Compiler-dependent Functions and Fortran 90 Modules for details on building the libraries and on why source code is dependent in this case.)

# Linking with Threading Libraries

Several compilers that Intel MKL support the OpenMP* threading technology. Starting with version 10.0, Intel MKL supports the implementations of OpenMP* that compilers provide. If an application uses OpenMP* and compiled with such a compiler calls Intel MKL 10.0 or lower, which is threaded with Intel compilers, performance issues and even failures may arise threading libraries from different compilers are not compatible. Starting with Intel MKL 10.0, solutions for these issues are provided from the Threading Layer and the Compiler Support Run-time libraries (RTL).

Threading Layer. Because of the internal structure of the library, threading represents a small amount of code. This is compiled by different compilers (Intel, Gnu and PGI* compilers on Linux*), and you should link in the appropriate threading layer.

RTL. This layer includes run-time libraries of the Intel compiler: the Intel Compatibility OpenMP* run-time library libomp and Intel® Legacy OpenMP* run-time library libguide. The Compatibility library libiomp is an extension of libguide that provides support for one additional threading compiler on Linux (GNU). That is, a program threaded with a GNU compiler can safely be linked with Intel MKL and libiomp and execute efficiently and effectively. So, you are encouraged to use libiomp rather than libguide, and for each scenario to choose the threading libraries and RTL when using Intel MKL (static cases only):

Table 5-2 shows different scenarios, depending on the threading compiler used, and 

# Table 5-2 Selecting Threading Libraries

| Compiler | Threaded? | Threading Layer | RTL Recommended | Comment |
|---|---|---|---|---|
| Intel | Does not matter | libmkml_intel_thread.a | libomp5.so | |
| PGI | Yes | libmkml_pgi_thread.a or libmkml_sequential.a | PGI* supplied | Use of libmkl_sequential_a removes threading from Intel MKL calls. |
| PGI | No | libmkml_intel_thread.a | libomp5.so | |
| PGI | No | libmkml_pgi_thread.a | PGI* supplied | |
| PGI | No | libmkml_sequential.a | None | |
| gnu | Yes | libmkml_gnu_thread.a | libomp5.so or GNU OpenMP run-time library | libomp5 offers superior scaling performance. |
| gnu | Yes | libmkml_sequential.a | None | |
| gnu | No | libmkml_intel_thread.a | libomp5.so | |
| other | Yes | libmkml_sequential.a | None | |
| other | No | libmkml_intel_thread.a | libomp5.so | |

# Linking with Computational Libraries

Typically, with the layered linking model, you must link your application with only one computational library. However, certain Intel MKL function domains require several computational libraries.

For each Intel MKL function domain, Table 5-3 lists computational libraries that you must include. For more information on linking with ScAPACK and Cluster FFTs, see.

# Table 5-3 Computational Libraries to Link, by Function

| Function | IA-32 Architecture | Intel® 64 or IA-64 Architecture |
|---|---|---|---|
| | Static | Dynamic | Static | Dynamic |
| BLAS, CBLAS, LAPACK, VSL, FFT, Trigonometric Functions | libmk_core.a | libmk_lapack.so libmk_core.so | libmk_core.a | libmk_lapack.so libmk_core.so |
| Iterative Sparse Solvers, Trust Region Solver, and GMP routines | libmk_solver.a | libmk_sequential.a | libmk_solver.a | libmk_sequential.a |
|
| Iterative Sparse Solvers, Trust Region Solver, and GMP routines | libmk_core.a | n/a | libmk_solver_lp64.a | libmk_sequential_lp64.a |
| LP64 interface | n/a | n/a | libmk_solver_ilp64.a | libmk_sequential_ilp64.a |
| Direct Sparse Solver/PARDISO Solver | libmk_core.a | libmk_lapack.so libmk_core.so | libmk_core.a | libmk_lapack.so libmk_core.so |

# Table 5-3 Computational Libraries to Link, by Function (continued)

| Function | IA-32 Architecture | Intel® 64 or IA-64 Architecture |
|---|---|---|---|
| ScalAPACK¹ | libmk_scalapack_core.a | libmk_lapack.so libmk_core.so | libmk_scalapack_lp64.a | libmk_sequential_lp64.a |
| | See below | See below | | |
| ScAPACK, ILP64 interface¹ | n/a | n/a | libmk_scalapack_ilp64.a | libmk_sequential_ilp64.a |
| Cluster Fourier Transform Functions¹ | libmk_cdft_core.a | n/a | libmk_cdft_core.a | n/a |

+1. Also add the library with BLACS routines using the used MPI API. For details, see Linking with ScalAPACK and Cluster FFTs.

See also:

Linking with Compiler RTLs.

# Linking with Compiler RTLs

You are strongly encouraged to dynamically link in the Intel Compatibility OpenMP* run-time library libomp or Intel Legacy OpenMP* run-time library libguide. Linking to static OpenMP* run-time library is not recommended because it is very easy with complex software to link in more than one copy of the library (too many threads) and may cause correctness problems if one copy is initialized.

However, if you link with libomp/libguide statically, the version of libomp/libguide you link depends on which compiler you use:
