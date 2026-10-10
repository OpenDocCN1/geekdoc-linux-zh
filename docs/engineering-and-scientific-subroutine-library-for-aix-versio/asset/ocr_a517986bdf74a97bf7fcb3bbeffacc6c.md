# SGETRI, DGETRI, CGETRI, ZGETRI, SGEICD, and DGEICD

+   - The computational error message may occur multiple times with processing continuing after each error, because the default for the number of allowable errors for error code 2149 is set to be unlimited in the ESSl error option table.

**For SGEICD and DGEICD:**

+   - The index *i* of the first pivot element having a value equal to 0 is identified in the computational error message.
+   - These subroutines return 0 for *rcond* and *det*, if you requested them.
+   - The return code is set to 2.
+   - *i* can be determined at run time by use of the ESSl error-handling facilities. To obtain this information, you must use ERRSET to change the number of allowable errors for error code 2105 in the ESSl error option table; otherwise, the default value causes your program to terminate when this error occurs. For details, see “What Can You Do about ESSl Computational Errors?” on page 47.

**Input-Argument Errors:**

+   1. *lda* ≤ 0
+   2. *n* < 0
+   3. *n* > *lda*
+   4. *iopt* ∉ *0*, 1, 2, 3, or 4
+   5. *lwork* ∉ 0, *lwork* ∉ −1, and *lwork* < max(1, *n*)
+   6. Error 2015 is recoverable or *naux*=0, and *naux* is too small—that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.

# Example 1

This example computes the inverse of matrix A, where matrix A is the transformed matrix factored by SGETRF in “Example 3” on page 447 and the input contents of IPVt are the same as the output contents of IPVt in “Example 3” on page 447.

**Note:** Because *lwork* is 0, SGETRI dynamically allocates the work area used by this subroutine.

**Call Statement and Input:**

```
```
N  A  LDA IPVt   WORK LWORK INFO
CALL SGETRI(9 ,A ,9 , IPVt , WORK , 0 , INFO )
```
```

```
A = (same as output A in “Example 3” on page 447)
IPVt = (same as output IPVt in “Example 3” on page 447)
```

**Output:**

| A = | | | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | 0.333 | -0.667 | 0.333 | 0.000 | 0.000 | 0.000 | 0.042 | -0.042 | 0.000 |
| | 56.833 | -52.167 | -1.167 | -0.500 | -0.500 | -0.357 | 6.836 | -0.479 | -0.500 |
| | -55.167 | 51.833 | 0.833 | 0.500 | 0.500 | 0.214 | -6.735 | 0.521 | 0.500 |
| | -1.000 | 1.000 | 0.000 | 0.000 | 0.000 | 0.143 | -0.143 | 0.000 | 0.000 |
| | -1.000 | 1.000 | 0.000 | 0.000 | 0.000 | 0.000 | 0.000 | 0.000 | 0.000 |
| | -1.000 | 1.000 | 0.000 | 0.000 | 0.000 | 0.000 | -0.125 | 0.125 | 0.000 |
| | -226.000 | 206.000 | 5.000 | 3.000 | 2.000 | 1.429 | -27.179 | 1.750 | -2.000 |
| | 560.000 | -520.000 | -10.000 | -6.000 | -4.000 | -2.857 | 67.857 | -5.000 | -5.000 |
| | -325.000 | 305.000 | 5.000 | 3.000 | 2.000 | 1.429 | -39.554 | 3.125 | 3.000 |

```
INFO = 0
```