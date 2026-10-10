ESSL subroutine to perform the computation, error handling does not issue an error message and processing continues normally.) Figure 1 illustrates what happens when error 2015 is unrecoverable.

![](bbox=[0.13, 0.19, 0.88, 0.64])

* This check applies only to several NAUX1 arguments in the Fourier transform, convolution, and correlation subroutines.

> Figure 1. How to Obtain a NAUX Value from an Error Message, but Terminate

# The Second Way

In this case, you obtain the minimum required value of *naux* from the error message and from the updated *naux* argument returned to your program.

Use EINFO and ERRSET with an ESSL error exit routine, ENOTRM, to make error 2015 recoverable. This allows you to dynamically determine in your program the minimum sizes required for the auxiliary working storage areas, specified in the *naux* arguments. Run your program with the *naux* values smaller than required by the subroutine for the particular processor you are running on. As a general guideline, specify values smaller than those listed in the formulas. However, if a lower limit is specified in the syntax (only for several *naux1* arguments in the Fourier transform, convolution, and correlation subroutines), you should not go