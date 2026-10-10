# Chapter 14. Interpolation

The interpolation subroutines are described in this chapter.

# Overview of the Interpolation Subroutines

The interpolation subroutines provide the capabilities of doing polynomial interpolation, local polynomial interpolation, and one- and two-dimensional cubic spline interpolation (Table 161).

**Table 161. List of Interpolation Subroutines**

| Descriptive Name | Short- Precision Subroutine | Long- Precision Subroutine | Page |
| :--- | :--- | :--- | :--- |
| Polynomial Interpolation | SPINT | DPINT | 897 |
| Local Polynomial Interpolation | STPINT | DTPINT | 901 |
| Cubic Spline Interpolation | SCSINT | DCSINT | 904 |
| Two-Dimensional Cubic Spline Interpolation | SCSIN2 | DCSIN2 | 909 |

# Use Considerations

Polynomial interpolation (SPINT and DPINT) is a global scheme. As the number of data points increases, the degree of the interpolating polynomial is raised; therefore, the graph of the interpolating polynomial tends to be oscillatory.

Local polynomial interpolation (STPINT and DTPINT) is a local scheme. The data generated is affected only by locally grouped data points. The degree of the local interpolating polynomial is usually lower than a global interpolating polynomial.

# Performance and Accuracy Considerations

+   1. Doing extrapolation with SPINT and DPINT is not encouraged unless you know the consequences of doing polynomial extrapolation.
+   2. If performance is the overridding consideration, you should investigate using the general signal processing subroutines, DQINT and SQINT.
+   3. There are some ESSIL-specific rules that apply to the results of computations on the workstation processors using the ANSI/IEEE standards. For details, see “What Data Type Standards Are Used by ESSIL, and What Exceptions Should You Know About?” on page 44.