
# SGETMI、DGETMI、CGETMI 和 ZGETMI

![](img/5b0f44f3be6048723819b26aed7f6f03_449_0.png)

原地矩阵转置操作 $A \leftarrow A^{T}$ 表示为：

![](img/5b0f44f3be6048723819b26aed7f6f03_449_1.png)

如果 $n$ 为 0，则不执行计算。

## 错误条件

计算错误：无

输入参数错误：
- 1. $n < 0$ 或 $n > \mathbf{lda}$
- 2. $\mathbf{lda} \leq 0$

## 示例

此示例展示了矩阵 $A$ 的原地矩阵转置，该矩阵有 5 行和 5 列。

**调用语句和输入：**

```
 A LDA N
|
CALL SGETMI( A(2,3) , 10 , 5 )
```

![](img/5b0f44f3be6048723819b26aed7f6f03_449_2.png)

**输出：**

![](img/5b0f44f3be6048723819b26aed7f6f03_449_3.png)

# SGETMO、DGETMO、CGETMO 和 ZGETMO

## SGETMO、DGETMO、CGETMO 和 ZGETMO——通用矩阵转置（非原地）

这些子例程将 $m$ 乘 $n$ 的矩阵 $A$ 进行非原地转置，并将结果返回到矩阵 $B$ 中：

$B \leftarrow A^{\mathrm{T}}$

### 表 86. 数据类型

| A, B | 子例程 |
| :--- | :--- |
| 短精度实数 | SGETMO |
| 长精度实数 | DGETMO |
| 短精度复数 | CGETMO |
| 长精度复数 | ZGETMO |

### 语法

| Fortran | CALL SGETMO \| DGETMO \| CGETMO \| ZGETMO ($a$, $\text{lda}$, $m$, $n$, $b$, $\text{ldb}$) |
| :--- | :--- |
| C 和 C++ | sgetmo \| dgetmo \| cgetmo \| zgetmo ($a$, $\text{lda}$, $m$, $n$, $b$, $\text{ldb}$); |

### 输入时：

- $a$ 是具有 $m$ 行和 $n$ 列的矩阵 $A$。
    - 指定为：一个 $\text{lda}$ 乘（至少）$n$ 的数组，包含表 86 中指示的数据类型数值。
- $\text{lda}$ 是为 $a$ 指定的数组的 leading dimension（首维）。
    - 指定为：一个 fullword（全字长）整数；$\text{lda} > 0$ 且 $\text{lda} \geq m$。
- $m$ 是矩阵 $A$ 的行数和矩阵 $B$ 的列数。
    - 指定为：一个 fullword（全字长）整数；$m \geq 0$。
- $n$ 是矩阵 $A$ 的列数和矩阵 $B$ 的行数。
    - 指定为：一个 fullword（全字长）整数；$n \geq 0$。
- $b$ 参见“返回时”。
- $\text{ldb}$ 是为 $b$ 指定的数组的 leading dimension（首维）。
    - 指定为：一个 fullword（全字长）整数；$\text{ldb} > 0$ 且 $\text{ldb} \geq n$。

### 返回时：

- $b$ 是具有 $n$ 行和 $m$ 列的矩阵 $B$，包含矩阵转置操作的结果，即 $A^{\mathrm{T}}$。返回为：一个 $\text{ldb}$ 乘（至少）$m$ 的数组，包含表 86 中指示的数据类型数值。

### 注释

- 1. 矩阵 $B$ 不得与矩阵 $A$ 有任何共同元素；否则，结果不可预测。请参阅第 55 页的“概念”。
- 2. 为了在 CGETMO 中实现最佳性能，请将 $a$ 和 $b$ 指定的数组对齐到双字（doubleword）边界。

## 功能

矩阵 $A$ 进行非原地转置；即，矩阵 $A$ 中的 $m$ 行和 $n$ 列存储在矩阵 $B$ 的 $n$ 行和 $m$ 列中。对于元素为 $a_{ij}$ 的矩阵 $A$，其中 $i = 1, m$ 且 $j = 1, n$，非原地转置表示为 $b_{ji} = a_{ij}$，其中 $i = 1, m$ 且 $j = 1, n$。

对于以下输入矩阵 $A$：

![](img/5b0f44f3be6048723819b26aed7f6f03_452_0.png)

非原地矩阵转置操作 $B \leftarrow A^{T}$ 表示为：

![](img/5b0f44f3be6048723819b26aed7f6f03_452_1.png)

如果 $m$ 或 $n$ 为 0，则不执行计算。

### 错误条件

计算错误：无

输入参数错误：
- 1. $m < 0$ 或 $m > lda$
- 2. $n < 0$ 或 $n > ldb$
- 3. $lda \leq 0$
- 4. $ldb \leq 0$

### 示例 1

此示例展示了矩阵 $A$ 的非原地矩阵转置，该矩阵有 5 行和 4 列，结果存入矩阵 $B$。

**调用语句和输入：**

```
CALL SGETMO( A(2,3) , 10 , 5 , 4 , B(2,2) , 6 )
```

![](img/5b0f44f3be6048723819b26aed7f6f03_452_2.png)

**输出：**

```
B = [
       1.0 2.0 3.0 4.0 5.0
       6.0 7.0 8.0 9.0 10.0
       11.0 12.0 13.0 14.0 15.0
       16.0 17.0 18.0 19.0 20.0
     ]
```

### 示例 2

此示例使用与示例 1 相同的输入矩阵 $A$，表明只要输入数据和输出数据不重叠，转置可以在同一数组中实现。在输出时，数组中的输入数据不会被覆盖。

**调用语句和输入：**

```
        A    LDA     M     N    B     LDB
        |     |      |     |    |      |
CALL SGETMO( A(2,3), 10, 5, 4, A(7,1), 10 )
```

```
A = [
       . . . . . .
       . . 1.0 6.0 11.0 16.0 .
       . . 2.0 7.0 12.0 17.0 .
       . . 3.0 8.0 13.0 18.0 .
       . . 4.0 9.0 14.0 19.0 .
       . . 5.0 10.0 15.0 20.0 .
       1.0 2.0 3.0 4.0 5.0 . .
       6.0 7.0 8.0 9.0 10.0 . .
       11.0 12.0 13.0 14.0 15.0 . .
       16.0 17.0 18.0 19.0 20.0 . .
     ]
```

# 第 10 章. 线性代数方程

本章描述了提供在四个领域的线性代数方程子例程。

## 线性代数方程子例程概览

本节描述了四个线性代数方程领域中各自的子例程：

- 密集线性代数方程（表 87）
- 带状线性代数方程（表 88）
- 稀疏线性代数方程（表 89）
- 线性最小二乘法（表 90）

**注意：** 某些线性代数方程是根据 Level 2 BLAS、Level 3 BLAS 和 LAPACK 事实标准设计的。如果这些子程序不符合已批准的标准，IBM 将考虑对其进行更新以使其符合。如果 IBM 更新这些子程序，更新可能需要修改调用应用程序。有关 Level 2 和 3 BLAS 的详细信息，请参阅参考文献 [34] 和 [36]。有关 LAPACK 例程的详细信息，请参阅参考文献 [8]。

## 密集线性代数方程子例程

密集线性代数方程子例程为实数和复数通用矩阵及其转置、正定实对称矩阵和复数 Hermitian 矩阵、实对称不定矩阵以及三角矩阵的线性方程组提供解。这些子例程中的一些对应于参考文献 [34]、[36] 和 [8] 中描述的 Level 2 BLAS、Level 3 BLAS 和 LAPACK 例程。

### 表 87. 密集线性代数方程子例程列表

| 描述性名称 | 短精度子例程 | 长精度子例程 | 页码 |
| :--- | :--- | :--- | :--- |
| 通用矩阵分解和多右端向量求解 | SGESV<sup>△</sup> | DGESV<sup>△</sup> | 440 |
| | CGESV<sup>△</sup> | ZGESV<sup>△</sup> | |
| 通用矩阵分解 | SGETRF<sup>△</sup> | DGETRF<sup>△</sup> | 444 |
| | CGETRF<sup>△</sup> | ZGETRF<sup>△</sup> | |
| | SGEF | DGEF | 452 |
| | CGEF | ZGEF | |
| | | DGEF<sup>§</sup> | |
| 通用矩阵、其转置或其共轭转置 | SGGETRS<sup>△</sup> | DGGETRS<sup>△</sup> | 448 |
| 多右端向量求解 | SGETRS<sup>△</sup> | ZGETRS<sup>△</sup> | |
| | SGESM | DCGESM | 459 |
| | CCGESM | | |
| 通用矩阵、其转置或其共轭转置求解 | SGES | DGES | 455 |
| | CGES | ZGES | |
| 通用矩阵分解、条件数倒数和 | SGEFCD | DCGEFCD | 464 |
| 行列式 | | | |
| 正定实对称矩阵分解和多 | SPPSV<sup>△</sup> | DPPSV<sup>△</sup> | 468 |
| 右端向量求解 | | | |
| 正定实对称或复数 Hermitian 矩阵分解和多右端向量求解 | SPOSV<sup>△</sup> | DPOSV<sup>△</sup> | 472 |
| | CPOSV<sup>△</sup> | ZPOSV<sup>△</sup> | |
| 正定实对称或复数 Hermitian 矩阵分解 | SPOTRF<sup>△</sup> | DPOTRF<sup>△</sup> | 477 |
| | CPOTRF<sup>△</sup> | ZPOTRF<sup>△</sup> | |
| | SPOF | DPOF | |
| | CPOF | ZPOF | |
| | SPPTRF<sup>△</sup> | DPPTRF<sup>△</sup> | |
| | SPPF | DPPF | |
| | | DPPF<sup>§</sup> | |
| 正定实对称或复数 Hermitian 矩阵多右端向量求解 | SPOTRS<sup>△</sup> | DPOTRS<sup>△</sup> | 488 |
| | CPOTRS<sup>△</sup> | ZPOTRS<sup>△</sup> | |
| | SPOSM | DPOSM | |
| | CPOSM | ZPOSM | |
| | SPPTRS<sup>△</sup> | DPPTRS<sup>△</sup> | |
| 正定实对称矩阵求解 | SPFS | DPFS | 495 |
| 正定实对称矩阵分解、条件数倒数和行列式 | SPFFCD | DPFFCD | 498 |
| | SPOFCD | DPOFCD | |
| 对称不定矩阵分解和多右端向量求解 | | DBSSV | 504 |
| 对称不定矩阵分解 | | DBSTRF | 510 |
| 对称不定矩阵多右端向量求解 | | DBSTRS | 515 |
| 通用矩阵逆、条件数倒数和行列式 | SGETRI<sup>△</sup> | DGETRI<sup>△</sup> | 519 |
| | CGETRI<sup>△</sup> | ZGETRI<sup>△</sup> | |
| | SGEICD | DGEICD | |
| 正定实对称或复数 Hermitian 矩阵逆、条件数倒数和行列式 | SPOTRI<sup>△</sup> | DPOTRI<sup>△</sup> | 526 |
| | CPOTRI<sup>△</sup> | ZPOTRI<sup>△</sup> | |
| | SPFICD | DPFICD | |
| | SPOICD | DPOICD | |
| 具有单个右端向量的三角方程组求解 | STRSV* | DTRSV* | 535 |
| | CTRSV* | ZTRSV* | |
| | STPSV* | DTPSV* | |
| | CTPSV* | ZTPSV* | |
| 具有多个右端向量的三角方程组求解 | STRSM* | DTRSM* | 541 |
| | CTRSM* | ZTRSM* | |
| 三角矩阵逆 | STRTRI<sup>△</sup> | DTRTRI<sup>△</sup> | 548 |
| | CTRTRI<sup>△</sup> | ZTRTRI<sup>△</sup> | |
| | STPTRI<sup>△</sup> | DTPTRI<sup>△</sup> | |
| | CTPTRI<sup>△</sup> | ZTPTRI<sup>△</sup> | |
| | STRI<sup>§</sup> | DTRI<sup>§</sup> | |
| | STPI<sup>§</sup> | DTPI<sup>§</sup> | |

<sup>*</sup> Level 2 BLAS  
<sup>△</sup> LAPACK  
<sup>§</sup> 此子例程仅提供用于从早期版本的 ESRL 迁移，不用于新程序。不再提供此子例程的文档。


