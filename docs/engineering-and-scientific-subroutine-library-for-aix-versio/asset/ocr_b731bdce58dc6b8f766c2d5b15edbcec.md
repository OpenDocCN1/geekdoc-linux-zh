# # Use Considerations

This section describes some key points about using the matrix operations subroutines.

# ## Specifying Normal, Transposed, or Conjugate Transposed Input Matrices

On each invocation, the matrix operation subroutines can perform one of several possible computations, using different forms of the input matrices $A$ and $B$. For the real and complex versions of the subroutines, there are four and nine combinations, respectively, depending on the characters specified for the $transa$ and $transb$ arguments:

+   - **'N'** Normal form
+   - **'T'** Transposed form subroutines)
+   - **'C'** Conjugate transposed form

The four and nine possible combinations are defined as follows:

| Real Combinations | Complex Combinations |
|---|---|
| $AB$ | $AB$ |
| $A^T B$ | $A^T B$ |
|  | $A^H B$ |
| $AB^T$ | $AB^T$ |
| $A^T B^T$ | $A^T B^T$ |
|  | $A^H B^T$ |
|  | $A B^H$ |
|  | $A^T B^H$ |
|  | $A^H B^H$ |

# ## Transposing or Conjugate Transposing:

This section describes some key points about using transposed and conjugate transposed matrices.

# ### On Input

In every case, the input arrays for the matrix, its transpose, or its conjugate transpose should be stored in the original untransposed form. You then specify the desired form of the matrix to be used in the computation in the $transa$ or $transb$ arguments. For a description of matrix transpose and matrix conjugate transpose, see “Matrices” on page 61.

# ### On Output

If you want to compute the transpose or the conjugate transpose of a matrix operation—that is, the output stored in matrix $C$—you should use the matrix identities described in Special Usage for each subroutine description. Examples are provided in the subroutine descriptions to show the use of these matrix identities. This accomplishes the transpose or conjugate transpose as part of the multiply operation.