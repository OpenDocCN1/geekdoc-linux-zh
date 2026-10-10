# SSINF and DSNF

due to symmetry, only the first n/2 values are given in the output\u2014that is, $y_{k}$k \u2001k = 0, 1, ..., n/2\u22121 for each i = 1, 2, ..., m. Returned as: an array of (at least) length 1+(n / 2\u22121)\u2009inc1y+ (m\u22121)\u2009inc2y, containing numbers of the data type indicated in Table 142 on page 780.

```
`aux1` is the working storage for this subroutine, where:
* If `init` \u2260 0, it contains information ready to be passed in a subsequent invocation of this subroutine.
* If `init` = 0, its contents are unchanged.
Returned as: the contents are not relevant.
```

# Notes

+   1. `aux1` should **not** be used by the calling program between calls to this subroutine with `init` \u2260 0 and `init` = 0. However, it can be reused after intervening calls to this subroutine with different arguments.
+   2. When using the ESSL SMP library, for optimal performance, the number of threads specified should be the same for `init` \u2260 0 and `init` = 0.
+   3. For optimal performance, the preferred value for `inc1x` and `inc1y` is 1. This implies that the sequences are stored with stride 1. In addition, `inc2x` and `inc2y` should be close to n/2.

It is possible to specify sequences in the transposed form\u2014that is, as rows of a two-dimensional array. In this case, `inc2x` (or `inc2y`) = 1 and `inc1x` (or `inc1y`) is equal to the leading dimension of the array. One can specify either input, output, or both in the transposed form by specifying appropriate values for the stride parameters. For selecting optimal values of `inc1x` and `inc1y` for _SSINF, you should use \u201cSTRIDE\u2014Determine the Stride Value for Optimal Performance in Specified Fourier Transform Subroutines\u201d on page 963. Example 3 in the STRIDE subroutine description explains how it is used for _SSNF.

If you specify the same array for X and Y, then `inc1x` and `inc1y` must be equal, and `inc2x` and `inc2y` must be equal. In this case, output overwrites input. If m = 1, the `inc2x` and `inc2y` values are not used by the subroutine. If you specify different arrays for X and Y, they must have no common elements; otherwise, results are unpredictable. See \u201cConcepts\u201d on page 55.

# Processor-Independent Formulas for SSINF for NAUX1 and NAUX2

**NAUX1 Formulas::**
If n \u2264 16384, use `naux1` = 60000.
If n > 16384, use `naux1` = 20000+30n.

**NAUX2 Formulas::**
If n \u2264 16384, use `naux2` = 25000.
If n > 16384, use `naux2` = 20000+32n.
For the transposed case, where `inc2x` = 1 or `inc2y` = 1, and where n \u2265 252, add the following to the above storage requirements:
(n/4+257)(min(128, m)).

# Processor-Independent Formulas for DSNF for NAUX1 and NAUX2

**NAUX1 Formulas::**
If n \u2264 16384, use `naux1` = 50000.
If n > 16384, use `naux1` = 20000+60n.