Otherwise, *naux2* ≥ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For all other values specified less than the minimum value, you have the option of having the minimum value returned in this argument. For details, see “*Using Auxiliary Storage in ESML*” on page 32.

*aux3* 
this argument is provided for migration purposes only and is ignored. Specified as: an area of storage, containing *naux3* long-precision real numbers.

*naux3* 
this argument is provided for migration purposes only and is ignored. Specified as: a fullword integer.

# On Return:

*y* 
has the following meaning, where:
If *init* ≠ 0, this argument is not used, and its contents remain unchanged. If *init* = 0, this is the array *Y*, containing *n*1 rows and *n*2 columns of results of the real discrete Fourier transform of *X*. The data in each column of *Y* is stored with stride 1. Returned as: an *inc2y* by (at least) *n*2 array, containing numbers of the data type indicated in Table 145 on page 800. See “*Notes*” for more details.

*aux1* 
is the working storage for this subroutine, where:
If *init* ≠ 0, it contains information ready to be passed in a subsequent invocation of this subroutine. If *init* = 0, its contents are unchanged. Returned as: the contents are not relevant.

# Notes

+   1. *aux1* should **not** be used by the calling program between program calls to this subroutine with *init* ≠ 0 and *init* = 0. However, it can be reused after intervening calls to this subroutine with different arguments.
+   2. When using the ESML SMP library, for optimal performance, the number of threads specified should be the same for *init* ≠ 0 and *init* = 0.
+   3. If you specify the same array for *X* and *Y*, then (2*inc2x*) must equal *inc2y*. In this case, output overwrites input. If you specify different arrays *X* and *Y*, they must have no common elements; otherwise, results are unpredictable. See “*Concepts*” on page 55.
+   4. For selecting optimal strides (or leading dimensions *inc2x* and *inc2y*) for your input and output arrays, you should use “*STRIDE—Determine the Stride Value for Optimal Performance in Specified Fourier Transform Subroutines*” on page 963. Example 6 in the STRIDE subroutine description explains how it is used for these subroutines.
+   5. Be sure to align array *Y* on a doubleword boundary, and specify an even number for *inc2y*, if possible.

# Processor-Independent Formulas for SCRFT2 for NAUX1 and NAUX2

The required values of *naux1* and *naux2* depend on *n1* and *n2*.

**NAUX1 Formulas:**
If max(*n*1/2, *n*2) ≤ 8192, use *naux1* = 45000.