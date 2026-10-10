# SCOSF and DCOSF

Specified as: a fullword integer; $n \leq 37748736$ and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. For all other values specified less than 37748736, you have the option of having the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to ESSLL” on page 38.

$m$
is the number of sequences to be transformed.
Specified as: a fullword integer; $m > 0$.

$scale$
is the scaling constant $scale$. See “Function” on page 776 for its usage.
Specified as: a number of the data type indicated in Table 141 on page 773, where $scale > 0.0$ or $scale < 0.0$.

$aux1$
is the *working storage* for this subroutine, where:
If $init \neq 0$, the working storage is computed.
If $init = 0$, the working storage is used in the computation of the Fourier transforms.
Specified as: an area of storage, containing $nau\times l$ long-precision real numbers.

$nau\times l$
is the number of doublewords in the working storage specified in $aux1$.
Specified as: a fullword integer; $nau\times l \geq$ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For all other values specified less than the minimum value, you have the option of having the minimum value returned in this argument. For details, see “Using Auxili ary Storage in ESSLL” on page 32.

$aux2$
has the following meaning:
If $nau\times 2 = 0$ and error 2015 is unrecoverable, $aux2$ is ignored.
Otherwise, it is the working storage used by this subroutine, which is available for use by the calling program between calls to this subroutine.
Specified as: an area of storage, containing $nau\times 2$ long-precision real numbers. On output, the contents are overwritten.

$nau\times 2$
is the number of doublewords in the working storage specified in $aux2$.
Specified as: a fullword integer, where:
If $nau\times 2 = 0$ and error 2015 is unrecoverable, SCOSF and DCOSF dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.
Otherwise, $nau\times 2 \geq$ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For all other values specified less than the minimum value, you have the option of having the minimum value returned in this argument. For details, see “Using Auxili ary Storage in ESSLL” on page 32.

# On Return:

$y$
has the following meaning, where:
If $init \neq 0$, this argument is not used, and its contents remain unchanged.
If $init = 0$, this is array $Y$, consisting of the results of the $m$ discrete Fourier transforms, where each Fourier transform is real and of length $n$. However,

774