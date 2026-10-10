most rapidly and the value of the second (column) subscript expression increasing least rapidly. Following are the locations of the elements in the array:

| Relative Location | Array Element |
| :--- | :--- |
| 1 | A(E1,F1) (starting column 1) |
| 2 | A(E1+1,F1) |
| ... | ... |
| E2−E1+1 | A(E2,F1) |
| (E2−E1+1)+1 | A(E1,F1+1) (starting column 2) |
| (E2−E1+1)+2 | A(E1+1,F1+1) |
| ... | ... |
| (E2−E1+1)(2) | A(E2, F1+1) |
| (E2−E1+1)(2)+1 | A(E1,F1+2) (starting column 3) |
| (E2−E1+1)(2)+2 | A(E1+1,F1+2) |
| ... | ... |
| (E2−E1+1)(F2−F1) | A(E2,F2−1) |
| (E2−E1+1)(F2−F1)+1 | A(E1,F2) (starting column F2−F1+1) |
| (E2−E1+1)(F2−F1)+2 | A(E1+1,F2) |
| ... | ... |
| (E2−E1+1)(F2−F1+1) | A(E2,F2) |

For example, the 3 by 4 array A specified in the DIMENSION statement as A(2:4,1:4) and containing the following elements:

```
$A = \begin{bmatrix} 11 & 12 & 13 & 14 \\ 21 & 22 & 23 & 24 \\ 31 & 32 & 33 & 34 \end{bmatrix}$
```

has its elements arranged in storage as follows:

| Relative Location | Array Element Value |
| :--- | :--- |
| 1 | 11 (starting column 1) |
| 2 | 21 |
| 3 | 31 |
| 4 | 12 (starting column 2) |
| 5 | 22 |
| 6 | 32 |
| 7 | 13 (starting column 3) |
| 8 | 23 |
| 9 | 33 |
| 10 | 14 (starting column 4) |
| 11 | 24 |
| 12 | 34 |

Each element A(I,J) of the array A, declared A(1:n, 1:m), containing real or complex data, occupies the storage location whose address is given by the following formula:

```
address {A(I,J)} = address {A} + (I−1) + n(J−1)f
```