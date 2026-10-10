# SPOSV, DPOSV, CPOSV, ZPOSV

$L$ is a unit lower triangular matrix.
$U$ is an upper triangular matrix.

If $n$ is 0, no computation is performed and the subroutine returns after doing some parameter checking. If $n > 0$ and $nrhs$ is 0, no solutions are computed and the subroutine returns after factoring the matrix.

See references [8], [38], and [72].

# Error Conditions

+   * **Resource Errors:** Unable to allocate internal work area.

+   * **Computational Errors:**
+   	* Matrix $A$ is not positive definite.
+   	* The order $i$ of the **first** minor encountered having a nonpositive determinant is identified in the computational error message.
+   	* The computational error message may occur multiple times with processing continuing after each error, because the default for the number of allowable errors for error code 2148 is set to be unlimited in the ESLL error option table.

+   * **Input-Argument Errors:**
+   	1. $uplo \neq$ 'U' or 'L'
+   	2. $n < 0$
+   	3. $nrhs < 0$
+   	4. $n > lda$
+   	5. $lda \le 0$
+   	6. $n > ldb$
+   	7. $ldb \le 0$

# Example 1

This example shows how to solve the system $AX = B$, where:
Matrix $A$ is the same used as input in “Example 1” on page 482 for SPOTRF.
Matrix $B$ is the same used as input in “Example 1” on page 490 for SPOTRS.

**Call Statement and Input:**

```
```
          UPLO  N   NRHS  A   LDA   BX    LDB     INFO
            |     |     |     |     |     |       |
CALL SPOSV( 'L' ,   9 ,   2 ,   A ,  9 ,  BX ,  9 , INFO)
```
```

+   * A = (same as input A in “Example 1” on page 482)
+   * BX = (same as input BX in “Example 1” on page 490)

**Output:**

```
```
A  = [ 1.0   .    .    .    .    .    .    .    .   
       1.0  1.0   .    .    .    .    .    .    .   
       1.0  1.0  1.0   .    .    .    .    .    .   
       1.0  1.0  1.0  1.0   .    .    .    .    .   
       1.0  1.0  1.0  1.0  1.0   .    .    .    .   
       1.0  1.0  1.0  1.0  1.0  1.0   .    .    .   
       1.0  1.0  1.0  1.0  1.0  1.0  1.0   .    .   
       1.0  1.0  1.0  1.0  1.0  1.0  1.0  1.0   .   
       1.0  1.0  1.0  1.0  1.0  1.0  1.0  1.0  1.0 ]
```
```