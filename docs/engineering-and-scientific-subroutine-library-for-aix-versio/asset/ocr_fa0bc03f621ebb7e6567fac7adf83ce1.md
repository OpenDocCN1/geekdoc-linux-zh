Call Statement and Input:

```
```
                  N  A  NA    IDIAG  ITRAN   AUX    NAUX
                  |  |  |      |      |       |       |
   CALL DSKTRN( 9 , A , 33 , IDIAG , ITRAN , AUX , 9  )

   A          = (11.0, 22.0, 12.0, 33.0, 23.0, 13.0, 44.0, 34.0, 24.0,
                 14.0, 55.0, 45.0, 35.0, 25.0, 66.0, 56.0, 46.0, 36.0,
                 26.0, 77.0, 67.0, 57.0, 47.0, 88.0, 78.0, 68.0, 58.0, 48.0,
                 38.0, 28.0, 99.0, 89.0, 79.0, 69.0)
   IDIAG      = (1,  2,  4,  7,  11,  15,  20,  23, 30, 34)
   ITRAN      = (0, 1, -1)
```
```

Output:

```
```
   A          = (11.0, 12.0, 22.0, 13.0, 23.0, 33.0, 14.0, 24.0, 34.0,
                 44.0, 25.0, 35.0, 45.0, 55.0, 26.0, 36.0, 46.0, 56.0,
                 66.0, 57.0, 67.0, 77.0, 28.0, 38.0, 48.0, 58.0, 68.0,
                 78.0, 88.0, 69.0, 79.0, 89.0, 99.0)
   IDIAG      = (1,  3,  6, 10, 14, 19, 22, 29, 33, 34)
```
```

# Example 2

This example shows how to convert the same 9 by 9 symmetric sparse matrix $A$ in Example 1 from profile-in skyline storage mode to diagonal-out skyline storage mode.

Assuming that DSKFS last performed a solve on matrix $A$, the direction of the transformation is positive; that is, ITRAN(3) is 1. This provides the best performance here.

Call Statement and Input:

```
```
                  N  A  NA    IDIAG  ITRAN   AUX    NAUX
                  |  |  |      |      |       |       |
   CALL DSKTRN( 9 , A , 33 , IDIAG , ITRAN , AUX , 9  )

   A          =(same as output A in Example 1)
   IDIAG      =(same as output IDIAG in Example 1)
   ITRAN      = (1,  0,  1)
```
```

Output:

```
```
   A          =(same as input A in Example 1)
   IDIAG      =(same as input IDIAG in Example 1)
```
```