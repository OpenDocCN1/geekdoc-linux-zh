
MPI 中的通信器有两个用途。最显而易见的用途是描述一个进程集合。这一特性允许使用任何进程集合来使用集合例程，如`MPI_Bcast`或`MPI_Allreduce`。这种能力对于分层算法尤为重要，也有助于将计算划分为子任务，每个子任务都有自己的进程集合。例如，在 9.2 节的管理者-工作者示例中，将每个任务分配给一小部分进程可能是合适的，特别是如果这导致问题描述仅驻留在快速内存缓存中时。MPI 通信器非常适合于此；在创建新通信器时，MPI 例程`MPI_Comm_split`是唯一需要的例程。使用相对于通信器的秩来指定消息的来源和目的地也有助于将并行任务分解为更小但仍具有并行性的子任务，每个子任务都有自己的通信器。

MPI 通信器的一个更微妙但同样重要的用途涉及每个通信器包含的通信上下文。这种上下文对于编写能够安全、稳健地与其他代码（包括其他库和用户特定的应用程序代码）结合以构建完整应用程序的软件库至关重要。如果正确使用，通信上下文可保证消息被适当的例程接收，即使其他例程不够谨慎。考虑图 10.8（摘自 [6, Section 6.1.2]）中的示例。在这个例子中，有两个例程，由单独的库或软件模块提供。其中一个，`SendRight`，向右侧邻居发送消息并从左侧接收。另一个，`SendEnd`，从进程 0（最左侧）向最后一个进程（最右侧）发送消息。这两个例程在`MPI_Recv`调用中均使用`MPI_ANY_SOURCE`而不是特定的源。如图 10.8 所示，消息可能会混淆，导致程序接收到错误的数据。我们如何防止这种情况？几种方法行不通。一种是避免使用`MPI_ANY_SOURCE`。这解决了这个例子，但前提是`SendRight`和`SendEnd`都遵循此规则。这种方法对于由个人或团队编写的代码可能足够（尽管脆弱），但对于库则不够。例如，如果`SendEnd`由商业供应商编写且未使用`MPI_ANY_SOURCE`，而`SendRight`由不同的供应商或经验不足的程序员编写并使用了`MPI_ANY_SOURCE`，那么程序仍然会失败，并且看起来像是`SendEnd`出了故障（因为来自`SendEnd`的消息最先被接收）。

另一种行不通的方法是使用消息标签（message tags）来区分消息。同样，如果一个组编写了所有代码，并非常小心地为不同的软件模块分配消息标签，这是可行的。然而，在 MPI 接收调用中使用`MPI_ANY_TAG`仍然可以绕过这种方法。此外，如 [6] 中的图 6.5 所示，即使不使用`MPI_ANY_SOURCE`和`MPI_ANY_TAG`，不同的代码模块仍然可能接收到错误的消息。

MPI 通信器中的通信上下文为这些问题提供了解决方案。例程`MPI_Comm_dup`从输入通信器创建一个新的通信器，该通信器包含相同的进程（以相同的秩顺序），但具有新的通信上下文。在一个通信上下文中发送的 MPI 消息只能在该上下文中接收。因此，任何希望确保其所有消息仅在该库内被看到的软件模块或库，只需在开始时调用`MPI_Comm_dup`即可获得一个新的通信器。所有编写良好的使用 MPI 的库都会创建一个仅在该库内使用的私有通信器。

支持库的开发是 MPI 的设计目标之一。在这方面，MPI 非常成功。许多库和应用程序现在使用 MPI，并且由于 MPI 的可移植性，这些应用程序中的大多数都在 Beowulf 集群上运行。表 10.1 提供了使用 MPI 提供并行性的部分库列表。更完整的描述和列表可在`www.mcs.anl.gov/mpi/libraries`和`sal.kachinotech.com/G/3`上找到。

## 10.5 更多关于集合操作的内容

MPI 的优势之一是其可扩展的集合通信和计算例程的集合。图 10.9 展示了最重要的一些集合通信例程的功能。作为其实用性的例子，我们考虑一个简单示例。假设我们要收集程序运行在其上的所有节点的名称，并且我们希望所有 MPI 进程都具有这个名称列表。使用`MPI_Allgather`这是一个简单的任务：

```
char my_hostname[MAX_LEN], all_names[MAX_PROCS][MAX_LEN];
MPI_Allgather( my_hostname, MAX_LEN, MPI_CHAR,
               all_names, MAX_LEN, MPI_CHAR, MPI_COMM_WORLD );
```

此代码假设主机名不超过`MAX_LEN`个字符（包括末尾的空字符）。更好的代码会检查这一点：

```
char my_hostname[MAX_LEN], all_names[MAX_PROCS][MAX_LEN];
MPI_Allreduce( &my_name_len, &max_name_len, 1, MPI_INT, MPI_MAX,
               MPI_COMM_WORLD );
if ( max_name_len > MAX_LEN) {
    printf( "Error: names too long (%d)", max_name_len );
}
MPI_Allgather( my_hostname, MAX_LEN, MPI_CHAR,
all_names, MAX_LEN, MPI_CHAR, MPI_COMM_WORLD );
```

然而，这两种方法都移动了比必要更多的数据。一种更好的方法是首先收集每个处理器名称的大小，然后从每个处理器收集所需的确切字符数。这使用了全收集例程的“v”（代表向量）版本，`MPI_Allgatherv`，如图 10.10 所示。

这个例子提供了一种实现 9.3 节示例中操作的不同方式。许多并行代码可以使用 MPI 集合例程而不是 MPI 点对点通信来编写；此类代码通常具有更简单的逻辑结构，并且可以受益于集合通信例程的可扩展实现。

## 10.6 并行 I/O

MPI-2 提供了多种并行 I/O 操作，超出了我们在此能涵盖的范围。有关 MPI 中 I/O 的更详细讨论，请参阅 [7, Chapter 3]。

![](img/e2283ffaea56e577ac05056b4bb738fc_243_0.png)

当在`MPI_Recv`调用中使用`MPI_ANY_SOURCE`时，两种可能的消息匹配模式（摘自 [6]）。

图 10.7 用于网格二维分解的雅可比问题非阻塞交换代码。

```
void exchange_nbrs2d( double ulocal[][NY+2],
int i_start, int i_end, int j_start, int j_end,
int left, int right, int top, int bottom,
MPI_Datatype vectype )
{
MPI_Status statuses[8];
MPI_Request requests[8];
int c;

/* Begin send and receive from the left neighbor */
MPI_Isend( &ulocal[1][1], NY, MPI_DOUBLE, left, 0,
MPI_COMM_WORLD, &requests[0] );
MPI_Irecv( &ulocal[0][1], NY, MPI_DOUBLE, left, 0,
MPI_COMM_WORLD, &requests[1] );

/* Begin send and receive from the right neighbor */
c = i_end - i_start + 1;
MPI_Isend( &ulocal[c][1], NY, MPI_DOUBLE, right, 0,
MPI_COMM_WORLD, &requests[2] );
MPI_Irecv( &ulocal[c+1][1], NY, MPI_DOUBLE, right, 0,
MPI_COMM_WORLD, &requests[3] );

/* Begin send and receive from the top neighbor */
MPI_Isend( &ulocal[1][NY], 1, vectype, top, 0,
MPI_COMM_WORLD, &requests[4] );
MPI_Irecv( &ulocal[1][NY+1], 1, vectype, top, 0,
MPI_COMM_WORLD, &requests[5] );

/* Begin send and receive from the bottom neighbor */
MPI_Isend( &ulocal[1][1], 1, vectype, bottom, 0,
MPI_COMM_WORLD, &requests[6] );
MPI_Irecv( &ulocal[1][0], 1, vectype, bottom, 0,
MPI_COMM_WORLD, &requests[7] );

/* Wait for all communications to complete */
MPI_Waitall( 8, requests, statuses );
}
```

| 库 | 描述 | URL |
|---|---|---|
| PETSc | 偏微分方程（PDEs）的线性与非线性求解器 | www.mcs.anl.gov/petsc |
| Aztec | 稀疏线性方程组的并行迭代求解 | www.cs.sandia.gov/CRF/aztecl.html |
| Cactus | 偏微分方程（PDE）求解框架 | www.cactuscode.org |
| FFTW | 并行快速傅里叶变换（FFT） | www.fftw.org |
| PFPFPrint | 并行打印 | www.lnl1.gov/sccd/lc/ptcprint |
| HDF | 层次数据格式（HDF）文件的并行 I/O | hdf.ncsa.uiuc.edu/Parallel_HDF |
| NAG | 数值计算库 | www.nag.co.uk/numeric/fd/FDdescription.asp |
| ScaLAPACK | 并行线性代数 | www.netlib.org/scalapack |
| SPRNG | 可扩展的伪随机数生成器 | sprng.cs.fsu.edu |

表 10.1 使用 MPI 的库示例。

![](img/e2283ffaea56e577ac05056b4bb738fc_245_0.png)

图 10.9 MPI中集体数据移动的示意图。

MPI并行I/O方法的基本思想是，文件被一组进程集体打开，所有这些进程都被授予访问同一文件的权限。因此，MPI将通信子与文件相关联，允许对文件执行灵活的单个和集体操作。

```c
mylen = strlen(my_hostname) + 1; /* Include the trailing null */
MPI_Allgather(&mylen, 1, MPI_INT, all_lens, 1, MPI_INT, MPI_COMM_WORLD);
totlen = all_lens[size-1];
for (i=0; i<size-1; i++) {
    displs[i+1] = displs[i] + all_lens[i];
    totlen += all_lens[i];
}
all_names = (char *)malloc(totlen);
if (!all_names) MPI_Abort(MPI_COMM_WORLD, 1);
MPI_Allgatherv(my_hostname, mylen, MPI_CHAR, all_names, all_lens, displs, MPI_CHAR, MPI_COMM_WORLD);
/* Hostname for the jth process is &all_names[displs[j]] */
```

图 10.10 使用 `MPI_Allgather` 和 `MPI_Allgatherv`。

### 10.6.1 一个简单的例子

我们首先提供一个简单的例子，说明进程如何并行地将连续的数据块写入同一个文件。然后我们给出一个更复杂的例子，其中每个进程中的数据不是连续的，但可以通过 MPI 数据类型来描述。

对于我们的第一个例子，假设我们在完成第 9.3 节中求解泊松方程后，希望将解写入文件。我们不需要鬼元（ghost cells）的值，并且在一维分解中，每个进程中的行集在内存中构成一个连续区域，这大大简化了程序。程序的 I/O 部分如图 10.11 所示。

请记住，要从每个进程写入的数据（不包括鬼元，但包括边界数据）位于数组`local[i][j]`中，其中`i`从`i_start`到`i_end`，`j`从`0`到`NY-1`。

注意，MPI 文件对象的类型是`MPI_File`。此类文件对象的打开和关闭方式与常规文件类似。最显著的差异在于，打开文件是对由`MPI_File_open`第一个参数中的通信子指定的进程组执行的集体操作。单个进程可以通过指定单进程通信子`MPI_COMM_SELF`来打开文件。在这里，我们希望所有进程共享该文件，因此我们使用`MPI_COMM_WORLD`。

在讨论动态进程管理时，我们提到了 MPI info 对象。MPI info 对象是`key=value`对的集合，可用于封装各种可能不适用于所有 MPI 实现的特殊用途信息。在本节中，当需要这种类型的参数时，我们将始终使用`MPI_INFO_NULL`，因为我们没有特殊信息需要传递。有关`MPI_Info`的详细信息，请参见 [7, Chapter 2]。

```c
MPI_File outfile;
size = NX * (NY + 2);
MPI_File_open(MPI_COMM_WORLD, "solutionfile", MPI_MODE_CREATE | MPI_MODE_WRONLY, MPI_INFO_NULL, &outfile);

MPI_File_set_view(outfile, rank * (NY+2) * (i_end - i_start) * sizeof(double), MPI_DOUBLE, MPI_DOUBLE, "native", MPI_INFO_NULL);
MPI_File_write(outfile, &local[1][0], size, MPI_DOUBLE, MPI_STATUS_IGNORE);
MPI_File_close(&outfile);
```

图 10.11 雅可比解的并行 I/O。注意，这种文件视图的选择仅适用于单个输出步骤；如果需要雅可比方法的多个步骤的输出，则必须修改`MPI_File_set_view`的参数。

每个进程将看到的文件部分称为*file view*（文件视图），并通过调用`MPI_File_set_view`为每个进程设置。在我们的示例中，调用为

```c
MPI_File_set_view(outfile, rank * (NY+2) * (. . . ), MPI_DOUBLE, MPI_DOUBLE, "native", MPI_INFO_NULL)
```

第一个参数标识文件；第二个参数是位移（以字节为单位），指定该进程对文件的视图开始于文件中的位置。在这里，我们只是将要写入的数据大小乘以进程的排名，以便每个进程的视图从文件中的适当位置开始。此参数的类型是`MPI_Offset`，在支持大文件的系统上，它通常是一个 6 位整数。

下一个参数称为视图的*etype*（元素类型）；它指定文件中的数据单位。在这里，由于我们将写入一定数量的双精度浮点数，所以它只是`MPI_DOUBLE`。下一个参数称为*filetype*（文件类型）；它是描述文件中连续视图的灵活方式。在我们的情况下，由于没有要写入的非连续单元，我们可以直接使用 etype，`MPI_DOUBLE`。通常，任何 MPI 预定义或衍生数据类型都可以用于 etypes 和 filetypes。我们将在下一个例子中更详细地探讨这种用法。

下一个参数是一个字符串，定义要使用的*data representation*（数据表示）。原生表示法意味着磁盘上的数据表示方式与内存中的完全一致，这提供了最快的 I/O 性能，但可能以可移植性为代价。我们通过为最后一个参数提供`MPI_INFO_NULL`来指定我们没有额外信息。

调用`MPI_File_write`也很简单。要写入的数据是一个连续的双精度浮点数组，尽管它由（分布式）矩阵的几行组成。在每个进程上，它从`&local[0][1]`开始，因此数据以（地址，计数，数据类型）形式描述，就像 MPI 消息一样。我们通过传递`MPI_STATUS_IGNORE`来忽略状态。最后，我们（集体地）使用`MPI_File_close`关闭文件。

### 10.6.2 一个更复杂的例子

并行 I/O 不仅仅需要调用`MPI_File_write`而不是*write*。关键思想是识别*对象*（跨进程），而不是每个进程的贡献。我们通过一个常规分布式数组的例子来说明这一点。

图 10.12 中的代码写出了一个在进程中通过二维分解分布的数组。为了说明 MPI 接口的表达能力，我们展示了一个复杂的情况，其中，如在雅可比示例中一样，分布式数组被*ghost cells*（鬼元）包围。这个例子在*Using MPI 2* [7] 的第 3 章中更详细地讨论，包括没有鬼元的分布式数组的较简单情况。

这个例子可能看起来很复杂，但每一步都相对简单。

1. 建立一个通信子，代表一个虚拟进程数组，该数组与分布式数组的分布方式相匹配。这种方法使用`MPI_Cart_create`例程，并使用`MPI_Cart_coords`来查找调用进程在此进程数组中的坐标。这种特定的进程排序选择很重要，因为它与`MPI_Type_create_subarray`所需的排序相匹配。
