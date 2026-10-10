
# SGER, DGER, CGERU, ZGERU, CGERC, ZGERC

## 示例 5

M N ALPHA X INCX Y INCY A LDA

```
CALL  SGER(
4 , 3 , 2.0 ,
X , 1 ,
Y , 1 ,
A(-1,1) , 4
)
```

X = (3.0, 2.0, 1.0, 4.0)
Y = (1.0, 2.0, 3.0)
A =（与示例 4 中的输入 A 相同）

输出：

A =
| 7.0 | 14.0 | 21.0 |
| 6.0 | 10.0 | 16.0 |
| 5.0 | 6.0 | 8.0 |
| 12.0 | 18.0 | 25.0 |

## 示例 6

本示例展示了一个秩一更新，其中所有数据项都包含复数，并且在计算中使用了转置 $y^{H}$。矩阵 $A$ 包含在一个更大的数组 $A$ 中。向量 $x$ 和 $y$ 的步长为正。数组 $A$ 的 Fortran `DIMENSION` 语句必须遵循示例 1 中给出的相同规则。在此示例中，数组 $A$ 声明为 $A(1:10,0:2)$。

**调用语句和输入：**

M N ALPHA X INCX Y INCY A LDA

```
CALL  CGERU(
5 , 3 , ALPHA ,
X , 1 ,
Y , 1 ,
A(1,0) , 10
)
```

ALPHA = (1.0, 0.0)
X = {(1.0, 2.0), (4.0, 0.0), (1.0, 1.0), (3.0, 4.0),
(2.0, 0.0)}
Y = {(1.0, 2.0), (4.0, 0.0), (1.0, -1.0)}

A =
| (1.0, 2.0) | (3.0, 5.0) | (2.0, 0.0) |
| (2.0, 3.0) | (7.0, 9.0) | (4.0, 8.0) |
| (7.0, 4.0) | (1.0, 4.0) | (6.0, 0.0) |
| (8.0, 2.0) | (2.0, 5.0) | (8.0, 0.0) |
| (9.0, 1.0) | (3.0, 6.0) | (1.0, 0.0) |
| ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... |

输出：

A =
| (-2.0, 6.0) | (7.0, 13.0) | (5.0, 1.0) |
| (6.0, 11.0) | (23.0, 9.0) | (8.0, 4.0) |
| (6.0, 7.0) | (5.0, 8.0) | (8.0, 0.0) |
| (3.0, 12.0) | (14.0, 21.0) | (15.0, 1.0) |
| (11.0, 5.0) | (11.0, 6.0) | (3.0, -2.0) |
| ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... |

## 示例 7

本示例展示了一个秩一更新，其中所有数据项都包含复数，并且在计算中使用了共轭转置 $y^{H}$。矩阵 $A$ 包含在一个更大的数组 A 中。向量 x 和 y 的步长为正。数组 A 的 Fortran DIMENSION 语句必须遵循示例 1 中给出的相同规则。在此示例中，数组 A 声明为 A(1:10,0:2)。

**调用语句和输入：**

M N ALPHA X INCX Y INCY A LDA

```
CALL CGERC( 5, 3, ALPHA, X, 1, Y, 1, A(1,0), 10 )
```

ALPHA = (1.0, 0.0)
X = ((1.0, 2.0), (4.0, 0.0), (1.0, 1.0), (3.0, 4.0),
(2.0, 0.0))
Y = ((1.0, 2.0), (4.0, 0.0), (1.0, -1.0))
A =（与示例 6 中的输入 A 相同）

**输出：**

A =
| (6.0, 2.0) | (7.0, 13.0) | (1.0, 3.0) |
| (6.0, -5.0) | (23.0, 9.0) | (8.0, 12.0) |
| (10.0, 3.0) | (5.0, 8.0) | (6.0, 2.0) |
| (19.0, 0.0) | (14.0, 21.0) | (7.0, 7.0) |
| (11.0, -3.0) | (11.0, 6.0) | (3.0, 2.0) |
| ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... |

# SSPMV, DSPMV, CHPMV, ZHPMV, SSYMV, DSYMV, CHEMV, ZHEMV, SSLMX 和 DSLMX——实对称或复数埃尔米特矩阵的矩阵-向量乘积

SSPMV、DSPMV、CHPMV、ZHPMV、SSYMV、DSYMV、CHEMV 和 ZHEMV 使用标量 $\alpha$ 和 $\beta$、矩阵 $\boldsymbol{A}$ 以及向量 $\boldsymbol{x}$ 和 $\boldsymbol{y}$，计算实对称矩阵或复数埃尔米特矩阵的矩阵-向量乘积：

$y \leftarrow \beta y + \alpha A x$

SSLMX 和 DSLMX 使用标量 $\alpha$、矩阵 $\boldsymbol{A}$ 以及向量 $\boldsymbol{x}$ 和 $\boldsymbol{y}$，计算实对称矩阵的矩阵-向量乘积：

$y \leftarrow y + \alpha A x$

使用以下存储模式：

- 对于 SSPMV、DSPMV、CHPMV 和 ZHPMV，矩阵 $\boldsymbol{A}$ 存储在上部打包存储模式或下部打包存储模式中。
- 对于 SSYMV、DSYMV、CHEMV 和 ZHEMV，矩阵 $\boldsymbol{A}$ 存储在上部存储模式或下部存储模式中。
- 对于 SSLMX 和 DSLMX，矩阵 $\boldsymbol{A}$ 存储在下部打包存储模式中。

| $\alpha, \beta, A, x, y$ | 子程序 |
| --- | --- |
| 短精度实数 | SSPMV、SSYMV 和 SSLMX |
| 长精度实数 | DSPMV、DSYMV 和 DSLMX |
| 短精度复数 | CHPMV 和 CHEMV |
| 长精度复数 | ZHPMV 和 ZHEMV |

**注意：** SSPMV 和 DSPMV 是 Level 2 BLAS 子程序。您应使用这些子程序，而不是 SSLMX 和 DSLMX，后者仅提供以保持与早期版本 ESSL 的兼容性。

# 语法

Fortran：
```fortran
CALL SSPMV | DSPMV | CHPMV | ZHPMV (uplo, n, alpha, ap, x, incx, beta, y, incy)
CALL SSYMV | DSYMV | CHEMV | ZHEMV (uplo, n, alpha, a, lda, x, incx, beta, y, incy)
CALL SSLMX | DSLMX (n, alpha, ap, x, incx, y, incy)
```

C 和 C++：
```c
sspmv | dspmv | chpmv | zhpmv (uplo, n, alpha, ap, x, incx, beta, y, incy);
ssymv | dsymv | chesmv | zhsmv (uplo, n, alpha, a, lda, x, incx, beta, y, incy);
sslmx | dslmx (n, alpha, ap, x, incx, y, incy);
```

**进入时：**

- $uplo$ 指示矩阵 $A$ 使用的存储模式，其中：
  - 如果 $uplo$ = 'U'，$A$ 存储在上部打包或上部存储模式中。
  - 如果 $uplo$ = 'L'，$A$ 存储在下部打包或下部存储模式中。
  - 指定为：单个字符。必须是 'U' 或 'L'。
- $n$ 是向量 $\boldsymbol{x}$ 和 $\boldsymbol{y}$ 中的元素数量以及矩阵 $A$ 的阶数。
  - 指定为：全字整数；$n \geq 0$。
- $\alpha$ 是缩放常数 $\alpha$。
  - 指定为：第 304 页表 68 中指示的数据类型的数字。
- $ap$ 的含义如下：
  - 对于 SSPMV 和 DSPMV，$ap$ 是阶数为 $n$ 的实对称矩阵 $A$，存储在上部或下部打包存储模式中。
  - 对于 CHPMV 和 ZHPMV，$ap$ 是阶数为 $n$ 的复数埃尔米特矩阵 $A$，存储在上部或下部打包存储模式中。
  - 对于 SSLMX 和 DSLMX，$ap$ 是阶数为 $n$ 的实对称矩阵 $A$，存储在下部打包存储模式中。
  - 指定为：长度至少为 $n(n+1)/2$ 的一维数组，包含第 304 页表 68 中指示的数据类型的数字。
- $a$ 的含义如下：
  - 对于 SSYMV 和 DSYMV，$a$ 是阶数为 $n$ 的实对称矩阵 $A$，存储在上部或下部存储模式中。
  - 对于 CHEMV 和 ZHEMV，$a$ 是阶数为 $n$ 的复数埃尔米特矩阵 $A$，存储在上部或下部存储模式中。
  - 指定为：$lda$ 乘以（至少）$n$ 的数组，包含第 304 页表 68 中指示的数据类型的数字。
- $lda$ 是为 $a$ 指定的数组的先行维数。
  - 指定为：全字整数；$lda > 0$ 且 $lda \geq n$。
- $x$ 是长度为 $n$ 的向量 $x$。
  - 指定为：长度至少为 $1+(n-1)|incx|$ 的一维数组，包含第 304 页表 68 中指示的数据类型的数字。
- $incx$ 是向量 $x$ 的步长。
  - 指定为：全字整数，其中：
    - 对于 SSPMV、DSPMV、CHPMV、ZHPMV、SSYMV、DSYMV、CHEMV 和 ZHEMV，$incx < 0$ 或 $incx > 0$。
    - 对于 SSLMX 和 DSLMX，$incx$ 可以是任何值。
- $\beta$ 是缩放常数 $\beta$。
  - 指定为：第 304 页表 68 中指示的数据类型的数字。
- $y$ 是长度为 $n$ 的向量 $y$。
  - 指定为：长度至少为 $1+(n-1)|incy|$ 的一维数组，包含第 304 页表 68 中指示的数据类型的数字。
- $incy$ 是向量 $y$ 的步长。
  - 指定为：全字整数；$incy > 0$ 或 $incy < 0$。

**返回时：**

- $y$ 是长度为 $n$ 的向量 $y$，包含计算结果。
  - 返回为：一维数组，包含第 304 页表 68 中指示的数据类型的数字。

# 注释

1. 所有子程序都接受 `uplo` 参数的小写字母。
2. 向量 $\boldsymbol{y}$ 不得与向量 $\boldsymbol{x}$ 或矩阵 $A$ 拥有公共元素；否则，结果不可预测。参见第 55 页的“概念”。
3. 在输入时，假定复数埃尔米特矩阵 $A$ 的对角线元素的虚部为零，因此您无需设置这些值。
4. 有关对称矩阵如何存储在上部或下部打包存储模式以及上部或下部存储模式中的描述，参见第 64 页的“对称矩阵”。有关复数埃尔米特矩阵如何存储在上部或下部打包存储模式以及上部或下部存储模式中的描述，参见第 69 页的“复数埃尔米特矩阵”。

# 功能

这些子程序执行以下两部分中描述的计算。参见参考文献 [36]、[37] 和 [81]。对于 SSPMV、DSPMV、CHPMV、ZHPMV、SSYMV、DSYMV、CHEMV 和 ZHEMV，如果 $n$ 为零，或者 $\alpha$ 为零且 $\beta$ 为一，则不执行计算。对于 SSLMX 和 DSLMX，如果 $n$ 或 $\alpha$ 为零，则不执行计算。

对于 SSLMX、SSPMV、SSYMV、CHPMV 和 CHEMV，中间结果以长精度累积。然而，对于向量 $y$ 的每个元素，可能会发生多次中间存储。

**对于 SSPMV、DSPMV、CHPMV、ZHPMV、SSYMV、DSYMV、CHEMV 和 ZHEMV：**

这些子程序计算实对称矩阵或复数埃尔米特矩阵的矩阵-向量乘积：
$y \leftarrow \beta y + \alpha A x$

- 其中：
  - $y$ 是长度为 $n$ 的向量。
  - $\alpha$ 是一个标量。
  - $\beta$ 是一个标量。
  - $A$ 是阶数为 $n$ 的实对称或复数埃尔米特矩阵。
  - $x$ 是长度为 $n$ 的向量。

其表达式如下：

$$
\begin{bmatrix} y_{1} \\ . \\ . \\ . \\ y_{n} \end{bmatrix} \leftarrow \beta\begin{bmatrix} y_{1} \\ . \\ . \\ . \\ y_{n} \end{bmatrix} + \alpha\begin{bmatrix} a_{11} & ... & a_{1n} \\ . & & . \\ . & & . \\ . & & . \\ a_{n1} & ... & a_{nn} \end{bmatrix}\begin{bmatrix} x_{1} \\ . \\ . \\ . \\ x_{n} \end{bmatrix}
$$

**对于 SSLMX 和 DSLMX：**

这些子程序计算存储在下部打包存储模式中的实对称矩阵的矩阵-向量乘积：
$y \leftarrow y + \alpha A x$

- 其中：
  - $y$ 是长度为 $n$ 的向量。
  - $\alpha$ 是一个标量。
  - $A$ 是阶数为 $n$ 的实对称矩阵。
  - $x$ 是长度为 $n$ 的向量。

