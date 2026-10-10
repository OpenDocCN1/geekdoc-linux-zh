# Convolutions and Correlations by Fourier Methods

The convolution and correlation subroutines that use the Fourier methods determine a sequence length $n$, whose Fourier transform is computed using ESSL subroutines. In the simple case where $iy0 = 0$ for convolution or $iy0 = -nh+1$ for correlation, $n$ is chosen as a value greater than or equal to the following, which is also acceptable to the Fourier tranform subroutines:

$nt = min(nh+nx-1, ny)$ for convolution and correlation
$nt = min(nx+nx-1, ny)$ for autocorrelation

which is also acceptable to the Fourier subroutines.

# Related Computation Considerations

This section describes some key points about using the related-computation subroutines.

# Accuracy Considerations

+   - Many of the subroutines performing short-precision computations provide increased accuracy by accumulating results in long precision. This is noted in the functional description for each subroutine.
+   - There are ESSL-specific rules that apply to the results of computations on the workstation processors using the ANSI/IEEE standards. For details, see “What Data Type Standards Are Used by ESSL, and What Exceptions Should You Know About?” on page 44.