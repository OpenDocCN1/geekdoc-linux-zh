**Upper-Triangular-Band-Packed Storage Mode**: Only the band elements of the upper triangular part of an upper triangular band matrix, including the main diagonal, are stored for upper-triangular-band-packed storage mode.

For a matrix $\mathbf{U}$ of order $n$ and an upper band width of $k$, the array must have a leading dimension, $lda$, greater than or equal to $k+1$, and the size of the second dimension must be (at least) $n$.

Using array UTB, which is declared as $UTB(lda,n)$, where $p = lda = k+1$, the elements of an upper triangular band matrix are stored as follows:

![](bbox=[0.25, 0.36, 0.8, 0.5])

where “$*$” means you do not store an element in that position in the array.

Following is an example of an upper triangular band matrix $\mathbf{U}$ of order 6 and an upper band width of 3.

Given the following matrix $\mathbf{U}$:

![](bbox=[0.4, 0.72, 0.6, 0.8])

you store it in upper-triangular-band-packed storage mode in array UTB, declared as $UTB(4,6)$, as follows:

![](bbox=[0.35, 0.89, 0.65, 0.95])

Following is an example of how to transform your upper triangular band matrix to upper-triangular-band-packed storage mode:

```
```
DO 20 J=1,N
    M=K+1-J
    DO 10 I=MAX(1,J-K),J
        UTB(M+I,J)=U(I,J)
    10 CONTINUE
20 CONTINUE
```
```