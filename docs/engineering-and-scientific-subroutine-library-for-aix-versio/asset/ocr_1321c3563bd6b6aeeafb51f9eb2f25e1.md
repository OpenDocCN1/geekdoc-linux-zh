# ### In Storage

The positive definite symmetric tridiagonal matrix is stored in the same way the symmetric tridiagonal matrix is stored. For a description of this storage technique, see “Symmetric Tridiagonal Matrix” on page 89.

# ## Sparse Matrix

A sparse matrix is a matrix having a relatively small number of nonzero elements.

Consider the following as an example of a sparse matrix A:

![](bbox=[0.41, 0.24, 0.59, 0.32])

# ### In Storage

A sparse matrix can be stored in full-matrix storage mode or a packed storage mode. When a sparse matrix is stored in **full-matrix storage mode**, all its elements, including its zero elements, are stored in an array.

The seven packed storage modes used for storing sparse matrices are described in the following sections:

+   - “Compressed-Matrix Storage Mode”
+   - “Compressed-Diagonal Storage Mode” on page 91
+   - “Storage-by-Indices” on page 94
+   - “Storage-by-Columns” on page 95
+   - “Storage-by-Rows” on page 95
+   - “Diagonal-Out Skyline Storage Mode” on page 97
+   - “Profile-In Skyline Storage Mode” on page 99

> **Note:** When the elements of a sparse matrix are stored using any of these storage modes, the ESSL subroutines do not check that all elements are nonzero. You do not get an error if any elements are zero.

**Compressed-Matrix Storage Mode:** The sparse matrix A, stored in compressed-matrix storage mode, uses two two-dimensional arrays to define the sparse matrix storage, A C and K A . See reference [75]. Given the m by n sparse matrix A, having a maximum of n z nonzero elements in each row:

+   - A C is defined as AC(lda,nz), where the leading dimension, lda, must be greater than or equal to m. Each row of array A C contains the nonzero elements of the corresponding row of matrix A. For each row in matrix A containing less than n z nonzero elements, the corresponding row in array A C is padded with zeros. The elements in each row can be stored in any order.

+   - K A is an integer array defined as KA(lda,nz), where the leading dimension, lda, must be greater than or equal to m. It contains the column numbers of the matrix A elements that are stored in the corresponding positions in array A C. For each row in matrix A containing less than n z nonzero elements, the corresponding row in array K A is padded with any values from 1 to n. **Because this array is used by the ESSL subroutines to access other target vectors in the computation, you must adhere to these required values to avoid errors.**