
```
$u_{i,j} = \frac{1}{4}(u_{i+1,j} + u_{i-1,j} + u_{i,j+1} + u_{i,j-1} - h^2 f_{i,j}). \quad (9.3.4)$
```

雅可比迭代的每一步都根据 `$u_{i,j}^N$` 计算 `$u_{i,j}^{N+1}$` 的新近似值：

```
$u_{i,j}^{N+1} = \frac{1}{4}(u_{i+1,j}^N + u_{i-1,j}^N + u_{i,j+1}^N + u_{i,j-1}^N - h^2 f_{i,j}). \quad (9.3.5)$
```

这是我们计算泊松问题解近似值的算法。我们强调，雅可比法是一种很差的数值方法，但相同的通信模式适用于许多通过迭代技术求解的有限差、有限体积或有限元离散化。在该算法的单处理器版本中，解 `$u$` 由一个二维数组 `$u$` 表示，迭代如下：

```c
double u[NY+2], u_new[NY+2], f[NY+2];
int i, j;
for (i=1;i<=NX;i++)
  for (j=1;j<=NY;j++)
    u_new[i][j] = 0.25 * (u[i+1][j] + u[i-1][j] + u[i][j+1] - h*h*f[i]);
```

在这里，我们让 `$u[0][j], u[i+1][j], u[i][0]$` 保存边界条件 `$g$` 的值。为了将此方法并行化，必须首先决定如何跨进程分解数据结构 `$u$`。存在许多分解方法。最简单的方法是将区域划分为带（如图 9.8 所示）。令数组 `$u$` 的局部表示为 `$local$`，即每个进程声明一个包含该进程持有的 `$u$` 值的数组。没有进程拥有所有的 `$u$`；数据结构在所有进程之间分解。每个进程上实现雅可比方法的代码为：

```c
for (i=i_start;i<=end;i++)
for (j=1;j<=NY;j++)
  local_new[i-i_start][j] = 0.25 * (local[i_start+1][j] + local[i_start-1][j] + local[i_start][j+1] - h*h*f[i_start]);
```

其中 `$i\_start$` 和 `$end$` 描述该进程的范围（在实践中循环从零到结束）；我们使用这种公式来与单处理器代码对应。我们定义了 `$local$`，使得 `$local[0][j]$` 对应单处理器版本代码中的 `$u[i\_start][j]$`。使用像 `$local$` 这样的变量名来明确哪些变量是分布式数据结构是一个是一个好主意。

从这段代码中可以看到我们需要通信的数据。对于 `$i=start$`，我们需要 `$u[i-1][j]$` 的值；对于 `$i=end$`，我们需要 `$u[i+1][j]$`。这些值属于相邻进程且必须通信。此外，我们需要一个存储这些值的地方。可以使用单独的数组，但对于规则网格，常用的方法是使用鬼单元（ghost cells），在本地数组中留出空间存放来自相邻进程的值。在这种情况下，我们只需要一列相邻数据，因此我们将让 `$ulocal[1][j]$` 对应于 `$u[i\_start][j]$`。这使得循环的代码更改为：

```
exchange_nbrs( u_local, i_start, i_end, left, right );
for (i_local=1; i_local<i_end-i_start+1; i_local++)
  for (j=1; j<=NY; j++)
    u_new[i_local][j] =
      0.25 * (u_local[i_local+1][j] + u_local[i_local][j] + 
      u_local[i_local][j+1] + u_local[i_local][j-1] - 
      h*h*f[i_local][j]);
```

我们将 `$i$` 转换为描述 `$u\_start$` 的相对值。即，`exchange_nbrs` 在相邻进程之间交换数据。图 9.9 显示了一个简单的运行时。我们注意 ISO/ANSI C（与 Fortran）不支持多维数组的运行时定义。为了保持这些 C 示例简单，我们使用了数组定义。C 的另一种方法是将数组作为一维数组传递并计算相应的偏移量。

值 `$left$` 和 `$right$` 分别用于左侧和右侧邻居的秩。可以通过以下简单计算：

```c
int rank, size, left, right;
...
MPI_Comm_rank(MPI_COMM_WORLD, &rank);
MPI_Comm_size(MPI_COMM_WORLD, &size );
left = rank - 1;
right = rank + 1;
if (left < 0) left = MPI_PROC_NULL;
if (right >= size) right = MPI_PROC_NULL;
```

特殊秩 `MPI\_PROC\_NULL` 指向网格的边缘。如果在 MPI 通信调用中使用 `MPI\_PROC\_NULL` 作为源或目的秩，该操作将被忽略。

```c
void exchange_nbrs( double ulocal[][NY+2], int i_start, int i_end,
int left, int right )
{
  MPI_Status status;
  int c;

  /* 从左邻居发送并接收 */
  MPI_Send(ulocal[1][1], NY, MPI_DOUBLE, left, 0,
  MPI_COMM_WORLD );
  MPI_Recv(ulocal[0][1], NY, MPI_DOUBLE, left, 0,
  MPI_COMM_WORLD, &status );

  /* 从右邻居发送并接收 */
  c = i_end - i_start + 1;
  MPI_Send(ulocal[c][1], NY, MPI_DOUBLE, right, 0,
  MPI_COMM_WORLD );
  MPI_Recv(ulocal[c+1][1], NY, MPI_DOUBLE, right, 0,
  MPI_COMM_WORLD, &status );
}
```

# 图 9.9

代码的简单版本。请见文中关于该例程局限性的讨论。

## 9.4 集合操作

集合操作是由属于通信器的所有进程调用的 MPI 函数。（如果通信器是 `MPI_COMM_WORLD`，这意味着所有

# 使用 MPI 进行并行编程

```c
/* 更好的交换代码。 */
void exchange_nbrs( double ulocal[][NY+2], int i_start, int i_end,
    int left, int right )
{
    MPI_Status status;
    int c;

    /* 向左邻居发送并接收 */
    MPI_Sendrecv(&ulocal[1], NY, MPI_DOUBLE, left, 0,
        &ulocal[c+1], NY, MPI_DOUBLE, right, 0,
        MPI_COMM_WORLD, &status);

    /* 向右邻居发送并接收 */
    c = i_end - i_start + 1;
    MPI_Sendrecv(&ulocal[c], NY, MPI_DOUBLE, right, 0,
        &ulocal[c+1], NY, MPI_DOUBLE, left, 0,
        MPI_COMM_WORLD, &status);
}
```

**图 9.10** 交换代码更好的版本。

进程，但 MPI 也允许在其他进程集上进行集合操作。集合操作涉及通信，有时也涉及计算，但由于它们描述了特定的通信和计算模式，MPI 的实现可能对其进行优化，这种优化程度是通过 `MPI_Send` 和 `MPI_Recv` 等 MPI 点对点操作来表达时所无法实现的。此外，使用集合操作也更容易表达这些模式。

在这里，我们介绍两种最常用的集合操作，并展示如何完全使用集合操作来表示并行程序中的通信，而完全不使用任何单独的 `MPI_Send` 或 `MPI_Recv`。

图 9.11 所示的程序通过数值积分计算 `$\pi$` 的值。由于

$$

\int_0^1 \frac{1}{1+x^2} dx = \arctan(x)|_0^1 = \arctan(1) - \arctan(0) = \frac{\pi}{4}$$

```

我们可以通过对函数 `$f(x) = 4/(1+x^2)$` 从 0 到 1 积分来计算 `$\pi$`。

我们通过将区间 [0, 1] 划分为若干个子区间，然后让每个进程计算某些子集的面积来计算一个近似值。我们可以使用管理器/工作者算法来实现，但在这里我们预先分配工作。事实上，每个工作者都可以计算自己的任务集，因此“管理器”也可以是一个工作者，而不仅仅是管理工作池。矩形越多，需要做的工作就越多，所得的 `$\pi$` 近似值也就越精确。为了实验，让我们让子区间的数量成为命令行参数。（尽管 MPI 标准不保证任何进程都能接收到命令行参数，但在许多实现中，特别是对于 Beowulf 集群，可以假设至少句柄为 0 的进程可以使用 `argc` 和 `argv`，尽管它们在调用 `MPI_Init` 之前可能没有意义。）进程 0 将子区间的数量 `$n$` 设置为 `argv[1]`。一旦进程知道了 `$n$`，它就可以通过声领每隔 `$n$` 个矩形中的一个（从编号为 1 的矩形开始）来声领大约 `$1/n$` 的工作。进程 `$j$` 计算矩形 `$j, j+n, j+2n$` 等等的面积。

然而，并不是所有的 MPI 实现都让所有进程都能使用命令行参数。不过，我们首先让进程 0 逐接地向其他每个进程发送数据，但这种方法效率很低。如果我们知道相同的消息被传递给所有其他进程，我们可以请求 MPI 实现通过一系列 `MPI_Send` 和 `MPI_Recv` 以更高效的方式来完成。

广播（`MPI_Broadcast`）是 MPI **集合**操作的一个示例。集合操作必须由通信器中的所有进程调用。这允许实现以以特殊的方式来安排集合操作所指定的通信和计算。在 `MPI_Broadcast` 的情况下，实现可能会使用通信树（有时称为生成树），在 в树中，进程 0 将其消息发送给第二个进程，然后进程再发送给另外两个进程，依此类推。通过这种方式，通信是并行进行的，所有消息都在 `$\log n$` 步内被送达。

`MPI_Broadcast` 的精确语义有时会令人困惑。前三个参数（广播的**根**、计数、数据类型）指定了哪一个进程拥有要发送给其他进程的数据。在我们的案例中，是进程 0。`MPI_Broadcast` 在根进程上的作用类似于 `MPI_Send`，在所有其他进程上的作用类似于 `MPI_Recv`，但调用本身在每个进程上看起来是完全相同的。最后一个参数是该集合调用所属的通信器。通信器中的所有进程必须执行相同的调用。在调用之前，`$n$` 仅在根进程有效；在 `MPI_Broadcast` 返回后，所有进程都拥有 `$n$` 值的副本。

接下来，每个进程（包括进程 0）都将其矩形的面积加到局部变量 `mypi` 中。然而，我们没有将这些值发送给一个进程并由其进行处理，而是使用了另一个集合操作 `MPI_Reduce`。

```c

#include "mpi.h"

#include <stdio.h>

#include <math.h>

double f(double a) { return (4.0 / (1.0 + a*a)); }

int main(int argc, char *argv[])

{

    int n, myid, numprocs, i;

    double PI25DT = 3.1415926535897932384;

    double mypi, pi, sum, x;

    double startTime;

    MPI_Init(&argc, &argv);

    MPI_Comm_rank(MPI_COMM_WORLD, &myid);

    MPI_Comm_size(MPI_COMM_WORLD, &numprocs);

    if (myid == 0) {

        n = atoi(argv[1]);

    }

    double h = 1.0 / n;

    sum = 0.0;

    for (i = myid; i < n; i += n) {

        x = (i + 0.5) * h;

        sum += f(x);

    }

    MPI_Reduce(&sum, &pi, 1, MPI_DOUBLE, MPI_SUM, 0, MPI_COMM_WORLD);

    if (myid == 0) {

        endTime = MPI_Wtime();

        printf("pi = %.15f, error = %.15e, wall clock time = %f\n", pi, fabs(pi - PI25DT), endTime - startTime);

    }

    MPI_Finalize();

    return 0;

}

```

```c

#include "mpi.h"

#include <stdio.h>

#define SIMPLE_SPRNG   /* simple interface */

#define USE_MPI        /* use MPI header */

#include "sprng.h"    /* SPRNG header file */

#define BATCHSIZE 100000

int main(int argc, char *argv[])

{

    int i, j, numer = 0, total, numbatches, rank, numprocs;

    double x, y, approx, pi = 3.141592653589793238462463;

    MPI_Init(&argc, &argv);

    MPI_Comm_size(MPI_COMM_WORLD, &numprocs);

    MPI_Comm_rank(MPI_COMM_WORLD, &rank);

    if (rank == 0) {

        numbatches = atoi(argv[1]);

        MPI_Bcast(&numbatches, 1, MPI_INT, 0, MPI_COMM_WORLD);

        for (i = 0; i < numbatches; i++) {

            for (j = 0; j < BATCHSIZE; j++) {

                x = sprng(); y = sprng();

                if (x * x + y * y < 1.0)

                    numer++;

            }

        }

        MPI_Reduce(&numer, &total, 1, MPI_INT, MPI_SUM, 0, MPI_COMM_WORLD);

        if (rank == 0) {

            total = BATCHSIZE * (i + 1) * numprocs;

            approx = 4.0 * (double)total / total;

            printf("pi = %.16f, error = %.16f, points = %d\n", approx, pi - approx, total);

        }

    }

    MPI_Finalize();

}

```

图 9.12
使用蒙特卡洛方法计算 `$\pi$`。

# 使用 MPI 的并行编程

- 用于在各种环境中构建 `MPICH` 的配置脚本，包括 Linux 集群，
- 像本章中这样的简单示例程序，
- MPI 合规性测试程序，
- 性能基准程序，
- 几个 MPI 性能分析库，
- 用于事件日志和 X 图形的 MPI 扩展 `MPE` 库，
- 使用 `MPE` 库进行图形输出的更复杂的示例，
- `Jumpshot` 并行进程管理系统。

`MPICH` 的架构设计可以使用多种通信基础设施。这些被称为“设备（devices）”。对于 Beowulf 环境最相关的设备是 `ch-p4` 和 `ch-p4mpd` 设备。`ch-p4` 设备具有更多一些功能，包括利用共享内存通信以及具有不同执行二进制文件的能力。另一方面，`ch-p4mpd` 设备提供的启动速度比 `MPD` 进程管理器快得多（见第 9.6.5 节）。要运行你的第一个 MPI 程序，请执行以下步骤：

1. 从 `www.mcs.anl.gov/mpi/mpich` 下载 `mpich.tar.gz`，或者从 `ftp://ftp.mcs.anl.gov/pub/mpi/mpich.tar.gz` 下载
2. 执行 `tar xvf mpich.tar.gz; cd mpich`
3. 执行 `configure <options> > configure.log`。大多数用户在配置时需要为安装指定一个前缀：

```bash

configure --prefix=/usr/local/mpich-1.2.2 &configure.log

```

默认情况下，这将创建 `ch-p4` 设备。

4. 执行 `make >& make.log`
5. 执行 `make install >& install.log`
6. 将 `<prefix>/bin` 目录添加到你的路径中；例如，对于 `tcsh`，执行：

```bash

setenv PATH <prefix>/bin:$PATH

rehash
```
