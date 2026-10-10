![](bbox=[0.3, 0.09, 0.9, 0.31])

You use the partial factorization function when, for design or storage reasons, you must factor the matrix *A* in stages. When doing a partial factorization, you must use the same skyline storage mode for all parts of the matrix as it is progressively factored.

+   5. Your various arrays must have no common elements; otherwise, results are unpredictable.

+   6. You have the option of having the minimum required value for *naux* dynamically returned to your program. For details, see "Using Auxiliary Storage in ESSL" on page 32.

# Function

This subroutine can factor, compute the determinant of, and solve general sparse matrix *A*, stored in skyline storage mode. For all computations, input matrix *A* can be stored in either diagonal-out or profile-in skyline storage mode. Output matrix *A* can also be stored in either of these modes and can be different from the mode used for input.

Matrix *A* is factored into the following form using specified pivot processing:

```
$A = LU$
```

where:

+   *U* is an upper triangular matrix.

+   *L* is a lower triangular matrix.

The transformed matrix *A*, factored into its *LU* form, is stored in packed format in arrays *AU* and *AL*. The inverse of the diagonal of matrix *U* is stored in the corresponding elements of array *AU*. The off-diagonal elements of the upper triangular matrix *U* are stored in the corresponding off-diagonal elements of array *AU*. The off-diagonal elements of the lower triangular matrix *L* are stored in the corresponding off-diagonal elements of array *AL*. (The diagonal elements stored in array *AL* do not have meaningful values.)

The partial factorization of matrix *A*, which you can do when you specify the factor-only option, assumes that the first *IPARM*(3) rows and columns are already factored in the input matrix. It factors the remaining *n*–*IPARM*(3) rows and columns in matrix *A*. (See "Notes" on page 610 for an illustration.) It updates only the elements in arrays *AU* and *AL* corresponding to the part of matrix *A* that is factored.