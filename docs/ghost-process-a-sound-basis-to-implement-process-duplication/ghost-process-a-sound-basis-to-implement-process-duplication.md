
# Ghost Process：在 Linux 集群中实现进程复制、迁移和检查点重启的基础方案

## 摘要

进程管理机制（进程复制、迁移和检查点/重启）对于集群系统的高性能和高可用性非常有用。

单映像（single image approach）方法旨在为检查点进程、进程迁移和进程复制提供一种全局进程管理服务机制。在此背景下，虚拟化的通用机制非常困难，而传统的操作系统并没有提供此类机制。

本文提出了一种用于虚拟化“幽进程”（ghost process）的内核服务，并扩展了 Linux 内核。幽进程机制已在基于 Linux 的 Kerrighed 系统映像中得以实现。

**关键词：** Linux 集群、分布式操作系统、系统映像、进程虚拟化。

为了简化集群的使用、提高易用性，并利用集群的分布式资源，进程管理机制在这方面非常有用。进程复制允许在集群节点上部署并行执行的进程。虽然传统的检查点机制可以扩展集群并在执行特定负载期间利用集群资源，但在创建检查点时，可能无法正确地将检查点放置在集群节点上。动态负载均衡策略对于保持集群平衡至关重要。这些策略通过高效的进程管理机制实现，将进程从一个节点移动到另一个节点。

## 1 引言

如今，集群被越来越广泛用于执行数值应用。需要相应的机制来实现进程迁移。首先，进程迁移可以通过检查点/重启机制实现：进程在共享文件系统（如使用 `NFS`）上创建检查点，并从节点上的文件系统恢复。第二种方法类似于 `Condor`：为了效率，直接通过网络迁移进程。在这样的系统中，进程从一个节点中提取，直接发送到另一个节点，并创建一个新进程。我们针对这种方法使用 `OpenSSI`[3] 或 `Most`[1]。

目前，没有哪个系统能以高效的方式提供全套机制，`Genesis`[4] 基于微内核，且没有提供一个完整的单元，如：

为了效率和易用性，对集群中全局进程管理（进程复制、迁移、检查点/重启）所需的机制进行内核级实现是非常理想的。Linux 内核没有为进程虚拟化提供系统服务和接口。

在本文中，我们介绍了基于 Linux 内核的进程虚拟化幽进程机制，它提供了一个用于虚拟化进程的服务和 API。该机制允许进程管理机制的实现。例如，我们展示了集群规模的进程迁移实现：一种新的迁移机制以及进程检查点/重启机制。

幽进程机制已基于 Linux 的 KIRRIGED 系统映像 (SSI) 集群操作系统[9] 中实现。它已被用于在 Kirriged 中高效实现进程检查点/重启。结合相关的检查点/重启机制和其他全局资源管理机制（例如全局信号管理机制，这些不在本文的讨论范围内），它实现了进程的全局管理。

本文的结构组织如下：第 2 节涉及集群全局进程管理。第 3 节描述了我们提出的进程虚拟化进程概念。第 4 节展示了如何在集群上实现进程迁移和检查点/重启。第 5 节提供了幽机制在检查点/重启应用框架下的评估。最后，第 6 节给出结论。

## 2 背景

Linux 内核提供了一些简单的接口来管理单机上的进程。遗憾的是，没有接口可以从系统中提取进程以创建一个独立于本地环境的进程的“映像”。

为了实现方便的进程虚拟化，我们需要一个能够提取任何进程的服务以及一个管理进程的简单接口。进程管理机制不应与进程本身关联。对于迁移，进程被提取并通过网络传输到节点，而检查点则保存在稳定设备上。因此，进程虚拟化接口应该为全局进程管理机制提供一种简单的实现。这种能力对于开发适应硬件的全局管理机制也同样重要。例如，通过共享资源访问，进程迁移可以在使用特定编程的网络技术上进行。第 3.1 节描述了进程虚拟化服务，第 3.2 节介绍了虚拟化接口并定义了资源访问。

## 3 用于进程虚拟化的“幽”概念

在系统中，进程由两类信息表示：内核中可用的进程信息（如打开的文件、内存段、信号）以及操作系统数据结构中可用的进程状态。寄存器值的提取更为困难。在大多数系统中，这些值仅在优先级系统中才可用。例如，在 Linux 中，寄存器值仅在内核执行期间（如拦截期间）返回时可用。因此，为了在系统中创建幽进程，必须修改系统以使寄存器值可用。它还能够在任何时间描述进程的激活状态，即使进程没有运行。这种机制能够描述进程的激活状态，即使进程没有运行（注：原文此处似乎有重复，翻译已根据逻辑顺顺）*。因此，进程虚拟化接口应该提供一种全局进程管理机制的简单实现。第 3.1 节描述了进程虚拟化服务，第 3.2 节展示了虚拟化接口并定义了资源访问。

*注：原文此处存在表述重复，翻译时保持了语意连贯。*

为了实现方便的进程虚拟化，我们需要一个能够提取任何进程的服务以及一个管理进程的简单接口。进程管理机制不应与进程本身关联。对于迁移，进程被提取并通过网络传输到节点，而检查点则保存在稳定设备上。因此，进程虚拟化接口应该提供一种全局进程管理机制的简单实现。这种能力对于开发适应硬件的全局管理机制也同样重要。例如，通过共享资源访问，进程迁移可以在使用特定编程的网络技术上进行。第 3.1 节描述了进程虚拟化服务，第 3.2 节展示了虚拟化接口并定义了资源访问。

### 3.1 进程虚拟化的实现

为了效率和易用性，对集群中全局进程管理（进程复制、迁移、检查点/重启）所需的机制进行内核级实现是非常理想的。Linux 内核没有为进程虚拟化提供系统服务和接口。

在本文中，我们介绍了基于 Linux 内核的进程虚拟化幽进程机制，它提供了一个用于虚拟化进程的服务和 API。该机制允许进程管理机制的实现。例如，我们展示了集群规模的进程迁移实现：一种新的迁移机制以及进程检查点/重启机制。

幽进程机制已在基于 Linux 的 KIRRIGED 系统映像 (SSI) 集群操作系统[9] 中实现。它已被用于在 Kirriged 中高效实现进程检查点/重启。结合相关的检查点/重启机制和其他全局资源管理机制（例如全局信号管理机制，这些不在本文的讨论范围内），它实现了进程的全局管理。

### 3.2 资源访问接口

**内存访问** 列表 2 显示了管理内存缓冲区的接口。

该接口集成在幽灵进程（ghost process）管理中，可以使用列表 3 所示的接口将文件与幽灵进程关联。

#### 列表 2 用于内存访问的 Kerrighed API

```c
// 初始化函数 */
// int buf_create, create_new_buffer(buffer size);
// 读取函数 */
// int buf_read(buffer, size);
// 写入函数 */
// int buf_write(buffer, source, size);
// 将内存访问方法插入
// 幽灵进程实例的函数 /*
// int associate_buffer_to_ghost(buffer, ghost);
```

**网络访问** `KERRIGED` 提供了一个通过网络发送/接收数据的接口（见列表 4）。

#### 列表 4 用于网络访问的 Kerrighed API

```c
// 读取函数 */
// int network_read(remote_node_id, variable, size);
// 写入函数 */
// int network_write(remote_node_id, variable, size);
// 将网络访问方法插入
// 幽灵进程实例的函数 /*
// int associate_node_to_ghost(remote_node_id, channel, ghost);
```

**文件访问** `KERRIGED` 还提供了一个管理文件读写操作的接口（见列表 3）。

#### 列表 3 用于文件访问的 Kerrighed API

```c
// 初始化函数 */
// int file_open(file, pathname);
// 读取函数 */
// int file_read(file, destination, size);
// 写入函数 */
// int file_write(file, source, size);
// 结束函数 */
// int file_close(file);
// 将文件访问方法插入
// 幽灵进程实例的函数 /*
// int associate_file_to_ghost(file, ghost);
```

### 3.3 总结

幽灵进程机制是一种进程虚拟化机制，它允许以简单的方式实现全局进程管理，如复制、迁移和检查点/重启（checkpoint/restart）。

为了使用幽灵进程机制，下一节详细介绍了两种全局进程管理机制的实现：(i) 进程迁移和 (ii) 进程检查点/重启。

## 4 使用进程创建全局进程管理机制

第 3.2 节描述的 API 用于创建新的机制来全局管理进程。对于每种机制（例如进程迁移或复制），在创建幽灵进程后，系统程序员必须管理创建该幽灵进程的源进程，并管理从幽灵进程创建的新活动进程。我们将在第 4.1 节的进程迁移示例和第 4.2 节的进程检查点示例中进行说明。

### 4.1 进程迁移

例如，列表 5 显示了一种实现进程迁移的简单方法：从源节点的内存中提取幽灵进程，然后通过网络将幽灵进程发送到远程目的地。在目的端，需要导入幽灵进程，然后由幽灵进程创建一个新的活动进程。当新进程在目的地创建时，会向源节点发送一个确认。接收到的确认后会被销毁。

```c
// 进程迁移：在源节点执行的算法 /
void migrate_ghost(pid) {
    // 查找要迁移的进程 /
    pid task = find_task_by_pid(pid);
    // 创建幽灵进程的新实例 /
    ghost ghost = create_new_ghost();
    // 将幽灵进程插入内存 /
    plug_resource_interface(MEMORY_WRITE, ghost);
    // 在内存中导出 /
    export_ghost(ghost);
    // 将幽灵进程发送到远程节点 /
    send_ghost(ghost, remote_node_id);
    // 进程创建后等待来自远程节点的确认 /
    distant_pid = wait_ack(remote_node_id);
    // 销毁源节点上的幽灵进程 /
    destroy_process(process);
}
```

```c
// 进程迁移：在目的节点执行的算法 /
void receive_migrated_ghost(pid) {
    // 从源节点接收幽灵进程，幽灵进程保存在缓冲区中 /
    memory_buffer = receive_ghost(original_node_id);
}
```

```c
// 创建幽灵进程的新实例 /
ghost = create_new_ghost();
// 将缓冲区与幽灵进程关联 /
associate_buffer_to_ghost(buffer, ghost);
// 将幽灵进程插入只读接口的内存中 /
plug_resource_interface(MEMORY_READ, ghost);
// 如果幽灵进程已加载，则创建一个进程 /
new_pid = import_process(ghost, process);
// 如果进程创建成功，则向源节点发送确认 /
send_ack(original_node_id, new_node_id);
```

### 4.2 检查点/重启机制

进程检查点非常简单。需要提取进程镜像并将其存储在稳定存储中。进程重启机制也很简单。从存储设备中保存的进程镜像创建一个活动进程。在 Kubernetes 中，检查点存储在内存或磁盘中。

本节详细介绍了检查点/重启机制的实现。对于内存检查点，幽灵进程需要使用本地内存。我们在第 4.3 节中介绍了将检查点存储在内存中的机制实现。

### 4.3 内存检查点/重启的实现

进程检查点非常简单。需要提取进程镜像并将其存储在稳定存储中。进程重启机制也很简单。从存储设备中保存的进程镜像创建一个活动进程。

对于内存检查点，幽灵进程需要使用本地内存。我们在第 4.3 节中介绍了将检查点存储在内存中的机制实现。

### 4.4 磁盘检查点/重启的实现

进程检查点非常简单。需要提取进程镜像并将其存储在稳定存储中。进程重启机制也很简单。从存储设备中保存的进程镜像创建一个活动进程。

#### 4.3.1 内存检查点算法

对于内存检查点，幽灵进程需要使用本地内存。我们在第 4.3 节中介绍了将检查点存储在内存中的机制实现。

```c
// 进程迁移：在源节点执行的算法 /
void migrate_ghost(pid) {
    // 查找要迁移的进程 /
    pid task = find_task_by_pid(pid);
    // 创建幽灵进程的新实例 /
    ghost ghost = create_new_ghost();
    // 将幽灵进程插入内存 /
    plug_resource_interface(MEMORY_WRITE, ghost);
    // 在内存中导出 /
    export_ghost(ghost);
    // 将幽灵进程发送到远程节点 /
    send_ghost(ghost, remote_node_id);
    // 进程创建后等待来自远程节点的确认 /
    distant_pid = wait_ack(remote_node_id);
    // 销毁源节点上的幽灵进程 /
    destroy_process(process);
}
```

![](img/758d342663593ae2e0648d2aefd9a8ae_5_0.png)

| 矩阵大小 | 幽灵进程大小 (KB) |
|---|---|



| 500 | 229 |

| 750 | 334 |

| 1000 | 429 |

| 1250 | 629 |

| 1500 | 729 |

| 2000 | 933 |

我们已经看到幽灵进程机制由两部分组成：幽灵进程的定义和资源访问。对于内存检查点，幽灵进程需要使用本地内存。我们在第 4.3 节中介绍了将检查点存储在内存中的机制实现。

# 5. 评估

在本节中，我们通过幽灵进程机制在检查点/重启机制中的应用对其进行评估。评估是在集群操作系统的这些实现中完成的。我们的集群是一个集群，每个节点都是包含 1 GHz 处理器、5 MB 内存、100Mbps 以太网和硬盘的 PC。所有评估都是通过执行顺序版本的改进格拉姆-施密特（`mgs`）应用程序完成的。`mgs` 从一组向量产生这些向量所生成空间的正交基。

与应用程序内存空间的大小成正比。内存空间越大，影子进程（ghost process）就越大。对于 `mgs` 应用程序，内存大小会影响影子空间，因为其他进程信息具有恒定的大小（例如，应用程序始终访问相同的文件）。

在提取过程中期间的内存是总检查点（checkpoint）时间的大部分。因此，使用本地内存的检查点机制的效率取决于导出机制的效率。

图 5 显示了从内存检查点重启进程所需的时间。重启的成本与检查点的成本（使用本地内存）相似。影子机制导出的效率决定了这一点。影子进程的导入时间是重启时间的大部分。

![](img/758d342663593ae2e0648d2aefd9a8ae_6_0.png)

图 4. 创建内存进程检查点的成本

我们评估了进程检查点/重启机制的成本，并考虑了导出/导入机制的成本。因此，我们计算了创建检查点的总时间（即从进程检查点开始到影子进程内存结束的时间）以及导出时间。注意，进程创建时间是总检查点创建时间的一部分。

## 5.2 使用本地 DC 进行检查点/重启机制的评估

内核的文件 API 使用本地文件系统。当创建检查点以存储影子进程时，该文件也会存储在本地文件缓存中（使用本地内存以确保数据物理存储在磁盘上）。此外，为了确保没有缓存效应影响所有性能，所有重启都在机器重启后进行。

图 6 显示了不同矩阵大小在本地磁盘上对进程进行检查所需的时间。随着内存

![](img/758d342663593ae2e0648d2aefd9a8ae_6_1.png)

图 6. 进程磁盘检查点的成本

## 5.1 使用本地内存进行检查点/重启机制的评估

图 4 显示了在本地内存中对进程进行检查的时间，展示了总检查点创建时间和影子进程过期时间。影子进程

![](img/758d342663593ae2e0648d2aefd9a8ae_6_2.png)

检查点的访问时间（导出阶段）是总检查点时间的大部分。

图 7 显示了从存储在磁盘上的检查点重启进程的成本，该检查点文件未缓存。重启成本源于磁盘访问。我们在配置中观察到，磁盘检查点的成本是内存检查点成本的约 10 倍。

图 5. 从内存检查点重启成本

## 5.3 总结

性能评估表明，对于内存和磁盘中的检查点/重启，性能都直接取决于影子管理的效率。因此，通过提高影子进程的效率（以及内存访问、保存在机制中的数据保存效率，以及特别是资源分配的效率），全局进程管理机制的整体效率将得到提高。

![](img/758d342663593ae2e0648d2aefd9a8ae_7_0.png)

# 结论

在本文中，我们展示了用于进程虚拟化的影子机制，以及如何利用它来确保各种全局进程管理机制的易于实现。影子进程机制为进程虚拟化提供了完整服务（导出/导入机制），并为影子进程实例访问共享资源的一组接口。通过影子进程，各种进程管理机制可以扩展到集群规模。这种方法保证了全局进程管理新机制维护和开发的便利性。第二个好处是，提高影子进程机制和全局进程管理的效率可以变得更加高效。

影子进程机制已在 `KERRIG` 全局集群操作系统实现。`KERRIG` 使用基于影子进程的进程复制和检查点重启机制。

`Kerrid` 提供了负责资源管理的不同分布式服务。结合全局内存管理、影子进程（导入进程复制同步服务，以及无同步集群），在 `Kerrid` 中实现了一套完整的进程。

提供进程虚拟化机制的系统（例如进程迁移、进程检查点）运行在内核级，并基于特定的内核补丁。然而，所有这些补丁都是相似的。因此，应该使用通用补丁并集成该补丁，以简化此类集群系统虚拟化机制的开发。影子进程机制可以很容易移植到此类补丁上。

# 参考文献

- [1] A. Barak and O. La. 用于高性能计算的 MOSIX 多机系统。Generation Computer Systems, 13(4):361–372, 1998.

- [2] J. Bakery and M. Livny. Deploying a high checkpoint. In R. Buyya, High Performance Cluster Computing: Architectures and Systems, 1999.

- [3] D. J. Harris and E. Roman. The design and implementation of lab checkpoint. Technical Report, Berkeley Lab, 2005.

- [4] G. Gremicki, M. Hoblich, and J. Sick. Efficiency gains and easy to use cluster systems. Parallel Computer, 28(4):557–606, 2002.

- [5] Henderson and L. Robert. Scheduling under the portable batch system. In G. French and L. Rudolph, Scheduling for Parallel Processing, 5th European Workshop on OpenMP (EUOMP '93), Sept. 1995. Lecture Notes in Computer Science, 940.

- [6] E. Marshall. The Bewfoot service department. In Industrial Cluster Systems (ICS) 2002, pages 129–132, New York City, USA, 2002.

- [7] D. Gray, G. Gallard, R. Lont, C. Morin, and J.-Berth. A cluster system for running OpenMP. In 5th European Workshop on OpenMP (EUOMP '03), Sept. 2003.

- [8] A. Gulić, F. Daulis, Y. Paindandre, R. Witcher, and S. Zona. Process migration. ACM Computing Systems (CSUR), 33(2):241–299, 2000.

- [9] C. Morin, P. Gallard, R. Lont way, and G. Wallard. Towards efficient scheduling: Image processing operating system. Generation Computer Systems, 2004.

- [10] C. Morin, R. Lontiaux, G. Gallard, G. Utard, R. Badnadh, and L. Rilling. Kerrigid: a single image cluster system for high performance computing. In: Proc of 2003: Parallel processing, volume 279 of Lect. Notes in Comput. Sci. pages 1291–1294. Springer Verlag, Aug. 2003.

- [11] E. Pagnon. Transparent checkpointing of parallel processes. International Symposium on Parallel and Distributed Processing Symposium, Nice, France, apr. 2003.

- [12] G. Wallard, C. J.-Berth, and L. Rilling. New approach to configurable dynamic scheduling in clusters based on single image techniques. In Industrial Track of the International Parallel and Distributed Processing Symposium, Nice, France, apr.

- [13] B. J. Waller. Open system image cluster project. Technical report. Hewlett-Packard, 2000.
