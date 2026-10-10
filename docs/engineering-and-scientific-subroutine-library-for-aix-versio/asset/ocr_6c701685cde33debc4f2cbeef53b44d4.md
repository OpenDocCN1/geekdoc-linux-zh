+   *   The second array contains a sequence of integers indicating the element positions (indices) of the nonzero elements of the sparse vector x stored in full-vector storage mode. This is referred to as the indices array.

For example, the sparse vector x shown above might have its five nonzero elements stored in ascending order in array X of length 5, as follows:

X = (1.0, 2.0, 3.0, 4.0, 5.0)

in which case, the array of indices, INDEX, also of length 5, contains:

INDEX = (3, 5, 6, 8, 10)

If the sparse vector x has its elements stored in random order in the array X as:

X = (5.0, 3.0, 4.0, 1.0, 2.0)

then the array INDEX contains:

INDEX = (10, 6, 8, 3, 5)

In general terms, this storage technique can be expressed as follows:

+   -   For each xi ≠ 0, for j = 1, n
+       -   there exists i, where 1 ≤ i ≤ nz,
+       -   such that X(i) = xi and INDEX(i) = j.

where:

+   *   x1, ...xn are the n elements of sparse vector x, stored in full-vector storage mode.
+   *   X is the array containing the nz nonzero elements of sparse vector x; that is, vector x is stored in compressed-vector storage mode.
+   *   INDEX is the array containing the nz indices indicating the element positions.

To avoid an error when using the INDEX array to access the elements in any other target vector, the length of the target vector must be greater than or equal to max(INDEX(i)) for i = 1, nz.

# Matrices

A matrix, also referred to as a general matrix, is an m by n ordered collection of numbers. It is represented symbolically as:

```
A = [ a11 · · · a1n
      · · · · · · ·
      a_m1 · · · a_mn ]
```

where the matrix is named A and has m rows and n columns. The elements of the matrix are aij, where i = 1, m and j = 1, n.

Matrices can contain either real or complex numbers. Those containing real numbers are called real matrices; those containing complex numbers are called complex matrices.