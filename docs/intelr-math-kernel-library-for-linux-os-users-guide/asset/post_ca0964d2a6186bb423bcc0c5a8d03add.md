
# Linking Your Application with the Intel® Math Kernel Library

- If you use the Intel compiler, link in the libomp/libguide version that comes with
it compiler, that is, use the -openmp option.

- If you do not use the Intel compiler, link in the libomp/libguide version that
comes with Intel MKL.

If you link with dynamic versions of libomp/libguide (recommended), that is, use
libomp5.so or libguide.so, make sure LD_LIBRARY_PATH is defined correctly.
Set Environment Variables for details.

# Linking with System Libraries

On Linux OS*, libomp/libguide both rely on the native pthread library for
multi-threading. Any time libomp/libguide is required, add -lpthread to your link line
afterwards (the order of listing libraries is important).

# Linking Examples

The section provides specific linking examples that use Intel® compilers on systems based
on the IA-32, Intel® 64, and IA-64 architectures. In these examples, <MKL path> and
<MKL include> placeholders are replaced with user-defined environment variables
$MKLPATH and $MKLINCLUDE, see examples for linking on ScLAPACK
and Cluster FFT in Chapter 9.

The following examples use the .f source file. C/C++ users should instead specify
a .cpp (C++) or .c file and change the fortran linker to icc.

For assistance in finding the right line, use the Web-based advisor available
from http://software.intel.com/en-us/articles/intel-mkl-link-line-advisor.

# Linking on Systems Based on the IA-32 Architecture

1. Static linking of myprog.f and parallel Intel MKL:
ifort myprog.f -LMKLPATH $MKLINCLUDE
-Wl,--start-group $MKLPATH/libmkl_thread.a $MKLPATH/libmkl_core.a -Wl,--end-group
-libomp5 -lpthread

2. Dynamic linking of myprog.f and parallel Intel MKL:
ifort myprog.f -LMKLPATH $MKLINCLUDE
-lmkl_intel -lmkl_intel_thread -lmkl_core -liomp5 -lpthread

3. Static linking of myprog.f and sequential version of Intel MKL:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-Wl,--start-group $MKLPATH/libmkl_sequential.a $MKLPATH/libmkl_core.a -Wl,--end-group
-lpthread

4. Dynamic linking of myprog.f and sequential version of Intel MKL:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-lmkl_sequential -lmkl_core -lpthread

5. Static linking of myprog.f, for Fortran 95 LAPACK interface, and parallel Intel MKL:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -I$MKLINCLUDE/
-lmkl_lapack95
-Wl,--start-group $MKLPATH/libmkl_intel.a
$MKLPATH/libmkl_intel_thread.a $MKLPATH/libmkl_core.a -Wl,--end-group
-liomp5

6. Static linking of myprog.f, for Fortran 95 BLAS interface, and parallel Intel MKL:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE/32 -lmkl_blas95
-Wl,--start-group $MKLPATH/libmkl_intel.a
$MKLPATH/libmkl_intel_thread.a $MKLPATH/libmkl_core.a -Wl,--end-group
-liomp5

7. Static linking of myprog.f, parallel version of an iterative sparse solver, and parallel Intel MKL:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -lmkl_solver
-Wl,--start-group $MKLPATH/libmkl_intel.a
$MKLPATH/libmkl_intel_thread.a $MKLPATH/libmkl_core.a -Wl,--end-group
-liomp5

8. Static linking of myprog.f, sequential version of an iterative sparse solver, and sequential Intel MKL:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -lmkl_solver_sequential
-Wl,--start-group $MKLPATH/libmkl_intel.a
$MKLPATH/libmkl_sequential.a $MKLPATH/libmkl_core.a -Wl,--end-group
-lpthread

# Linking Systems Based on the Intel 64 and IA-64 Architectures

1. Static linking of myprog.f and parallel Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a
$MKLPATH/libmkl_intel_thread.a $MKLPATH/libmkl_core.a -Wl,--end-group
-liomp5

2. Dynamic linking of myprog.f and parallel Intel MKL supporting LP64 interface:
See Fortran 95 Interfaces to LAPACK and BLAS for information on how to build Fortran 95 LAPACK and BLAS interface libraries.
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -liomp5 -lpthread

3. Static linking of myprog.f and sequential version of Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-Wl,--start-group $MKLPATH/libmkl_sequential_lp64.a $MKLPATH/libmkl_core.a -Wl,--end-group
-lpthread

4. Dynamic linking of myprog.f and sequential version of Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-lmkl_intel_lp64 -lmkl_sequential -lmkl_core -lpthread

5. Static linking of myprog.f and parallel Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_intel_thread.a -Wl,--end-group
-liomp5 -lpthread

6. Dynamic linking of myprog.f and parallel Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -liomp5 -lpthread

7. Static linking of myprog.f, Fortran 95 LAPACK¹, and parallel Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -I$MKLINCLUDE/em64/lp64
-lmkl_lapack_95_lp64
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_intel_thread.a -Wl,--end-group
-liomp5

8. Static linking of myprog.f, Fortran 95 BLAS¹, and parallel Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -I$MKLINCLUDE/em64/lp64
-lmkl_blas_95
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_intel_thread.a -Wl,--end-group
-liomp5

9. Static linking of myprog.f, parallel version of an iterative sparse solver, and parallel Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -lmkl_solver
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_intel_thread.a $MKLPATH/libmkl_core.a -Wl,--end-group
-liomp5

10. Static linking of myprog.f, sequential version of an iterative sparse solver, and sequential Intel MKL supporting LP64 interface:
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -lmkl_solver_sequential
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_sequential.a $MKLPATH/libmkl_core.a -Wl,--end-group
-lpthread
