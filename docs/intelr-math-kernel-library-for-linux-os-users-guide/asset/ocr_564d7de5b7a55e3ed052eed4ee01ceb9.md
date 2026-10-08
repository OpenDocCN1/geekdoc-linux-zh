| Table 2-1 | What You Need to Know Before You Begin (continued) |
| --- | --- |
| Threading model | **Action:** Identify whether and how your application is threaded:
> - Threaded with the Intel® compiler
> - Threaded with a third-party compiler
> - Not threaded
**Reason:** The compiler you use to thread your application determines threading library you should link with your application. For applications threaded with a third-party compiler you may need to use Intel MKL in the sequential mode (for more information, see Sequential Mode of the Library and Linking with Threading Libraries).
**Action:** Determine the number of threads you want Intel MKL to use.
**Reason:** Intel MKL is based on the OpenMP® threading. By default, the OpenMP sets the number of threads that Intel MKL uses. If you need a different number, you have set it yourself using one of the available mechanisms. For more information, see Using the Intel® MKL Parallelism.
**Action:** Decide which linking model is appropriate for linking your application with Intel MKL libraries:
> - Static
> - Dynamic
**Reason:** For information on the benefits of each linking model, command syntax and examples, link libraries, and other linking topics, how to save disk by creating a custom dynamic library, see Linking Your Application with the Intel® Math Kernel Library |
 MPI used | **Action:** Decide what MPI you will use with the Intel MKL cluster server. You are strongly encouraged to use Intel® MPI 3.x.
**Reason:** To link with ScalAPACK/or Cluster FFT, the libraries corresponding to your particular MPI should be listed on the link line (see Working with the Intel® Math Kernel Cluster Software). |

# # Compiler Support

Intel MKL supports compilers identified in the Release Notes. However, the library has been successfully used with other compilers as well.

Intel MKL provides a set of functions to simplify program development by specifying enumerated values and prototypes for the respective functions (for the list of includes, see Table A-2). Calling Intel MKL functions from your application without an appropriate include file may lead to incorrect behavior of the functions.

# # Steps to Get Started

This section helps you get started with Intel MKL on Linux* OS.