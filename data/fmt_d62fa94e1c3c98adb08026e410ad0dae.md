
`sys_close()` 关闭文件描述符 `fd`。任何现有文件锁（`i_flock`）会被删除并执行释放。`sys_mkdir()` 在检查权限后，通过 `inode` 操作 `mkdir()` 创建目录 `file_name`。`sys_mkknod` 创建伪文件，`mode` 指定要创建的伪文件的类型和访问权限。对于设备文件，`dev` 设备号。允许所有用户创建 FIFO。对于所有其他类型，都需要用户权限。

## 实现

所有系统调用都通过 `syscall` 宏工作。在 Alpha 机器上没有 `sys_create0` 函数。系统调用 `mkfifo` 在 C 库中是通过 `mknod()` 实现的：

```c
int mkfifo(const char path, mode_t Mode) {

    return mknod (path, mode | S_IFIFO, 0);

}
```

## 错误

`ENFILE` - 如果打开的文件过多。`EACCES` - 如果该目录没有执行权限。

`ENFILE` - 如果系统或进程没有可用的空文件描述符。这两个值都定义在 `<linux/fs.h>` 中。

`EEXIST` - 要创建的文件已经作为目录存在。`EISDIR` - 如果要打开的目录无法读取，或者 `sys_open` 设置了 `O_CREATE` 或 `O_TRUNC` 标志。

`ENOENT` - 如果路径无效。`EPERM` - 如果文件的索引节点（inode）不允许请求的操作。

| 系统调用 | pipe | POSIX |

`File: arch/i386/kernel/sys_i386.c`

```c
int sys_pipe(unsigned long *fildes);
```

`sys_pipe()` 创建两个描述符并将它们写入由 `fildes` 指向的字段中。如果进程有两个空闲描述符，则 `fildes[0]` 用于读操作，`fildes[1]` 用于写操作。

## 实现

该系统调用通过 `syscall` 宏进行转换。由于其他架构使用栈寄存器作为内核函数的参数参数，因此它已被移动到体系相关的目录。

## 错误

`EMFILE` - 如果系统中没有空闲描述符。`ENFILE` - 如果进程没有空闲描述符。`EINVAL` - 如果 `fd` 无效。

| 系统调用 | quotactl | LINUX |

`File: kernel/sched.c`

```c
#include <linux/sys.h>
#include <linux/quota.h>
```

`int sys_quotactl(int cmddo, char *special, int Id, caddr_t addr);`

此内核函数代表配额程序的入口。目前，仅考虑了磁盘配额；对于进程配额，使用 `rlimits` 可能是最合适的方法。配额如下：

```c
struct dquote { /* 对应的 ID (uid, gid) */

    unsigned int dq_id_d;      /* 类型 */

    short dq_type;            /* 设备 */

    kdev_t dq_dev;           /* 标志 */

    short dq_flags;          /* 引用计数 */

    short dq_count;          /* VFS 挂载点 */

    struct vfsmount *dq_mnt;

    struct dqublk *dq_dqb;   /* 使用情况 */

    struct wait_queue *dq_wait; /* 等待配额变化的

                            /* 进程 */

    struct dquote *dq_cprev;

    struct dquote *dq_next;

    struct dquote *hash_prev;

    struct dquote *hash_next;

};

struct dqublk {

    u32 dq_hardlimit;      /* 可用块硬限制 */

    u32 dq_softlimit;      /* 可用块软限制 */

    u32 dq_curblocks;      /* 当前块数 */

    u32 dq_ihardlimit;     /* 可用索引节点硬限制 */

    u32 dq_isoftlimit;     /* 索引节点软限制 */

    u32 dq_curinodes;      /* 当前索引节点数 */

    time_t dq_dbtime;       /* 软限制

                            /* 超额（块） */

    time_t dq_dtime;        /* 软限制

                            /* 超额（索引节点） */

};
```
