Gaussian elimination performs successive row transformations on the concatenated matrix having the objective of transforming the left-side of the concatenated matrix—the original A matrix—into the identity and the right side into the inverted form of A.

This requires three discrete steps. The first step is to convert the matrix into triangular form, in which the transformations systematically set each element of the bottom triangle to zeros beginning with the lower-left element and each element along each upper-left to lower-right diagonal as shown below.

![](bbox=[0.118, 0.294, 0.733, 0.355])

For purpose of this simple example, assume that the original A matrix contains no zero elements. This allows the matrix to be converted to triangular form using the following row transformations:

+   1. set element (3,0) to zero R3 → R3−($A_{3,0}/A_{2,0}$)R2
2. set element (2,0) to zero R2 → R2−($A_{2,0}/A_{1,0}$)R1
3. set element (3,1) to zero R3 → R3−($A_{3,1}/A_{2,1}$)R1
4. set element (1,0) to zero R1 → R1−($A_{1,0}/A_{0,0}$)R0
5. set element (2,1) to zero R2 → R2−($A_{2,1}/A_{1,1}$)R1
6. set element (3,2) to zero R3 → R3−($A_{3,2}/A_{2,2}$)R1

This gives the result:

| R0 | 1.0 | 2.0 | 3.0 | 1.0 | 0.0 | 0 | 0 |
| R1 | 0 | -3.0 | -2.0 | -1.0 | -2.0 | 1.0 | 0 | 0 |
| R2 | 0 | 0 | -10.3 | -2.7 | -2.3 | -1.3 | 1.0 | 0 |
| R3 | 0 | 0 | 0 | 0.9 | 1.2 | -1.0 | -1.2 | 1 |

Assuming the input matrix is stored in row-major order in array a and the identity matrix is stored in array b, the code that performs this is as follows:

```
for (i=3; i>0; i--) {
    for (j=0; j<4; j++) {
        coeff = -a[(i+j)*4+j]/a[((i+j)-1)*4+j];
        for (k=0; k<4; k++) {
            b[(i+j)*4+k] += coeff * b[((i+j)-1)*4+k];
            a[(i+j)*4+k] += coeff * a[((i+j)-1)*4+k];
        }
    }
}
```