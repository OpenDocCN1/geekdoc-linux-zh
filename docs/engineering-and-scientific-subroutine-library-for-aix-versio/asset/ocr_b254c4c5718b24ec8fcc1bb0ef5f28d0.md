# SSPR2, DSPR2, CHPR2, ZHPR2, SSYR2, DSYR2, CHER2, ZHER2, SSLR2, and DSLR2

+   * $ap$ is the matrix *A* of order *n*, containing the results of the computation. Returned as: a one-dimensional array, containing numbers of the data type indicated in Table 70 on page 319.

+   * *a* is the matrix *A* of order *n*, containing the results of the computation. Returned as: a two-dimensional array, containing numbers of the data type indicated in Table 70 on page 319.

# Notes

+   1. All subroutines accept lowercase letters for the *uplo* argument.

+   2. The vectors **x** and **y** must have no common elements with matrix *A*; otherwise, results are unpredictable. See "Concepts" on page 55.

+   3. On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix *A* are assumed to be zero, so you do not have to set these values. On output, if $\alpha \neq$ zero, the imaginary parts of the diagonal elements are set to zero.

+   4. For a description of how symmetric matrices are stored in upper- or lower-packed storage mode and upper or lower storage mode, see "Symmetric Matrix" on page 64. For a description of how complex Hermitian matrices are stored in upper- or lower-packed storage mode and upper or lower storage mode, see "Complex Hermitian Matrix" on page 69.

# Function

These subroutines perform the computation described in the two sections below. See references [36], [37], and [81]. If *n* or $\alpha$ is zero, no computation is performed.

For SSPR2, SSYR2, SSLR2, CHPR2, and CHER2, intermediate results are accumulated in long precision.

**SSPR2, DSPR2, SSYR2, DSYR2, SSLR2, and DSLR2:** These subroutines compute the rank-two update of a real symmetric matrix:

$$A \leftarrow A + \alpha x y^T + \alpha y x^T$$

where:
* *A* is a real symmetric matrix of order *n*.
* $\alpha$ is a scalar.
* **x** is a vector of length *n*.
* $\mathbf{x}^{\mathrm{T}}$ is the transpose of vector **x**.
* **y** is a vector of length *n*.
* $\mathbf{y}^{\mathrm{T}}$ is the transpose of vector **y**.

It is expressed as follows: