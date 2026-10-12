
# MPI 矩阵转置示例

## 15. MPI_Scatter 用于将输入矩阵的部分发送到每个处理器：

```c
MPI_Scatter(a, N*NL, MPI_INT, a_local, N*NL, MPI_INT, 0, MPI_COMM_WORLD);
```

## 16. 处理器执行矩阵转置：

```c
transpose(N, a_local, b_local);
```

## 17. 矩阵由根处理器收集：

```c
MPI_Gather(b_local, N*NL, MPI_INT, b, N*NL, MPI_INT, 0, MPI_COMM_WORLD);
```

## 18. 根处理器调用 print_matrix 例程来打印输入和输出矩阵：

```c
if (iproc == 0)
{
  print_matrix("Input", N, a);
  print_matrix("Output", N, b);
}
```

```c
free(a);
free(a_local);
free(b);
free(b_local);
```

## 19. 调用 MPI_Finalize 函数以结束程序：

```c
MPI_Finalize();

exit(0);
```

# 使用 PVM 编程

并行虚拟机 `PVM` 软件包是另一个用于编程 Beowulf 计算机系统的消息传递库。`PVM` 项目于 1989 年启动于橡树岭奇国家实验室 `Oakridge National Laboratory`。然而，`PVM` 软件包在开发消息传递并行程序仍然被广泛使用。

# 与 MPI 的比较

随着用于开发消息传递程序的 `MPI` 标准的引入，以及基于该标准的高质量软件包的出现，越来越多的人正转向使用 `MPI` 而非 `PVM`，原因是 `MPI` 支持许多 `PVM` 不具备的功能。这包括非阻塞发送/接收原语、用户定义数据类型、用于点对点和集合操作的通信器，以及定义虚拟拓扑并分配给进程的能力。`MPI` 标准支持异构性，允许并行程序运行在数据表示不兼容的计算机上。然而，`MPI` 标准并没有强制要求实现支持节点之间的通信。如果你正在构建一个由异构节点组成的 Beowulf 集群，让并行应用程序运行的最简单方法是使用 `PVM`。`PVM` 在用户应用层支持异构性。如果机器中的计算机具有不兼容的数据表示，并行程序可以在发送数据时指定特殊的编码。这意味着 `PVM` 在将数据打包到缓冲区中时，会将数据转换为标准格式。当数据在接收端被解包时，它将从标准格式转换为接收端的内部数据。

# 获取和安装 PVM

`PVM` 源码可以从 `http://www.netlib.org/pvm3/index.html` 免费获取。可以从该网站下载 gzipped 版本。`PVM` 还附带了一份用户指南，解释了安装过程以及一个网络计算的教程。在本文讨论的剩余部分，假设你已经下载并安装了 `PVM`。

# PVM 库函数回顾

`PVM` 程序通过调用 `pvm_spawn` 来扩展消息传递。`pvm_mytid` 函数必须是消息传递程序中的第一个 `PVM` 调用。它返回一个正整数整数或负值。该函数格式为：

```c
int pvm_mytid();
```

`pvm_parent` 函数返回调用进程的任务标识符或负值。该函数格式为：

```c
int pvm_parent();
```

新的 `PVM` 进程使用 `pvm_spawn` 启动。`pvm_spawn(char *progName, char **argv, intOption, char *where, int ntasks)`。第三个参数 参数可以具有以下值：

| Option | Meaning |
| :--- | :--- |
| `PvmTaskDefault` | PVM 选择机器 |
| `PvmTaskHost` | 用户指定的机器 |
| `PvmTaskArch` | 用户指定的架构 |
| `PvmTaskDebug` | 使用调试器启动进程 |
| `PvmTaskTrace` | 为进程生成跟踪数据 |

`pvm_spawn` 返回启动的任务数。小于请求数量的值表示错误。

`PVM` 进程使用 `pvm_joininggroup` 例程加入组。该例程格式为：

```c
int pvm_joininggroup(char *group);
```

该函数返回调用进程的实例号或负值。加入组的主要用途是与组成成员同步。在 `PVM` 中，进程使用 `pvm_barrier` 例程进行同步。该例程格式为：

```c
int pvm_barrier(char *group, int n);
```

属于组的进程直到共有 `n` 个进程到达屏障才能离开。该库函数返回一个表示成功或错误的状态码。

在 `PVM` 中，进程通过发送和接收消息进行通信。发送消息是一个三步序列。首先，调用 `pvitsend` 清空消息缓冲区并准备发送消息。该函数格式为：

```c
int pvitsend(int encoding)
```

该库函数有一个参数——发送消息的编码方案。其取值为：

| Encoding Scheme | Meaning |
| :--- | :--- |
| `PvmDataDefault` | 用于异构系统的 XDR 编码 |
| `PvmDataRaw` | 无编码 |
| `PvmDataInPlace` | 数据留原地 |

第二步是打包要发送的消息。`PVM` 为每种支持的数据类型都有打包例程。

## 第24 章

封装好的消息通过 `pvm_send` 例程发送到目标地。该例程的形式如下：
