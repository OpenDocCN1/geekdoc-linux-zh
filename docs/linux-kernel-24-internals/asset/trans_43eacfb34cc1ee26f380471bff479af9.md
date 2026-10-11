

挂载时有效的根 inode！

- 5. 然后我们初始化 `s->s_op`，这意味着从这一点开始，我们可以调用 `iget()` 来访问 inode 缓存，这将导致调用 `s_op->read_inode()`。该操作会找到包含指定（由 `inode->i_ino` 和 `inode->i_dev` 指定）inode 的块并将其读入。如果我们无法获取根 inode，则释放 inode 位图并将超级块缓冲区交还给缓冲区缓存，然后返回 `NULL`。如果成功读取了根 inode，则分配一个名为 `/`（因为这是根）的 dentry，并用该 inode 对其进行实例化。
- 6. 现在，我们遍历文件系统上的所有 inode 并将它们全部读入，以设置内部 inode 位图中相应的位，并计算其他一些内部参数，例如最后一个 inode 的偏移量以及最后一个文件的起始/结束块。我们读取的每个 inode 都会通过 `iput()` 交还给 inode 缓存——我们不会比需要的时间更长时间地持有其引用。
- 7. 如果文件系统不是以只读方式挂载的，我们将超级块缓冲区标记为脏，并设置 `s->s_dirty` 标志（TODO：我为什么要这样做？最初，我这样做是因为 `minix_read_super()` 这样做，但 minix 和 BFS 似乎都没有在 `read_super()` 中修改超级块）。
- 8. 一切顺利，所以我们向 VFS 级别的调用者（即 `fs/super.c:read_super()`）返回这个已初始化的超级块。

当 `read_super()` 函数成功返回后，VFS 通过调用 `fs/super.c:get_sb_bdev()` 中的 `get_filesystem(fs_type)` 获得文件系统模块的引用，以及块设备的引用。

现在，让我们看看在文件系统进行 I/O 时会发生什么。我们已经检查了在调用 `iget()` 时 inode 是如何被读取的，以及在调用 `iput()` 时它们是如何被释放的。读取 inode 会设置（除其他内容外）`inode->i_op` 和 `inode->i_fop`；打开文件会将 `inode->i_fop` 传播到 `file->f_op`。

让我们检查 `link(2)` 系统调用的代码路径。系统调用的实现位于 `fs/namei.c:sys_link()` 中：

- 1. 用户空间的名称通过 `getname()` 函数复制到内核空间，该函数还执行错误检查。
- 2. 使用与 dcache 交互的 `path_init()/path_walk()` 将这些名称转换为 nameidata。结果存储在 `old_nd` 和 `nd` 结构中。
- 3. 如果 `old_nd.mnt != nd.mnt`，则返回 "cross-device link" EXDEV 错误——不能在不同文件系统之间创建链接，在 Linux 中这意味着不能在不同挂载的文件系统实例（或特定地，不同文件系统）之间创建链接。
- 4. 通过 `lookup_create()` 创建对应于 `nd` 的新 dentry。
- 5. 调用通用的 `vfs_link()` 函数，该函数检查我们是否可以在目录中创建新条目，并调用 `dir->i_op->link()` 方法，这将我们带回到文件系统特定的 `fs/bfs/dir.c:bfs_link()` 函数。
- 6. 在 `bfs_link()` 内部，我们检查是否试图链接目录，如果是，则以 EPERM 错误拒绝。这与标准（ext2）的行为相同。
- 7. 我们通过调用辅助函数 `bfs_add_entry()` 尝试将新的目录项添加到指定目录中，该函数遍历所有条目以查找未使用的槽位（`de->ino == 0`），并在找到时，将名称/inode 对写入对应的块并将其标记为脏（以非超级块优先级）。
- 8. 如果我们成功添加了目录项，则操作没有失败的方式，因此我们递增 `inode->i_nlink`，更新 `inode->i_ctime`，并将此 inode 标记为脏，同时用该 inode 实例化新的 dentry。

其他相关的 inode 操作如 `unlink() / rename()` 等以类似的方式工作，因此详细检查它们并没有太大收获。

## 3.8 执行域和二进制定位

Linux 支持从磁盘加载用户应用程序二进制文件。更有趣的是，这些二进制文件可以存储在不同的格式中，并且操作系统通过系统调用对程序的响应可以根据需要偏离常规（常规是指 Linux 的行为），以模拟其他 UNIX 变体（COFF 等）中发现的格式，同时也模拟其他变体（Solaris, UnixWare 等）的系统调用行为。这就是执行域和二进制定位格式的作用所在。

每个 Linux 任务都在其 `task_struct (p->personality)` 中存储了一个 personality（个性/人格）。当前存在的（在内核官方中或作为附加补丁） personalities 包括对 FreeBSD、Solaris、UnixWare、OpenServer 以及其他许多流行操作系统的支持。`current->personality` 的值分为两部分：

- 1. 高三个字节 – bug 模拟：`STICKY_TIMEOUTS`、`WHOLE_SECONDS` 等
- 2. 低字节 – 真正的 personality，一个唯一的编号。

通过更改 personality，我们可以改变操作系统处理某些系统调用的方式，例如，向 `current->personality` 添加 `STICKY_TIMEOUT` 会使 `select(2)` 系统调用保留最后一个参数（timeout）的值，而不是存储未睡眠的时间。某些有缺陷的程序依赖于有缺陷的操作系统（非 Linux），因此 Linux 提供了一种方法来模拟 bug，在源代码不可用因此无法修复 bug 的情况下。

执行域是由单个模块实现的一组连续的 personality 范围。通常，单个执行域实现单个 personality，但有时也可以在单个模块中实现“接近”的 personality，而无需太多的条件判断。

执行域在 `kernel/exec_domain.c` 中实现，与 2.2.x 相比，在 2.4 内核中进行了完全重写。通过读取 `/proc/execdomains` 文件，可以查看内核当前支持的执行域列表以及它们支持的 personality 范围。除了 `PER_LINUX` 之外，执行域可以作为动态加载模块实现。

用户界面通过 `personality(2)` 系统调用，它设置当前进程的 personality，或者如果参数设置为不可能的 personality `0xffffffff`，则返回 `current->personality` 的值。显然，该系统调用本身的行为不依赖于 personality。

内核接口用于执行域注册，由两个函数组成：

- `int register_exec_domain(struct exec_domain *);` 通过将其链接到单链表 `exec_domains` 来注册执行域，并在读写自旋锁 `exec_domains_lock` 的写保护下进行操作。成功返回 `0`，失败返回 `non-zero`。
- `int unregister_exec_domain(struct exec_domain *);` 通过将其从 `exec_domains` 列表中解除链接来注销执行域，再次使用写模式的 `exec_domains_lock` 自旋锁。成功返回 `0`。

`exec_domains_lock` 是读-写自旋锁的原因是，只有注册和注销请求会修改列表，而执行 `cat /proc/filesystems` 会调用 `fs/exec_domain.c::get_exec_domain_list()`，这只需要对列表进行读访问。

注册新的执行域定义了“lcall7 处理器”和一个信号编号转换映射。实际上，ABI 补丁将此执行域概念扩展以包含额外信息（如 socket 选项、socket 类型、地址族和 errno 映射）。

二进制定位格式以类似的方式实现，即在 `fs/exec.c` 中定义一个单链表 formats，并由读-写锁 `binfmt_lock` 保护。与 `exec_domains_lock` 一样，`binfmt_lock` 在大多数情况下以读模式获取，除了二进制格式的注册/注销外。注册新的二进制定位格式增强了 `execve(2)` 系统调用，增加了新的 `load_binary()` / `load_shlib()` 函数以及 core_dump() 的能力。`load_shlib()` 方法仅由旧的 `usrleib` 系统调用使用，而 `load_binary()` 方法由 `do_execve()` 中的 `search_binary_handler()` 调用，后者实现了 `execve(2)` 系统调用。

进程的 personality 在加载二进制定位格式时由相应格式的 `load_binary()` 方法通过一些启发式方法确定。例如，为了确定 UnixWare7 二进制文件，首先使用 `elfmark(1)` 实用工具标记二进制文件，该工具将 ELF 头的 `e_flags` 设置为魔术值 0x314B4455，这在 ELF 加载时会被检测到，并将 `current->personality` 设置为 `PER_UW7`。如果此启发式方法失败，则使用更通用的方法，例如将 ELF 解释器路径视为 `/usr/lib/ld.so.1` 或 `/usr/lib/libc.so.1` 以指示 SVR4 二进制文件，并将 personality 设置为 `PER_SVR4`。可以编写一个小实用工具，利用 Linux 的 `prace(2)` 能力单步执行代码，强制运行中的程序进入任何 personality。

一旦知道 personality（因此也知道了 `current->exec_domain`），系统调用将按以下方式处理。让我们假设一个进程通过 lcall7 门指令进行系统调用。由于在 `arch/i386/kernel/traps.c:trap_init()` 中进行了准备，这将控制权转移到 `arch/i386/kernel/entry.S` 中的 `ENTRY (lcall7)`。在适当的栈布局转换后，`entry.S:lcall7` 从 `current` 获取 `exec_domain` 的指针，然后获取 `exec_domain` 中 lcall7 处理器的偏移量（这在汇编代码中硬编码为 4，因此你不能在 `struct exec_domain` 的 C 声明中移动 handler 字段）并跳转到它。因此，在 C 中，它看起来像这样：

```c
static void UW7_lcall7(int segment, struct pt_regs * regs)
{
    abI_dispatch(regs, &uw7_funcs[regs->eax & 0xff], 1);
}
```

其中 `abi_dispatch()` 是实现此 personality 的系统调用 `uw7_funcs` 的函数指针表的包装器。

## 4. Linux 页缓存

在本章中，我们描述 Linux 2.4 的页缓存。页缓存——顾名思义——是物理页面的缓存。在 UNIX 世界中，页缓存的概念随着 SVR4 UNIX 的引入而变得流行，它取代了用于数据 IO 操作的缓冲区缓存。

虽然 SVR4 页缓存仅用于文件系统数据缓存，因此使用 struct vnode 和文件中的偏移量作为哈希参数，但 Linux 页缓存旨在更通用，因此使用

