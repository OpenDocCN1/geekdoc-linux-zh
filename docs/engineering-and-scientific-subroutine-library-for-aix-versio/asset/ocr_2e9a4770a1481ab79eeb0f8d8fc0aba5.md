# STPINT and DTPINT

*naux* is the size of the work area specified by *aux*—that is, the number of elements in *aux*.

Specified as: a fullword integer, where:

If *naux* = 0 and error 2015 is unrecoverable, STPINT and DTPINT dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.

Otherwise, *naux* ≧ *nint*+*m*.

# On Return:

*s* is the vector *s* of length *m*, containing the resulting interpolated values; that is, each *sᵢ* is the value of the interpolating polynomial evaluated at *tᵢ*.

Returned as: a one-dimensional array of (at least) length *m*, containing numbers of the data type indicated in Table 163 on page 901.

# Notes

+   1. Vectors *x*, *y*, and *t* must have no common elements with vector *s* or work area *aux*; otherwise, results are unpredictable. See “Concepts” on page 55.
+   2. The elements of vector *x* must be distinct and must be sorted into ascending order; that is, *x₁* < *x₂* < ... < *xₙ*. Otherwise, results are unpredictable. For details on how to do this, see “ISORT, SSORT, and DSORT—Sort the Elements of a Sequence” on page 879.
+   3. The elements of vector *t* should be sorted into ascending order; that is, *t₁* ≦ *t₂* ≦ *t₃* ≦ ... ≦ *tₘ*. Otherwise, performance is affected.
+   4. You have the option of having the minimum required value for *naux* dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSL” on page 32.

# Function

Polynomial interpolation is performed at specified abscissas, *tᵢ* for *i* = 1, *m*, in vector *t*, using *nint* points selected from the following data:

(*xⱼ*, *yⱼ*) for *j* = 1, *n*

where:

*x₁* < *x₂* < *x₃* < ... < *xₙ*
*xⱼ* are elements of vector *x*.
*yⱼ* are elements of vector *y*.

The points (*xⱼ*, *yⱼ*), used in the interpolation at a given abscissa *tᵢ*, are chosen as follows, where *k* = *nint*/2:

For *tᵢ* ≦ *xₖ₊₁*, the first *nint* points are used.

For *tᵢ* > *xₙ₋ₙᵢₙₜ₊ₖ*, the last *nint* points are used.

Otherwise, points *h* through *h*+*nint*–1 are used, where:

*xₕ₊ₖ₋₁* < *tᵢ* ≦ *xₕ₊ₖ*

The interpolated value at each *tᵢ* is returned in *sᵢ* for *i* = 1, *m*. See references [17] and [56]. If *n*, *nint*, or *m* is 0, no computation is performed. For a definition of the polynomial interpolation function performed through a set of data points, see “Function” on page 898.

For STPINT, the Newton divided differences and interpolating values are accumulated in long precision.