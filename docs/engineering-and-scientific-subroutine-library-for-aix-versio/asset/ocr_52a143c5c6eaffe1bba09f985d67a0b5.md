# SRCFT3 and DRCFT3

the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to ESSL” on page 38.

**n2**  is the length of the second dimension of the three-dimensional data in the array to be transformed.

Specified as: a fullword integer; *n2* ≤ 37748736 and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. For all other values specified less than 37748736, you have the option of having the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to ESSL” on page 38.

**n3**  is the length of the third dimension of the three-dimensional data in the array to be transformed.

Specified as: a fullword integer; *n3* ≤ 37748736 and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. For all other values specified less than 37748736, you have the option of having the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to ESSL” on page 38.

**isign**  controls the direction of the transform, determining the sign *Isign* of the exponents of *Wn1*, *Wn2*, and *Wn3*, where:

If *isign* = positive value, *Isign* = +(transforming time to frequency).

If *isign* = negative value, *Isign* = −(transforming frequency to time).

Specified as: a fullword integer; *isign* > 0 or *isign* < 0.

**scale**  is the scaling constant *scale*. See “Function” on page 815 for its usage.

Specified as: a number of the data type indicated in Table 147 on page 812, where *scale* > 0.0 or *scale* < 0.0.

**aux**  has the following meaning:

If *naux* = 0 and error 2015 is unrecoverable, *aux* is ignored.

Otherwise, it is a storage work area used by this subroutine.

Specified as: an area of storage, containing *naux* long-precision real numbers. On output, the contents are overwritten.

**naux**  is the number of doublewords in the working storage area specified in *aux*.

Specified as: a fullword integer, where:

If *naux* = 0 and error 2015 is unrecoverable, SRCFT3 and DRCFT3 dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.

Otherwise, *naux* ≥ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For all other values specified less than the minimum value, you have the option of having the minimum value returned in this argument. For details, see “Using Auxiliary Storage in ESSL” on page 32.

# On Return:

**y**  is the array *Y*, containing the elements resulting from the three-dimensional discrete Fourier transform of the data in *X*. Each element *y* *k1k2k3*, using zero-based indexing, is stored in *Y*(*k1*+*k2*(*inc2*)+*k3*(*inc3*)). For *k1* = 0, 1, ..., *n1*/2, *k2* = 0, 1, ..., *n2*−1, and *k3* = 0, 1, ..., *n3*−1. Due to complex conjugate symmetry, the output consists of only the first *n1*/2+1 values along the first dimension of the array, for *k1* = 0, 1, ..., *n1*/2. The strides for the