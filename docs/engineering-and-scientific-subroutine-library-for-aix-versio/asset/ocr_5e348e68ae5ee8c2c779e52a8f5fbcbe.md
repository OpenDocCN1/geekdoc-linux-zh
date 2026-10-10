# SCSINT and DCSINT

If init = 2, the coefficients are uninitialed. The value in $c_{21}$ is used as the spline derivative at $x_{n}$.

If init = 3, the coefficients are unitialed. The value in $c_{1}$ is used as the spline derivative at $x_{1}$ and the value in $c_{21}$ is used as the spline derivative at $x_{n}$.

If init > 3, the coefficients in $c$ were computed for data points $(x_{\rho}, y_{\rho})$ for $j=1, n$ on a previous call to this subroutine.

Specified as: a fullword integer. It can have any value.

$\mathbf{t}$ is the vector $\mathbf{t}$ of length $m$, containing the abscissas at which the spline is evaluated.

Specified as: a one-dimensional array of (at least) length $m$, containing numbers of the data type indicated in Table 164 on page 904.

$s$ See "On Return."

$m$ is the number of elements in vectors $\mathbf{t}$ and $\mathbf{s}$—that is, the number of points at which the spline interpolation is evaluated.

Specified as: a fullword integer; $m \geqslant 0$.

# On Return:

$c$ is the matrix $\mathbf{C}$, containing the coefficients of the spline through the data points $(x_{j}, y_{j})$ for $j=1, n$. Returned as: an $n$ by (at least) 4 array, containing numbers of the data type indicated in Table 164 on page 904.

init is an indicator that is set to indicate that the coefficients have been initialized. (If you call this subroutine again with the same data, this value should be specified for init.) Returned as: a fullword integer; init = 4.

$s$ is the vector $\mathbf{s}$ of length $m$, containing the resulting values of the spline; that is, each $s_{i}$ is the value of the spline evaluated at $t_{i}$. Returned as: a one-dimensional array of (at least) length $m$, containing numbers of the data type indicated in Table 164 on page 904.

# Notes

+   1. In your C program, argument init must be passed by reference.
+   2. Vectors $\mathbf{x}, \mathbf{y}$, and $\mathbf{t}$ must have no common elements with matrix $\mathbf{C}$ and vector $\mathbf{s}$, and matrix $\mathbf{C}$ must have no common elements with vector $\mathbf{s}$; otherwise, results are unpredictable.
+   3. The elements of vector $\mathbf{x}$ must be distinct and must be sorted into ascending order; that is, $x_{1} < x_{2} < \ldots < x_{n}$. Otherwise, results are unpredictable. For details on how to do this, see “ISORT, SSORT, and DSORT—Sort the Elements of a Sequence” on page 879.

# Function

Interpolation is performed at specified abscissas, $t_{i}$ for $i=1, m$, in vector $\mathbf{t}$, using the cubic spline passing through the data points:
$(x_{j}, y_{j})$ for $j=1, n$.
where:
$x_{1} < x_{2} < x_{3} < \ldots < x_{n}$
$x_{i}$ are elements of vector $\mathbf{x}$.
$y_{i}$ are elements of vector $\mathbf{y}$.