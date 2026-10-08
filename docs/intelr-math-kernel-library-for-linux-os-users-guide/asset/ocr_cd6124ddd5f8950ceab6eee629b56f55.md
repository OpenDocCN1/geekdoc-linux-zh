# 2 Intel® Math Kernel Library User's Guide

| Table 2-1 | What You Need to Know Before You Begin (continued) |

+   **Action:** Identify all Intel MKL function domains that you require:
* BLAS
* Sparse BLAS
* LAPACK
* PBLAS
* ScalACK
* Sparse Solver routines
* Vector Mathematical Library functions
* Vector Statistical Library functions
* Fourier Transform functions (FFT)
* Cluster FFT
* Trigonometric Transform routines
* Poisson, Laplace, and Helmholtz Solver routines
* Optimization (Trust-Region)
* GMP* arithmetic functions

Mathematical problem

**Reference:** The function you intend to use narrows the search in the *Reference Manual* for specific needs. Additionally, if you are using the Intel MKL cluster software, your link is function-domain specific (see [Working with the Intel® Math Kernel Library, Cluster Software](https://www.example.com/mkl)). Coding tips may also depend on the function domain (see [Tips and Techniques to Improve Performance](https://www.example.com/tips)).

**Action:** Though Intel MKL provides support for both Fortran and C/C++, not all the function support a particular language environment, for example, C/C++ or Fortran 90/95. Identify the language interfaces that your function supports ([Intel® Math Kernel Library Interfaces Support](https://www.example.com/interfaces)).

Programming language

**Reason:** In case your function does not directly support the needed, you can use mixed-programming (see [Mixed-language Programming with Intel® MKL](https://www.example.com/mixed)).

For a list of language-specific interfaces and modules and an example how to generate them, see also [Using Language-Specific Interfaces with Intel® MKL](https://www.example.com/using).

**Action:** If your system is based on the Intel 64 or IA-64 architecture, identify whether your application performs calculations with huge data arrays (of more than 2³¹¹ elements).

Range of integer data

**Reason:** To operate on huge data arrays, you need to use the ILP64 interface, where integers are 64-bit; otherwise, use the default, LP64, interface, where integers are 32-bit (see [Support for ILP64 Programming](https://www.example.com/ilp64)).