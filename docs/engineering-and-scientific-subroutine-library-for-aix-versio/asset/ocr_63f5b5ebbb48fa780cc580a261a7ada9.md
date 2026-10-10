# SGTNPF, DGTNPF CGTNPF, and ZGTNPF

```
```
			N    C    D    E    IOPT
		|    |    |    |    |
	CALL DGTNPF( 4 , C , D , E , 0    )

C      = ( . , 1.0, 1.0, 1.0)
D      = (1.0, 2.0, 3.0, 1.0)
E      = (1.0, 1.0, 1.0, . )

Output:
C      = ( . , -1.0, -1.0, 1.0)
D      = (-1.0, -1.0, -1.0, -1.0)
E      = (1.0, 1.0, -1.0, . )
```
```

# Example 2

This example shows a factorization of the tridiagonal matrix $\boldsymbol{A}$, of order 4:

![](bbox=[0.37, 0.3, 0.73, 0.36])

# Call Statement and Input:

```
```
			N    C    D    E    IOPT
		|    |    |    |    |
	CALL ZGTNPF( 4 , C , D , E , 0    )

C      = ( . , (1.0, 1.0), (2.0, 2.0), (3.0, 3.0))
D      = ((7.0, 7.0), (8.0, 8.0), (9.0, 9.0), (10.0, 10.0))
E      = ((4.0, 4.0), (5.0, 5.0), (6.0, 6.0), . )

Output:
C      = ( . , (-0.142, 0.0), (-0.269, 0.0), (3.0, 3.0))
D      = ((-0.0714, 0.0714), (-0.0673, 0.0673), (-0.0854, 0.0854),
	(-0.05, 0.05))
E      = ((4.0, 4.0), (5.0, 5.0), (-0.6, 0.0), . )
```
```

# Notes:

+   1. A `"./` means you do not have to store a value in that position in the array. However, these storage positions are required and may be overwritten during the computation.