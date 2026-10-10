```
IPARM(1)  =  20
IPARM(2)  =    0
IPARM(3)  =    0
RPARM(1)  =  1.0-7
```

AD   = $\begin{bmatrix} 2.0 & -1.0 & 0.0 \\ 2.0 & -1.0 & 0.0 \\ 2.0 & -1.0 & 0.0 \\ 2.0 & -1.0 & 0.0 \\ 2.0 & -1.0 & 1.0 \\ 2.0 & -1.0 & 1.0 \\ 2.0 & -1.0 & 1.0 \\ 2.0 & 0.0 & 1.0 \\ 2.0 & 0.0 & 1.0 \end{bmatrix}$

LA    =   (0,  2,  -4)      
B     =   (1,  1,  1,  1,  2,  2,  2,  3,  3)
X     =   (0,  0,  0,  0,  0,  0,  0,  0,  0)

**Output:**
X       =   (1.0,  1.0,  1.0,  1.0,  1.0,  1.0,  1.0,  1.0,  1.0)    
IPARM(4) =    8
RPARM(3) =  0.308D-17

# ## Example 2

This example finds the solution of the linear system $Ax = b$ for the same sparse matrix *A* as in Example 1, which is stored in compressed-diagonal storage mode in arrays *AD* and *LA*. The system is solved using the generalized minimum residual method, restarted after 5 steps and preconditioned with an incomplete LU factorization. Most of the input is the same as in Example 1.

# **Call Statement and Input:**

```
       M      ND      AD    LDA     LA    B     X     IPARM     RPARM     AUX1    NAUX1     AUX2    NAUX2    
       |      |       |     |       |     |     |       |       |       |       |       |       |       |
CALL DSDGCG( 9 ,    3 ,  AD ,    9 ,  LA ,  B , X , IPARM , RPARM ,  AUX1 ,   109  ,  AUX2 ,    46  )
```

```
IPARM(1) =   20
IPARM(2) =    5
IPARM(3) =   10
RPARM(1) =   1. D-7
AD       =(same as input AD in Example 1)
LA       =(same as input LA in Example 1)
B        =   (1,  1,  1,  1,  2,  2,  2,  3,  3)
X        =   (0,  0,  0,  0,  0,  0,  0,  0,  0)
```

**Output:**
X       =   (1.0,  1.0,  1.0,  1.0,  1.0,  1.0,  1.0,  1.0,  1.0)   
IPARM(4) =    6
RPARM(3) =  0.250D-15