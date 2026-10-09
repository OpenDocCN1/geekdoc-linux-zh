

## 9.3 二维雅可比方法示例，采用一维分解

并行计算机在科学计算中的一种常见用途是近似求解偏微分方程（PDE）。最常在教科书出现的偏微分方程之一是泊松方程（此处展示二维形式）：

$$
\begin{aligned}
&\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = f(x, y) \quad \text{在 } \Gamma \text{ 内} & (9.3.1) \\
&u = g(x, y) \quad \text{在 } \partial\Gamma \text{ 上} & (9.3.2)
\end{aligned}
$$

该方程用于描述许多物理现象，包括流体流动和静电学。该方程由两部分组成：应用于区域内 $\Gamma$ 内任意点的微分方程（9.3.1）以及未知量 $u$ 在 $\Gamma$ 边界上的取值规范（记号 $\partial\Gamma$ 表示“$\Gamma$ 的边界”）。例如，若使用此方程模拟区域内的温度平衡分布，则边界条件 $g(x,y)$ 指定了边界上施加的温度，$f(x,y)$ 为零，而 $u(x,y)$ 是区域内的温度。为了简化本示例的后续部分，我们将仅考虑一个由正方形组成的简单区域 $\Gamma$（参见图 9.8）。

![](img/e2283ffaea56e577ac05056b4bb738fc_210_0.png)

为了计算 $u(x,y)$ 的近似值，我们必须首先将问题缩减为有限规模。我们无法确定 $u$ 在所有点的值；相反，我们将在区域内的有限个点 $(x_i, y_i)$ 处近似 $u$，其中 $x_i = i \times h$ 且 $y_j = j \times h$。（当然，我们可以通过插值在区域内的其他点定义 $u$ 的值，但近似值由 $u$ 在点 $(x_i, y_j)$ 处的值定义。）这些点在图 9.8 中显示为黑色圆盘。由于这种规则间距，这些点构成了*规则网格*。在每个这样的点上，我们用有限差分来近似偏导数。例如，

$$
\frac{\partial^2 u}{\partial x^2}(x_i, y_j) \approx \frac{u(x_{i+1}, y_j) - 2u(x_i, y_j) + u(x_{i-1}, y_j)}{h^2}
$$

如果我们用 $u_{i,j}$ 表示方程 9.3.1 在点 $(x_i, y_j)$ 处解的近似值，我们就得到了关于 $u$ 值的以下联立线性方程组：

$$
\frac{u_{i+1,j} - 2u_{i,j} + u_{i-1,j}}{h^2} + \frac{u_{i,j+1} - 2u_{i,j} + u_{i,j-1}}{h^2} = f(x_i, y_j). \quad (9.3.3)
$$

对于沿边界的 $u$ 值（例如在 $x = 0$ 或 $y = 1$ 处），使用边界条件 $g$ 的值。如果 $h = 1/(n + 1)$（即网格内部有 $n \times n$ 个点），这将给我们 $n^{2}$ 个需要求解的联立线性方程。

可以使用许多方法来解决这些方程。事实上，如果你手头有这个问题，你应该使用表 10.1 中描述的某个数值库。在本节中，我们描述了一个非常简单（且低效）的算法，因为从并行计算的角度来看，它说明了如何编程更有效的通用方法。我们使用的方法称为*雅可比*方法，用于求解线性方程组。雅可比方法通过改写方程来计算方程 9.3.3 解的连续近似值，如下所示：

$$
\begin{aligned}
&u_{i+1,j} - 2u_{i,j} + u_{i-1,j} + u_{i,j+1} - 2u_{i,j} + u_{i,j-1} = h^2 f(x_{i},y_{j}) \\
&u_{i,j} = \frac{1}{4}\left(u_{i+1,j} + u_{i-1,j} + u_{i,j+1} + u_{i,j-1} - h^2 f_{i,j}\right). \quad (9.3.4)
\end{aligned}
$$

雅可比迭代的每一步都根据周围 $u^{N}$ 的值计算 $u_{i,j}^{N+1}$ 的新近似值：

$$
u_{i,j}^{N+1} = \frac{1}{4}\left(u_{i+1,j}^{N} + u_{i-1,j}^{N} + u_{i,j+1}^{N} + u_{i,j-1}^{N} - h^2 f_{i,j}\right). \quad (9.3.5)
$$

这是我们计算泊松问题解近似的算法。我们强调，雅可比方法是一种糟糕的数值方法，但相同的通信模式适用于许多通过迭代技术求解的有限差分、体积或单元离散化方法。

在该算法的单处理器版本中，解 \(u\) 由二维数组 `u[max_n][max_n]` 表示，迭代过程编写如下：

```c
double u[NX+2][NY+2], u_new[NX+2][NY+2], f[NX+2][NY+2];
int    i, j;
...
for (i=1; i<=NX; i++)
    for (j=1; j<=NY; j++)
        u_new[i][j] = 0.25 * (u[i+1][j] + u[i-1][j] +
                               u[i][j+1] + u[i][j-1] - h*h*f[i][j]);
```

在这里，我们让 `u[0][j]`、`u[n+1][j]`、`u[i][0]` 和 `u[i][n+1]` 保存边界条件 \(g\) 的值（这些对应于方程 9.3.1 中的 \(u(0,y)\)、\(u(1,y)\)、\(u(x,0)\) 和 \(u(x,1)\)）。为了并行化此方法，我们首先必须决定如何在进程中分解数据结构 \(u\) 和 `u_new`。存在许多可能的分解方式。最简单的方法之一是将区域划分为如图 9.8 所示的条带。

让数组 \(u\) 的局部表示为 `u_local`；也就是说，每个进程声明一个包含该进程持有的 \(u\) 部分的数组 `u_local`。没有进程拥有全部 \(u\)；代表 \(u\) 的数据结构在*所有*进程之间*分解*。在每个进程中用于实现雅可比方法的代码是

```c
for (i=i_start; i<=i_end; i++)
    for (j=1; j<=NY; j++)
        u_local_new[i-i_start][j] =
            0.25 * (u_local[i-i_start+1][j] + u_local[i-i_start-1][j] +
                    u_local[i-i_start][j+1] + u_local[i-i_start][j-1] -
                    h*h*f_local[i-i_start][j]);
```

其中 `i_start` 和 `i_end` 描述了此进程上的条带（实际上，循环应从零到 `i_end-i_start`；我们使用这种形式以保持与单处理器代码的对应关系）。我们定义了 `u_local`，使得 `u_local[0][j]` 对应于该代码单处理器版本中的 `u[i_start][j]`。使用如 `u_local` 这样能明显表明哪些变量是分布式数据结构一部分的变量名通常是一个好主意。

从这段代码中，我们可以看到需要通信哪些数据。对于 $i=i_{\text{start}}$，我们需要 $u[i_{\text{start}}-1][j]$ 的值；对于 $i=i_{\text{end}}$，我们需要 $u[i_{\text{end}}+1][j]$ 的值。这些值属于相邻进程，必须通过通信传递。此外，我们需要一个位置来存储这些值。我们可以使用单独的数组，但对于规则网格，最常见的方法是使用幽灵或光晕单元，即在 $u_{\text{local}}$ 数组中预留额外空间以保存来自相邻进程的值。在这种情况下，我们只需要相邻数据的一列，因此我们将让 $u_{\text{local}}[i][j]$ 对应于 $u[i_{\text{start}}][j]$。这将改变循环单次迭代的代码为

```c
exchange_nbrs( u_local, i_start, i_end, left, right );

for (i_local=1; i_local<=i_end-i_start+1; i_local++)
    for (j=1; j<=NY; j++)
        u_local_new[i_local][j] =
            0.25 * ( u_local[i_local+1][j] + u_local[i_local-1][j] +
                     u_local[i_local][j+1] + u_local[i_local][j-1] -
                     h*h*u_local[i_local][j] );
```

在这里，我们将 i 索引转换为相对于 $u_{\text{local}}$ 的起始位置而不是 $u$ 的相对位置。剩下的就是描述在相邻进程之间交换数据的例程 `exchange_nbrs`。一个非常简单的例程如图 9.9 所示。

我们注意到 ISO/ANSI C（与 Fortran 不同）不允许多维数组的运行时维数指定。为了简化这些 C 语言示例，我们使用数组的编译时维数指定。C 语言中的一种替代方法是作为一维数组传递数组并计算适当的偏移量。

值 `left` 和 `right` 分别用于左侧和右侧邻居的秩。可以通过使用以下内容简单地计算这些值：

```c
int rank, size, left, right;

MPI_Comm_rank( MPI_COMM_WORLD, &rank );
MPI_Comm_size( MPI_COMM_WORLD, &size );

left = rank - 1;
right = rank + 1;

if (left < 0) left = MPI_PROC_NULL;
if (right >= size) right = MPI_PROC_NULL;
```

特殊的秩 `MPI_PROC_NULL` 指示网格的边缘。如果在 MPI 通信调用中使用 `MPI_PROC_NULL` 作为源或目标秩，则

