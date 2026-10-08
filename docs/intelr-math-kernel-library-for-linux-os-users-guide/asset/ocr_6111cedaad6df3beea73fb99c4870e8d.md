# 6 Intel® Math Kernel Library User's Guide

and Intel MKL are using the same threading library. If the user's program is threaded by some other means, Intel MKL may operate in multithreaded mode and the performance may suffer due to overuse of the resources.

Here are several cases with recommendations depending on the threading model you employ:

# Table 6-1 How to Avoid Conflicts in the Execution Environment for Your Threads Model

| Threading model | Discussion |
|---|--- |
| You thread the program using OS threads (pthreads on the Linux*). | If more than one thread calls Intel MKL, and the function being called, it may be important that you turn off Intel MKL threading. Set the number of threads to be any of the available means (see Techniques to Set the Number of Threads). |
| You thread the program using OpenMP directives and/or pragmas and compile the program using a compiler other than the one from Intel. | This is more problematic because setting of the OMP_THREADS environment variable affects both compiler's threading library and libomp (libgomp). In this case, choose the threading library that matches the Intel MKL with the OpenMP compiler you employ (see Linking Examples MKL in the sequential). If this is not possible, use Intel MKL in the sequential mode. To do this, you should link with the threading library: libmkl_sequential.a or libmkl_sequential.so (see High-level Directory Structure). |
| There are multiple programs running on a multiple-cpu system, for example, a parallelized program that uses MPI for communication in which each processor is treated as a node. | The software will see multiple processors even though each processor has a separate MPI process running on. In this case, one of the solutions is to set the number of threads to any of the available means (see Techniques to Set the Number of Threads). Section Optimized LINPACK Benchmark for Clusters discusses another solution for a Hybrid (OpenMP*) mode. |

See also:

Linking with Compiler Support RTLs.