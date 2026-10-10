
## Chapter 5. Programming Considerations
- C++ Program Procedures ... 159
- Processing Your Program on Linux ... 160
- Dynamic Linking Versus Static Linking ... 161
- Fortran Program Procedures ... 161
- C Program Procedures ... 162
- C++ Program Procedures ... 162

## Chapter 6. Migrating Your Programs
- Migrating ESSL Version 3 Release 3 Programs to Version 4 Release 1 ... 165
- ESSL Subroutines ... 165
- Planning for Future Migration ... 165
- Migrating between IBM p5server pSeries and R5/6000 Processors ... 166
- Auxiliary Storage ... 166
- Bitwise-Identical Results ... 166
- Migrating from Other Libraries to ESSL ... 166
- Migrating from ESSL/370 ... 166
- Migrating from Another IBM Subroutine Library ... 166
- Migrating from LAPACK ... 166
- Migrating from a Non-IBM Subroutine Library ... 167

## Chapter 7. Handling Problems
- Where to Find More Information About Errors ... 169
- Getting Help from IBM Support ... 169
- National Language Support ... 170
- Dealing with Errors ... 171
- Program Exceptions ... 171
- ESSL Input-Argument Error Messages ... 171
- ESSL Computational Error Messages ... 172
- ESSL Resource Error Messages ... 172
- ESSL Informational and Attention Messages ... 173
- Miscellaneous Error Messages ... 175
- Messages ... 176
- Message Conventions ... 176
- Input-Argument Error Messages(2001-2099) ... 176
- Computational Error Messages(2100-2199) ... 182
- Input-Argument Error Messages(2200-2299) ... 184
- Resource Error Messages(2400-2499) ... 184
- Informational and Attention Error Messages(2600-2699) ... 184
- Miscellaneous Error Messages(2700-2799) ... 184

## Part 2. Reference Information

## Chapter 8. Linear Algebra Subprograms
- Overview of the Linear Algebra Subprograms ... 189
- Vector-Scalar Linear Algebra Subprograms ... 189
- Sparse Vector-Scalar Linear Algebra Subprograms ... 190
- Matrix-Vector Linear Algebra Subprograms ... 191
- Sparse Matrix-Vector Linear Algebra Subprograms ... 192
- Use Considerations ... 192
- Performance and Accuracy Considerations ... 192

### Vector-Scalar Subprograms
- ISAMAX, IDAMAX, ICAMAX, and IZAMAX—Position of the First or Last Occurrence of the Vector Element Having the Largest Magnitude ... 195
- ISAMIN and IDAMIN—Position of the First or Last Occurrence of the Vector Element Having the Minimum Absolute Value ... 198
- ISMAX and IDMAX—Position of the First or Last Occurrence of the Vector Element Having the Maximum Value ... 201
- ISMIN and IDMIN—Position of the First or Last Occurrence of the Vector Element Having the Minimum Value ... 204
- SASUM, DASUM, SCASUM, and DZASUM—Sum of the Magnitudes of the Elements in a Vector ... 207
- SAXPY, DAXPY, CAXPY, and ZAXPY—Multiply a Vector X by a Scalar, Add to a Vector Y, and Store in the Vector Y ... 210
- SCOPY, DCOPY, CCOPY, and ZCOPY—Copy a Vector ... 213
- SDOT, DDOT, CDOTU, ZDOTU, CDOTC, and ZDOTC—Dot Product of Two Vectors ... 216
- SNAXPY and DNAXPY—Compute SAXPY or DAXPY N Times ... 220
- SNDOT and DNDOT—Compute Special Dot Products N Times ... 225
- SNRM2, DNRM2, SCNRM2, and DZNRM2—Euclidean Length of a Vector with Scaling of Input to Avoid Destructive Underflow and Overflow ... 230
- SNORM2, DNORM2, CNORM2, and ZNORM2—Euclidean Length of a Vector with No Scaling of Input ... 233
- SROTG, DROTG, CROTG, and ZROTG—Construct a Givens Plane Rotation ... 236
- SROT, DROT, CROT, ZROT, CSCROT, and ZDCROT—Apply a Plane Rotation ... 242
- SSCAL, DSCAL, CSCAL, ZSCAL, CSSCAL, and ZDSCAL—Multiply a Vector X by a Scalar and Store in the Vector X ... 246
- SSWAP, DSWAP, CSWAP, and ZSWAP—Interchange the Elements of Two Vectors ... 249
- SVEA, DVEA, CVEA, and ZVEA—Add a Vector X to a Vector Y and Store in a Vector Z ... 252
- SVES, DVES, CVES, and ZVES—Subtract a Vector Y from a Vector X and Store in a Vector Z ... 256
- SVEM, DVEM, CVEM, and ZVEM—Multiply a Vector X by a Vector Y and Store in a Vector Z ... 260
- SYAX, DYAX, CYAX, ZYAX, CSYAX, and ZDYAX—Multiply a Vector X by a Scalar and Store in a Vector Y ... 264
- SZAXPY, DZAXPY, CZAXPY, and ZZAXPY—Multiply a Vector X by a Scalar, Add to a Vector Y, and Store in a Vector Z ... 267

### Sparse Vector-Scalar Subprograms
- SSCTR, DSCTR, CSCTR, ZSCTR—Scatter the Elements of a Sparse Vector X into Compressed-Vector Storage Mode into Specified Elements of a Sparse Vector Y in Full-Vector Storage Mode ... 271
- SGTHR, DGTHR, CGTHR, and ZGTHR—Gather Specified Elements of a Sparse Vector Y in Full-Vector Storage Mode into a Sparse Vector X in Compressed-Vector Storage Mode ... 274
- SGTHRZ, DGTHRZ, CGTHRZ, and ZGTHRZ—Gather Specified Elements of a Sparse Vector Y in Full-Vector Mode into a Sparse Vector X in Compressed-Vector Mode, and Zero the Same Specified Elements of Y ... 277
- SAXPYI, DAXPYI, CAXPYI, and ZAXPYI—Multiply a Sparse Vector X in Compressed-Vector Storage Mode by a Scalar, Add to a Sparse Vector Y in Full-Vector Storage Mode, and Store in the Vector Y ... 280
- SDOTI, DDOTI, CDDOTI, ZDDOTI, CDOTCI, and ZDOTCI—Dot Product of a Sparse Vector X in Compressed-Vector Storage Mode and a Sparse Vector Y in Full-Vector Storage Mode ... 283

### Matrix-Vector Subprograms
- SGEMV, DGEMV, CGEMV, ZGEMV, SGEMX, DGEMX, CGEMTX, and ZGEMX—Matrix-Vector Product for a General Matrix, Its Transpose, or Its Conjugate Transpose ... 287
- SGER, DGER, CGERU, ZGERU, CGERC, and ZGERC—Rank-One Update of a General Matrix ... 297
- SSYRV, DSPMV, CHPMV, ZHPMV, SSYVM, DSYVM, CHEMV, ZHEMV, SSLMV, and DSLMX—Matrix-Vector Product for a Real Symmetric or Complex Hermitian Matrix ... 304
- SSPR, DSPR, ZHPR, SSYR, DSYR, CHER, ZHER, SSLR1, and DSLR1—Rank-One Update of a Real Symmetric or Complex Hermitian Matrix ... 312
- SSPR2, DSPR2, CHPR2, ZHPR2, SSYR2, DSYR2, CHER2, ZHER2, SSLR2, and DSLR2—Rank-Two Update of a Real Symmetric or Complex Hermitian Matrix ... 319
- SGBMV, DGBMV, CGBMV, and ZGBMV—Matrix-Vector Product for a General Band Matrix, Its Transpose, or Its Conjugate Transpose ... 327
- SSBMV, DSBMV, CHBMV, and ZHBVM—Matrix-Vector Product for a Real Symmetric or Complex Hermitian Band Matrix ... 333
- STRMV, DTRMV, CTRMV, ZTRMV, STPMV, DTPMV, CTPMV, and ZTPMV—Matrix-Vector Product for a Triangular Matrix, Its Transpose, or Its Conjugate Transpose ... 338
- STBMV, DTBMV, CTBMV, and ZTBVM—Matrix-Vector Product for a Triangular Band Matrix, Its Transpose, or Its Conjugate Transpose ... 344

### Sparse Matrix-Vector Subprograms
- DSMX—Matrix-Vector Product for a Sparse Matrix in Compressed-Matrix Storage Mode ... 350
- DSMT—Transpose a Sparse Matrix in Compressed-Matrix Storage Mode ... 353
- DSDMX—Matrix-Vector Product for a Sparse Matrix or Its Transpose in Compressed-Diagonal Storage Mode ... 357

## Chapter 9. Matrix Operations
- Overview of the Matrix Operation Subroutines ... 361
- Use Considerations ... 362
  - Specifying Normal, Transposed, or Conjugate Transposed Input Matrices ... 362
  - Transposing or Conjugate Transposing ... 362
  - Performance and Accuracy Considerations ... 363
    - In General ... 363
    - For Large Matrices ... 363
    - For Combined Operations ... 363

### Matrix Operation Subroutines
- SGEADD, DGEEADD, CGEADD, and ZGEADD—Matrix Addition for General Matrices or Their Transposes ... 365
- SGESUB, DGESUB, CGESUB, and ZGESUB—Matrix Subtraction for General Matrices or Their Transposes ... 371
- SGEMUL, DGEMUL, CGEMUL, and ZGEMUL—Matrix Multiplication for General Matrices, Their Transposes, or Conjugate Transposes ... 377
- SGEMMS, DGEMMS, CGEMMS, and ZGEMMS—Matrix Multiplication for General Matrices, Their Transposes, or Conjugate Transposes Using Winograd’s Variation of Strassen’s Algorithm ... 386
- SGEMM, DGEMM, CGEMM, and ZGEMM—Combined Matrix Multiplication and Addition for General Matrices, Their Transposes, or Conjugate Transposes ... 391
- SSYM, DSYM, CSSYM, ZSSYM, CHEMM, and ZHEMM—Matrix-Matrix Product Where One Matrix is Real or Complex Symmetric or Complex Hermitian ... 399
- STRMM, DTRMM, CTRMM, and ZTRMM—Triangular Matrix-Matrix Product ... 406
- SYRSK, DSYRK, CSYRK, ZSYRK, CHERK, and ZHERK—Rank-K Update of a Real or Complex Symmetric or Complex Hermitian Matrix ... 412
- SSYR2K, DSYR2K, CSYR2K, ZSYR2K, CHER2K, and ZHER2K—Rank-2K Update of a Real or Complex Symmetric or a Complex Hermitian Matrix ... 418
- SGETM1, DGETM1, CGETM1, and ZGETM1—General Matrix Transpose (In-Place) ... 425
- SGETMO, DGETMO, CGETMO, and ZGETMO—General Matrix Transpose (Out-of-Place) ... 428

## Chapter 10. Linear Algebraic Equations
- Overview of the Linear Algebraic Equation Subroutines ... 431
  - Dense Linear Algebraic Equation Subroutines ... 431
  - Banded Linear Algebraic Equation Subroutines ... 433
  - Sparse Linear Algebraic Equation Subroutines ... 433
  - Linear Least Squares Subroutines ... 434

### Dense and Banded Linear Algebraic Equation Considerations
- Use Considerations ... 434
- Performance and Accuracy Considerations ... 435
- Sparse Matrix Direct Solver Considerations ... 435
