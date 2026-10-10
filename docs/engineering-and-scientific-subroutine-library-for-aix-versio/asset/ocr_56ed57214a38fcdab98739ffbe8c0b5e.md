# DGEQRF

TAU = [1.000000   1.400000]
INFO = 0

# Example 2

This example shows the $QR$ factorization of a general matrix $A$ of size 4x5.

> **Note**: Because $lwork = 0$, DGEQRF dynamically allocates the work area used by this subroutine.

# Call Statements and Input:

```
```
              M     N     A   LDA TAU     WORK    LWORK   INFO
              |     |     |   |   |        |       |       |
CALL DGEQRF (  4,   5,   A,   4, TAU,  WORK,   0,   INFO)
```
General matrix $A$ of size $4 \times 5$:
```

```
```
A = [ .500000   -.500000    1.207107  .000000   1.707107
      .500000  -1.500000   -.500000    2.414214  .707107
      .500000  -.500000     .207107   .000000    .292893
      .500000  -1.500000   -.500000   -.414214  -.707107]
```
```

# Output:

General matrix $A$ of size $4 \times 5$:

```
```
A = [-1.000000   1.000000   -.207107  -1.000000  -1.000000
     .333333     2.000000    1.207107  -1.000000   1.000000
     .333333     -.200000    .707107   .000000     1.000000
     .333333      .400000    .071068   -2.000000  -1.000000]
```
```

Vector $\boldsymbol{\tau}$ of length 4:

```
```
TAU = [ 1.500000   1.666667   1.989949   .000000 ]
INFO = 0
```
```