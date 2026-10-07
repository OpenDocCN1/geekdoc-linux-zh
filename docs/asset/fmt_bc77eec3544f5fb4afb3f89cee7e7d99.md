
图 10.7
用于网格二维分解的 Jacobi 问题的非阻塞交换代码。

# MPI 编程中的高级话题

（最右侧）。这两个例式在 `MPI_Recv` 调用中都使用了 `MPI_ANY_SOURCE` 而不是特定的源。如图 10.8 所示，消息可能会混淆，导致程序接收到错误的数据。然而，我们可以防止这种情况发生吗？有几种方法行不通。一种方法是避免使用 `MPI_ANY_SOURCE`。这解决了问题，但只有当 `SendRight` 和 `SendEnd` 都遵循这一规则时才有效。对于单人或团队编写的代码，这种方法可能是足够的（尽管很脆弱），但对于库文件来说是不够的。例如，如果 `SendEnd` 是由商业供应商编写的且没有使用 `MPI_ANY_SOURCE`，但 `SendRight` 是另一个供应商或缺乏经验的程序员编写的，程序仍然会失败，而且看起来像是 `SendEnd` 的错（因为先收到了来自 `SendEnd` 的消息）。

另一种行不通的方法是使用消息标签（tags）来区分消息。同样，如果某人整合了所有代码并非常小心地为不同的软件模块分配标签，那么是可以做到的。然而，在 MPI 接收中使用 `MPI_ANY_TAG` 可能会绕过这种方法。此外，如 [13] 中的图 6.5 所示，即使不使用 `MPI_ANY_SOURCE` 和 `MPI_ANY_TAG`，不同的代码模块仍然可能接收错误的消息。

`MPI` 通信器（communicator）中的通信上下文（context）为这些问题提供了解决方案。运行时 `MPI_Comm_dup` 从输入通信器创建一个新的通信器，它包含相同的进程（相同的秩顺序），但具有新的通信上下文。在一个通信上下文中发送的 MPI 消息只能在该上下文中接收。因此，任何想要确保其所有消息仅在该库内部可见的软件模块或库都需要在开始时调用 `MPI_Comm_dup` 来获取一个新的通信器。所有使用 MPI 编写良好的库都会创建一个仅在该类库内部使用的私有通信器。

支持库的开发是 MPI 设计目标之一。在这一方面，MPI 非常成功。许多库和应用程序现在都使用 MPI，由于 MPI 的可移植性，这些程序大部分都运行在 Beowulf 集群上。表 10.1 提供了 MPI 用于提供并行性的库的部分列表。更完整的描述和列表可以在 `www.mcs.anl.gov/mpi/libraries` 以及 `sal.kinatech.com/C/3` 获取。

# 10.5 更多关于集体操作

MPI 的优势之一是它拥有一可扩展的集体通信和计算程序。图 10.9 显示了一些最重要的集体通信程序的功能。作为其用性的示例，我们考虑一个简单的例子。

| 进程 0 | 进程 1 | 进程 2 |
| :--- | :--- | :--- |
| **SendRight** | `MPI_Send` | `MPI_Send` | `MPI_Recv` |
| **SendEnd** | `MPI_Send` | `MPI_Recv` | |

(a) 预期的消息路径

| 进程 0 | 进程 1 | 进程 2 |
| :--- | :--- | :--- |
| **SendRight** | `MPI_Send` | `MPI_Send` | `MPI_Recv` |
| **SendEnd** | `MPI_Send` | `MPI_Recv` | |

(b) 可能但非预期的路径

假设我们想要收集程序运行的所有节点名称，并且我们希望所有的 MPI 进程拥有这个名称列表。使用 `MPI_Allgather` 是一项简单的任务：

```c
MPI_Allgather(myhostname, mylen, MPI_CHAR, all_names, max, MPI_CHAR, MPI_COMM_WORLD);
```

218

第10章

```c
MPI_File outfile;
size = NX * (NY + 2);
MPI_File_open( MPI_COMM_WORLD, "solutionfile",MPI_MODE_CREATE | MPI_MODE_WRONLY,
MPI_INFO_NULL, &outfile );
MPI_File_set_view( outfile,
rank * (NY+2) * (i_end - i_start) * sizeof(double),
MPI_DOUBLE, MPI_DOUBLE, "native", MPI_INFO_NULL );
MPI_File_write( outfile, ulocal[1][0], size, MPI_DOUBLE,
MPI_File_close(&outfile );
```

图 10.11
Jacobi 的并行 I/O。注意，这种文件视图（file view）的选择仅适用于单个输出步骤；如果需要 Jacobi 方法的多个步骤，则必须修改 `MPI_File.set_view` 的参数。

`MPI` 对象信息是一个键值对（key=value pairs），可用于封装各种特殊用途信息，这些信息可能不适用于所有的 MPI 实现。当需要时，每当需要此类类型的参数且我们没有特殊信息要传递时，我们将使用 `MPI_INFO_NULL`。关于文件 `MPI_Info` 的详细信息，请参阅 [14, 第 2 章]。

每个进程看到的文件部分称为文件视图（file view），它通过调用 `MPI_File_set_view` 为每个进程设置。在我们的示例中，该调用为：

```c
MPI_File_set_view( outfile, rank * (NY+2) * ( ... ),
MPI_DOUBLE, MPI_DOUBLE, "native", MPI_INFO_NULL
```

第一个参数标识文件，第二个参数是文件中的偏移量（以字节为单位），进程的文件视图从此处开始。在这里，我们简单地将要写入的数据的大小乘以进程的秩（rank），以便每个进程的视图从文件中合适的位置开始。该参数的类型是 `MPI_Offset`，在支持大文件的系统上，预计它是一个 64 位整数。

下一个参数称为视图的元素类型（etype）；它指定了文件中数据的单位。这里只是 `MPI_DOUBLE`，因为我们将写入若干个双浮点数（doubles）。下一个参数称为文件类型（filetype）；它是描述文件中非连续单元的一种灵活方式。在我们的案例中，由于没有写入的非连续单元，我们可以直接使用 etype `MPI_DOUBLE`。通常情况下，任何 MPI 预定义或派生数据类型都可以用于 etype 和 filetype，更多细节请见下例所示。

# MPI 编程中的高级主题

下一个参数是定义要使用的数据表示方法的字符串。原生表示（native representation）表示按照数据在内存中的原始格式表示数据，这提供了最快的 I/O 性能，但可能以可移植性为代价。我们通过为最后一个参数提供 `MPI_INFO_NULL` 来指定我们没有额外信息。

随后 `MPI_File_write` 的调用变得非常直观。要写入的数据是一个连续的双浮点数数组，尽管它由（分布式的）矩阵的几行组成。在每个进程上，它从 `@ ulocal[0]` 开始，因此数据以（地址，计数，数据类型）的形式描述，就像对于 MPI 消息处理一样。我们通过传递 `MPI_STATUS_IGNORE` 来忽略状态。最后，我们（集体地）使用 `MPI_File_close` 关闭文件。

## 10.6.2 一个更复杂的示例

并行 I/O 不仅仅需要调用 `MPI_File_write` 代替 `write`。关键思想是识别对象（跨进程的），而不是每个进程的贡献。我们通过一个规则分布数组的示例来说明这一点。

10.12 中的代码写入了一个分布在进程中的、采用二维分解的数组。为了说明接口的表达力，我们展示了一个复杂情况：在 Jacobi 示例中，由于被多个影单元（ghost cells）包围，数组在内存中是非连续的（这在 [14] 中有更深入的介绍）。3. 以写入模式打开文件（`MPI_MODE_WRONLY`），并使用我们刚刚构造的数据类型设置文件视图。

4. 创建一个描述要写入数据的数据类型。我们在这里使用 `MPI_Type_subarray` 来定义不包含影单元的局部部分。如果没有影单元，我们可以在 `MPI_File_write` 调用中直接使用 `MPI_DOUBLE` 作为数据类型。

5. 使用 `MPI_File_close` 集体写入文件，并关闭文件。

这种视图看起来很复杂，但对于没有影单元的局部数组来说是简单的。

图 10.12

C 程序，写入一个由于影单元的存在而在内存中是非连续的数组（源自 [14] 中的示例）。

通过使用 MPI 数据类型描述数据及其在文件中的位置，并结合集体文件操作，MPI 实现可以充分利用 I/O 系统。结果是，使用 MPI I/O 执行的 I/O 操作比使用单个 Unix I/O 操作性能提升了百倍 [35]。

第一步是描述 `MPI_Put` 操作可能将数据放置的内存区域（该区域也可被 `MPI_Get` 访问或被 `MPI_Accumulate` 更新）。这是通过 `MPI_Win_create` 例程完成的：

```cpp
MPI_Win win;
double ulocal[MAX_NX] [NY2];
MPI_Win_create(ulocal, (NY+2)*(end_i-start+3)*sizeof(double), sizeof(double), MPI_INFO_NULL, MPI_COMM_WORLD, &win);
```

输入参数依次为：数组、数组的大小、数组基本单元的大小（在本例中为 `sizeof(double)`）、一个“提示”对象，以及指定哪些进程可以使用 RMA 访问数组的通信器。`MPI_Win_create` 是一个在该通信器上的集体调用。输出是一个 MPI 窗口对象。当窗口不再需要时，应该使用 `MPI_Win_free` 释放它。

RMA 操作在两个哨兵之间进行。一个哨兵开始一个允许访问窗口对象的周期，另一个则结束该周期。这些周期被称为 epoch（纪）。最简单的开始和结束 epoch 的例程是 `MPI_Win_fence`。该例程是在创建窗口对象的进程上集体调用的，它既结束了上一个 epoch 又启动了一个新的 epoch。该例程被称为“fence”（栅），是因为另一个进程启动的所有 RMA 操作（在 fence 返回之前的 epoch 中启动）以及在 fence 之后启动（通过该进程上匹配的 fence）的任何 RMA 操作，在 fence 返回之前都不会开始。这看起来可能很复杂，但实际上很好用。在实践中，`MPI_Win_fence` 仅用于将 RMA 操作分组成。这紧密遵循了 BSP 和 Cray SHMEM 模型，尽管增加了处理任何进程子集的能力。

有三个例程可启动 RMA 中的数据传输。这些 `MPI_Put`、`MPI_Get` 和 `MPI_Accumulate` 都是非阻塞的，就像 MPI 点对点通信是非阻塞的一样，它们在开始的那个 epoch 结束时完成（例如，在关闭的 `MPI_Win_fence` 处）。由于这些例程同时指定了数据的源和目的，因此它们的参数比点对点通信例程多。通过一次看几个参数，可以很容易地理解它们。

> ²MPI 为 RMA 有两种 epoch：访问 epoch（access epoch）和暴露 epoch（exposure epoch）。对于此处使用的示例，这些 epoch 是同时发生的，我们将它们都统称为 epoch。

# MPI 编程中的高级主题

- 1. 前三个参数描述源数据；即调用进程上的数据。这些是是通常的“缓冲区、计数、数据类型”参数。
- 2. 下一个参数是目标进程的秩（rank）。它充当 `MPI_Send` 目的地的功能。该秩相对于创建 MPI 窗口对象时使用的通信器。
- 3. 接下来的三个参数描述目标缓冲区。计数和数据类型参数与 `MPI_Recv` 的含义相同，但缓冲区的位置被指定为相对于目标进程上 `MPI_Win_create` 指定内存起始位置的偏移。该偏移量是以 `MPI_Win_create` 的位移参数为单位的，通常是基本数据类型的大小。
- 4. 最后一个参数是 MPI 窗口对象。

注意，没有 MPI 请求（request）；`MPI_Win_fence` 会完成所有之前的 RMA 操作。`MPI_Win_fence` 为 RMA 操作提供了一个所有进程参与的集体同步模型。这被称为活动目标同步（active target synchronization）。

通过这些例程，我们可以创建一个使用 RMA 代替点对点通信的网格交换版本。图 10.13 显示了一种可能的

另一种形式的访问不需要目标进程进行任何 MPI 调用（即使是 fence）。这被称为被动目标同步（passive target synchronization）。源进程使用 `MPI_Win_lock` 开始一个访问 epoch 并使用 `MPI_Win_unlock` 解锁该 epoch。由于这种 RMA 的被动性，本地内存（作为 `MPI_Win_create` 的第一个参数传递）应该用 `MPI_Alloc_mem` 分配并用 `MPI_Free_mem` 释放。有关被动目标 RMA 操作的更多信息，请参见 [14, 第 6 章]。还要注意，对于 2001 年，MPI 实现支持被动目标 RMA 操作。预计更多实现将在 2002 年支持这些操作。

关于远程内存访问更完整的讨论可以在 [14, 第 5 和 6 章] 中找到。本节描述了 RMA 例程。大多数目前的 RMA 实现强调功能而非性能。随着实现的成熟，RMA 操作的性能也将提高。

> ³`MPI_Win_lock` 和 `MPI_Win_unlock` 的名称实际上是误导；请将它们视为 beginRMA 和 end-RMA。

```cpp
void exchang_nbrs( double u_local[][][NY+2], int i_start, int i_end,
int left, right, MPI_Win win )
{
  MPI_Aint left_ghost_disp, right_ghost_disp;
  int c;
  MPI_Win_fence(0, win);
/* 将左边缘放入左邻居的最右侧
  影子单元中。参见关于 right_ghost_disp 的文本 */
  right_ghost_disp = 1 + (NY+2) * (i_end-i_start+2);
  MPI_Put(&u_local[1] [1], NY, MPI_DOUBLE,
         right_ghost_disp, NY, MPI_DOUBLE, win);
/* 将右边缘放入右邻居的最左侧
  单元 */
  left_ghost_disp = 1;
  c = i_end - i_start + 1;
  MPI_Put(&u_local[1] [1], NY, MPI_DOUBLE,
         left_ghost_disp, NY, MPI_DOUBLE, win);
  MPI_Win_fence(0, win);
}
```

# 10.13 使用 RMA 进行邻居交换的内存访问

# 10.8 C++ 和 Fortran 90

MPI 对 C 和 Fortran 77 的绑定。这些绑定非常相似；主要的区别在于错误代码的处理（C 中返回，Fortran 中通过最后一个参数设置）。在 MPI-2 中为 C++ 增加了绑定，并为 Fortran 定义了 MPI 模块。C++ 绑定提供了一个比 C 绑定更灵活的模型，但 MPI 对象定义在 MPI 命名空间。大多数 MPI 对象都有对应的类，例如数据类型的 `Datatype`。通信器和请求略有不同。有一个抽象基类 `Comm`，具有四个派生类：`Intracomm`、`Intercomm`、`Graphcomm` 和 `Cartcomm`。大多数通信器是内部的；请求有两个派生类：持久性请求和通用请求（MPI-2 新增）。

# MPI 编程中的高级主题

大多数 MPI 操作是相应对象的方法；例如，大多数点对点和集体通信都是通信器的方法。少数例程（如 `Init` 和 `Finalize`）是独立的。一个简单的 C++ MPI 程序如图 10.14 所示。

```cpp
#include "mpi.h"
#include <iostream.h>
int main(int argc, char *argv[])
{
    int data;
    MPI::Init();
    if (MPI::COMM_WORLD.Get_rank() == 0) {
        // 从进程 0 广播数据到所有其他进程
        cout << "Enter an int" << endl;
        cin >> data;
    }
    MPI::COMM_WORLD.Bcast(data, 1, MPI::INT, 0);
    MPI::Finalize();
    return 0;
}
```
