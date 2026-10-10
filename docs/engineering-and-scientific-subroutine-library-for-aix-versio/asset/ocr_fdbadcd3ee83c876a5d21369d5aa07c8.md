should remember that the elements of an array are selected as they are arranged in storage, regardless of the number of dimensions defined in the array. Stride is used to step through array storage until $n$ elements are selected. ESSL processing stops at that point. For example, given the following two-dimensional array, declared as A(1:7, 1:4):

Matrix A is:

$ \begin{bmatrix} 1.0 & 8.0 & 15.0 & 22.0 \\ 2.0 & 9.0 & 16.0 & 23.0 \\ 3.0 & 10.0 & 17.0 & 24.0 \\ 4.0 & 11.0 & 18.0 & 25.0 \\ 5.0 & 12.0 & 19.0 & 26.0 \\ 6.0 & 13.0 & 20.0 & 27.0 \\ 7.0 & 14.0 & 21.0 & 28.0 \end{bmatrix}$

with A(3,1) specified for vector $x$, a stride of 2, and the number of elements to be processed as 12, the resulting vector $x$ is: $$(3.0,\ 5.0,\ 7.0,\ 9.0,\ 11.0,\ 13.0,\ 15.0,\ 17.0,\ 19.0,\ 21.0,\ 23.0,\ 25.0)$$

This is not a conventional use of arrays, and you should be very careful when using this technique.

# Zero Stride

When a zero stride is specified for a vector, the starting point for the vector is the only element used in the computation. The starting point for the vector is at the location specified by the argument for the vector, just as though you had specified a positive stride. For example, if you specify X for vector $x$, where X is defined as: $$x=(5.0,\ 4.0,\ 3.0,\ 2.0,\ 1.0)$$

and you specify the number of elements, $n$, to be processed as 6, then processing begins at the first element, which is 5.0. This element is used for each of the six elements in vector $x$.

This makes the conceptual vector $x$ appear as: $$(5.0,\ 5.0,\ 5.0,\ 5.0,\ 5.0,\ 5.0)$$

The following general formula shows how to calculate each vector position in a one-dimensional array: $$x_{i}=X(\text{BEGIN}) \text{ for } i=1, n$$

# Negative Stride

When a negative stride is specified for a vector, the location specified for the vector is actually the location of the last element in the vector. In other words, the vector is in reverse order in the array: $(x_{n}, x_{n-1}, \ldots, x_{1})$. You specify the end of the vector, $(x_{n})$. ESSL then calculates where the starting point $(x_{1})$ is by using the following arguments:

+   - The location of the vector in the array
+   - The stride for the vector, $inc$
+   - The number of elements, $n$, to be processed

If you specify vector $x$ at location X(BEGIN) in array X with a negative stride of $inc$ and $n$ elements to be processed, then the following formula gives the starting point of vector $x$ in the array: $$X(\text{BEGIN}+( -n+1)(inc))$$