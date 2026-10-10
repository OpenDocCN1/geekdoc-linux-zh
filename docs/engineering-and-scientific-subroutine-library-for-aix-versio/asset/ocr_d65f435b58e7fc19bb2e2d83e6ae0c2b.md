starting point for each of the next $p - 1$ successive blocks of elements in the array. The stride, $inc3$, is added to the starting point $p - 1$ times. In this example, the stride for the third dimension is 21, and the number of blocks of elements, $p$, to be processed is 3, so the starting points in array $A$ are $A(2, 2, 1)$, $A(2, 2, 2)$, and $A(2, 2, 3)$. These are elements 30.0, 51.0, and 72.0. These array elements then correspond to the sequence elements $a_{111}$, $a_{112}$, and $a_{113}$, respectively.

In general terms, this results in the following starting positions for the blocks of elements in the array:

```
A(BEGINI, BEGINJ, BEGINK)
A(BEGINI, BEGINJ, BEGINK+1)
A(BEGINI, BEGINJ, BEGINK+2)
.
.
A(BEGINI, BEGINJ, BEGINK+p-1)
```

Using $m=4$, $n=2$, and $p=3$ to define the elements of the three-dimensional data structure in this example, the resulting three-dimensional sequence is defined as follows, in three blocks, for planes 0-2, respectively:

| **Plane 0:** | **Plane 1:** | **Plane 2:** | **Plane 0:** | **Plane 1:** | **Plane 2:** |
| :----------- | :----------- | :----------- | :----------- | :----------- | :----------- |
| $a_{000}$ $a_{010}$ | $a_{101}$ $a_{111}$ | $a_{002}$ $a_{012}$ | 30.0 37.0 | 51.0 58.0 | 72.0 79.0 |
| $a_{100}$ $a_{110}$ | $a_{201}$ $a_{211}$ | $a_{102}$ $a_{112}$ | 31.0 38.0 | 52.0 59.0 | 73.0 80.0 |
| $a_{200}$ $a_{210}$ | $a_{301}$ $a_{311}$ | $a_{202}$ $a_{212}$ | 32.0 39.0 | 53.0 60.0 | 74.0 81.0 |
| $a_{300}$ $a_{310}$ | | $a_{302}$ $a_{312}$ | 33.0 40.0 | 54.0 61.0 | 75.0 82.0 |

As shown in this example, the three-dimensional sequence does not have to include all the blocks of elements in the array. In this case, the three-dimensional sequence includes only the second through the fourth block of elements in the array. The first block is not used. Elements of an array are selected as they are arranged in storage, regardless of the number of dimensions defined in the array. Therefore, when using a one- or two-dimensional array to store your three-dimensional sequence, you should understand how your array elements are stored to ensure that elements are selected properly. See “Setting Up Arrays in Fortran” on page 108 for a description of array storage.

**Note:** Three-dimensional sequences are used by the three-dimensional Fourier transform subroutines. By specifying certain stride values for $inc2$ and $inc3$ and declaring your arrays to have certain number of dimensions, you achieve optimal performance in these subroutines. See “Setting Up Your Data” on page 746 and the Notes section for each subroutine.