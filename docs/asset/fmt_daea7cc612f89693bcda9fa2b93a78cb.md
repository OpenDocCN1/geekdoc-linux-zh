
对于 `SSLR2` 和 `DSLR2`，矩阵 $A$ 以按下打包存储模式存储。

### 表 70. 数据类型

| | 子程序 |
| :-- | :-- |
| $\alpha, A, x, y$ | |
| 短精度实数 | `SSPR2`, `SSYR2` 和 `SSLR2` |
| 长精度实数 | `DSPR2`, `DSYR2` 和 `DSLR2` |
| 短精度复数 | `CHPR2` 和 `CHER2` |
| 长精度复数 | `ZHPR2` 和 `ZHER2` |

> **注意：** `SSPR2` 和 `DSPR2` 是 2 级 BLAS 子例程。您应该使用这些子例程，而不是 `SSLR2` 和 `DSLR2`，后者仅为兼容早期版本的 ESSL 而提供。

## 语法

| Fortran | `CALL SSPR2 | DSPR2 | CHPR2 | ZHPR2 (*uplo, n, alpha, x, incx, y, incy, ap*)` |
| :-- | :-- |
| | `CALL SSYR2 | DSYR2 | CHER2 | ZHER2 (*uplo, n, alpha, x, incx, y, incy, a, lda*)` |
| | `CALL SSLR2 | DSLR2 (*n, alpha, x, incx, y, incy, ap*)` |
| C 和 C++ | `sspr2 | dspr2 | chpr2 | zhpr2 (*uplo, n, alpha, x, incx, y, incy, ap*);` |
| | `ssyr2 | dsyr2 | chyr2 | zher2 (*uplo, n, alpha, x, incx, y, incy, a, lda*);` |
| | `sslr2 | dsrlr2 (*n, alpha, x, incx, y, incy, ap*);` |

## 入口时：

`*uplo*` 指示矩阵 $A$ 使用的存储模式，其中：

如果 `*uplo*` = 'U'，则 $A$ 以按上打包或按上存储模式存储。

如果 `*uplo*` = 'L'，则 $A$ 以按下打包或按下存储模式存储。

`n` 是向量 **x** 和 **y** 中的元素数量，也是矩阵 **A** 的阶数。

指定为：全字整数；$n \geq 0$。

`alpha` 是缩放常数 $\alpha$。

指定为：表 70（第 319 页）中指示的数据类型的数值。

`x` 是长度为 $n$ 的向量 **x**。

指定为：长度至少为 $1+(n-1)\lvert incx\rvert$ 的一维数组，包含表 70（第 319 页）中指示的数据类型的数值。

`incx` 是向量 **x** 的跨距。

指定为：全字整数，其中：

对于 `SSPR2`, `DSPR2`, `CHPR2`, `ZHPR2`, `SSYR2`, `DSYR2`, `CHER2` 和 `ZHER2`，$incx < 0$ 或 $incx > 0$。

对于 `SSLR2` 和 `DSLR2`，`incx` 可以取任何值。

`y` 是长度为 $n$ 的向量 **y**。

指定为：长度至少为 $1+(n-1)\lvert incy\rvert$ 的一维数组，包含表 70（第 319 页）中指示的数据类型的数值。

`incy` 是向量 **y** 的跨距。

指定为：全字整数，其中：

对于 `SSPR2`, `DSPR2`, `CHPR2`, `ZHPR2`, `SSYR2`, `DSYR2`, `CHER2` 和 `ZHER2`，$incy < 0$ 或 $incy > 0$。

对于 `SSLR2` 和 `DSLR2`，`incy` 可以取任何值。

`ap` 具有以下含义：

对于 `SSPR2` 和 `DSPR2`，`ap` 是以按上或按下打包存储模式存储的 $n$ 阶实对称矩阵 **A**。

对于 `CHPR2` 和 `ZHPR2`，`ap` 是以按上或按下打包存储模式存储的 $n$ 阶复埃尔米特矩阵 **A**。

对于 `SSLR2` 和 `DSLR2`，`ap` 是以按下打包存储模式存储的 $n$ 阶实对称矩阵 **A**。

指定为：长度至少为 $n(n+1)/2$ 的一维数组，包含表 70（第 319 页）中指示的数据类型的数值。

`a` 具有以下含义：

对于 `SSYR2` 和 `DSYR2`，`a` 是以按上或按下存储模式存储的 $n$ 阶实对称矩阵 **A**。

对于 `CHER2` 和 `ZHER2`，`a` 是以按上或按下存储模式存储的 $n$ 阶复埃尔米特矩阵 **A**。

指定为：`lda` 行乘以（至少）$n$ 列的数组，包含表 70（第 319 页）中指示的数据类型的数值。

`Lda` 是为 `a` 指定的数组的主维。

指定为：全字整数；$Lda > 0$ 且 $Lda \geq n$。

## 出口时：

### `SSPR2`, `DSPR2`, `CHPR2`, `ZHPR2`, `SSYR2`, `DSYR2`, `CHER2`, `ZHER2`, `SSLR2`, 和 `DSLR2`

- `ap` 是阶数为 $n$ 的矩阵 $A$，包含计算结果。返回形式为：一维数组，包含表 70（第 319 页）中指定的数据类型的数值。

- `a` 是阶数为 $n$ 的矩阵 $A$，包含计算结果。返回形式为：二维数组，包含表 70（第 319 页）中指定的数据类型的数值。

## 说明

1. 所有子例程都接受小写字母作为 `uplo` 参数。

2. 向量 $\mathbf{x}$ 和 $\mathbf{y}$ 不得与矩阵 $A$ 有任何公共元素；否则，结果不可预测。参见第 55 页的“基本概念”。

3. 在输入时，假定复数厄米矩阵 $A$ 的对角元素的虚部为零，因此您无需设置这些值。在输出时，如果 $\alpha \neq$ 零，则对角元素的虚部被设为零。

4. 关于对称矩阵在上部或下部打包存储模式以及上部或下部存储模式下如何存储的描述，参见第 64 页的“对称矩阵”。关于复数厄米矩阵在上部或下部打包存储模式以及上部或下部存储模式下如何存储的描述，参见第 69 页的“复数厄米矩阵”。

## 功能

这些子例程执行以下两部分描述的计算。参见参考文献 [36]、[37] 和 [81]。如果 `n` 或 `alpha` 为零，则不执行任何计算。

对于 `SSPR2`、`SSYR2`、`SSLR2`、`CHPR2` 和 `CHER2`，中间结果以长精度进行累加。

**`SSPR2`, `DSPR2`, `SSYR2`, `DSYR2`, `SSLR2`, 和 `DSLR2`：** 这些子例程计算实对称矩阵的二阶更新：

$$A \leftarrow A + \alpha x y^T + \alpha y x^T$$

其中：

- $A$ 是阶数为 $n$ 的实对称矩阵。
- $\alpha$ 是一个标量。
- $\mathbf{x}$ 是长度为 $n$ 的向量。
- $\mathbf{x}^{\mathrm{T}}$ 是向量 $\mathbf{x}$ 的转置。
- $\mathbf{y}$ 是长度为 $n$ 的向量。
- $\mathbf{y}^{\mathrm{T}}$ 是向量 $\mathbf{y}$ 的转置。

其表达式如下：

$$\begin{bmatrix} a_{11} & \cdots & a_{1n} \\ \vdots & \vdots & \\ \vdots & \vdots & \\ a_{n1} & \cdots & a_{mn} \end{bmatrix} \leftarrow \begin{bmatrix} a_{11} & \cdots & a_{1n} \\ \vdots & \vdots & \\ \vdots & \vdots & \\ a_{n1} & \cdots & a_{mn} \end{bmatrix} + \alpha \begin{bmatrix} x_1 \\ \vdots \\ x_n \end{bmatrix} \begin{bmatrix} y_1 & \cdots & y_n \end{bmatrix} + \alpha \begin{bmatrix} y_1 \\ \vdots \\ y_n \end{bmatrix} \begin{bmatrix} x_1 & \cdots & x_n \end{bmatrix}$$

**`CHPR2`, `ZHPR2`, `CHER2`, 和 `ZHER2`：** 这些子例程计算复数厄米矩阵的二阶更新：

$$\boldsymbol{A} \leftarrow \boldsymbol{A} + \alpha \boldsymbol{x} \boldsymbol{y}^\mathrm{H} + \bar{\alpha} \boldsymbol{y} \boldsymbol{x}^\mathrm{H}$$

其中：

- $A$ 是阶数为 $n$ 的复数厄米矩阵。
- $\alpha$ 是一个标量。
- $\mathbf{x}$ 是长度为 $n$ 的向量。
- $\mathbf{x}^\mathrm{H}$ 是向量 $\mathbf{x}$ 的共轭转置。
- $\mathbf{y}$ 是长度为 $n$ 的向量。
- $\mathbf{y}^\mathrm{H}$ 是向量 $\mathbf{y}$ 的共轭转置。

其表达式如下：
