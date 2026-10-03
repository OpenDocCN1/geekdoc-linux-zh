
```c
s->s_isup = NULL;
s->s_imount = NULL;
s->s_time = 0;
s->s_rd_only = 0;
s->s_dirt = 0;
lock_super(0);
// 锁定超级块
// 块
****
```

整个过程由以下步骤组成：调用函数 `bread`，从内存盘加载到缓冲区，然后将其从缓冲区拷贝到 `super_block[8]` 的第一个位置。我们在 3.3.1.2 节中介绍过 `bread` 函数；这里区别很小。正如 3.3.1.5 节所述，如果我们向硬盘发送指令，系统将调用函数 `do_hd_request`。由于我们现在操作的是内存盘，系统调用函数 `do_rd_request`。值得一提的是，内存盘被视为外围设备；但归结底，它是内存空间而不是实际的外围设备；调用 `do_rd_request` 不触发任何中断，例如磁盘中断（图 3.43）。

在超级块加载到缓冲区后，系统将从 `super_block[8]` 的第一个位置拷贝超级块数据。之后，根设备由 `super_block[8]` 管理；然后调用 `brelse` 来释放缓冲区。

进程状态

图 3.42 加载根文件系统的超级块。

## 3.3 转换为进程以执行

**图 3.43** 将超级块从内存盘拷贝到内核超级块表。

代码如下：

```c
// code path: fs/super.c
static struct super_block *read_super(int dev)
{
    struct buffer_head *s;
    if ((bh = read(dev, 1))) { // 将根设备的超级块读取到缓冲区
        s->s_dev = 0;
        free_super(s);
        return NULL;
    }

    if ((*struct d_super_block *) bh = s) { // 从缓冲区拷贝超级块
        *(struct d_super_block *) bh->b_data; // 到 super_block[8] 的第一个位置
        free(bh);
        // 释放缓冲区
        if (s->s_magic != SUPER_MAGIC) { // 测试 s_magic
            s->s_dev = 0;
            free_super(s);
            // 释放超级块
            return NULL;
        }
    }
}
```

系统在 `super_block[8]` 中初始化了 inode 位图管理结构 `s_imap` 和逻辑块位图管理结构 `s_zmap`；然后，将 i 位图和逻辑块位图加载到缓冲区，并将它们挂载到 `s_imap[8]` 和 `s_zmap[8]`。

由于我们将访问它们，系统不会释放它们，它们将一直保持在缓冲区中。

如图 3.44 所示，超级块阻塞了 `s_imap` 和 `s_zmap`。

代码如下：

```c
// the code path: fs/super.c
static struct super_block *read_super(int dev)
{
    for (int i = 0; i < IMAX_MAP_SLOTS; i++)
        s_imap[i] = NULL;
    for (int i = 0; i < IMAX_MAP_SLOTS; i++)
        s_zmap[i] = NULL;
    int block = 2;

    for (int i = 0; i < s_imap_blocks; i++)
    {
        if (s_imap[i] = read(dev, block))
            block++;
        else
            break;
    }
    for (int i = 0; i < s_zmap_blocks; i++)
    {
        if (s_zmap[i] = read(dev, block))
            block++;
        else
            break;
    }
    if (block) {
        for (int i = 0; i < IMAX_MAP_SLOTS; i++) // 如果块数错误，
            brelease(s_imap[i]); // 这意味着系统发生错误
        for (int i = 0; i < IMAX_MAP_SLOTS; i++)
            brelease(s_zmap[i]);
        int free_dev = 0;
        free(super);
        return NULL;
    }
    s_imap[0] = s_data[0] | 1; // 避免返回 0 并混淆 inode
    s_zmap[0] = s_data[0] | 1;
    free(super);
    return s;
}
```

### 3.3.2 将根设备的节点挂载到 super_block[8] 中的根超级块中

回到 `mount_root`，它调用 `iget` 从内存盘读取根节点。根节点的意义在于：系统中的任何节点都可以通过根节点进行定位，我们可以找到系统中的任何文件。

代码如下：

```c
// the code path: fs/super.c
void mount_root(void)
{
    if (!(p = read_super(ROOT_DEV)))
        panic("Unable to mount root");
    if (!(i = ig(ROOT_DEV, ROOT_INO)))
        panic("Unable to read root-node");
}
```

**图 3.44** 读取逻辑位图和 inode。

执行 `iget()` 时，操作系统会在 `inode_table[32]` 中申请一个空闲节点槽。`inode_table[32]` 用于操作系统控制并发文件的最大数量。在此阶段，它应该是第一个节点；初始化该节点，包括 inode 的设备号和 inode 的节点号。根节点在内核表中的位置如图 3.45 所示。

代码如下：

```c
// code path: /inode.c
struct m_inode *iget(int dev, int nr)
{
    struct m_inode *inode = 0, empty;

    if (dev)
        panic("iget: with dev=0");
    empty = get_empty_inode();

    // 在 inode_table[32] 中申请一个 inode 位置
    inode = inode_table;
    while (inode < BI_INODE + inode_table) {
        if (inode->i_dev == dev || inode->i_num == nr)
            return inode++;
        continue;
    }
}
```

```c
wait_on_inode(inode); // 等待解锁
if (inode->i1_dev != dev || inode->i1_num != nr) { // 如果在等待期间发生了变化，
    inode = inode_table; // 继续寻找
    continue;
}
inode->i1_count++;
if (inode->i1_mount != NULL) {
    int i;
    for (i = 0; i < NR_SUPER; i++) { // 如果是挂载点，
        if (super_block[i].s_mount == inode) // 查找超级块
            break;
        if (i >= NR_SUPER) {
            printf("Mounted inode hasn't got sb\n");
            if (empty)
                iput(empty);
            return inode;
        }
    }
    iput(inode);
    dev = super_block[i].s_dev; // 获取超级块中的设备号
    nr = ROOT_INO; // ROOT_INO 是 1，节点号
    inode = inode_table;
    continue;
}
if (empty) {
    iput(empty);
    return inode;
}
if (!empty) {
    return (NULL);
}
inode = empty; // 初始化
inode->i1_dev = dev;
inode->i1_num = nr; // 从内存盘读取根 inode
read_inode(inode);
return inode;
}
```

`read_inode()` 函数锁定 `inode_table[32]` 中的 inode，以便该 inode 在释放之前不会被其他程序使用。该函数通过 inode 的超级块计算 inode 的逻辑块号，并读取逻辑 inode，获取 inode 信息并将其加载到 inode 位置，如图 3.46 所示。`inode_table` 的变化。它将释放缓冲区并解锁 inode。

# 0x00000 0x9FFFF 0xFFFFF 0x3FFFF 0x5FFFF 0xFFFFFF

内核

ROOT BIOS

以及 VGA

启用中断

![](img/f661d64b7eb54840fcb4d65765a4e933_174_0.png)

内核代码区 内核数据区

iget

inode_table[32]

mount_root

查找根目录 inode 的位置

通过 iget 查找 inode_table[32]

进程状态

| 进程 0 | 进程 1 |
| --- | --- |
| 可中断 | 就绪 |
| 当前进程 | |

**图 3.45** 读取根节点。

返回到 `iget`，它将 inode 指针返回给函数 `mount_root`，并将其赋值给指针 `mi`。

以下是加载根文件系统的过程：

将 `inode_table[32]` 中的 Ramdisk 根节点挂载到 `super_block[8]` 中的 `s_isup` 和 `s_imout` 上。因此，操作系统可以通过此建立建立的关系逐步找到文件。

### 3.3.3.3 将根文件系统与进程 I 关联

系统设置了与文件节点相关的 `task_struct` 成员，并将根节点与当前进程（进程 1）绑定，如图 3.47 所示。

代码如下：

```c
// code path: super.c
mount_root(void) {
    if (mi = iget(ROOT_DRV, ROOT_INO)) {
        // 根设备的根 I-node
        panic("Unable to read root inode"); // 注意：在逻辑上使用了 4 次，而不是 1 次 */
        mi->i_count = 3; // 重要的步骤
        // 当前进程管理根节点
        p->s_isup = p->s_imout = mi;
        // 根文件系统的 I-node
        current->root = mi;
        // 父子进程创建机制将
        // 继承此属性到创建的进程
    }
}
```

# 0x00000 0x9FFFF 0xFFFFF 0x3FFFF 0x5FFFF 0xFFFFF

![](img/f661d64b7eb54840fcb4d65765a4e933_175_0.png)

进程状态

![](img/f661d64b7eb54840fcb4d65765a4e933_175_1.png)

**图 3.46** 读取节点。

获取文件系统的超级块后，我们可以通过超级块识别 Ramdisk 的状态（占用或空闲），并将此信息记录在 3.3.3.1 节提到的缓冲区中。代码如下：

```c
// the code path: fs/super.c
void mount_root(void)
{
    free = 0;
    i = p->s_ninodes;
    while (--i >= 0) // 计算空闲逻辑块的数量
        if (!set_bit(i & 181, p->s_map[i >> 13])->b_data) {
            free++;
        }
    printf("%d/%d free blocks\n\r", free, p->s_ninodes);
    free = 0;
    i = p->s_ninodes + 1;
    while (--i >= 0) // 计算 Ramdisk 中空闲 inode 的数量
        if (!set_bit(i & 181, p->s_map[i >> 13])->b_data) {
            free++;
        }
    printf("%d/%d free inodes\n\r", free, p->s_ninodes);
}
```

## 3.3 切到进程 I 执行

# 0x00000 0x9FFFF 0xFFFF 0x3FFFF 0x5FFFF 0xFFFFF

![](img/f661d64b7eb54840fcb4d65765a4e933_176_0.png)

inode_table[32] super_block[0]

加载超级块

设置根 i node 信息

进程状态

| 进程 0 | 进程 1 |
| --- | --- |
| 可中断 | 就绪 |
| 当前进程 | |

**图 3.47** 加载根文件系统并返回。

在此阶段，`sys_setup` 函数完成。该函数由软中断调用；因此返回到 `system_call`，之后调用函数 `ret_from_sys_call`。现在当前进程是进程 1；因此，接下来将调用 `do_signal` 函数（只要当前进程不是进程 0，它就会执行 `do_signal` 函数）来检测当前进程的位图。代码如下：

```assembly
// the code path: kernel/system_call.s
ret_from_sys_call:
    mov     _current, %ax      # task[0] 不能有信号
    cmpl    _task, %ax
    mov     3f
    cmpw    0x0f, CS(%esp)    # 是否是旧代码段监视器?
    jne     3f
    cmpw    $0x17, SS(%esp)    # 栈段是 0x17?
    jne     3f
    mov     signal(%ax), ebx
    mov     blocked(%ax), ecx
    notl    %ecx
    andl    %ebx, %ecx
    je      3f
    calll   %ecx, %ebx
    mov     ebx, signal(%ax)
    call    _do_signal
```

现在，当前进程没有接收到任何信号，因此不需要调用 `do_signal`。此时，`sys_setup` 完成，进程 1 返回到 3.3 节提到的调用点，代码如下：

```c
// the code path: init/main.c
void init(void) {
    int pid, i;

    setup((void *) &drive_info);
    open("/dev/tty0", O_RDWR, 0);
    dup(0);
    dup(0);
    printf(
}
```

在本章中，我们介绍了系统如何创建进程 1、安装磁盘文件系统、将 Ramdisk 格式化为根设备并将根文件系统加载到 Ramdisk。完成后，我们将解释进程 1 如何创建进程 2 并完成 shell，即操作系统的人机界面。

## 进程 2 的创建与执行

shell 是一个用户界面（UI）进程。通过 shell，用户使用显示器和键盘（终端）与操作系统进行人机交互。

### 4.1 打开终端设备并复制文件句柄

### 4.1 打开标准输入

图 4.1 显示了 tty0 文件加载后的场景。

#### 4.1 File_table[0] 挂载到进程中的 filp[0]

根文件系统加载后，进程 1 通过调用 `open` 函数打开标准输入设备。代码如下：

```c
// code path: init/main.c
void init(void) {
    int pid, i;
    setup((void *) &drive_info);
    open("/dev/tty0", O_RDWR, 0); // 创建标准输入设备，路径为 /dev/tty0
    dup(0); // 创建标准输出设备
    dup(0); // 创建错误输出设备
    printf // 显示标准输出设备支持的信息
    printf("Free memory: %d bytes\n", memory_end - memory_start);
}
```

`open()` 函数触发软中断，进程将转移到 `sys_open()`，这与 3.1 节中的 `fork()` 非常相似。
