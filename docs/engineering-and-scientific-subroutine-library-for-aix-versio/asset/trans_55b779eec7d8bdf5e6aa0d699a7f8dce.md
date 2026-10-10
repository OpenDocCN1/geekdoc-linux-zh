
# SGESUB, DGESUB, CGESUB, 和 ZGESUB

## 示例 6
本示例展示了计算 $C \leftarrow A-B$ 的过程，其中 $A$、$B$ 和 $C$ 分别包含在更大的数组 $A$、$B$ 和 $C$ 中，并且这些数组包含复数数据。

**调用语句和输入：**

```
CALL CGESUB( A , 6 , 'N' , B , 5 , 'N' , C , 5 , 4 , 3 )
```

$$
\begin{array}{ll}
A &= \begin{bmatrix}
(1.0, 5.0) & (9.0, 2.0) & (1.0, 9.0) \\
(2.0, 4.0) & (8.0, 3.0) & (1.0, 8.0) \\
(3.0, 3.0) & (7.0, 5.0) & (1.0, 7.0) \\
(6.0, 6.0) & (3.0, 6.0) & (1.0, 4.0) \\
\cdot & \cdot & \cdot
\end{bmatrix}
\end{array}
$$

$$
\begin{array}{ll}
B &= \begin{bmatrix}
(1.0, 8.0) & (2.0, 7.0) & (3.0, 2.0) \\
(4.0, 4.0) & (6.0, 8.0) & (6.0, 3.0) \\
(6.0, 2.0) & (4.0, 5.0) & (4.0, 5.0) \\
(7.0, 2.0) & (6.0, 4.0) & (1.0, 6.0) \\
\cdot & \cdot & \cdot
\end{bmatrix}
\end{array}
$$

**输出：**

$$
\begin{array}{ll}
C &= \begin{bmatrix}
(0.0, -3.0) & (7.0, -5.0) & (-2.0, 7.0) \\
(-2.0, 0.0) & (2.0, -5.0) & (-5.0, 5.0) \\
(-3.0, 1.0) & (3.0, 0.0) & (-3.0, 2.0) \\
(-1.0, 4.0) & (-3.0, 2.0) & (0.0, -2.0) \\
\cdot & \cdot & \cdot
\end{bmatrix}
\end{array}
$$

# SGEMUL, DGEMUL, CGEMUL, 和 ZGEMUL——通用矩阵、其转置或共轭转置的矩阵乘法

SGEMUL 和 DGEMUL 可以使用矩阵 $A$ 和 $B$ 或其转置以及矩阵 $C$ 执行以下任一矩阵乘法：

- $C \leftarrow A B$
- $C \leftarrow A^{T} B$
- $C \leftarrow A B^{T}$
- $C \leftarrow A^{T} B^{T}$

CGEMUL 和 ZGEMUL 可以使用矩阵 $A$ 和 $B$、其转置或共轭转置以及矩阵 $C$ 执行以下任一矩阵乘法：

- $C \leftarrow A B$
- $C \leftarrow A^{H} B$
- $C \leftarrow A^{H} B^{H}$
- $C \leftarrow A B^{T}$
- $C \leftarrow A^{T} B^{T}$
- $C \leftarrow A^{H} B^{T}$
- $C \leftarrow A B^{H}$
- $C \leftarrow A^{T} B^{H}$
- $C \leftarrow A^{H} B^{H}$

表 78. 数据类型

| | A, B, C | 子程序 |
|---|---|---|
| | 单精度实数 | SGEMUL |
| | 双精度实数 | DGEMUL |
| | 单精度复数 | CGEMUL |
| | 双精度复数 | ZGEMUL |

## 语法

| Fortran | CALL SGEMUL \| DGEMUL \| CGEMUL \| ZGEMUL (a, lda, transa, b, ldb, transb, c, ldc, l, m, n) |
|---|---|
| C 和 C++ | sgemul \| dgemul \| cgemul \| zgemul (a, lda, transa, b, ldb, transb, c, ldc, l, m, n); |

## 进入时：

$a$ 是矩阵 $A$，其中：

- 如果 $transa$ = 'N'，计算中使用 $A$，且 $A$ 有 $l$ 行和 $m$ 列。
- 如果 $transa$ = 'T'，计算中使用 $A^T$，且 $A$ 有 $m$ 行和 $l$ 列。
- 如果 $transa$ = 'C'，计算中使用 $A^H$，且 $A$ 有 $m$ 行和 $l$ 列。

**注意：** 不应移动数据以形成 $A^T$ 或 $A^H$；即，矩阵 $A$ 始终以非转置形式存储。

指定为：一个二维数组，包含表 78 中所示数据类型的数字，其中：

- 如果 $transa$ = 'N'，其大小必须为 $lda$ 乘以（至少）$m$。
- 如果 $transa$ = 'T' 或 'C'，其大小必须为 $lda$ 乘以（至少）$l$。

$lda$ 是指定给 $a$ 的数组的前导维度。

指定为：一个全字整数；$lda > 0$ 且：

- 如果 $transa$ = 'N'，$lda \geq 1$。
- 如果 $transa$ = 'T' 或 'C'，$lda \geq m$。

$transa$ 指示在计算中使用的矩阵 $A$ 的形式，其中：

- 如果 $transa$ = 'N'，计算中使用 $A$。
- 如果 $transa$ = 'T'，计算中使用 $A^{T}$。
- 如果 $transa$ = 'C'，计算中使用 $A^{H}$。
- 指定为：单个字符；对于 SGEMUL 和 DGEMUL，$transa$ = 'N' 或 'T'；对于 CGEMUL 和 ZGEMUL，$transa$ = 'N'、'T' 或 'C'。

$b$ 是矩阵 $B$，其中：

- 如果 $transb$ = 'N'，计算中使用 $B$，且 $B$ 有 $m$ 行和 $n$ 列。
- 如果 $transb$ = 'T'，计算中使用 $B^{T}$，且 $B$ 有 $n$ 行和 $m$ 列。
- 如果 $transb$ = 'C'，计算中使用 $B^{H}$，且 $B$ 有 $n$ 行和 $m$ 列。

**注意：** 不应移动数据以形成 $B^{T}$ 或 $B^{H}$；即，矩阵 $B$ 始终以非转置形式存储。

指定为：一个二维数组，包含表 78（第 377 页）中所示数据类型的数字，其中：

- 如果 $transb$ = 'N'，其大小必须为 $ldb$ 乘以（至少）$n$。
- 如果 $transb$ = 'T' 或 'C'，其大小必须为 $ldb$ 乘以（至少）$m$。

$ldb$ 是指定给 $b$ 的数组的前导维度。
指定为：一个全字整数；$ldb > 0$ 且：

- 如果 $transb$ = 'N'，$ldb \geq m$。
- 如果 $transb$ = 'T' 或 'C'，$ldb \geq n$。

$transb$ 指示在计算中使用的矩阵 $B$ 的形式，其中：

- 如果 $transb$ = 'N'，计算中使用 $B$。
- 如果 $transb$ = 'T'，计算中使用 $B^{T}$。
- 如果 $transb$ = 'C'，计算中使用 $B^{H}$。
- 指定为：单个字符；对于 SGEMUL 和 DGEMUL，$transb$ = 'N' 或 'T'；对于 CGEMUL 和 ZGEMUL，$transb$ = 'N'、'T' 或 'C'。

$c$ 参见“返回时”（第 379 页）。

$ldc$ 是指定给 $c$ 的数组的前导维度。
指定为：一个全字整数；$ldc > 0$ 且 $ldc \geq 1$。

$l$ 是矩阵 $C$ 的行数。
指定为：一个全字整数；$0 \le l \le ldc$。

$m$ 具有以下含义，其中：

- 如果 $transa$ = 'N'，它是矩阵 $A$ 的列数。
- 如果 $transa$ = 'T' 或 'C'，它是矩阵 $A$ 的行数。

此外：

- 如果 $transb$ = 'N'，它是矩阵 $B$ 的行数。
- 如果 $transb$ = 'T' 或 'C'，它是矩阵 $B$ 的列数。

$n$ 是矩阵 $C$ 的列数。
指定为：一个全字整数；$n \geq 0$。

## 返回时：

$c$ 是 $l$ 乘以 $n$ 的矩阵 $C$，包含计算结果。返回为：$ldc$ 乘以（至少）$n$ 个表 78（第 377 页）中所示数据类型的数字。

## 备注

1. 所有子程序接受 $transa$ 和 $transb$ 参数的小写字母。
2. 矩阵 C 不得与矩阵 $A$ 或 $B$ 有任何共同元素；否则，结果不可预测。参见“概念”（第 55 页）。

## 功能
矩阵乘法表示如下，其中 $a_{ik}$、$b_{kj}$ 和 $c_{ij}$ 分别是矩阵 $A$、$B$ 和 $C$ 的元素：

$c_{ij} = \sum_{k=1}^{m} a_{ik} \, b_{kj}$ 对应于 $C \leftarrow A \, B$

$c_{ij} = \sum_{k=1}^{m} \overline{a}_{ki} \, b_{kj}$ 对应于 $C \leftarrow A^{T} \, B$

$c_{ij} = \sum_{k=1}^{m} \overline{a}_{ki} \, b_{kj}$ 对应于 $C \leftarrow A^{H} \, B$

$c_{ij} = \sum_{k=1}^{m} a_{ik} \, b_{jk}$ 对应于 $C \leftarrow A \, B^{T}$

$c_{ij} = \sum_{k=1}^{m} a_{ki} \, b_{jk}$ 对应于 $C \leftarrow A^{T} \, B^{T}$

$c_{ij} = \sum_{k=1}^{m} \overline{a}_{ki} \, b_{jk}$ 对应于 $C \leftarrow A^{H} \, B^{T}$

$c_{ij} = \sum_{k=1}^{m} \overline{a}_{ik} \, \overline{b}_{jk}$ 对应于 $C \leftarrow A \, B^{H}$

$c_{ij} = \sum_{k=1}^{m} a_{ki} \, \overline{b}_{jk}$ 对应于 $C \leftarrow A^{T} \, B^{H}$

$c_{ij} = \sum_{k=1}^{m} \overline{a}_{ki} \, \overline{b}_{jk}$ 对应于 $C \leftarrow A^{H} \, B^{H}$

对于 $i = 1$，$l$ 和 $j = 1$，$n$

参见参考文献 [40]。如果 $l$ 或 $n$ 为 0，则不执行任何计算。如果 $l$ 和 $n$ 大于 0，且 $m$ 为 0，则返回一个 $l$ 乘以 $n$ 的零矩阵。

# 特殊用法

**等价规则：** 通过以下等价规则，您可以计算这些子程序执行的某些计算的转置 $C^T$ 或共轭转置 $C^{H}$：

**转置**

$(AB)^T = B^T A^T$

$(A^T B)^T = B^T A$

**共轭转置**

$(AB)^H = B^{H} A^{H}$

$(A^H B)^H = B^H A$

$(AB^H)^H = BA^H$

$(A^H B^{H})^{H} = BA$

在编写这些情况的调用序列时，请小心按照规则指示的顺序编写矩阵参数和维度参数。另外，请小心您的输出数组（接收 $C^T$ 或 $C^{H}$）的维度足够大，以容纳结果转置或共轭转置矩阵。参见“示例 2”（第 381 页）和“示例 4”（第 383 页）。

