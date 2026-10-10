

## 表 10. 矩阵运算子程序列表（续）

| 描述性名称 | 短精度子程序 | 长精度子程序 | 页码 |
| :--- | :--- | :--- | :--- |
| 一般矩阵或其转置的矩阵减法 | SGESUB<br>CGESUB | DGESUB<br>ZGESUB | 371 |
| 一般矩阵、其转置或共轭转置的矩阵乘法 | SGEMUL<br>CGEMUL | DGEMUL<br>ZGEMUL<br>DGEMUL<sup>a</sup> | 377 |
| 使用 Winograd 变体 Strassen 算法计算一般矩阵、其转置或共轭转置的矩阵乘法 | SGEMMS<br>CGEMMS | DGEMMS<br>ZGEMMS | 386 |
| 一般矩阵、其转置或共轭转置的矩阵乘法与加法组合 | SGEMM\*\*<br>CGEMM\*\* | DGEMM\*\*<br>ZGEMM\*\* | 391 |
| 其中一个矩阵为实对称、复对称或复埃尔米特矩阵的矩阵-矩阵乘积 | SSYMM\*\*<br>CSYM\*\*<br>CHEMM\*\* | DSYMM\*\*<br>CSYM\*\*<br>ZHEMM\*\* | 399 |
| 三角矩阵-矩阵乘积 | STRMM\*\*<br>CTRM M\*\* | DTRMM\*\*<br>ZTRMM\*\* | 406 |
| 实对称、复对称或复埃尔米特矩阵的秩-K 更新 | SSYRK\*\*<br>CSYRK\*\*<br>CHERK\*\* | DSYRK\*\*<br>ZSYRK\*\*<br>ZHERK\*\* | 412 |
| 实对称、复对称或复埃尔米特矩阵的秩-2K 更新 | SSYR2K\*\*<br>CSYR2K\*\*<br>CHE R2K\*\* | DSYR2K\*\*<br>ZSYR2K\*\*<br>ZHER2K\*\* | 418 |
| 一般矩阵转置（原地） | SGETMI<br>CGETMI | DGETMI<br>ZGETMI | 425 |
| 一般矩阵转置（非原地） | SGETMO<br>CGETMO | DGETMO<br>ZGETMO | 428 |

\* 3 级 BLAS

<sup>a</sup> 此子程序仅用于从早期版本 ESSL 迁移，不打算用于新程序中。

## 线性代数方程

-   线性代数方程包括：
    -   稠密线性代数方程（表 11）
    -   带状线性代数方程（表 12）
    -   稀疏线性代数方程（表 13）
    -   线性最小二乘法（表 14）

> 注意：某些线性代数方程是根据 2 级 BLAS、3 级 BLAS 以及 LAPACK 事实标准设计的。如果这些子程序不符合批准的标准，IBM 将考虑对其进行更新以使其符合。如果 IBM 更新了这些子程序，更新可能需要对调用应用程序进行修改。有关 2 级和 3 级 BLAS 的详细信息，请参阅 [34] 和 [36]。有关 LAPACK 的详细信息，请参阅 [8]。

## 稠密线性代数方程

稠密线性代数方程子程序为实和复一般矩阵及其转置、正定实对称和复埃尔米特矩阵、实对称不定矩阵以及三角矩阵的线性方程组提供解。这些子程序中的某些对应于参考文献 [34]、[36] 和 [8] 中描述的 2 级 BLAS、3 级 BLAS 和 LAPACK 例程。

### 表 11. 稠密线性代数方程子程序列表

| 描述性名称 | 短精度子程序 | 长精度子程序 | 页码 |
| :--- | :--- | :--- | :--- |
| 一般矩阵分解和多个右端项求解 | SGE<sup>‡</sup><br>CGES<sup>‡</sup> | DGES<sup>‡</sup><br>ZGES<sup>‡</sup> | 440 |
| 一般矩阵分解 | SGET<sup>†</sup><br>CGET<sup>†</sup> | DGET<sup>†</sup><br>ZGET<sup>†</sup> | 444 |
| | SGES<br>CGES | DGES<br>ZGES | 452 |
| | DGEF<br>ZGEF<br>DGEFF<sup>a</sup> | | |
| 一般矩阵、其转置或其共轭转置<br>多个右端项求解 | SGES<sup>‡</sup><br>CGES<sup>‡</sup> | DGES<sup>‡</sup><br>ZGES<sup>‡</sup> | 448 |
| | SGESM<br>CGESM | DGESM<br>ZGESM | 459 |
| 一般矩阵、其转置或其共轭转置求解 | SGES<br>CGES | DGES<br>ZGES | 455 |
| 一般矩阵分解、条件数倒数和行列式 | SGEFCD | DGEFCD | 464 |
| 正定实对称矩阵分解和<br>多个右端项求解 | SPPSV<sup>‡</sup> | DPYSV<sup>‡</sup> | 468 |
| 正定实对称或复埃尔米特矩阵<br>分解和多个右端项求解 | SPOSV<sup>‡</sup><br>CPOSV<sup>‡</sup> | DPOSV<sup>‡</sup><br>ZPOSV<sup>‡</sup> | 472 |
| 正定实对称或复埃尔米特矩阵<br>分解 | SPOT<sup>†</sup><br>CPOT<sup>†</sup><br>SPOF<br>CPPTRF<sup>‡</sup><br>SPPF | DPOF<sup>†</sup><br>ZPOF<sup>†</sup><br>DPOF<br>ZPOF<br>DPPTRF<sup>‡</sup><br>DPFF<br>DPPFP<sup>a</sup> | 477 |
| 正定实对称或复埃尔米特矩阵<br>多个右端项求解 | SPOTS<sup>‡</sup><br>CPOSS<sup>‡</sup><br>SPOSM<br>CPOSM<br>SPPTRS<sup>‡</sup> | DPOTS<sup>‡</sup><br>ZPOTS<sup>‡</sup><br>DPOSM<br>ZPOSM<br>DPPTRS<sup>‡</sup> | 488 |
| 正定实对称矩阵求解 | SPPS | DPPS | 495 |
| 正定实对称矩阵分解、条件<br>数倒数和行列式 | SPPFCD<br>SPOFCD | DPPFCD<br>DPOFCD | 498 |
| 对称不定矩阵分解和多个<br>右端项求解 | | DBSSV | 504 |
| 对称不定矩阵分解 | | DBSTRF | 510 |
| 对称不定矩阵多个右端项求解 | | DBSTRS | 515 |
| 一般矩阵逆、条件数倒数和<br>行列式 | SGET<sup>†</sup><br>CGET<sup>†</sup><br>SQEIC | DGET<sup>†</sup><br>ZGET<sup>†</sup><br>DGEICD | 519 |
| 正定实对称或复埃尔米特矩阵<br>逆、条件数倒数和行列式 | SPOT<sup>†</sup><br>CPO<sup>†</sup><br>SPPICD<br>SPOICD | DPOT<sup>†</sup><br>ZPO<sup>†</sup><br>DPPICD<br>DPOICD | 526 |

### 表 11. 稠密线性代数方程子程序列表（续）

| 描述性名称 | 短精度子程序 | 长精度子程序 | 页码 |
| :--- | :--- | :--- | :--- |
| 具有单个右端项的三角方程组求解 | STRSV\*\*<br>CTRSV\*\*<br>STPSV\*\*<br>CTPSV\*\* | DTRSV\*\*<br>ZTRSV\*\*<br>DTPSV\*\*<br>ZTPSV\*\* | 535 |
| 具有多个右端项的三角方程组求解 | STRSM\*\*<br>CTRSM\*\* | DTRSM\*\*<br>ZTRSM\*\* | 541 |
| 三角矩阵逆 | STRTRI<sup>◆</sup><br>CTRTRI<sup>◆</sup><br>STPTRI<sup>◆</sup><br>CTPPRI<sup>◆</sup><br>STRI<sup>§</sup><br>CTRI<sup>§</sup><br>STPI<sup>§</sup> | DTRTRI<sup>◆</sup><br>ZTRTRI<sup>◆</sup><br>DTPTRI<sup>◆</sup><br>ZTPTRI<sup>◆</sup><br>DTPI<sup>§</sup><br>ZTPI<sup>§</sup> | 548 |

\*\* 2 级 BLAS<br>\*\* 3 级 BLAS<br><sup>◆</sup> LAPACK<br><sup>§</sup> 此子程序仅用于从早期版本 ESSL 迁移，不打算用于新程序中。此子程序的文档不再提供。

## 带状线性代数方程

带状线性代数方程子程序为实一般带状矩阵、正定实对称带状矩阵、实或复一般三对角矩阵、正定实对称三对角矩阵以及实或复三角带状矩阵的线性方程组提供解。

### 表 12. 带状线性代数方程子程序列表

| 描述性名称 | 短精度子程序 | 长精度子程序 | 页码 |
| :--- | :--- | :--- | :--- |
| 一般带状矩阵分解 | SGBF | DGBF | 557 |
| 一般带状矩阵求解 | SGBS | DGBS | 561 |
| 正定对称带状矩阵分解 | SPBF<br>SPBCHF | DPBF<br>DPBCHF | 563 |
| 正定对称带状矩阵求解 | SPBS<br>SPBCHS | DPBS<br>DPBCHS | 566 |
| 一般三对角矩阵分解 | SGTF | DGTF | 569 |
| 一般三对角矩阵求解 | SGTS | DGTS | 572 |
| 一般三对角矩阵无旋转的组合分解和求解 | SGTNP<br>CGTNP | DGTNP<br>ZGTNP | 574 |
| 一般三对角矩阵无旋转分解 | SGTNP<br>CGTNP | DGTNP<br>ZGTNP | 577 |
| 一般三对角矩阵无旋转求解 | SGTNS<br>CGTNS | DGTNS<br>ZGTNS | 580 |
| 正定对称三对角矩阵分解 | SPTF | DPTF | 583 |
| 正定对称三对角矩阵求解 | SPTS | DPTS | 585 |
| 三角带状方程求解 | STBSV\*\*<br>CTBSV\*\* | DTBSV\*\*<br>ZTBSV\*\* | 587 |

