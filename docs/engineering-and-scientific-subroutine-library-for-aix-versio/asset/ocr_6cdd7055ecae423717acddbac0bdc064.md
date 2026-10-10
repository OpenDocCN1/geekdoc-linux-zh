For example, if you specify $X(2)$ for vector $x$, where $X$ is declared as $X(1:9)$ and defined as:

X = (1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0)

and if you specify a stride of $-2$, and four elements to be processed, processing begins at the following element in $X$:

$X(2+(-4+1)(-2)) = X(8)$

where element $X(8)$ is 8.0.

To find each of the $n$ successive element positions in the array, you successively add the stride to the starting point $n-1$ times. Suppose the formula calculated a starting point of $X(SP)$; the elements selected are:

$X(SP)$
$X(SP+inc)$
$X(SP+(2)inc)$
$X(SP+(3)inc)$
$...$
$...$
$X(SP+(n-1)inc)$

In the above example, the resulting elements selected from $X$ for vector $x$ are $X(8)$, $X(6)$, $X(4)$, and $X(2)$. This makes the resulting vector $x$ appear as follows:

(8.0, 6.0, 4.0, 2.0)

The following general formula can be used to calculate each vector element position in a one-dimensional array:

$x_{i} = X(BEGIN+(-n+i)(inc))$ for $i = 1, n$

# ## Sparse Vector

A sparse vector is a vector having a relatively small number of nonzero elements.

Consider the following as an example of a sparse vector $x$ with $n$ elements, where $n$ is 11, and vector $x$ is:

(0.0, 0.0, 1.0, 0.0, 2.0, 3.0, 0.0, 4.0, 0.0, 5.0, 0.0)

# ## In Storage

There are two storage modes that apply to sparse vectors: full-vector storage mode and compressed-vector storage mode. When a sparse vector is stored in **full-vector storage mode**, all its elements, including its zero elements, are stored in an array.

For example, sparse vector $x$ is stored in full-vector storage mode in a one-dimensional array $X$, as follows:

$X$ = (0.0, 0.0, 1.0, 0.0, 2.0, 3.0, 0.0, 4.0, 0.0, 5.0, 0.0)

When a sparse vector is stored in **compressed-vector storage mode**, it is stored without its zero elements. It consists of two one-dimensional arrays, each with a length of $n_{2}$, where $n_{2}$ is the number of nonzero elements in vector $x$:

+   * The first array contains the nonzero elements of the sparse vector $x$, stored contiguously within the array.

**Note:** The ESSL subroutines do not check that all elements are nonzero. You do not get an error if any elements are zero.