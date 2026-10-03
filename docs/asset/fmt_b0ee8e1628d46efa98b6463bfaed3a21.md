
# 缓冲区块等待队列与进程调度分析

## 进程 A 读取文件并挂起

![](img/f661d64b7eb54840fcb4d65765a4e933_400_0.png)

进程状态

图 7.12 系统为进程 A 打开了文件 hello.txt。

进入 `read()` 函数后的具体执行过程已在第 3.3.1 节中进行了详细描述。代码如下：

```c
//code source:fs/buffer.c:
struct buffer_head * read(int dev, int block) //从硬盘读取数据
{
    if (!(bb = getblk(dev,block)))) //申请一个空闲缓冲区块
        //缓冲区块被锁定并绑定到
        buffer_rw_block (READ,bh); //请求项目，发送磁盘读取指令
        wait_on_buffer(bb); //挂起进程等待解锁
        if (bb->b_uptodate)//缓冲区块已就绪
            return bh;
}
```

进程 A 在 `wait_on_buffer()` 函数中被挂起。代码如下：

```c
//code source:fs/buffer.c
static inline void wait_on(struct buffer_head * bh) //挂起
// 进程等待缓冲区块被解锁，
{
    cli();//关闭中断
    while (bh->b_lock) //检测缓冲区块是否被锁定
        sleep(&bh->b_wait); //挂起等待缓冲区块的
        // 进程），并切换到
        //其他进程
    sti();//开启中断
}
```

## `lr_rw_block()` 执行与 `sleep_on()` 机制

当执行 `lr_rw_block()` 时，缓冲区块已被锁定（如第 3.3.1.1 节所述）。如果 `(bh->b_lock)` 的结果为真，则调用 `sleep_on()` 函数。传递给它的参数是 `&bh->b_wait`，它代表等待缓冲区块解锁的进程的指针。当系统初始化时，所有缓冲区块中的所有 `b_wait` 都被设置为 `NULL`（如第 2.10 节所述）。而该缓冲区块是一个新的应用，从未被其他进程使用过。此时 `bh->b_wait` 的值为 `NULL`。接下来，进程进入以下 `sleep_on()` 函数。

在 `sleep_on()` 函数中参数的作用是：`*p` 指向 `bh->b_wait`。`*p` 存储了进程 A 的指针，这意味着进程 A 正在等待缓冲区块被解锁。

在进程 A 挂起后，调用 `schedule()` 并切换到执行进程 B。同时，硬盘正在将数据传输到数据寄存器端口。这种情况所示：

图 7.13 中代表进程 A 的进度条变为灰色，这意味着进程 A 已挂起。

值得注意的是，代码中的 `tmp` 在进程 A 的内核栈中被存储为 `NULL`。`Bh->b_wait` 存储了进程 A 的指针（图 7.14）。

### 例 1：缓冲区块的进程等待队列

0x00000 0x9FFFF 0xFFFFFF 0x3FFFF 0x5FFFF 0xFFFFFF

![](img/f661d64b7eb54840fcb4d65765a4e933_402_0.png)

进程状态：

- 进程 0
- 进程 A
- 可中断
- 不可中断
- 当前进程

图 7.13 系统读取 hello.txt 中的数据并挂起进程 A。

![](img/f661d64b7eb54840fcb4d65765a4e933_402_1.png)

图 7.14 将进程 A 放入等待队列。

## 进程 B 打开文件并挂起

进程 B 在读取文件后被挂起。进程 B 首先执行语句 `fd = open("/mnt/user/user2/hello.txt", O_RDWR, 0644)`。`open()` 函数最终会被映射到 `sys_open()` 函数并执行。`sys_open()` 函数将在文件管理表 `file_table[64]` 中申请一个空闲条目，以挂载 `file_table[64]` 的空条目以及进程 B 中 `task_struct` 的 `filp`。虽然进程 B 和进程 A 打开的是同一个文件，但这两个进程对文件的操作是互不相关的。因此，需要两套账目（数据结构）。具体代码如下：

```c
//code source:fs/open.c
int sys_open(const char * filename, int flag, int mode)
for(fd = 0; fd<NR_OPEN; fd++)
    if ((current->filp[fd])
        break;
for (i = 0; i<NR_COUNT; i++,fd++)
    if (!current->filp[i])
        current->filp[fd] = f->i_node;      //绑定进程 B 中的 filp[20] 和项目
            // 对应 file_table[64]，并增加文件句柄计数；
            if ((i = inode(filename,flag,mode,inode))>0) //在 hello.txt
                文件中获取 i-node
        f->mode = inode->i_mode;             //使用 i-node 设置文件属性
        f->flags = flag;                      //使用 flag 设置文件操作
        f->fcount = 1;                        //引用计数加 1
        f->i_node = inode;                   //建立 i-node 和文件之间的关系
        f->pos = 0;                           //文件读写指针设置为 0
    return (fd);                         //将文件句柄返回给用户空间
```

绑定的场景如下：磁盘正在读取数据，这意味着进程 A 的读取尚未完成（图 7.15）。`open()` 获取了 hello.txt 中的节点并挂载了 `file_table[64]`。

hello.txt 节点的获取方式与 `wait_on_buffer()` 不同。具体代码所示：

```c
//code source:fs/buffer.c
static inline void wait_on(struct buffer_head * bh) //挂起
// 进程等待缓冲区块被解锁，
{
    cli();//关闭中断
    while (bh->b_lock) //检测缓冲区块是否被锁定
        sleep(&bh->b_wait); //挂起等待缓冲区块的
        // 进程），并切换到
        //其他进程
    sti();//开启中断
}
```
