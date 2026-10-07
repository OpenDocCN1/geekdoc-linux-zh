
使用 `vmstat` 命令查看系统中的空闲内存量。示例所示。

```
# vmstat 3
proc memory          page             disk           faults         cpu
r b w swap free re me pi po fr er f0 s2 s3 a5 in ay ca us my id
0 0 155868 2992 92 0 12 2 0 0 1 23 176 96 0 298
0 0 155868 3020 33 1 0 0 0 0 0 20 187 95 1 99
0 0 155868 3012 50 2 0 0 0 0 0 0 22 181 97 0 99
0 0 155868 3012 50 0 0 0 0 0 0 0 21 126 95 0 99
0 0 155804 17244 186 112 78 0 97 27 0 0 3 86 223 131 0 12 88
0 0 155868 45840 50 0 0 0 0 0 0 0 7 119 50 0 19
0 0 155868 45840 50 0 0 0 0 0 0 0 15 130 55 0 19
0 0 155868 45840 50 0 0 0 0 0 0 0 14 122 52 0 19
```

## 11.5.2. MADV_WILLNEED 标志

当我们第一次访问一个尚不在内存中的文件位置时，系统会逐个地读取文件的页。如果我们知道将要读取给定范围的所有内容，这种方法可能并非最优，我们可以使用 `MADV_WILLNEED` 标志对给定范围进行预读，如下所示。

```c
if ((addr = mmap((caddr_t)0, length, PROT_READ,
     MAP_SHARED, fd, offset)) == NULL) {
    perror("mmmap failed");
    exit(1);
}

(void) madvise(addr, length, MADV_WILLNEED);
munmap(addr, length);
```

`MADV_WILLNEED` 请求的范围是同步读取的，因此 `madvise` 调用将等待整个范围读取完成后返回。一个简单的测试演示了在 `MADV_WILLNEED` 之后读取文件时空闲内存是如何填充的。测试输出如下所示。

### 11.5.2.3 MADV_SEQUENTIAL 标志

默认情况下，内存系统在分配文件时读取它并将其留在内存中。`MADV_SEQUENTIAL` 标志可以告诉内存系统某个范围正在被顺序访问，并且可以释放已读取部分之后的内存。以下是一个在范围上使用 `MADV_SEQUENTIAL` 的示例。

```c
if ((addr = mmap((caddr_t)0, length, PROT_READ,
      MAP_SHARED, fd, offset)) == NULL) {
    perror("map failed");
    exit(1);
}

(void) madvise(addr, length, MADV_SEQUENTIAL);
(void) munmap(addr, length);
```

如果我们运行一个顺序读取进程的简单程序，可以通过查看 `vmstat` 命令的输出看到内是在被读取时被释放的。

```
# ./mmmap seqread test
# vmstat 3
procs memory free re mi pi po de disk faults in fo2 s3 s5 cpu cs us sy id
r b w w/s kr/s kw/s wait act svc_t tw %b
0 0 155864 3100 1 53 336 336 0 0 0 0 205 131 57 0 1 99
0 0 155864 3100 1 53 339 339 0 0 0 0 205 131 57 0 1 99
0 0 155864 3100 1 53 332 332 0 0 0 0 205 131 57 0 1 99
0 0 155864 3100 1 53 338 338 0 0 0 0 205 131 57 0 1 99
```

`MADV_SEQUENTIAL` 的另一个好处是文件是以每 64KB 为组进行预读的。你可以通过 `iostat` 命令查看 I/O 大小看出这一点。我们的 `iostat` 示例显示每秒读取 98 次 I/O，每秒共读取 6272 字节，平均 I/O 大小为 64 字节。

```
# iostat -x 5
device r/s w/s kr/s kw/s wait act svc_t tw %b
fd 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
sd6 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
ssd1 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
sd12 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
ssd13 98.0 0.0 0.0 0.0 0.0 3.7 73.7 0 93
ssd15 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
ssd16 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
ssd17 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
```

## 11.5.2. MADV_RANDOM 标志

默认情况下，文件读取时会执行预读（如 `MADV_SEQUENTIAL` 标志所示）。在某些情况下，我们可能知道访问模式是随机的。在这种情况下，预读没有用处，实际上会增加开销，因为 I/O 将按 64KB 而不是页大小（通常为 8KB）进行。通过指定 `MADV_RANDOM` 标志可以禁用预读，如下所示。

```c
if ((addr = mmap((caddr_t)0, length, PROT_READ,
     MAP_SHARED, fd, offset)) == NULL) {
    perror("mmap failed");
    exit(1);
}

(void) madvise(addr, length, MADV_RANDOM);
munmap(addr, length);
```

简单的测试显示我们现在每秒读取 151 次 IO，速率为每秒 198  KB，平均 I/O 大小为 8 KB，如下所示。

```
iostat -x 5
| device | r/s | w/s | kr/s | kw/s | act | svc_t | tw | tb |
|---|---|---|---|---|---|---|---|
| fd | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| sd6 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| ssd1 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| sd12 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| ssd13 | 151.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 100 |
| ssd15 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| ssd16 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| ssd17 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
```

## 11.6 Solaris 中的 64 位文件系统

多年来，Sun 提供的系统最大文件系统和文件大小为 2GB。这种限制是由内核中偏移类型的位宽造成的。大小限制出现在三个主要地方：磁盘地址类型 `daddr_t`；文件系统接口类型 `off_t`；以及用于设备驱动程序和某些文件系统接口的 `uio` 结构。Solaris 2.0 之前的类型均为 32 位，如下。

```c
typedef long daddr_t;
typedef long off_t;

struct uio {
    struct iovec *uio_iov;
    int uio_iovcnt;
    off_t uio_offset;
    short uio_segfl;
    short uio_mods;
    int uio_resid;
};
```

`daddr_t` 和 `uio` 结构被设备驱动程序和内核中的某些文件系统接口使用，而 `off_t` 类型在整个内核和用户态接口中广泛使用。

### 11.6.1 Solaris 2.0 中的 64 位设备支持

Solaris 2.0 通过 64 位数据类型 `long_t` 实现了部分 64 位设备支持。它带有额外的磁盘地址类型 `lldaddr_t`、额外的偏移类型 `loff_t` 以及支持 64 位的 `uio` 结构。扩展的磁盘地址和 `uio` 结构允许支持超过 2GB 的设备，并将文件系统跨越 2GB 限制，理论最大值为 $2^{64}$。Solaris 2.x 中的 UFS 文件系统可以扩展到 1TB，这是 UFS 特有的限制。

```c
typedef long daddr_t;
typedef long off_t;
typedef long long offset_t;
typedef long long daddr_t;
/* <磁盘地址> 类型 */
/* <偏移> 类型 */
/* 
 * 此处包含 64 位文件的部分支持，
 * 特用于访问超过 2GB 的设备。
 * 然而，支持超过 2GB 的设备需要编译器对 long 设备的支持。
 * XXX 此时假设是大端序机器 XXX
 */
typedef union loff {
    offset_t _f;      /* 完整的 64 位偏移值 */
    struct {
        long long_u;
        off_t _1;
    } /* 偏移值的高 32 位 */
      /* 偏移值的低 32 位 */
} loff_t;
typedef union lldaddr {
    daddr_t _f;      /* 完整的 64 位磁盘地址值 */
    struct {
        long long_u;
        daddr_t _1;
    } /* 磁盘地址值的高 32 位 */
        /* 磁盘地址值的低 32 位 */
} lldaddr_t;
```

Solaris 2.0 中没有用户接口访问大设备，这使得设备访问和大小限制在 2GB 以。

## 11.6.2 Solaris 2.5.1 中的 64 位文件应用程序接口

内存系统在分配文件时读取它并将其留在内存中。`MADV_SEQUENTIAL` 标志可以告诉内存系统某个范围正在被顺序访问，并且可以释放已读取部分之后的内存。`MADV_SEQUENTIAL` 在范围上使用的示例如下。

```c
if ((addr = mmap((caddr_t)0, length, PROT_READ,
     MAP_SHARED, fd, offset)) == NULL) {
    perror("mmap failed");
    exit(1);
}

(void) madvise(addr, length, MADV_RANDOM);
```

一个简单的测试显示我们现在每秒读取 151 次 IO，速率为每秒 198 KB，平均 I/O 大小为 8 KB，如下所示。

