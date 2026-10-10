# ## SCON and SCOR

40.0   50.0   52.0
29.0   38.0   47.0
18.0   25.0   32.0
8.0    12.0   16.0

# ## Example 4

This example shows how to compute a correlation of a sequence in H, which is a ramp function, and three sequences in X, a triangular function and its cyclic translates. It computes the full range of nonzero values of the correlation plus two extra points, which are set to 0. The arrays are declared as follows:

```
REAL+4    H(0:4999), X(0:4999), Y(0:4999)
REAL+8    AUX1, AUX2
```

# ### Call Statement and Input:

```
INIT   H   INC1H   X   INC1X   INC2X   Y   INC1Y   INC2Y   NH   NX   M   IY0   NY   AUX1   NAUX1   AUX2   NAUX2
CALL   SCOR(INIT, H , 1 , X , 1 , 10 , Y , 1 , 15 , 4, 10, 3, -3, 15, AUX1 , 0 , AUX2 , 0 )
```

```
INIT  =  0(for computation)
H     =  (1.0, 2.0, 3.0, 4.0)
```

X contains the following three sequences:

1.0   2.0   3.0
2.0   1.0   2.0
3.0   2.0   1.0
4.0   3.0   2.0
5.0   4.0   3.0
6.0   5.0   4.0
5.0   6.0   5.0
4.0   5.0   6.0
3.0   4.0   5.0
2.0   3.0   4.0

**Output: Y** contains the following three sequences:

4.0    8.0   12.0
11.0   10.0   17.0
20.0   15.0   16.0
30.0   22.0   18.0
40.0   30.0   22.0
50.0   40.0   30.0
52.0   50.0   40.0
48.0   52.0   50.0
40.0   48.0   52.0
30.0   40.0   48.0
16.0   22.0   28.0
7.0    10.0   13.0
2.0    3.0    4.0
0.0    0.0    0.0
0.0    0.0    0.0

# ## Example 5

This example shows how the output from Example 4 differs when the values for NY and INC2Y are 10 rather than 15. The output is the same except that it consists of only the first 10 values produced in Example 4.

**Output: Y** contains the following three sequences:

4.0    8.0   12.0
11.0   10.0   17.0
20.0   15.0   16.0
30.0   22.0   18.0
40.0   30.0   22.0