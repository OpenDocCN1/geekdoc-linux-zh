# Table 181. Level 2 BLAS Included in ESSL (continued)

| Descriptive Name | Short- Precision Subprogram | Long- Precision Subprogram |
|---|---|---|
| Rank-One Update of a Real Symmetric or Complex Hermitian Matrix | SSPR CHPR SSYR CHER | DSPPR ZHPPR DSYR ZHER |
| Rank-Two Update of a Real Symmetric or Complex Hermitian Matrix | SSPR2 CHPR2 SSYR2 CHER2 | DSPPR2 ZHPPR2 DSYR2 ZHER2 |
| Matrix-Vector Product for a General Band Matrix, Its Transpose, or Its Conjugate Transpose | SGBMV CGBMV | DGBMV ZGBMV |
| Matrix-Vector Product for a Real Symmetric or Complex Hermitian Band Matrix | SSBMV CHBMV | DSBMV ZHBMV |
| Matrix-Vector Product for a Triangular Matrix, Its Transpose, or Its Conjugate Transpose | STPMV CTPMV STRMV CTRMV | DTPMV ZTPMV DTRMV ZTRMV |
| Solution of a Triangular System of Equations with a Single Right-Hand Side | STPSV CTPSV STRSV CTRSV | DTPSV ZTPSV DTRSV ZTRSV |
| Matrix-Vector Product for a Triangular Band Matrix, Its Transpose, or Its Conjugate Transpose | STBMV CTBMV | DTBMV ZTBMV |
| Triangular Band Equation Solve | STBSV CTBSV | DTBSV ZTBSV |

# Level 3 BLAS

# Table 182. Level 3 BLAS Included in ESSL.

| Descriptive Name | Short- Precision Subprogram | Long- Precision Subprogram |
|---|---|---|
| Combined Matrix Multiplication and Addition for General Matrices, Their Transposes, or Conjugate Transposes | SGEMM CGEMM | DGEMM ZGEMM |
| Matrix-Matrix Product Where One Matrix is Real or Complex Symmetric or Complex Hermitian | SSYMM CSYMM CHEMM | DSYMM ZSYMM ZHEMM |
| Triangular Matrix-Matrix Product | STRMM CTRMM | DTRMM ZTRMM |
| Rank-K Update of a Real or Complex Symmetric or a Complex Hermitian Matrix | SSYRK CSYRK CHERK | DSYRK ZSYRK ZHERK |
| Rank-2K Update of a Real or Complex Symmetric or a Complex Hermitian Matrix | SSYR2K CSYR2K CHER2K | DSYR2K ZSYR2K ZHER2K |
| Solution of Triangular Systems of Equations with Multiple Right-Hand Sides | STRSM CTRSM | DTRSM ZTRSM |