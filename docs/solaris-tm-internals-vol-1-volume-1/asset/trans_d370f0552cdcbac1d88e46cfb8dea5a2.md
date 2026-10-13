
使用 `vmstat` 命令查看系统上的空闲内存量。示例如下。

```text
# vmstat 3
procs      memory      page      disk      faults      cpu
 r  b  swpd  free  ...
 0  0 155868  2982  0  92  0  0  0  0  0  0  23 172  96  0  2  98
 0  0 155868  3020  0  33  1  0  0  0  0  0  20 187  95  1  2  98
 0  0 155868  3012  0  50  2  0  0  0  0  0  22 181  97  0  1  99
 0  0 155868  3012  0  50  0  0  0  0  0  0  18 123  92  0  1  99
 0  0 155868  3012  0  50  0  0  0  0  0  0  21 126  95  0  1  99
 0  0 155868 17244 186 112 78  0 98  0 27  0  13  0  0  86 223 131  0 12  88
 0  0 155868  45840  0  50  0  0  0  0  0  0  7 119  50  0  1  99
 0  0 155868  45840  0  50  0  0  0  0  0  0  15 130  55  0  1  99
 0  0 155868  45840  0  50  0  0  0  0  0  0  14 122  52  0  1  99
```

### 11.5.2.2 MADV_WILLNEED 标志

当我们首次访问某个尚未读入内存的文件位置时，文件页面会被逐个读取。如果我们知道将要读取给定文件范围的大部分或全部内容，这种方法可能不是最优的，此时可以使用 `MADV_WILLNEED` 标志来预读整个给定范围，如下所示。

```c
if ((addr = mmap64((caddr_t)0, length, PROT_READ,
    MAP_SHARED, fd, offset)) == NULL) {
        perror("mmap failed");
        exit(1);
}

(void) madvise(addr, length, MADV_WILLNEED);
(void) munmap(addr, length);
```

`MADV_WILLNEED` 请求的范围是同步读取的，因此 `madvise` 系统调用会一直等待，直到整个范围全部读入后才返回。一个简单的测试程序演示了在 `MADV_WILLNEED` 之后，随着文件被读入，空闲内存如何下降。测试程序的输出如下所示。

```text
# ./mmap_willneed testfile
# vmstat 3
procs      memory      page      disk      faults      cpu
 r  b  swpd  free  ...
 0  0 155868 45760  0  50  0  0  0  0  0  0  7 121  53  0  1  99
 0  0 155864  3100  1  53  0  0 336 342  0 27  0  0  41 205 131  57  0  1  99
 0  0 155864  3964  2  54  0  0  0  0  0  0  0  0  15 122  53  0  1  99
 0  0 155864  3944  1  53  0  0  0  0  0  0  0  0   9 131  54  0  1  99
```

### 11.5.2.3 MADV_SEQUENTIAL 标志

默认情况下，内存系统会在文件被分配时将其读入，然后将其留在内存中。`MADV_SEQUENTIAL` 标志可以告诉内存系统某个范围正在被顺序访问，并且可以释放已读取位置之后的内存。下面展示了如何在某个范围上使用 `MADV_SEQUENTIAL` 的示例。

```c
if ((addr = mmap64((caddr_t)0, length, PROT_READ,
    MAP_SHARED, fd, 0, (off_t)0)) == NULL) {
        perror("mmap failed");
        exit(1);
}

(void) madvise(addr, length, MADV_SEQUENTIAL);
(void) munmap(addr, length);
```

如果我们运行一个顺序读取文件的简单进程，通过查看 `vmstat` 命令的输出，可以看到内存随着读取而被释放。

```text
# ./mmap_seqread testfile&
# vmstat 3
procs      memory            page              disk            faults      cpu
 r  b  w  swap free  re  mf  pi  po  fr  de  sr  s0  s1  s2  s3  in  sy  cs  us  sy  id
 0  0  0 155864 3100  1  53 336  0 336  0  0  0  0  0  41 205 131  57  0   1  99
 0  0  0 155864 3100  1  53 339  0 339  0  0  0  0  0  41 205 131  57  0   1  99
 0  0  0 155864 3100  1  53 332  0 332  0  0  0  0  0  41 205 131  57  0   1  99
 0  0  0 155864 3100  1  53 338  0 338  0  0  0  0  0  41 205 131  57  0   1  99
```

`MADV_SEQUENTIAL` 的另一个好处是文件会被提前读取，每次读取 64 千字节。通过 `iostat` 命令查看 I/O 大小可以看到这一点。下面的 iostat 示例显示，每秒读取 98 次 I/O，总共每秒读取 6272 千字节，平均 I/O 大小为 64 千字节。

```text
# iostat -x 5

device     r/s   w/s   kr/s   kw/s wait actv  svc_t  %w  %b
fd0        0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
sd6        0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd11      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd12      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd13     98.0   0.0 6272.0    0.0  0.0  3.7   73.7   0  93
ssd15      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd16      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd17      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
```

### 11.5.2.4 MADV_RANDOM 标志

默认情况下，文件读取会实现预读（如对 `MADV_SEQUENTIAL` 标志的描述）。在某些情况下，我们可能知道访问模式将是完全随机的。在这种情况下，预读没有任何益处，反而可能增加额外的开销，因为 I/O 将以 64 千字节的块大小进行，而不是以页大小的块（通常为 8 千字节）进行。我们可以通过指定 `MADV_RANDOM` 标志来禁用预读，如下例所示。

```c
if ((addr = mmap64((caddr_t)0, length, PROT_READ,
    MAP_SHARED, fd, off)) == NULL) {
        perror("mmap failed");
        exit(1);
}

(void) madvise(addr, length, MADV_RANDOM);
munmap(addr, length);
```

一个简单的测试程序显示，现在我们每秒读取 151 次 I/O，I/O 速率为每秒 1,198 千字节，平均 I/O 大小为 8 千字节，如下所示。

```text
# iostat -x 5

device        r/s  w/s  kr/s  kw/s  wait  actv  svc_t  %b
fd0           0.0  0.0  0.0   0.0   0.0   0.0   0.0    0
sd6d          0.0  0.0  0.0   0.0   0.0   0.0   0.0    0
ssd1          0.0  0.0  0.0   0.0   0.0   0.0   0.0    0
ssd12         0.0  0.0  0.0   0.0   0.0   0.0   0.0    0
ssd13       151.0  0.0  1198.0 0.0   0.0   0.0   10.2   0 100
ssd15         0.0  0.0  0.0   0.0   0.0   0.0   0.0    0
ssd16         0.0  0.0  0.0   0.0   0.0   0.0   0.0    0
ssd17         0.0  0.0  0.0   0.0   0.0   0.0   0.0    0
```

## 11.6 Solaris 中的 64 位文件

多年以来，Sun 公司交付的系统最大文件系统和文件大小为 2 吉字节。这个大小是内核中偏移量数据类型位数所造成的限制。该大小限制出现在三个主要位置：磁盘地址类型 `daddr_t`；文件系统接口 `off_t` 数据类型；以及用于设备驱动程序和某些文件系统接口的 `uio` 结构。Solaris 2.0 之前的类型都是 32 位的，如下所示。

```c
typedef long    daddr_t;
typedef long    off_t;

struct uio {
        struct  iovec *uio_iov;
        int     uio_iovcnt;
        off_t   uio_offset;
        short   uio_segflg;
        short   uio_fmode;
        int     uio_resid;
};
```

`daddr_t` 和 `uio_t` 结构被设备驱动程序以及内核中的某些文件系统接口使用，而 `off_t` 数据类型则广泛用于整个内核和用户态应用程序编程接口中。

### 11.6.1 Solaris 2.0 中的 64 位设备支持

Solaris 2.0 借助 64 位数据类型 `longlong_t` 实现了部分 64 位设备支持。Solaris 2.0 附带了一个额外的磁盘地址类型（`diskaddr_t`）、一个额外的偏移量类型（`lloff_t`）以及一个支持 64 位的 `uio` 结构。扩展的磁盘地址和 `uio` 结构使得设备支持超过 2 吉字节，并允许文件系统突破 2 吉字节的限制，达到理论上的最大值 2^63−1。Solaris 2.x 中的 UFS 文件系统可扩展到 1 太字节，这是 UFS 特有的限制。

```c
typedef long       daddr_t;       /* <磁盘地址> 类型 */
typedef long       off_t;         /* <偏移量> 类型 */

typedef longlong_t offset_t;
typedef longlong_t diskaddr_t;

/*
 * 此处包含对 64 位文件偏移量的部分支持，
 * 专门用于访问大于 2 GB 的设备。
 * 但是，对大于 2 GB 的设备的支持需要编译器
 * 支持 long long。
 * XXX 这些假定为 big-endian 机器 XXX
 */
typedef union lloff {
        offset_t _f;              /* 完整的 64 位偏移量值 */
        struct {
                long _u;          /* 偏移量值的高 32 位 */
                off_t _l;          /* 偏移量值的低 32 位 */
        } _p;
} lloff_t;

typedef union lldaddr {
        diskaddr_t _f;            /* 完整的 64 位磁盘地址值 */
        struct {
                long _u;           /* 磁盘地址值的高 32 位 */
                daddr_t _l;        /* 磁盘地址值的低 32 位 */
        } _p;
} lldaddr_t;
```

**头文件**  `<sys/types.h>`

Solaris 2.0 中没有用户接口可以访问大型设备，这限制了设备访问和文件大小在 2 吉字节以内。

### 11.6.2 Solaris 2.5.1 中的 64 位文件应用程序编程接口

随着数据库大小增长到超过 1 太字节，单个磁盘设备也增长到超过 2 吉字节，应用程序供应商需要一种机制来访问超过 2 吉字节的数据大小。完整的大型文件支持预计在 Solaris 2.6 中出现，但在 Solaris 2.5 中，添加了两个接口以提供大型设备支持。

