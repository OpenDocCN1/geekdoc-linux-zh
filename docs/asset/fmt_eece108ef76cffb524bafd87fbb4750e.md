
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

`头文件` `<sys/types.h>`

Solaris 2.0 中没有用户接口可以访问大型设备，这限制了设备访问和文件大小在 2 吉字节以内。

### 11.6.2 Solaris 2.5.1 中的 64 位文件应用程序编程接口

随着数据库大小增长到超过 1 太字节，单个磁盘设备也增长到超过 2 吉字节，应用程序供应商需要一种机制来访问超过 2 吉字节的数据大小。完整的大型文件支持预计在 Solaris 2.6 中出现，但在 Solaris 2.5 中，添加了两个接口以提供大型设备支持。

对于裸设备。虽然这看起来似乎并不是一个重大的新增功能，但许多数据库供应商使用裸设备来存储数据库表。大设备接口使数据库供应商能够在裸设备上寻址超过 2 GB 的空间。

由于 `read` 和 `write` 系统调用不包含磁盘偏移地址，因此只需添加一个可定位到 64 位地址的接口，即可实现大设备接口。新增的接口是 `llseek`，恰如其名，它是一个长的 lseek。注意这里使用了新的偏移类型 `offset_t`，而不是旧的 `off_t`。

```c
typedef longlong_t    offset_t;

offset_t llseek(int fdes, offset_t off, int sbase)
```

`头文件` `<sys/unistd.h>`

新的 `llseek` 接口允许进程在任何支持大访问的设备上跨越 64 位文件偏移量进行定位。只有裸磁盘设备允许大访问。由于 `llseek` 接口主要是为数据库供应商添加的，而且许多数据库供应商会利用异步 I/O，因此专门为大型（大于 2 GB）文件的异步 I/O 创建了两个新接口。

```c
typedef longlong_t    offset_t;

int aioread64(int fd, caddr_t *buf, int bufsz, offset_t offset,
              int whence, aio_result_t *resultp)

int aiowrite64(int fd, caddr_t *buf, int bufsz, offset_t offset,
               int whence, aio_result_t *resultp)
```

`头文件` `<sys/asynch.h>`

请注意，Solaris 2.5.1 的所有大设备接口都需要应用程序更改。

### 11.6.3 Solaris 2.6：大文件操作系统

Solaris 2.6 是第一个支持大于 2 GB 文件的 Solaris 版本。文件系统经过增强，可以处理跨越 2 GB 边界的文件，并且引入了 64 位文件 API，使应用程序能够访问大文件。

由于现有 API 在所有文件定位接口中都使用了 32 位偏移量，因此在不破坏 Unix 95、POSIX 和二进制兼容性的情况下，现有 API 无法更改。为此，Solaris 2.6 提供了一个过渡性的大文件接口。

#### 11.6.3.1 大文件峰会

Sun 并不是唯一需要解决大文件兼容性问题的供应商，业界召开了一次峰会，为 32 位环境规定了一套通用的大文件应用程序接口。（请参阅 http://www.sas.com/standard/large.file/ 上的大文件峰会文档。）大文件峰会规定了一组新的接口，类似于 Unix 95/POSIX 接口，但在接口名称中添加了 64 扩展。例如，32 位的 `lseek()` 有对应的 64 位 `lseek64()`。除了新接口之外，所有现有接口都具备大文件安全性，因此如果访问了大文件（或文件增长超过 2 GB 限制），会返回适当的错误条件。在大文件支持的上下文中，程序被视为处于以下两种状态之一：

- **大文件安全。** 程序将检测到对大文件执行的操作，并处理错误，而不会导致数据丢失或损坏。

- **大文件感知。** 程序能够正确处理大文件。

Solaris 2.6 中的以下更改提供了大文件支持：

- 在 32 位接口中针对大文件进行适当的错误处理和检查。在非大文件应用程序中，`open` 系统调用将无法打开大文件，并且所有 32 位文件 API 在遇到大小大于或等于 2 GB 的常规文件时都会返回 `EOVERFLOW`。
