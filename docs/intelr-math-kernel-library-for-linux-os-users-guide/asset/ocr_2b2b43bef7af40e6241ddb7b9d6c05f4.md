# Language-specific Usage Options

```
prod( conj(trans(m1)), conj(trans(m2)) )
```

These expressions are substituted in the release mode only with (NDEBUG preprocessor symbol defined). Supported uBLAS versions are Boost1.34.1, 1.35.0, 1.36.0, and 1.37.0. To get them, visit www.boost.

A code example provided in the <mkl_directory>/examples/ublas/source/svester.cpp file illustrates usage of the Intel MKL uBLAS header file for solving a special case of the Sylvester equation.

To run the Intel MKL examples, using the BOOST_ROOT parameter in the make command, for instance, when using Boost version 1.37.0:

```
make lib32 BOOST_ROOT=<your_path>/boost_1_37_0
```

# Invoking Intel® MKL Functions from Java* Applications

This section describes examples that are provided with the Intel MKL package and illustrate calling the libraries from Java.

# Intel MKL Java Examples

Java was positioned by its inventor, the Sun Microsystems Corporation as a "Write Once Run Anywhere" (WORA) language. Intel MKL may help to speed-up Java applications, while partially supporting the WORA philosophy, because Intel MKL editions are intended for a wide variety of operating systems and processors including most kinds of laptops, as well as many workstations and servers.

To demonstrate binding with Java, Intel MKL includes the set of Java examples found in the following directory:

```
<mkl directory>/examples/java -
```

The examples are provided for the following MKL functions:

+   * ?gemm, ?gemv, and ?7dot family from CBLAS
* The complete set of non-cluster FFT functions
* ESSL¹-like functions for one-dimensional convolution and correlation
* VSL Random Number Generators (RNG), except GetErrorCallback, SetErrorCallback, and
* ClearErrorCallback

You can see the example sources in the following directory:

```
<mkl directory>/examples/java/examples
```

IBM Engineering Scientific Subroutine Library (ESSL)*