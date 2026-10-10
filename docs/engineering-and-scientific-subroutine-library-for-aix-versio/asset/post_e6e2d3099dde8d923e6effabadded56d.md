
# **ISSRCH, SSSRCH, and DSSRCH**

# Chapter 14. Interpolation

The interpolation subroutines are described in this chapter.

## Overview of the Interpolation Subroutines

The interpolation subroutines provide the capabilities of doing polynomial interpolation, local polynomial interpolation, and one- and two-dimensional cubic spline interpolation (Table 161).

**Table 161. List of Interpolation Subroutines**

| Descriptive Name | Short- Precision Subroutine | Long- Precision Subroutine | Page |
| :--- | :--- | :--- | :--- |
| Polynomial Interpolation | SPINT | DPINT | 897 |
| Local Polynomial Interpolation | STPINT | DTPINT | 901 |
| Cubic Spline Interpolation | SCSINT | DCSINT | 904 |
| Two-Dimensional Cubic Spline Interpolation | SCSIN2 | DCSIN2 | 909 |

## Use Considerations

Polynomial interpolation (SPINT and DPINT) is a global scheme. As the number of data points increases, the degree of the interpolating polynomial is raised; therefore, the graph of the interpolating polynomial tends to be oscillatory.

Local polynomial interpolation (STPINT and DTPINT) is a local scheme. The data generated is affected only by locally grouped data points. The degree of the local interpolating polynomial is usually lower than a global interpolating polynomial.

## Performance and Accuracy Considerations

1.  Doing extrapolation with SPINT and DPINT is not encouraged unless you know the consequences of doing polynomial extrapolation.
2.  If performance is the overriding consideration, you should investigate using the general signal processing subroutines, DQINT and SQINT.
3.  There are some ESSIL-specific rules that apply to the results of computations on the workstation processors using the ANSI/IEEE standards. For details, see “What Data Type Standards Are Used by ESSIL, and What Exceptions Should You Know About?” on page 44.

## Interpolation Subroutines

This section contains the interpolation subroutine descriptions.

## SPINT and DPINT—Polynomial Interpolation

These subroutines compute the Newton divided difference coefficients and perform a polynomial interpolation through a set of data points at specified abscissas.

**Table 162. Data Types**

| $x, y, c, t, s$ | Subroutine |
| :--- | :---: |
| Short-precision real | SPINT |
| Long-precision real | DPINT |

## Syntax

| Language | Code |
| :--- | :--- |
| Fortran | CALL SPINT \| DPINT ($x, y, n, c, ninit, t, s, m$) |
| C and C++ | spint \| dpint ($x, y, n, c, ninit, t, s, m$); |

## On Entry:

$x$ is the vector **x** of length $n$, containing the abscissas of the data points used in the interpolations. The elements of $x$ must be distinct. Specified as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 162.

$y$ is the vector **y** of length $n$, containing the ordinates of the data points used in the interpolations. Specified as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 162.

$n$ is the number of elements in vectors **x**, **y**, and **c**—that is, the number of data points. Specified as: a fullword integer; $n \ge 0$.

$c$ is the vector **c** of length $n$, where:
If $ninit \le 0$, all elements of **c** are undefined on entry.
If $ninit > 0$, **c** contains the Newton divided difference coefficients, $c_j$ for $j = 1, ninit$, for the interpolating polynomial through the data points $(x_j, y_j)$ for $j = 1, ninit$. If $ninit < n$, the values of $c_j$ for $j = ninit+1, n$ are undefined.
Specified as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 162.

$ninit$ indicates the following:
If $ninit \le 0$, this is the first call to this subroutine with the data in **x** and **y**; therefore, none of the Newton divided difference coefficients in **c** have been initialized.
If $ninit > 0$, a previous call to this subroutine was made with the data points $(x_j, y_j)$ for $j = 1, ninit$, where:
-   If $ninit = n$, all the Newton divided difference coefficients in **c** were computed for the data points. No additional coefficients are computed on this entry.
-   If $ninit < n$, the first $ninit$ Newton divided difference coefficients in **c** were computed for the data points $(x_j, y_j)$ for $j = 1, ninit$. The coefficients are updated for the additional data points $(x_j, y_j)$ for $j = ninit+1, n$ on this entry.

Specified as: a fullword integer; $ninit \leq n$.

-   **t** is the vector **t** of length $m$, containing the abscissas at which interpolation is to be done.
    Specified as: a one-dimensional array of (at least) length $m$, containing numbers of the data type indicated in Table 162 on page 897.
-   **s** See “On Return.”
-   **m** is the number of elements in vectors **t** and **s**—that is, the number of interpolations to be performed.
    Specified as: a fullword integer; $m \geq 0$.

## On Return:

-   **c** is the vector **c** of length $n$, containing the coefficients of the Newton divided difference form of the interpolating polynomial through the data points ($x_j, y_j$) for $j = 1, n$. Returned as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 162 on page 897.
-   **ninit** is the number of coefficients, $n$, in output vector **c**. (If you call this subroutine again with the same data, this value should be specified for $ninit$.) Returned as: a fullword integer; $ninit = n$.
-   **s** is the vector **s** of length $m$, containing the resulting interpolated values; that is, each $s_i$ is the value of the interpolating polynomial evaluated at $t_i$. Returned as: a one-dimensional array of (at least) length $m$, containing numbers of the data type indicated in Table 162 on page 897.

## Notes

1.  In your C program, argument $ninit$ must be passed by reference.
2.  Vectors **x**, **y**, and **t** must have no common elements with vectors **c** and **s**, and vector **c** must have no common element with vector **s**; otherwise, results are unpredictable.
3.  The elements of vector **x** must be distinct; that is, $x_i \neq x_j$ if $i \neq j$ for $i, j = 1, n$.

## Function

Polynomial interpolation is performed at specified abscissas, $t_i$ for $i = 1, m$, in vector **t**, using the method of Newton divided differences through the data points: ($x_j, y_j$) for $j = 1, n$

where:

-   $x_j$ are elements of vector **x**.
-   $y_j$ are elements of vector **y**.

The interpolated value at each $t_i$ is returned in $s_i$ for $i = 1, m$. See references [17] and [56]. The interpolating values returned in **s** are computed using the Newton divided difference coefficients, as defined in the following section.

The divided difference coefficients, $c_j$ for $j = 1, n$, are returned in vector **c**. These coefficients can then be reused on subsequent calls to this subroutine, using the same data points ($x_j, y_j$), but with new values of $t_i$. If the number of data points is increased from one call this subroutine to the next, the new coefficients are computed, and the existing coefficients are updated (not recomputed). This feature can be used to test for the convergence of the interpolations through a sequence of an increasingly larger set of points.

## **SPINT and DPINT**

The values specified for *ninit* and *m* indicate which combination of functions are performed by this subroutine: computing the coefficients, performing the interpolation, or both. If *m* = 0, only the divided difference coefficients are computed. No interpolation is performed. If *n* = 0, no computation or interpolation is performed.

For **SPINT**, the Newton divided differences and interpolating values are accumulated in long precision.

**Newton Divided Differences and Interpolating Values:** The Newton divided differences of the following data points:

($x_{j}, y_{j}$) for $j=1, n$
where $x_{j}\neq x_{i}$ if $j\neq l$ for $j, l=1, n$

are denoted by $\delta_{k}y_{j}$ for $k=0, 1, 2, ..., n-1$ and $j=1, 2, ..., n-k$, and are defined as follows:

```
For k=0 and 1:
δ0yj=yj for j=1, 2, ..., n
δ1yj=(yj+1−yj)/(xj+1−xj) for j=1, 2, ..., n-1
For k=2, 3, ..., n-1:
δkyj=(δk−1yj+1−δk−1yj)/(yj+k−xj) for j=1, 2, ..., n-k
```

The value $s$ of the Newton divided difference form of the interpolating polynomial evaluated at an abscissa $t$ is given by:

```
s = yn + (t−xn) δ1yn−1
+ (t−xn−1)(t−xn) δ2yn−2
+ ... +(t−x2)(t−x3)... (t−xn) δn−1y1
```

Therefore, on output, the coefficients in vector *c* are as follows:

```
cn=yn
cn−1=δ1yn−1
cn−2=δ2yn−2
...
c1=δn−1y1
```

Also, the interpolating values in *s*, in terms of $c_{i}$ are as follows for $i=1, m$:

```
si = cn + (ti−xn) cn−1
+ (ti−xn−1)(ti−xn) cn−2
+ ...
+ (ti−x2)(ti−x3)... (ti−xn) c1
```

## **Error Conditions**

-   Computational Errors: None
-   **Input-Argument Errors:**
    1.  *n* < 0
    2.  *ninit* > *n*
    3.  *m* < 0

## **Example 1**

This example shows a quadratic polynomial interpolation on the initial call with the specified data points; that is, *NINIT* = 0, and *C* contains all undefined values. On output, *NINIT* and *C* are updated with new values.
