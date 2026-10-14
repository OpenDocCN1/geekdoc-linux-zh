
```c
(void)lseek(d1, (off_t) 1000, SEEK_SET);

child_processing();
} else {

    /* 父进程 */

    sleep(5);

}
}
```

```c
printf ("parent: current position = %ld\n",
  (long) lseek (d1, (off_t) 0, SEEK_CUR));
parent_processing ();
```

## ShareDesc.c

当执行这些操作时，两个进程都可以访问由 `d1` 引用的文件。只有子进程可以访问由 `d2` 的文件。描述符表之间的关系如图 6.4 所示。当子进程通过调用原语 `lseek` 改变第一个文件的位置时，该更改在父进程级别是立即可见的。

`Bbj>ShareDesc`
`parent: current position = 0`
`child: current position = 0`
`parent: current position = 1000`

![](img/2a00748fb2b118631f23d65044e52f82_184_0.png)

图 6.4：相关进程之间的描述符共享。

### 6.3.4 文件锁

在多个进程以共享模式访问同一文件的情况下，可能需要对进程进行同步，即使读写操作变为串行操作。Linux 提供了几种文件锁定机制，允许协作进程进行自我同步。Linux 提供的锁仅适用于协作进程。当使用 `read` 和 `write` 原语进行普通读写时，内核不会检查锁，而是由进程自行调用锁定系统调用。如果进程在未获取锁的情况下读写数据，Linux 将不会干预。

存在两种类型的锁：

- 1. 共享锁（Shared locks）：多个进程可以同时持有共享锁。这种锁用于仅对文件进行读操作并希望防止写入进程的进程。
- 2. 独斥锁（Exclusive locks）：只有一个进程可以持有独斥锁。这种锁用于执行写入的并发进程，它们希望防止同时写入，以及在写操作期间防止读取。

### 6.3.5 挂载文件系统

（注：此处原文存在大量重复和OCR错误，已根据要求进行清理并翻译）

# 互补系统调用

| 类型 | 字段 | 描述 |
| --- | --- | --- |
| void * | iov_base | 缓冲区地址 |
| int | iov_len | 缓冲区大小（字节） |

读取数据时，将根据 `iovec[0].iov_len` 指定的字节数，从 `iovec[0].iov_base` 地址开始读取并存储；然后根据 `iovec[1].iov_len` 指定的字节数，从 `iovec[1].iov_base` 地址开始读取，依此类推。

写入数据时，将根据 `iovec[0].iov_len` 指定的字节数，从 `iovec[0].iov_base` 地址开始写入并存储；然后根据 `iovec[1].iov_len` 指定的字节数，从 `iovec[1].iov_base` 地址开始写入，依此类推。

在读取或写入发生错误时，变量 `errno` 可以取以下值：

| 错误 | 含义 |
| --- | --- |
| EBADF | 输入/输出描述符无效 |
| EFAULT | vector 或其中一个字段 iov_base 包含无效地址 |
| EINTR | 系统调用因接收信号而中断 |
| EINVAL | 计数大于 MAX_IOV，或 fd 指向一个不可读不可写的对象 |
| EISDIR | fd 指向一个目录 |
| EPIPE | fd 指向一个没有读取进程的管道 |
| ENOSPC | 文件系统已满 |

### 6.4.2 输入/输出描述符的复制

由原始 `open` 返回并被所有输入/输出系统调用使用的输入/输出描述符是可以被复制的。这意味着一个进程有可能通过多个输入/输出描述符访问同一个已打开的文件。提供了两个系统调用来复制描述符：

```c
#include <unistd.h>
```

```c
int dup (int oldfd);
int dup2 (int oldfd, int newfd);
```

`dup` 调用复制描述符 `oldfd` 并返回另一个指向同一已打开文件的描述符。原始的 `dup2` 使描述符 `newfd` 等同于 `oldfd`，如果 `newfd` 对应一个已打开的文件，则在复制之前将其关闭。`dup` 和 `dup2` 返回新的输入/输出描述符，或者在发生错误时返回值 `-1`。

在发生错误时，变量 `errno` 取以下值：

| 错误 | 含义 |
| --- | --- |
| EBADF | 输入/输出描述符无效 |
| EFILE | 已达到当前进程打开的文件最大数量限制 |

这种描述符复制机制对于输入/输出重定向特别有用。进程可以将其标准输入或输出重定向到文件，然后以透明的方式使用标准库函数（例如 `scanf` 和 `printf` 示例，读/或写操作是在文件中进行的，而不是通过键盘或屏幕执行）。

以下程序段将其标准输出重定向到名为 `output` 的文件：

```c
int fd;

/* 打开输出文件 */
fd = open("output", O_WRONLY | O_CREAT | O_TRUNC);
if (fd == -1) {
    perror("open");
    exit(1);
}

/* 重定向标准输出（描述符 1） */
if (dup2(fd, 1) != 1) {
    perror("dup2");
    exit(1);
}
```

#### 6.4.3 文件属性

Linux 提供了三个系统调用来显示文件的属性。这些调用的语法如下：

```c
#include <sys/stat.h>
#include <unistd.h>

int stat (const char *pathname, struct stat *buf);
int fstat (int fd, struct stat *buf, struct stat *buf);
int lstat (const char *pathname, struct stat *buf);
```
