# # SGETRI, DGESI, CGETRI, ZGETRI, SGEICD, and DGEICD

n is the order of matrix A. 
   Specified as: a fullword integer; 0 ≤ n ≤ lda.

iopt indicates the type of computation to be performed, where:  
   If iopt = 0, the inverse is computed for matrix A. 
   If iopt = 1, the inverse and the reciprocal of the condition number are computed for matrix A. 
   If iopt = 2, the inverse and the determinant are computed for matrix A. 
   If iopt = 3, the inverse, the reciprocal of the condition number, and the determinant are computed for matrix A. 
   If iopt = 4, the inverse is computed using the factored matrix A. 
   Specified as: a fullword integer; iopt = 0, 1, 2, 3, 4.

rcond See "On Return" on page 521.

det See "On Return" on page 521.

aux has the following meaning, and its size is specified by naux:  
   If iopt = 0, 1, 2, or 3, then if naux = 0 and error 2015 is unrecoverable, aux is ignored. Otherwise, it is the storage work area used by this subroutine. 
   If iopt = 4, aux has the following meaning:  
   - For SGEICD, the first n locations in aux must contain the ipvt integer vector of length n, resulting from a previous call to CGEEF, SGETRF, or SGEECD. 
   - For DGEICD, the first ceiling(n/2) locations in aux must contain the ipvt integer vector of length n, resulting from a previous call to DGEEF, DGETRF, DGEECD, or DGEEFP. 
   Specified as: an area of storage, containing numbers of the data type indicated in Table 107 on page 519.

naux is the size of the work area specified by aux; that is, the number of elements in aux. 
   Specified as: a fullword integer, where:  
   If iopt ≠ 4, then if naux = 0 and error 2015 is unrecoverable, SGEICD and DGEICD dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program. 
   Otherwise, naux ≥ 100n. 
   Note: naux values specified for releases prior to ESSL Version 2 Release 2 will still work, but you may not achieve optimal performance.

ipvt is the integer vector ipvt of length n, containing the pivot indices resulting from a previous call to SGETRF, DGERTF, CGETRF, or ZGETRF. 
   Specified as: a one-dimensional array of (at least) length n, containing fullword integers, where 1 ≤ ipvt(i) ≤ n.

work has the following meaning:  
   If lwork = 0, work is ignored. 
   If lwork ≠ 0, work is the work area used by this subroutine, where: