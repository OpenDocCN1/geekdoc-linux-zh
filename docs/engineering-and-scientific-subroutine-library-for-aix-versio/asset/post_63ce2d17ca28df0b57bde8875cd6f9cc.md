
In some cases, you can specify a different algorithm in `IPARM(2)` when making calls with `init = 'S'`. (See “Example 2” on page 644.) However, DSRIS sometimes needs different information in `auxI` for different algorithms. When this occurs, DSRIS issues an attention message, continues processing the computation, and then requests the contents of `auxI`. Your performance is not improved in this case, which is functionally equivalent to calling DSRIS with `init = 'T'`.

- If you use the CG method with `init = 'T'`, you must use the CG method when you specify `init = 'S'`. However, if you use a different method with `init = 'T'`, you can use any other method, except CG, when you specify `init = 'S'`.
- These subroutines accept lowercase letters for the `stor` and `init` arguments.
- Matrix *A*, vector *x*, and vector *b* must have no common elements; otherwise, results are unpredictable.
- In this subroutine, a value of `IPARM(1) = 0` is permitted to force the solver to evaluate exactly `IPARM(1)` iterations. The algorithm computes a sequence of approximate solution vectors *x* that converge to the solution. The iterative procedure is stopped when the selected stopping criterion is satisfied or when more than the maximum number of iterations (in `IPARM(1)`) is reached.
    For the stopping criteria specified in `IPARM(5)`, the relative accuracy *ε* (in `RPARM(1)`) must be specified reasonably ($10^{-3}$ to $10^{-5}$). If you specify a larger *ε*, the algorithm takes fewer iterations to converge to a solution. If you specify a smaller *ε*, the algorithm requires more iterations and computer time, but converges to a more precise solution. If the value you specify is unreasonably small, the algorithm may fail to converge within the number of iterations it is allowed to perform.
- For a description of how sparse matrices are stored by rows, see “Storage-by-Rows” on page 95.
- You have the option of having the minimum required value for *nax* dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSL” on page 32.

## Function

The linear system:

$$ Ax = b $$

is solved using one of the following methods: conjugate gradient (CG), conjugate gradient squared (CGS), generalized minimum residual (GMRES), more smoothly converging variant of the CGS method (Bi-CGSTAB), or transpose-free quasi-minimal residual method (TFQMR), where:

- *A* is a sparse matrix of order *n*. The matrix is stored in arrays *AR, IA*, and *JA*. If it is general, it is stored by rows. If it is symmetric, it can be stored using *upper-* or *lower-storage-by-rows*.
- *x* is a vector of length *n*.
- *b* is a vector of length *n*.

One of the following preconditioners is used:

- an incomplete LU factorization
- an incomplete Cholesky factorization (for positive definite symmetric matrices)
- diagonal scaling
- symmetric successive over-relaxation (SSOR) with two possible choices for the diagonal matrix:
    - the absolute values sum of the input matrix
    - the diagonal obtained from the LU factorization

See references [38], [58], [84], [89], [92], and [98].

When you call this subroutine to solve a system for the first time, you specify *init* = 'T'. After that, you can solve the same system any number of times by calling this subroutine each time with *init* = 'S'. These subsequent calls use the coefficient matrix and preconditioner, stored in internal format in *aux1*. You optimize performance by doing this, because certain portions of the computation have already been performed.

## Error Conditions

**Resource Errors:** Error 2015 is unrecoverable, *naux* = 2, and unable to allocate work area.

**Computational Errors:** The following errors, with their corresponding return codes, can occur in this subroutine. For details on error handling, see “What Can You Do about ESSL Computational Errors?” on page 47.

- For error 2110, return code 1 indicates that the subroutine exceeded IPARM(1) iterations without converging. Vector $x$ contains the approximate solution computed at the last iteration.
- For error 2130, return code 2 indicates that the incomplete LU factorization of $A$ could not be completed, because one pivot was 0.
- For error 2124, the subroutine has been called with *init* = 'S', but the data contained in *aux1* was computed for a different algorithm. An attention message is issued. Processing continues, and the contents of *aux1* are reset correctly.
- For error 2134, return code 3 indicates that the data contained in *aux1* is not consistent with the input sparse matrix. The subroutine has been called with *init* = 'S', and *aux1* contains an incomplete factorization and internal data storage for the input matrix $A$ that was computed by a previous call to the subroutine when *init* = 'T'. This error indicates that *aux1* has been modified since the last call to the subroutine, or that the input matrix is not the same as the one that was factored. If the default action has been overridden, the subroutine can be called again with the same parameters, with the exception of IPARM(4) = 1 or 4.
- For error 2131, return code 4 indicates that the matrix is singular, because all elements in one row of the matrix contain zero.
- For error 2129, return code 5 indicates that the matrix is not positive definite.
- For error 2128, return code 8 indicates an internal ESSL error. Please contact your IBM Representative.

**Input-Argument Errors:**

1. $n < 0$
2. *stor* ≠ 'G', 'U', or 'L'
3. *init* ≠ 'T' or 'S'
4. IA($n+1$) $< 1$
5. IA($i+1$) − IA($i$) $< 0$, for any $i = 1, n$
6. IPARM(1) $< 0$
7. IPARM(2) $\neq 1, 2, 3, 4$, or 5
8. IPARM(3) $\leq 0$ and IPARM(2) = 3
9. IPARM(4) $\neq 1, 2, 3, 4$, or 5
10. RPARM(1) $< 0$
11. RPARM(3) $\leq 0$ and IPARM(4) = 3
12. *naux1* is too small—that is, less than the minimum required value. Return code 6 is returned if error 2015 is recoverable.
13. Error 1015 is recoverable or $n_{\text{aux2}} = 0$ and $n_{\text{aux2}}$ is too small—that is, less than the minimum required value. Return code 7 is returned for $n_{\text{aux2}}$ if error 1015 is recoverable.

## Example 1

This example finds the solution of the linear system \(\boldsymbol{Ax} = \boldsymbol{b}\) for the sparse matrix \(\boldsymbol{A}\), which is stored by rows in arrays \(\boldsymbol{AR}\), \(\boldsymbol{IA}\), and \(\boldsymbol{JA}\). The system is solved using the Bi-CGSTAB algorithm. The iteration is stopped when the norm of the residual is less than the given threshold specified in RPARM(1). The algorithm is allowed to perform 20 iterations. The process converges after 9 iterations. Matrix \(\boldsymbol{A}\) is:

![](img/5b0f44f3be6048723819b26aed7f6f03_667_0.png)

### Call Statement and Input:

```fortran
                  STOR  INIT     N      AR      JA      IA     B     X      IPARM    RPARM    AUX1     NAUX1     AUX2     NAUX2
                   |      |       |      |       |       |     |     |      |        |        |        |        |        |
CALL DSRIS( 'G' , 'I' , 9 , AR , JA , IA , B , X , IPARM , RPARM , AUX1 , 98 , AUX2 , 63 )
AR   = (2.0, 2.0, -1.0, 1.0, 2.0, 1.0, 2.0, -1.0, 1.0, 2.0, -1.0,
        1.0, 2.0, -1.0, 1.0, 2.0, -1.0, 1.0, 2.0, -1.0, 1.0, 2.0, 2.0)
JA   = (1, 2, 3, 2, 3, 1, 4, 5, 4, 5, 6, 5, 6, 7, 7, 8, 7, 8,
         9, 8, 9)
IA   = (1, 2, 4, 6, 9, 12, 15, 18, 21, 23)
B    = (2.0, 1.0, 3.0, 2.0, 2.0, 2.0, 2.0, 2.0, 3.0)
X    = (0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0)
IPARM(1) = 20
IPARM(2) = 4
IPARM(3) = 0
IPARM(4) = 1
IPARM(5) = 10
RPARM(1) = 1.0 D-7
RPARM(3) = 1.0
```

### Output:

```
X          = (1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0)
IPARM(6)  = 9
RPARM(2)  = 0.29D-16
```

## Example 2

This example finds the solution of the linear system \(\boldsymbol{Ax} = \boldsymbol{b}\) for the same sparse matrix \(\boldsymbol{A}\) used in Example 1. It also uses the same right-hand side in \(\boldsymbol{b}\) and the same initial guesses in \(\boldsymbol{x}\). However, the system is solved using a different algorithm, conjugate gradient squared (CGS). Because INIT is S, the best performance is achieved. The iteration is stopped when the norm of the residual is less than the given threshold specified in RPARM(1). The algorithm is allowed to perform 20 iterations. The process converges after 9 iterations.
