+   2. With $init = 0$ , the subroutine checks that the initialization arguments in the $auxl$ working storage correspond to the present arguments, and if so, performs the calculation of the autocorrelations.

# Error Conditions

Resource Errors: Error 2015 is unrecoverable, $n a u x 2 = 0$ , and unable to allocate work area.

Computational Errors: None

Input-Argument Errors:

+   1. $n x$ , $n y$ , $o r m \le 0$ 

+   2. $i n c l x$ , $i n c 2 x$ , $i n c l y$ , $o r i n c 2 y \neq 0$ (or incompatible)

+   3. The resulting correlation is too long.

+   4. The subroutine has not been initialized with the present arguments.

+   5. $n a u x l \le 2 l$ 

+   6. $n a u x l$ is too small-that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.

+   7. Error 2015 is recoverable or $n a u x 2 \neq 0$ , and $n a u x 2$ is too small-that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.

# Example 1

This example shows how to compute an autocorrelation for three short sequences in array X, where the input sequence length $\mathrm{NX}$ is equal to the output sequence length $\mathrm{NY}$. This gives all nonzero autocorrelation values. The arrays are declared as follows:

```
REAL+4 X(0:49999), Y(0:49999)  
REAL+8 AUX1(30788), AUX2(17105)
```

First, initialize $\mathrm{AUX} 1$ using the calling sequence shown below with $\mathrm{INIT} \neq 0$. Then use the same calling sequence with $\mathrm{INIT} = 0$ to do the calculation.

Call Statement and Input:

```
INIT       X     INCIX    INC2X    Y    INC1Y    INC2Y    NX    M     NY      AUX1      AUX2      NAUX2
              |     |      |       |     |        |        |     |     |       |         |         |
CALL SACORF(INIT, X, 1, 7, Y, 1, 7, 3, 7, AUX1, 2959, AUX2, 4354)

INIT   =  1(for initialization)
INIT   =  0(for computation)
```

X contains the following three sequences:

```
1.0 2.0 3.0
2.0 1.0 2.0
3.0 2.0 1.0
4.0 3.0 2.0
4.0 4.0 3.0
3.0 4.0 4.0
2.0 3.0 4.0
```

Output: $\mathrm{Y}$ contains the following three sequences:

```
59.0  59.0  59.0
54.0  50.0  44.0
43.0  39.0  30.0
```