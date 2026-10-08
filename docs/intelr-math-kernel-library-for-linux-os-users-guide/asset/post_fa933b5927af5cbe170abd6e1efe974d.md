
# Table 3-6 Detailed Structure of the Intel® 64 Architecture-specific Directory lib/em64t (continued)

| File | Contents |
|---|---|
| Interface layer | |
| libmkl_gf_ilp64.so | ILP64 interface library for the GNU Fortran and Absoft compilers |
| libmkl_gf_lp64.so | LP64 interface library for the GNU Fortran and Absoft compilers |
| libmkl_intel_ilp64.so | LP64 interface library for the Intel compilers |
| libmkl_intel_lp64.so | LP64 interface library for the Intel compilers |
| libmkl_intel_sp2dp.so | SP2DP interface library for the Intel compilers |
| Threading layer | |
| libmkl_gnu_thread.so | Threading library for the GNU Fortran and C compilers |
| libmkl_intel_thread.so | Threading library for the Intel compilers |
| libmkl_pgi_thread.so | Threading library for the PGI* compiler |
| libmkl_sequential.so | Sequential library |

# 3 Intel Math Kernel Library User's Guide

# Table 3-6 Detailed Structure of the Intel® 64 Architecture-specific Directory lib/em64t (continued)

| File | Contents |
|---|---|
| Computational layer | libmkl_avx.so | Kernel optimized for the Intel® Advanced Vector Extensions (Intel® AVX). |
| libmkl_core.so | Library dispatcher for dynamic load of processor-specific kernel |
| libmkl_def.so | Default kernel library |
| libmkl_mc.so | Kernel library for processors based on the Intel® Core™ microarchitecture |
| libmkl_mc3.so | Kernel library for the Intel® Core™ processors |
| libmkl_lapack.so | LAPACK and DSS/PARDISO routines and drivers |
| libmkl_scalapack_lp64.so | ScLAPACK routine library supporting the LP64 interface |
| libmkl_scalapack_lp64.so | ScLAPACK routine library supporting the LP64 interface |
| libmkl_vml_avx.so | VML/VSL optimized for the Intel® Advanced Vector Extensions (Intel® AVX). |
| libmkl_vml_def.so | VML/VSL part of default kernels |
| libmkl_vml_mc.so | VML/VSL for processors based on the Intel® Core™ microarchitecture |
| libmkl_vml_mc3.so | VML/VSL for the Intel® Core™ processors |
| libmkl_vml_p4n.so | VML/VSL for the Intel® Xeon® processor using the Intel® 64 architecture |
| libmkl_vml_mc2.so | VML/VSL for 45nm Hi-k Intel® Core™2 and Intel® Xeon® families |
| RTL | |
| libguide.so | Intel® Legacy OpenMP* run-time library for dynamic linking |
| libomp5.so | Intel® Compatibility OpenMP* run-time library for dynamic linking |
| libmkl_intelmpi_lp64.so | LP64 version of BLACS routines supporting Intel MPI 2.0/3.x and MPICH2 |
| libmkl_intelmpi_lp64.so | LP64 version of BLACS routines supporting Intel MPI 2.0 and 3.x, and MPICH2 |
| locale/en_US/mkl_msg.cat | Catalog of Intel MKL messages in English |
| locale/ja_JP/mkl_msg.cat | Catalog of Intel MKL messages in Japanese |

# Table 3-7 Detailed Structure of the IA-64 Architecture-specific Directory lib/64

| File | Contents |
| --- | --- |
| **Static Libraries** | |
| *Interface layer* | |
| libmkl_blas95_ilp64.a | Fortran 95 interface library for BLAS for the Intel® Fortran compiler. Supports the ILP64 interface |
| libmkl_blas95_lp64.a | Fortran 95 interface library for BLAS for the Intel® Fortran compiler. Supports the LP64 interface |
| libmkl_intel_ilp64.a | ILP64 interface library for the Intel compilers |
| libmkl_intel_lp64.a | LP64 interface library for the Intel compilers |
| libmkl_intel_sp2dp.a | SP2DP interface library for the Intel compilers |
| libmkl_gf_ilp64.a | ILP64 interface library for the GNU Fortran compiler |
| libmkl_gf_lp64.a | LP64 interface library for the GNU Fortran compiler |
| libmkl_lapack95_ilp64.a | Fortran 95 interface library for LAPACK for the Intel® Fortran compiler. Supports the ILP64 interface |
| libmkl_lapack_lp64.a | Fortran 95 interface library for LAPACK for the Intel® Fortran compiler. Supports the LP64 interface |
| *Threading layer* | |
| libmkl_intel_thread.a | Threading library for the Intel compilers |
| libmkl_gnu_thread.a | Threading library for the GNU Fortran and C compilers |
| libmkl_sequential.a | Sequential library |
| *Computational layer* | |
| libmkl_cdft_core.a | Cluster version of FFTs |
| libmkl_core.a | Kernel library for the IA-64 architecture |
| libmkl_scalapack_ilp64.a | ScLAPACK routine library supporting the ILP64 interface |
| libmkl_scalapack_lp64.a | ScLAPACK routine library supporting the LP64 interface |
| libmkl_solver_ilp64.a | Iterative Sparse Solver and Trust Region Solver library supporting the ILP64 interface |
| libmkl_solver_lp64_sequential.a | Sequential version of Iterative Sparse Solver and Trust Region Solver library supporting the LP64 interface |
| libmkl_solver_lp64.a | Iterative Sparse Solver, Trust Region Solver, and GMP routine library supporting the LP64 interface |
| libmkl_solver_lp64.a | Iterative Sparse Solver, Trust Region Solver, and GMP routine library supporting the LP64 interface |

# 3 Intel Math Kernel Library User's Guide

# Table 3-7 Detailed Structure of the IA-64 Architecture-specific Directory lib/64

| File | Contents |
|---|---|
| RTL | |
| libguide.so | Intel® Legacy OpenMP* run-time library for dynamic linking |
| libomp5.so | Intel® Compatibility OpenMP* run-time library for dynamic linking |
| libmkl_intelmpi_lp64.so | LP64 version of BLACS routines supporting Intel MPI 2.0/3.x and MPICH2 |
| libmkl_intelmpi_lp64.so | LP64 version of BLACS routines supporting Intel MPI 2.0 and 3.x, and MPICH2 |
| locale/en_US/mkl_msg.cat | Catalog of Intel MKL messages in English |
| locale/ja_JP/mkl_msg.cat | Catalog of Intel MKL messages in Japanese |

# Table 3-7 Detailed Structure of the IA-64 Architecture-specific Directory lib/64 (continued)

| File | Contents |
|---|---|
| Dynamic Libraries | |
| libmkl_gf_ilp64.so | ILP64 interface library for the GNU Fortran compiler |
| libmkl_gf_lp64.so | LP64 interface library for the GNU Fortran compiler |
| libmkl_intel_ilp64.so | ILP64 interface library for the Intel compilers |
| libmkl_intel_lp64.so | LP64 interface library for the Intel compilers |
| libmkl_intel_sp2dp.so | SP2DP interface library for the Intel compilers |
