
- `/proc/<pid>/pagedata` — 进程地址空间的另一种表示形式。提供页级引用和修改跟踪。
- `/proc/<pid>/watch` — `prwatch` 结构数组（定义在 `/usr/include/sys/procfs.h`），在内核通过向控制文件写入数据设置 `PCWATCH` 操作时创建。允许监视（观察）一个或多个地址空间范围，当对受监视页面进行内存引用时会产生陷阱。
- `/proc/<pid>/cwd` — 指向进程当前工作目录的符号链接。
- `/proc/<pid>/root` — 指向进程根目录的符号链接。
- `/proc/<pid>/fd` — 包含进程已打开文件引用的目录。
- `/proc/<pid>/fd/n` — 进程的已打开文件描述符。目录文件以符号链接形式表示。
- `/proc/<pid>/object` — 包含进程所链接的二进制共享对象文件的子目录。
- `/proc/<pid>/object/nn` — 二进制对象文件。进程的可执行二进制文件（a.out），以及进程所链接的共享对象文件。

除了进程级维护的文件对象和子目录之外，每个 `/proc/<pid>/` 目录还包含一个 `lwp` 子目录，其中包含几个与各 LWP 数据相关的文件对象。下面介绍这些子目录。

- `/proc/<pid>/lwp` — 包含表示进程中所有 LWP 的文件的子目录。
- `/proc/<pid>/lwp/<lwpid>` — 包含特定于某个 LWP 的 procfs 文件的子目录。
- `/proc/<pid>/lwp/<lwpid>/lwpctl` — 用于按 LWP 发出控制操作的控制文件。
- `/proc/<pid>/lwp/<lwpid>/lwpstatus` — 如 `/usr/include/sys/procfs.h` 中的 `lwpstatus` 结构所定义的 LWP 状态和状态信息。
- `/proc/<pid>/lwp/<lwpid>/lwpinfo` — LWP 的 `ps(1)` 命令信息，如同样位于 `/usr/include/sys/procfs.h` 的 `lwpinfo` 所定义。
- `/proc/<pid>/lwp/<lwpid>/lwpusage` — LWP 资源使用数据。参见第 318 页的“进程资源使用情况”。
- `/proc/<pid>/lwp/<lwpid>/xregs` — 额外的通用状态寄存器。该文件特定于处理器体系结构，在某些平台上可能不存在。在基于 SPARC 的系统中，此文件包含的数据由 `/usr/include/sys/procfs_isa.h` 中的 `prxregset` 结构定义。
- `/proc/<pid>/lwp/<lwpid>/gwindows` — 通用寄存器窗口。此文件仅存在于基于 SPARC 的系统中，表示 LWP 的通用寄存器集（硬件上下文的一部分），如 `/usr/include/sys/regset.h` 中的 `gwindows` 结构所定义。
- `/proc/<pid>/lwp/<lwpid>/asrs` — 辅助寄存器集。仅限 SPARC V9 架构（UltraSPARC）。这是 SPARC V9 架构定义的额外一组硬件寄存器。该文件表示辅助寄存器，仅存在于运行 64 位内核（Solaris 7 或更高版本）的基于 sun4u 的系统中，并且仅适用于 64 位进程。（请记住，64 位内核可以运行 32 位进程。32 位进程在其 lwp 子目录空间中不会拥有此文件。）

以上完整列出了 procfs 目录空间中的文件和子目录。再次提醒，请参阅 `proc(4)` 手册页，以了解 `/proc` 中各个文件的更详细信息以及可用控制消息的完整说明。

### 8.6.1 Procfs 实现

Procfs 以可动态加载的内核模块 `/kernel/fs/procfs` 的形式实现，系统会在启动时自动加载它。由于 `/etc/vfstab` 文件中的默认 `/proc` 条目，`/proc` 在系统启动期间被挂载。挂载阶段会调用 procfs 的 `prinit()`（初始化）和 `prmount()` 文件系统特定函数，这些函数会初始化 procfs 的 vfs 结构，并为顶层目录文件 `/proc` 创建和初始化一个 vnode。

`/proc` 文件的内核内存空间大部分是动态分配的，但会进行一项初始静态分配，用于提供支持系统所配置的最大进程数所需的目录槽位数量（参见第 290 页的“内核进程表”）。

内核中的 `procdir`（procfs 目录）指针被初始化为指向 `procent`（procfs 目录项）结构数组的指针。该数组的大小由启动时建立的 `v.v_proc` 变量得出，该变量表示系统可支持的最大进程数。`procdir` 中的条目维护一个指向进程结构的指针，并维护到数组中下一个条目的链接。`procdir` 数组通过进程 pid 结构中的 `pr_slot` 字段进行索引。`procdir` 槽位从数组中分配给进程，并在进程创建时（`fork()`）初始化，如图 8.16 所示。

![](img/220ae4af07df2fe8e5be69d27f885d1b_351_0.png)

procfs 目录项的具体格式在 procfs 内核代码中有描述。它以典型的磁盘文件系统为模型：内核中的每个目录项由一个目录名、目录内偏移量、长度字段和 inode 编号描述。`/proc` 文件对象的 inode 编号在内部由文件对象类型和进程 PID 推导得出。请注意，`/proc` 目录项不会缓存在目录名查找缓存（`dnlc`）中；按照定义，它们已经位于物理内存中。

由于 procfs 是一种文件系统，它构建在虚拟文件系统（VFS）和 vnode 框架之上。在 Solaris 中，文件系统的一个实例由 vfs 对象描述，其下的每个文件由 vnode 描述。vfs/vnode 架构在第 541 页的“Solaris 文件系统框架”中有描述。Procfs 构建 vfs 和 vnode 结构，这些结构用于引用文件系统操作（如挂载、卸载）的文件系统特定函数，以及 `/proc` 目录和文件对象操作（如打开、读取、写入）的文件系统特定函数。

除 vfs 和 vnode 结构之外，procfs 实现还定义了两种用于描述 `/proc` 文件系统中文件对象的主要数据结构。第一种是 `prnode`，它是链接到 vnode 的文件系统特定数据。正如内核 UFS 实现将 inode 定义为描述 UFS 文件的文件系统特定结构一样，procfs 也定义了 `prnode` 来描述 procfs 文件。`/proc` 目录中的每个文件都有一个 vnode 和 `prnode`。第二种结构 `prcommon` 存在于目录级，用于 `/proc` 的目录文件。也就是说，`/proc/<pid>` 和 `/proc/<pid>/lwp/<lwpid>` 目录各自有一个指向 `prcommon` 结构的链接。`/proc/<pid>` 和 `/proc/<pid>/lwp/<lwpid>` 内部的底层非目录文件对象没有关联的 `prcommon` 结构。原因是 `prcommon` 的功能是同步对与进程或进程中某个 LWP 关联的文件对象的访问。`prcommon` 结构为 procfs 客户端提供了特定目录内底层数据文件的通用文件抽象（见图 8.17）。

![](img/220ae4af07df2fe8e5be69d27f885d1b_352_0.png)

**图 8.17** *procfs 目录层次结构*

关于 `prnode` 和 `prcommon` 结构的定义，请参阅 `/usr/include/sys/proc/prdata.h`。

结构链接在 proc 结构和 LWP 级别维护，它们引用各自的 `/proc` 文件 vnode。每个进程都链接到其主 `/proc` vnode（即表示 `/proc/<pid>` 文件的 vnode），而进程中的每个 LWP 则链接到表示其 `/proc/<pid>/lwp/<lwpid>` 文件的 vnode，如图 8.18 所示。

![](img/220ae4af07df2fe8e5be69d27f885d1b_353_0.png)

**图 8.18** *procfs 数据结构*

图 8.18 部分展示了当 procfs 文件被打开进行读取或写入时，procfs 数据结构及相关链接的样子。注意，与某个进程关联的所有 vnode 都通过 `prnode` 中的 `pr_next` 指针链接在一起。当引用 procfs 目录和底层文件对象时，内核会动态创建必要的结构来满足客户端对文件 I/O 的请求。更简洁地说，procfs 的结构和链接是动态创建和销毁的。它们并不是在进程创建时就建立的（除了 `procdir` procfs 目录项和目录槽分配之外）。它们看起来始终存在，是因为每当发出 `open(2)` 请求或对 procfs 目录或数据文件对象进行查找时，这些文件总是可用的。（这有点像冰箱里的灯——你去看的时候它总是亮着的，但门关着的时候它并不亮。）
