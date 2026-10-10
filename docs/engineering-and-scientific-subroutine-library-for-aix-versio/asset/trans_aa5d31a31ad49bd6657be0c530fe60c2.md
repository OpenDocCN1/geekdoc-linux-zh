
## SGEMM、DGEMM、CGEMM 和 ZGEMM——针对一般矩阵及其转置或共轭转置的矩阵乘法与加法组合运算

SGEMM 和 DGEMM 可以使用标量 $\alpha$ 和 $\beta$、矩阵 $A$ 和 $B$ 或它们的转置以及矩阵 $C$，执行以下任意一种组合矩阵运算：

- $C \leftarrow \alpha AB+\beta C$
- $C \leftarrow \alpha AB^T+\beta C$
- $C \leftarrow \alpha A^TB+\beta C$
- $C \leftarrow \alpha A^TB^T+\beta C$

CGEMM 和 ZGEMM 可以使用标量 $\alpha$ 和 $\beta$、矩阵 $A$ 和 $B$ 及其转置或共轭转置以及矩阵 $C$，执行以下任意一种组合矩阵运算：

- $C \leftarrow \alpha AB+\beta C$
- $C \leftarrow \alpha AB^T+\beta C$
- $C \leftarrow \alpha AB^{H}+\beta C$
- $C \leftarrow \alpha A^TB+\beta C$
- $C \leftarrow \alpha A^TB^T+\beta C$
- $C \leftarrow \alpha A^TB^{H}+\beta C$
- $C \leftarrow \alpha A^{H}B+\beta C$
- $C \leftarrow \alpha A^{H}B^T+\beta C$
- $C \leftarrow \alpha A^{H}B^{H}+\beta C$

### 表 80. 数据类型

| A, B, C, $\alpha$, $\beta$      | 子程序 |
|-----------------------------|------------|
| 短精度实数        | SGEMM      |
| 长精度实数        | DGEMM      |
| 短精度复数     | CGEMM      |
| 长精度复数      | ZGEMM      |

## 语法

| **Fortran** | CALL SGEMM \| DGEMM \| CGEMM \| ZGEMM (transa, transb, l, n, m, alpha, a, lda, b, ldb, beta, c, ldc) |
|----|----|
| **C 和 C++** | sgemm \| dgem \| cgem \| zgem (transa, transb, l, n, m, alpha, a, lda, b, ldb, beta, c, ldc); |

**进入时：**

*transa* 指示在计算中使用的矩阵 A 的形式，其中：

- 如果 transa = 'N'，则在计算中使用 A。
- 如果 transa = 'T'，则在计算中使用 $A^{T}$。
- 如果 transa = 'C'，则在计算中使用 $A^{H}$。

指定为：单个字符；transa = 'N'、'T' 或 'C'。

*transb* 指示在计算中使用的矩阵 B 的形式，其中：

- 如果 transb = 'N'，则在计算中使用 B。
- 如果 transb = 'T'，则在计算中使用 $B^{T}$。
- 如果 transb = 'C'，则在计算中使用 $B^{H}$。

指定为：单个字符；transb = 'N'、'T' 或 'C'。

*l* 是矩阵 C 的行数。

指定为：全字整数；$0 \leq l \leq ldc$。

*n* 是矩阵 *C* 的列数。

指定为：全字整数；$n \geq 0$。

*m* 具有以下含义，其中：

- 如果 *transa* = ‘N’，它是矩阵 *A* 的列数。
- 如果 *transa* = ‘T’ 或 ‘C’，它是矩阵 *A* 的行数。

此外：

- 如果 *transb* = ‘N’，它是矩阵 *B* 的行数。
- 如果 *transb* = ‘T’ 或 ‘C’，它是矩阵 *B* 的列数。
- 指定为：全字整数；$m \geq 0$。

*alpha* 是标量 $\alpha$。

指定为：第 391 页表 80 中指示的数据类型的数值。

*a* 是矩阵 *A*，其中：

- 如果 *transa* = ‘N’，在计算中使用 *A*，且 *A* 有 *l* 行和 *m* 列。
- 如果 *transa* = ‘T’，在计算中使用 $A^{T}$，且 *A* 有 *m* 行和 *l* 列。
- 如果 *transa* = ‘C’，在计算中使用 $A^{H}$，且 *A* 有 *m* 行和 *l* 列。

**注意：** 不应移动数据以形成 $A^{T}$ 或 $A^{H}$；即，矩阵 *A* 始终以未转置的形式存储。

指定为：二维数组，包含第 391 页表 80 中指示的数据类型的数值，其中：

- 如果 *transa* = ‘N’，其大小必须为 *lda* 乘以（至少）*m*。
- 如果 *transa* = ‘T’ 或 ‘C’，其大小必须为 *lda* 乘以（至少）*l*。

*lda* 是为 *a* 指定的数组的先行维。

指定为：全字整数；$lda > 0$ 且：

- 如果 *transa* = ‘N’，$lda \geq l$。
- 如果 *transa* = ‘T’ 或 ‘C’，$lda \geq m$。

*b* 是矩阵 *B*，其中：

- 如果 *transb* = ‘N’，在计算中使用 *B*，且 *B* 有 *m* 行和 *n* 列。
- 如果 *transb* = ‘T’，在计算中使用 $B^{T}$，且 *B* 有 *n* 行和 *m* 列。
- 如果 *transb* = ‘C’，在计算中使用 $B^{H}$，且 *B* 有 *n* 行和 *m* 列。

**注意：** 不应移动数据以形成 $B^{T}$ 或 $B^{H}$；即，矩阵 *B* 始终以未转置的形式存储。

指定为：二维数组，包含第 391 页表 80 中指示的数据类型的数值，其中：

- 如果 *transb* = ‘N’，其大小必须为 *ldb* 乘以（至少）*n*。
- 如果 *transb* = ‘T’ 或 ‘C’，其大小必须为 *ldb* 乘以（至少）*m*。

*ldb* 是为 *b* 指定的数组的先行维。

指定为：全字整数；*ldb* > 0 且：

- 如果 *transb* = ‘N’，*ldb* $\geq$ *m*。
- 如果 *transb* = ‘T’ 或 ‘C’，*ldb* $\geq$ *n*。

*beta* 是标量 $\beta$。

指定为：第 391 页表 80 中指示的数据类型的数值。

*c* 是 *l* 乘以 *n* 的矩阵 *C*。

指定为：二维数组，包含第 391 页表 80 中指示的数据类型的数值。

*ldc* 是为 *c* 指定的数组的先行维。

指定为：全字整数；*ldc* > 0 且 *ldc* $\geq$ *l*。

**返回时：**

*c* 是 *l* 乘以 *n* 的矩阵 *C*，包含计算结果。

返回为：一个 *ldc* 乘以（至少）*n* 的数组，包含第 391 页表 80 中指示的数据类型的数值。

## 注释

1. 所有子程序都接受 *transa* 和 *transb* 参数的小写字母。
2. 对于 SGEMM 和 DGEMM，如果在 *transa* 或 *transb* 参数中指定 ‘C’，则将其解释为指定了 ‘T’。
3. 矩阵 *C* 不得与矩阵 *A* 或 *B* 具有公共元素；否则，结果不可预测。请参阅第 55 页的“概念”。

## 功能

组合矩阵加法与乘法表示如下，其中 $a_{ik}$、$b_{kj}$ 和 $c_{ij}$ 分别是矩阵 *A*、*B* 和 *C* 的元素：

![](img/5b0f44f3be6048723819b26aed7f6f03_417_0.png)

参见参考文献 [34] 和 [40]。在以下三种情况下，不执行任何计算：

- $l$ 为 0。
- $n$ 为 0。
- $\beta$ 为 1 且 $\alpha$ 为 0。

假设上述条件不存在，如果 $\beta \neq 1$ 且 $m$ 为 0，则返回 $\beta C$。

## 特殊用法

**等价规则：** 为 $A$ 和 $B$ 的矩阵乘法在第 380 页的“特殊用法”中定义的等价规则，也适用于此子程序执行的计算中的矩阵乘法部分。当您想要转置或共轭转置计算部分的乘法时，应使用等价规则。在为这些情况编写调用序列时，请注意按照规则指示的顺序编写矩阵参数和维数参数。此外，请注意您的输入和输出数组 C 具有足够大的维度以容纳结果矩阵。请参阅第 397 页的“示例 4”。

## 错误条件

**资源错误：** 无法分配内部工作区（仅限 CGEMM 和 ZGEMM）。

**计算错误：** 无

**输入参数错误：**

1. $lda, ldb, ldc \leq 0$
2. $l, m, n < 0$
3. $l > ldc$
4. $transa, transb \neq$ 'N'、'T' 或 'C'
5. $transa =$ 'N' 且 $l > lda$
6. $transa =$ 'T' 或 'C' 且 $m > lda$
7. $transb =$ 'N' 且 $m > ldb$
8. $transb =$ 'T' 或 'C' 且 $n > ldb$

## 示例 1

本示例展示了计算 $C \leftarrow \alpha AB + \beta C$，其中 $A$、$B$ 和 $C$ 分别包含在较大的数组 $A$、$B$ 和 $C$ 中。

**调用语句和输入：**

```
TRANSA TRANSB L N M ALPHA A LDA B LDB BETA C LDC
CALL SGEMM( 'N' , 'N' , 6 , 4 , 5 , 1.0 , A , 8 , B , 6 , 2.0 , C , 7 )
```

$A =$

$$
\begin{bmatrix}
1.0 & 2.0 & -1.0 & -1.0 & 4.0 \\
2.0 & 0.0 & 1.0 & 1.0 & -1.0 \\
1.0 & -1.0 & -1.0 & 1.0 & 2.0 \\
-3.0 & 2.0 & 2.0 & 2.0 & 0.0 \\
4.0 & 0.0 & -2.0 & 1.0 & -1.0 \\
-1.0 & -1.0 & 1.0 & -3.0 & 2.0 \\
... & ... & ... & ... & ...
\end{bmatrix}
$$

$B =$

$$
\begin{bmatrix}
1.0 & -1.0 & 0.0 & 2.0 \\
2.0 & 2.0 & -1.0 & -2.0 \\
1.0 & 0.0 & -1.0 & 1.0 \\
-3.0 & -1.0 & 1.0 & -1.0 \\
4.0 & 2.0 & -1.0 & 1.0 \\
... & ... & ... & ...
\end{bmatrix}
$$

$C =$

$$
\begin{bmatrix}
0.5 & 0.5 & 0.5 & 0.5 \\
0.5 & 0.5 & 0.5 & 0.5 \\
0.5 & 0.5 & 0.5 & 0.5 \\
0.5 & 0.5 & 0.5 & 0.5 \\
0.5 & 0.5 & 0.5 & 0.5 \\
0.5 & 0.5 & 0.5 & 0.5 \\
... & ... & ... & ...
\end{bmatrix}
$$

**输出：**

$C =$

$$
\begin{bmatrix}
24.0 & 13.0 & -5.0 & 3.0 \\
-5.0 & -4.0 & 2.0 & 4.0 \\
4.0 & 1.0 & 2.0 & 5.0 \\
-2.0 & 6.0 & -1.0 & -9.0
\end{bmatrix}
$$

