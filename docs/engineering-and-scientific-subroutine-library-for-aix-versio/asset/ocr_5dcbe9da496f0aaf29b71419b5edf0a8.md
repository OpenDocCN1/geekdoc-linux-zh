![](bbox=[0.29, 0.09, 0.74, 0.3])

# In Storage

The two storage modes used for storing general band matrices are described in the following sections:

+   * "General-Band Storage Mode"
+   * "BLAS-General-Band Storage Mode" on page 79

**General-Band Storage Mode:** (This storage mode is used only for square matrices.) Only the band elements of a general band matrix are stored for general-band storage mode. Additional storage must be provided for fill- in. General-band storage mode packs the matrix elements by columns into a two-dimensional array, such that each diagonal of the matrix appears as a row in the packed array.

For a matrix $A$ of order $n$ with band widths $ml$ and $mu$, the array must have a leading dimension, $lda$, greater than or equal to $2ml+mu+16$. The size of the second dimension must be (at least) $n$, the number of columns in the matrix.

Using array `AGB`, which is declared as `AGB(2ml+mu+16, n)`, the columns of elements in matrix $A$ are stored in each column in array `AGB` as follows, where $a_{11}$ is stored at `AGB(ml+mu+1, 1)`: