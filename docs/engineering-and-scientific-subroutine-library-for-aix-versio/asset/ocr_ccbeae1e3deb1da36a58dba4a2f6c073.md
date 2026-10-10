the argument $n$ correspond to the $sub\textbf{}$ arguments $t$ and $n$, respectively. For details on how to set up the subroutine, see "Programming Considerations for the SUBF Subroutine" on page 914.

# **Function**

The integral is approximated for a real valued function over a semi-infinite interval, using the Gauss-Rational quadrature method of specified order. The region of integration is:

$(a, \infty) \quad \text{ if } a+b > 0$
$(-\infty, a) \quad \text{ if } a+b < 0$

The method of order $n$ is theoretically exact for integrals of the following form, where $f$ is a polynomial of degree less than $2n$:

$\int_{a}^{\infty} f \left( \frac{1}{x+b} \right) \frac{1}{(x+b)^2} dx \qquad \text{ if } \; a+b > 0$

$\int_{-\infty}^{a} f \left( \frac{1}{x+b} \right) \frac{1}{(x+b)^2} dx \qquad \text{ if } \; a+b < 0$

The method of order $n$ is a good approximation when your integrand is closely approximated by a function of the following form, where $f$ is a polynomial of degree less than $2n$:

$f \left( \frac{1}{x+b} \right) \frac{1}{(x+b)^2}$

See references [28] and [95]. The result is returned as the function value to a Fortran, C, or C++ program.

# **Error Conditions**

**Computational Errors:**  None

+   **Input-Argument Errors:**
+   1. $a+b=0$
+   2. $n$ is not an allowable value, as listed in the syntax for this argument.

# **Example 1**

This example shows how to compute the integral of the function $f$ given by:

$\dot f(x) = \left( e^{1.0/x} \right) / \; x^2$

over the interval $(-\infty, -2.0)$, using the Gauss-Rational method with 10 points:

$\int_{-\infty}^{-2.0} \left( \frac{e^{1.0/x}}{x^2} \right) dx$

The user-supplied subroutine FUN1, which evaluates the integrand function, is coded in Fortran as follows: