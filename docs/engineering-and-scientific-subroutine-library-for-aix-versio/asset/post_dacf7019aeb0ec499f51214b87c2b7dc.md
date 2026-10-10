
## Part 1. Guide Information

This part of the book is organized into the following chapters, which provide guidance information on how to use ESSSL. It is organized as follows:

-   Learning about ESSSL
-   Designing your program
-   Setting up your data structures
-   Coding your program
-   Processing your program
-   Migrating your programs
-   Handling problems

## Chapter 1. Introduction and Requirements

This chapter introduces you to the Engineering and Scientific Subroutine Library (ESSL).

### Overview of ESSL

This section gives an overview of the ESSL capabilities and requirements.

ESSL is a state-of-the-art collection of subroutines providing a wide range of mathematical functions for many different scientific and engineering applications. Its primary characteristics are performance, functional capability, and usability.

### Performance and Functional Capability

The mathematical subroutines, in nine computational areas, are tuned for performance on the RS/6000. The computational areas are:

-   Linear Algebra Subprograms
-   Matrix Operations
-   Linear Algebraic Equations
-   Eigensystem Analysis
-   Fourier Transforms, Convolutions and Correlations, and Related Computations
-   Sorting and Searching
-   Interpolation
-   Numerical Quadrature
-   Random Number Generation

ESSL provides two run-time libraries:

-   The **ESSL Symmetric Multi-Processing (SMP) Library** provides thread-safe versions of the ESSL subroutines for use on all SMP (for example, p690) processors. In addition, a subset of these subroutines are also multithreaded versions; that is, they support the shared memory parallel processing programming model. You do not have to change your existing application programs that call ESSL to take advantage of the increased performance of using the SMP processors; you can simply re-link your existing application programs. For a list of the multithreaded subroutines in the ESSL SMP Library, see Table 24 on page 26.
-   The **ESSL Serial Library** provides thread-safe versions of the ESSL subroutines for use on all processors. You may use this library to develop your own multithreaded applications.

All libraries are designed to provide high levels of performance for numerically intensive computing jobs. All versions provide mathematically equivalent results.

The **ESSL Serial Library** and the **ESSL SMP Library** support both 32-bit environment and 64-bit environment applications.

The ESSL subroutines can be called from application programs written in Fortran, C, and C++. ESSL runs under the AIX and Linux operating systems.

### Usability

ESSL is designed for usability:

-   It has an easy-to-use call interface.
-   If your existing application programs use the ESSL Serial library, you only need to re-link your program to take advantage of the increased performance of the ESSL SMP Library.
-   It supports a 64-bit environment.

The data model used for the 64-bit environment is referred to as LP64. This data model supports 32-bit integers and 64-bit pointers. In accordance with the LP64 data model, all ESSL integer arguments remain 32-bit except for the iusadr argument for ERRSET. See “ERRSET—ESSL ERRSET Subroutine for ESSL” on page 958.

-   It has informative error-handling capabilities, enabling you to calculate auxiliary storage sizes and transform lengths.
-   An online book that can be displayed using an Hypertext Markup Language (HTML) document browser, is available for use with ESSL.

### The Variety of Mathematical Functions

This section describes the mathematical functions included in ESSL.

#### Areas of Application

ESSL provides a variety of mathematical functions for many different types of scientific and engineering applications. Some of the industries using these applications are: Aerospace, Automotive, Electronics, Petroleum, Finance, Utilities, and Research. Examples of applications in these industries are:

-   Structural Analysis
-   Computational Chemistry
-   Fluid Dynamics Analysis
-   Seismic Analysis
-   Reservoir Modeling
-   Quantitative Analysis
-   Time Series Analysis
-   Computational Techniques
-   Mathematical Analysis
-   Dynamic Systems Simulation
-   Nuclear Engineering
-   Electronic Circuit Design

#### What ESSL Provides

The subroutines provided in ESSL, summarized in Table 1, fall into the following groups:

-   Nine major areas of mathematical computation, providing the computations commonly used by the industry applications listed above
-   Utilities, performing general-purpose functions

**To help you select the ESSL subroutines that fulfill your needs for performance, accuracy, storage, and so forth, see “Selecting an ESSL Subroutine” on page 25.**

### Table 1. Summary of ESSL Subroutines

| ESSL Area of Computation | Integer<br>Subroutines | Short-Precision<br>Subroutines | Long-Precision<br>Subroutines |
| :--- | :---: | :---: | :---: |
| **Linear Algebra Subprograms:** | | | |
| Vector-scalar | 0 | 41 | 41 |
| Sparse vector-scalar | 0 | 11 | 11 |
| Matrix-vector | 1 | 32 | 32 |
| Sparse matrix-vector | 0 | 0 | 3 |
| **Matrix Operations:** | | | |
| Addition, subtraction, multiplications, rank-k updates, rank-2k updates, and matrix transposes | 0 | 25 | 26 |
| **Linear Algebraic Equations:** | | | |
| Dense linear algebraic equations | 3 | 49 | 54 |
| Banded linear algebraic equations | 0 | 18 | 18 |
| Sparse linear algebraic equations | 0 | 0 | 11 |
| Linear least squares | 0 | 3 | 5 |
| **Eigensystem Analysis:** | | | |
| Solutions to the algebraic eigensystem analysis problem and the generalized eigensystem analysis problem | 0 | 8 | 8 |
| **Signal Processing Computations:** | | | |
| Fourier transforms | 0 | 15 | 11 |
| Convolutions and correlations | 0 | 10 | 2 |
| Related computations | 0 | 6 | 6 |
| **Sorting and Searching:** | | | |
| Sorting, sorting with index, and binary and sequential searching | 5 | 5 | 5 |
| **Interpolation:** | | | |
| Polynomial and cubic spline interpolation | 0 | 4 | 4 |
| **Numerical Quadrature:** | | | |
| Numerical quadrature on a set of points or on a function | 0 | 6 | 6 |
| **Random Number Generation:** | | | |
| Generating vectors of uniformly distributed and normally distributed random numbers | 0 | 3 | 3 |
| **Utilities:** | | | |
| General service operations | 8 | 0 | 3 |
| **Total ESSL Subroutines** | 13 | 236 | 249 |

## ESSL—Processing Capabilities

ESSL provides two run-time libraries, the ESSL SMP Library and the ESSL Serial Library. These libraries are designed to provide high levels of performance for numerically intensive computing jobs on the IBM eServer pSeries and RS/6000 processors.

To order ESSL, specify one of the program numbers below:

-   **ESSL for AIX**
    -   5765-F82
-   **ESSL for Linux**
    -   5765-G17

Most of the subroutine calls are compatible with those in the ESSL/370 product.

### Accuracy of the Computations

ESSL provides accuracy comparable to libraries using equivalent algorithms with identical precision formats. Both short- and long-precision real versions of the subroutines are provided in most areas of ESSL. In some areas, short- and long-precision complex versions are also provided, and, occasionally, an integer version is provided. The data types operated on by the short-precision, long-precision, and integer versions of the subroutines are ANSI/IEEE 32-bit and 64-bit binary floating-point format, and 32-bit integer. See the *ANSI/IEEE Standard for Binary Floating-Point Arithmetic, ANSI/IEEE Standard 754–1985*, for more detail. (There are ESSL-specific rules that apply to the results of computations on workstation processors using the ANSI/IEEE standards. For details, see "What Data Type Standards Are Used by ESSL, and What Exceptions Should You Know About?" on page 44.)

For more information on accuracy, see "Getting the Best Accuracy" on page 43.

### High Performance of ESSL

*Algorithms:* The ESSL subroutines have been designed to provide high performance. (See references [32], [43], and [44].) To achieve this performance, the subroutines use state-of-the-art algorithms tailored to specific operational characteristics of the hardware, such as cache size, Translation Lookupside Buffer (TLB) size, and page size.

Most subroutines use the following techniques to optimize performance:

-   Managing the cache and TLB efficiently so the hit ratios are maximized; that is, data is blocked so it stays in the cache or TLB for its computation.
-   Accessing data stored contiguously—that is, using stride-1 computations.
-   Exploiting the large number of available floating-point registers.
-   Using algorithms that minimize paging.
-   On the SMP processors:
    -   The ESSL SMP Library is designed to exploit the processing power and shared memory of the SMP processor. In addition, a subset of the ESSL SMP subroutines have been coded to take advantage of increased performance from multithreaded (parallel) programming techniques. For a list of the multithreaded subroutines in the ESSL SMP Library, see Table 24 on page 26.
    -   Choosing the number of threads depends on the problem size, the specific subroutine being called, and the number of physical processors you are running on. To achieve optimal performance, experimentation is necessary; however, picking the number of threads equal to the number of online processors generally provides good performance in most cases. In some cases, performance may increase if you choose the number of threads to be less than the number of online processors.
