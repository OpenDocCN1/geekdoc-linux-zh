
```c
if (dir_i->mount) {
    put(dir_i);
    return -EPERM;
}
sb->s_mount = dir_i;

dir_i->i_mount = 1;
dir_i->i_dir = 1;

/* NOTE: we don't put(dir_i) */
return 0;
} /* we that in umount */
```
//determine the inode of mnt is not installed
//with other file system
//mount dir_i in root file system with
//s_mount in super block
//mark dir_i indicate that inode has been
//mounted with file system
//mark dir_i indicate that the information
//of inode has been modified

我们将通过 5.2 和 5.8 节中的三个文件操作示例来解释文件系统是如何工作的。

- 示例 1：用户进程在硬盘上打开文件并读取内容。
- 示例 2：用户进程在硬盘上创建一个新文件并写入内容。
- 示例 3：用户进程关闭并删除文件。

## 示例 1：用户进程打开硬盘上存在的文件并读取内容

此示例分为部分：打开文件和读取文件。代码如下：

```c
void main() {
    //open file
    char buffer[12000];
    int fd = open("/mnt/user/user1/hello.txt", O_RDWR, 0644);
    //read out file
    int size = read(fd, buffer, sizeof(buffer));
    return;
}
```

## 5.2 打开文件

打开文件的第一步是找到进程正在操作哪个文件。查找过程分为两个阶段：

- 用户进程 `task_struct` 中的 `filp[20]` 与内核中的 `file_table[64]` 绑定。
- 用户进程打开的文件对应的节点注册在 `file_table[64]` 中。

操作系统根据用户进程的需求访问文件。内核可以通过 `filp[20]` 多次或一次控制打开文件的过程。一旦打开一个文件或另一个文件，`filp[20]` 中的某项会被占用以存储指针（例如，如果用户两次打开 "hello.txt" 文件，则 `filp[20]` 中的两个项会被占用）。因此，在一个进程中，同时打开的文件总数不能超过 20。

在操作系统中，`file_table[64]` 是管理所有打开进程的数据结构。它记录了以下信息：不同的进程打开不同的文件，不同的进程打开同一个文件，以及同一个进程多次打开不同的文件。类似于 `filp[20]`，一旦文件被打开，就会记录在 `file_table[64]` 中。

![](img/f661d64b7eb54840fcb4d65765a4e933_251_0.png)

图 5.2 打开文件的概览。

此过程包含三个步骤。

步骤 1：将用户进程的 `task_struct` 中的 `filp[20]` 与内核中的 `file_table[64]` 绑定。

步骤 2：使用用户提供的目录名 "/mnt/user/user1/user2/hello.txt" 作为线索来打开文件 "hello.txt" 的节点。

步骤 3：对应于 hello.txt 的 i node 被注册在 `file_table[64]` 中。

调用 `function()` 函数完成打开文件的任务。该函数最终映射到 `sys_open()`。第 4.4.1 节介绍了 `sys_open()` 的映射过程及其基本实现。我们将解释 `sys_open()` 的实现细节并分析其设计。

## 5.2.1 将用户进程中的 `filp[20]` 绑定到 `file_table[64]`

在 `sys_open()` 中，将 `filp[20]` 与 `file_table[64]` 绑定的代码如下：

```c
#include <linux/fs.h>

#define NR_OPEN 256
#define NR_FILE 64

struct file {
    unsigned short f_mode;     // 文件操作模式
    unsigned short f_flags;    // 文件打开或控制的标志位
    unsigned short f_count;    // 文件句柄数量
    struct inode *f_inode;     // 指向对应文件的 inode
    off_t f_pos;               // 文件位置（读取和偏移量）
}; // 进程打开的最大文件数
// 操作系统打开的最大挂的文件数
```

```c
#include <linux/sched.h>

struct file *filp[NR_OPEN]; // 用于管理文件的指针数组
```

```c
#include <fs/file_table.c>

struct file *file_table[NR_FILE]; // 记录操作系统已打开的控制信息
// files
```

```c
#include <fs/open.c>

int sys_open(const char *filename, int flag, int mode) {
    struct inode *inode;
    struct file *file;
    int fd;

    inode = 0777 & ~current->umask; // 设置模式为用户可用
    for (fd = 0; fd < NR_OPEN; fd++) // 在当前进程的 filp[20] 中查找空项
        if (!current->filp[fd]) // 检查结构 filp[20] 是否超出限制或已空
            break;
    if (fd >= NR_OPEN)
        return -EINVAL;

    current->close_exec_ &= (1 << fd); // 设置标志为 0（将在第 6 章解释）
    f = file_table[fd];
    for (i = 0; i < f; i++) // 在 file_table[64] 中查找空项
        if (!f->count) break; // 检查 file_table[64] 是否超出限制或
    if (i >= NR_FILE) // 不（最大值为 64）
        return -EINVAL;
    (current->filp[fd] = f)->count++; // 将当前进程的 filp[20] 与 file_table[64] 中的对应项绑定，并增加文件句柄的挂载计数
    //handle
}
```

为了完成该任务，会分别在 `filp[20]` 和 `file_table[64]` 中查找空项。系统将当前进程中的 `filp[20]` 与 `file_table[64]` 中的对应项绑定，并增加 `file_table[64]` 中对应项的文件句柄挂载计数（注意，这种操作是复杂的，且无法预估许多文件的情况。例如，并不总能找到 `filp[20]` 和 `file_table[64]` 的空项。这意味着当使用两个数据结构限制时，会给出错误）。

### 5.2.2 获取文件名

本节分析路径 `/mnt/user/user2/hello.txt` 以查找 hello.txt 的节点。与 4.1 节引入的 i_node 查找方法的区别在于，hello.txt 文件存储在磁盘中，搜索过程将从根节点在磁盘中查找文件。从图 5.3 所示，解析过程显而易见，流程如下：

- 查找目录目
- 查找目录目 → 查找目录 i 号
- 查找目录目 → 查找目录 i 号

最终找到 hello.txt 文件。

### 5.2.3 获取目录文件的 i_node

程序调用获取 i_node 的过程如图 5.4 所示。图 5.3 解析路径的过程。

## 5.3 文件操作

获取目录文件 i node 的目标通过调用 `open_namei()` 实现。代码如下：

```c
//路径名:fs/open.c:
int sys_open(const char *filename, int flag, int mode) {
    if ((i = open_namei(filename, &inode)) < 0) {
        current->filp[fd] = NULL;
        f->count = 0;
        return i;
    }
}
```

`open_namei()` 根据用户请求设置打开文件的 flag 和 mode。代码如下：

## 5.4 打开文件

//路径名:include/fcntl.h; 进制形式：

```c
#define O_ACCMODE      0003  // 文件访问掩码
#define O_RDONLY       0000  // 只读标志
#define O_WRONLY       0001  // 只写标志
#define O_RDWR         0002  // 读写标志
#define O_CREAT        0020  // 创建新文件标志
#define O_EXCL         /*fcntl */  // 独占标志
#define O_NOCTTY       0400  /*fcntl */  // 无终端控制标志
#define O_TRUNC        0100  /*fcntl */  // 截断标志
#define O_APPEND       0200  // 追加标志
#define O_NONBLOCK     0400  /*fcntl */  // 非阻塞标志
#define O_NODELAY_NONBLOCK
```

//路径名:include/fcntl.h; 二进制格式：（设置 flag 的规则）

```c
#define O_ACCMODE      0000 0000 0011
#define O_RDONLY       0000 0000 0000
#define O_WRONLY       0000 0000 0001
#define O_RDWR         0000 0000 0011
#define O_CREAT        0000 0000 0100 /*fcntl */
#define O_EXCL         0000 1000 0000 /*fcntl */
#define O_NOCTTY       0000 0001 0000 /*fcntl */
#define O_TRUNC        0000 0010 0000 /*fcntl */
#define O_APPEND       0000 0100 0000
#define O_NONBLOCK     0000 1000 0000 /*fcntl */
#define O_NODELAY_NONBLOCK
```

//路径名:fs/name.c; const char *pathname, int flag, mode;

```c
int open(const char *pathname, int flag, int mode) {
    struct m_inode *res_inode; // pathname=/mnt/user/user1/user2/hello.txt
    const char *basename; // basename=
    int fd;
    struct m_inode *inode *di;
    struct buffer_head *bh;
    struct dir_entry *de;
    inode = 0777 & ~current->umask; // 设置模式为用户可用
    for (fd = 0; fd < NR_OPEN; fd++) // 在当前进程的 filp[20] 中查找空项
        if (!current->filp[fd]) // 检查结构 filp[20] 是否超出限制或已空
            break;
    if (fd >= NR_OPEN)
        return -EINVAL;
    current->close_exec_ &= (1 << fd); // 设置标志为 0（将在第 6 章解释）
    f = file_table[fd];
    for (i = 0; i < f; i++) // 在 file_table[64] 中查找空项
        if (!f->count) break; // 检查 file_table[64] 是否超出限制或
    if (i >= NR_FILE) // 不（最大值为 64）
        return -EINVAL;
    (current->filp[fd] = f)->count++; // 将当前进程的 filp[20] 与 file_table[64] 中的对应项绑定，并增加文件句柄的挂载计数
}
```

为了完成该任务，会分别在 `filp[20]` 和 `file_table[64]` 中查找空项。系统将当前进程中的 `filp[20]` 与 `file_table[64]` 中的对应项绑定，并增加 `file_table[64]` 中对应项的文件句柄挂载计数（注意，这种操作是复杂的，且无法预估许多文件的情况。例如，并不总能找到 `filp[20]` 和 `file_table[64]` 的空项。这意味着当使用两个数据结构限制时，会给出错误）。

```c
if ((de = find_entry(inode, thisname, name))) // (通过节点获取目录项
    iput(inode);
    // 如果未找到目录项，则释放 inode
    return NULL;
}
inr = de->inode; // 从目录项获取节点号
didev = inode->i_dev; // 从 inode 获取设备号
brel(bh);
iput(inode);
// 使用后释放每个目录文件的所有节点
// 以避免浪费 inode_table 中的空间
if ((inode = iget(dev, inr))) {
    return NULL;
}
getinode;
```

`find_entry()` 的主要任务如下：首先，函数通过 inode 确定目录文件中的目录项。然后，从对应目录文件的第一个逻辑块开始，将逻辑块持续从外设加载到缓冲区中，函数持续搜索指定的目录直到找到目标为止。

代码如下：

```c
//path:include/linux/fs.h
#define BLOCK_SIZE 1024
//path names/name.h
static struct buffer_head *find_entry(struct inode m_inode ** dir,
    const char *name, int namelen, struct dir_entry ** res_dir)
// 获取 name 的目录项
{
    int entries;
    int block;
    struct buffer_head *bh;
    struct dir_entry *de;
    struct super_block *sb;

#ifdef NO_TRUNCATE
    if (namelen > NAME_LEN) // 在 NO_TRUNCATE 的前提下，如果长度超过 14 则返回 "NULL"
        return NULL;
#else
    if (namelen > NAME_LEN) // 或者截断文件名长度
        name = NAME_LEN;
#endif
    entries = (*dir)->i_size / sizeof(struct dir_entry);
    // 根据文件长度信息（即 i_size）计算目录项的数量
    *res_dir = NULL;
    if (!inode)) // 文件名长度为 0 或不存在
        return NULL;
    // 检查 '.'，因为我们可能需要对它进行某些“特殊处理”
    if (name && get_fs_byte(name) == '.' && get_fs_byte(name + 1) == '.')
        // 处理目录项为 .. 的情况
```

```c
    if ((block = (*dir)->i_block[0]))
        // 确定目录文件的第一个逻辑块是否
        return NULL;
    if ((bh = read((dir)->i_dev, block))) // 将逻辑块读入指定的缓冲区
        return NULL;
    i = 0;
    de = (struct dir_entry *)bh->b_data; // 指向缓冲区的头部
    while (i < entries) { // 在所有目录项中搜索 name
        if (strcmp(de->name, name) == 0) goto BLOCK_SIZE - b_data;
        // 在逻辑块中未找到指定的目录项
        brel(bh);
        bb = NULL;
    }
```

```c
    // 然后在将下一个逻辑块读入缓冲区后，继续搜索 mnt 目录文件
    if ((block = map(dir, DIR_ENTRIES_PER_BLOCK)) ||
        (hb = head(*dir->ai_dev->block))) {
        i += DIR_ENTRIES_PER_BLOCK;
        continue;
    }
    de = (struct dir_entry *)hb->b_data;
    if (match(name, name, de)) // (匹配目录项
        *res_dir = de; // 如果找到 mnt，将其传递给 *res_dir
        return bh;

    de++;
    ni++;
    brelease(bh);
    return NULL; // 如果检查完所有目录文件后未找到 mnt 则返回 NULL
}
```
