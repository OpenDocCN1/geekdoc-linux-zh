
| PID | USERNAME | THR | PRI | SIZE | RES | STATE | TIME | CPU | COMMAND |
|---|---|---|---|---|---|---|---|---|---|
| 9036 | oracle | 1 | 0 | 1612M | 1580M | sleep | 4:19 | 0.00% | oracle |
| 10260 | oracle | 1 | 0 | 1528M | 1507M | sleep | 1:49 | 0.00% | oracle |
| 9050 | oracle | 2 | 0 | 1525M | 1504M | sleep | 0:35 | 0.00% | oracle |
| 45022 | oracle | 2 | 0 | 1525M | 1505M | sleep | 1:58 | 0.00% | oracle |
| 22583 | oracle | 2 | 0 | 1513M | 1492M | sleep | 1:34 | 0.00% | oracle |
| 27378 | oracle | 1 | 0 | 1512M | 1491M | sleep | 1:57 | 0.00% | oracle |
| 27784 | oracle | 1 | 0 | 1511M | 1490M | sleep | 8:50 | 0.00% | oracle |
| 27370 | oracle | 1 | 0 | 1510M | 1489M | sleep | 8:13 | 0.00% | oracle |
| 27372 | oracle | 1 | 0 | 1510M | 1489M | sleep | 1:06 | 0.00% | oracle |
| 27376 | oracle | 1 | 0 | 1510M | 1489M | sleep | 5:32 | 0.00% | oracle |
| 27382 | oracle | 1 | 0 | 1510M | 1490M | sleep | 4:40 | 0.00% | oracle |
| 20965 | oracle | 2 | 0 | 1509M | 1487M | sleep | 1:03 | 0.00% | oracle |
| 15192 | oracle | 2 | 0 | 1506M | 1486M | sleep | 4:11 | 0.00% | oracle |
| 27430 | oracle | 1 | 0 | 1506M | 1485M | sleep | 0:16 | 0.00% | oracle |
| 27422 | oracle | 1 | 0 | 1506M | 1485M | sleep | 0:16 | 0.00% | oracle |

## 第 2 章 · 内存与处理器调优

通过进程。这本质上是将处理扩展缓存的负担从应用程序转移出来，交给了操作系统（OS）。应用程序只需通过系统调用来映射内存页，并在不再需要时取消页映射。与扩展缓存带来的整体收益相比，映射和取消映射缓冲区的开销是微乎其微的。大多数情况下，通过 L2 缓存页表从虚拟地址映射到物理地址的缓冲区映射是一项低成本操作。Solaris 8 通过允许 32 位进程访问超过 4 GB 的物理内存，扩展了内存（XMEM）。Solaris 8 使用文件系统（xmemfs）来实现扩展内存访问。在芯片制造商和操作系统供应商（OS vendors）迁移到 64 位环境之前，扩展缓存功能对系统性能至关重要。这允许大型数据库利用大型扩展缓存，并在数据中更多地减少 I/O。

Solaris 7 提供了 64 位功能以及 64 位开发环境。Solaris 7 的 64 位选项需要诸如 UltraSPARC 这样的 64 位架构。对于 Intel 平台，Solaris 7 的 64 位选项将需要 Intel 的新一代 IA-64（64 位）微处理器。

Sequent 通过 `virtwin()` 和 `shmat()` 系统提供扩展缓存功能，用于将扩展缓存缓冲区映射到用户进程地址空间。扩展缓存功能上的 Oracle 8。Oracle 8 扩展缓存功能允许 SGA 缓冲区池层位于虚拟地址空间之外。缓冲区仅在需要时才映射到一组窗口页（window panes）中。

HP-UX 11.0 提供了 64 位操作系统功能，包括大内存段和大文件等特性。HP-UX 11.0 允许共享内存大小达到 8 TB，最大文件系统和文件大小为 128 GB，进程数据大小为 4 TB。V2200 HP 企业级服务器支持 64 位 HP-UX 11.0，并且与 T 类服务器相比有显著的性能提升。HP 也在与 Intel 合作，并协助设计了 IA-64 架构。

在 Solaris (SPARC) 和 HP-UX 11.0 等提供 64 位支持的平台上，提供了 64 版本的 Oracle 8 和 Oracle 8i。Oracle 8 和 Oracle 8i 的 64 位版本允许您利用 64 位平台的优势（例如允许更大的内存配置、更多的用户和更多的进程）来提高性能和可扩展性。这允许实现更大的数据库配置以及更大的内存池。

### 大页大小

另一个有助于提高大型 SGA 性能的有用功能是大页大小（large page size）功能。这允许使用 1 MB 或 4 MB 的页大小，而不是取决于平台默认的 4 KB 或 8 KB。使用大页大小功能可以减少内核内存分配器和页守护进程（page daemon）的工作，从而提高虚拟内存的效率。大页功能对于大型 SGA 最有用。

### 2.12 共享内存参数

在 Solaris 2.6 中，创建大型共享内存段时会使用 4 MB 的大页。当通过 `shmat()` 调用连接到共享内存段时，您应该设置 `SHM_SHARE_MMU` 标志。此外，您指定的虚拟地址应该是 4 MB 对齐的，并且应该启用 ISM（亲密共享内存，Intimate Shared Memory）。

HP-UX 11.0 提供了变动页大小选项，允许您根据工作负载的类型指定分页大小。大页大小可用于进程文本、进程数据、进程堆、共享内存和共享库。使用 `chattr` 命令，您可以指定文本或数据页大小。内核也会为具有 `default` 页大小的可执行文件透明地选择页大小。内核使用大小来决定可执行文件的页大小。为了使用大页大小，内存地址必须是对齐的。HP-UX 11.0 提供了变动页大小，包括 `vps_pagesize`、`vps_ceiling` 和 `vps_chattr`。`vps_pagesize` 参数指定了默认页大小。`vps_ceiling` 参数指定了允许的内存限制。`vps_chattr` 参数指定了共享内存。

此处...2的。

### 2.12 共享内存参数（此处应为 2.13 共享内存调优）

### 2.13 调整共享内存

```
set shmsys:ism_off=1   *** 禁用 ISM

set shmsys:ism_off=0 *** 默认行为

set shmsys:share_page_table=1 *** 强制使用 ISM

set shmsys:share_page_table=0 *** 默认行为
```

若要在 Solaris 内核中强制使用 ISM（共享内存映射），请编辑 `/etc/system` 文件并添加以下条目：

```
set shmsys:share_page_table=1 *** 强制使用 ISM
```

如果 `is_off` 参数设置为 1，则 ISM 连接将禁用应用程序对 ISM 的请求。如果 `share_page_table` 参数设置为 1，无论应用程序如何，所有共享内存连接都将使用 ISM。`share_page_table` 参数的优先级高于 `is_off` 参数，因此会强制使用 ISM。由于应用程序控制 ISM 的使用，因此没有必要使用这些 /etc/kernel 参数。对于 Oracle 服务器，设置 `init.ora` 参数 `use_ism=TRUE` 或 `_use_ism-TRUE`（Oracle 8）会导致使用 ISM（如果可能的话）。

要在 Oracle 服务器内部启用 ISM 使用，请设置 `init.ora` 参数 `use_ism=TRUE`。在具有大量并发用户的 Solaris 系统上，启用此功能可以极大提高性能。在 Oracle 8 中，该参数是一个下划线参数（即 `_use_ism`），默认值是启用 ISM。

你可以使用 `/usr/proc/bin/pmap` 或 `truss` 工具来验证是否实际上正在使用 ISM。`/usr/proc/bin/pmap` 显示给定进程的进程地址映射。`pmap` 工具将列出由进程连接的共享内存段。例如，使用 `ps` 命令获取实例的数据库写器（database writer）进程的 ID。使用 `pmap` 工具报告数据库写器进程的进程地址映射，如下所示：

```
myhost>/usr/proc/bin/pmap -x 27103
```
