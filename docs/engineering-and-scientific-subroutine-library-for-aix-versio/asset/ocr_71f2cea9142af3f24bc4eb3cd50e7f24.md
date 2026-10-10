# SGESVF and DGESVF

If iopt = 0, 1, 10, or 11, this argument is not used in the computation.  
If iopt = 2 or 12, it is the leading dimension of the array specified for b.  
Specified as: a fullword integer. It must have the following values, where:  
If iopt = 0, 1, 10, or 11, ldb > 0.  
If iopt = 2 or 12, ldb > 0 and ldb >= max(m, n).

+   * **nb**  
+     has the following meaning, where:  
+     If iopt = 0, 1, 10, or 11, this argument is not used in the computation.  
+     If iopt = 2 or 12, it is the number of columns in matrix B.  
+     Specified as: a fullword integer; if iopt = 2 or 12, nb > 0.

+   * **s**  
+     See "On Return."

+   * **m**  
+     is the number of rows in matrices A and B.  
+     Specified as: a fullword integer; m >= 0.

+   * **n**  
+     is the number of columns in matrix A and the number of elements in  
+     vector s.  
+     Specified as: a fullword integer; n >= 0.

+   * **aux**  
+     has the following meaning:  
+     Ifiaux = 0 and error 2015 is unrecoverable, aux is ignored.  
+     Otherwise, it is the storage work area used by this subroutine. Its size is  
+     specified by *naux*.  
+     Specified as: an area of storage, containing numbers of the data type  
+     indicated in Table 124 on page 675.

+   * **naux**  
+     is the size of the work area specified by *aux*—that is, the number of  
+     elements in *aux*.  
+     Specified as: a fullword integer, where:  
+     If naux = 0 and error 2015 is unrecoverable, SGESVF and DGESVF  
+     dynamically allocate the work area used by the subroutine. The work area is  
+     deallocated before control is returned to the calling program.  
+     Otherwise, it must have the following value, where:  
+     If iopt = 0 or 10, naux >= n+max(m, n).  
+     If iopt = 1 or 11, naux >= 2n+max(m, n).  
+     If iopt = 2 or 12, naux >= 2n+max(m, n, nb).

**On Return:**

+   * **a**  
+     has the following meaning, where:  
+     If iopt = 0, or 10, A is overwritten; that is, the original input is not  
+     preserved.  
+     If iopt = 1, 2, 11, or 12, A contains the real orthogonal matrix V, of order n,  
+     in its first n rows and n columns. If iopt = 11 or 12, if the columns of V are  
+     swapped to correspond to the sorted singular values. If m > n, rows n+1,  
+     n+2, ..., m of array A are overwritten; that is, the original input is not  
+     preserved.