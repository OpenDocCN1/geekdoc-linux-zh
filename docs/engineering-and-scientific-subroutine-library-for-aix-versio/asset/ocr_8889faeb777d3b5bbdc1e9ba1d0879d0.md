# ## SCONF and SCORF

## SCONF and SCORF—Convolution or Correlation of One Sequence with One or More Sequences Using the Mixed-Radix Fourier Method

These subroutines compute the convolutions and correlations, respectively, of a sequence with one or more sequences using the mixed-radix Fourier method. The input and output sequences contain short-precision real numbers.

**Note:** Two invocations of these subroutines are necessary: one to prepare the working storage for the subroutine, and the other to perform the computations.

# ### Syntax

| Fortran | CALL SCONF \| SCORF (init, h, inc1h, x, inc1x, inc2x, y, inc1y, inc2y, nh, nx, m, iy0, ny, aux1, aux1x, aux2, nau2) |
| --- | --- |
| C and C++ | sconf \| scorf (init, h, inc1h, x, inc1x, inc2x, y, inc1y, inc2y, nh, nx, m, iy0, ny, aux1, nau1x, aux2, nau2); |

# ### On Entry:

*init*    is a flag, where:

If init ≠ 0, trigonometric functions, the transform of the sequence in h, and other parameters, depending on arguments other than x, are computed and saved in aux1. The contents of x and y are not used or changed.

If init = 0, the convolutions or correlations of the sequence that was in h at initialization with the sequences in x are computed. h is not used or changed. The only arguments that may change after initialization are x, y, and aux2. All scalar arguments must be the same as when the subroutine was called for initialization with init ≠ 0.

Specified as: a fullword integer. It can have any value.

h    is the array H, consisting of the sequence of length Nh to be convolved or correlated with the sequences in array X.

Specified as: an array of (at least) length 1+(Nh-1)|inc1h|, containing short-precision real numbers.

*inc1h*    is the stride between the elements within the sequence in array H.

Specified as: a fullword integer; inc1h > 0.

x    is the array X, consisting of m input sequences of length Nx, each to be convolved or correlated with the sequence in array H.

Specified as: an array of (at least) length 1+(Nx-1)inc1x+(m-1)inc2x, containing short-precision real numbers.

*inc1x*    is the stride between the elements within each sequence in array X.

Specified as: a fullword integer; inc1x > 0.

*inc2x*    is the stride between the first elements of the sequences in array X.

Specified as: a fullword integer; inc2x > 0.

y    See “On Return” on page 836.

*inc1y*    is the stride between the elements within each sequence in output array Y.

Specified as: a fullword integer; inc1y > 0.