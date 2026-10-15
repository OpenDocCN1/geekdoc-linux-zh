
## Linux 内核内部 - 370 -

时间限制有其含义。通常，在查询时，限制的过期时间是以秒为单位提供的。限制通过设备的 `vfsmount` 结构设置。该值用于更新限制（新过期时间 = 当前时间 + 间隔）。

此外，以下结构用于管理：

```c
struct dqsstats {
    u32 drops;         /* 读取的配额数 */
    u32 reads;         /* 写入的配额数 */
    u32 writes;        /* 占据页数 */
    u32 cache_hits;    /* 使用的配额 */
    u32 allocated_quots; /* 分配的配额 */
    u32 free_quots;    /* 空闲配额 */
    u32 syncs;         /* 同步操作数 */
};
```

`cmddo` 参数包含调用的命令和类型。可以通过 `QCMD(cmd, type)` 宏进行解析。函数再次解析 `cmddo`。如果没有给出 `cmd`，后三个参数具有以下含义（另有规定）：

- `special` - 所需设备类型 - `id` 是 `UID`、`GID` 还是 `dq_mnt` 数组的索引。
- `Id` - 配额所指的 ID。

以下值是允许的命令：

- `Q_GETQUOTA` - 提供配额及其当前使用情况。非特权进程只能调用自己的配额。
- `QSYNC` - 执行配额列表的同步。
- `Q_GETSTATS` - `addr` 是指向 `dqsstats` 结构的指针。然而，只输入已用和空闲配额。
- `Q_QUOTA` - 启用配额。`addr` 持文件名，类型作为 `mnt_quota` 数组的索引。
- `Q_QUOTAOFF` - 关闭配额。当 `type=-1` 时，所有 `mnt_quotas`。

该函数读取多个条目，只要它们的大小之和（通过当前名称的偏移量及其长度计算）不超过 `count` 值。返回值为 `count` 与实际读取的条目大小之间的差。

## Implementation

库函数 `readdir` 使用了这两个系统调用。当没有 `sys_getdents()` 可用时，调用旧的 `sys_readdir()` 调用。两个内核函数都通过 0x80 中断直接跳转到其中一个。

## Errors

- `EBADF` - 如果 `fd` 无效。
- `ENOTDIR` - 如果不存在 `sys_readdir()` 文件操作。

![](img/04698aadad5d50fd4b3564ae373ff0bd_373_0.png)

### File: `fs/stat.c`

```c
int sys_readlink(const char *path, char *buf, int bufsize);
```

`sys_readlink()` 函数读取符号链接指向的路径。相应的 `inode` 操作将向缓冲区 `buf` 中存储最多 `bufsize` 个字符。`buf` 末尾不会添加空字节。然而，该函数返回路径的长度。

## Implementation

该系统调用通过 `syscall` 宏进行转换。

## Errors

- `EINVAL` - 如果 `bufsize` 为负数、文件系统不支持该调用或路径未被引用；
- `ENOENT` - 如果路径不存在。

![](img/04698aadad5d50fd4b3564ae373ff0bd_373_1.png)

### File: `fs/select.c`

```c
#include <sys/time.h>
#include <sys/types.h>
int sys_select(int n, fd_set *inp, fd_set *outp, fd_set *exp, struct timeval *tvp)
```

`sys_select()` 函数允许输入和输出的多路复用。时间被转换为 `jiffies` 并作为进程的超时时间持续。进程在调用后睡眠，直到 `inp`、`outp` 或 `exp` 中的其中一个描述符可用，或者时间跨 `tvp` 结束。

函数返回可用描述符的数量。如果 `personality` 中设置了 `STICKY_TIME_OUT` 标志，它也会被更新。为其使用定义的几个宏：

- `FD_ZERO(fdset)` - 删除所有 `fdset` 位
- `FD_CLR(fd, fdset)` - 删除 `fdset` 中的描述符 `fd`
- `FD_SET(fd, fdset)` - 设置描述符 `fd/fdset`
- `FD_ISSET(fd, fdset)` - 检查 `fdset` 中的描述符 `fd`。如果已设置则返回非零值。

## Implementation

该系统调用通过 `syscall` 宏进行转换。

## Errors

- `EBADF` - 如果其中一个字段中存在无效描述符。
- `EINTR` - 如果接收到非阻塞信号。
- `EINVAL` - 如果 `fd` 为负数。
- `ENOMEM` - 如果内核中的内部表没有足够的内存。

| System call | stat | newstat |
|---|---|---|
| | fstat | | |
| lstat | newstat | | |

### File: `is/stat.c`

```c
#include <sys/stat.h>
```
