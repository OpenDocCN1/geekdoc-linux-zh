
```
if (count & FREQ == 0)
    ec_negl( read(STDIN_FILENO, buf2, sizeof(buf2)) )
count++;
)
timestop("synchronous");
printf("read %d blocks\n", count);
return;

EC_CLEANUP_BGN
    EC_PLUSH("asynchronous")
EC_CLEANUP_END
)
```
（`timestart` 和 `timestop` 在 1.7.2 节中有介绍。）

标准输入连接到一个管道，该管道由一个名为 `feed` 的程序填充：

$ feed | sio

`feed` 是一个写操作非常迟缓的程序——它每 20 秒才写一次：

```
int main(void)
{
    char buf[512];

    memset(buf, 'x', sizeof(buf));
    while (true) {
        sleep(20);
        write(STDOUT_FILENO, buf, sizeof(buf));
    }
}
```

如前文所示的管道中，`sio` 运行至完成时耗时 0.12 秒用户 CPU 时间、0.73 秒系统 CPU 时间，总耗时 200.05 秒。显然，大量的实际耗时（elapsed time）都花在了等待管道输入上。

这是一个人为构造的示例，但即便如此，它也提供了一个通过异步 I/O 来缩短总耗时的机会。如果管道的读取可以异步进行，那么在此期间就可以读取文件，如下面的重写代码所示：

```
static void asynchronous(void)
{
    int fd, count = 0;
    size_t nread;
    char buf1[512], buf2[512];
    struct aiocb cb;
    const struct aiocb *list[1] = { &cb };
    memset(&cb, 0, sizeof(cb));
    cb.aio_fildes = STDIN_FILENO;
    cb.aio_buf = buf2;
    cb.aio_nbytes = sizeof(buf2);
    cb.aio_sigevent.sigev_notify = SIGEV_NONE;
    ec_neg1( fd = open(PATH, O_RDONLY) )
    timestart();
    while (true) {
        ec_neg1( nread = read(fd, buf1, sizeof(buf1)) )
        if (nread == 0)
            break;
        if (count & FREQ == 0) {
            if (count > 1) {
                ec_neg1( aio_suspend(list, 1, NULL) )
                ec_cv( aio_error(&cb) )
            }
            ec_neg1( aio_read(&cb) )
        }
        count++;
    }
    timestop("asynchronous");
    printf("read %d blocks\n", count);
    return;

cleanup:
    EC_CLEANUP_BGN
    EC_FLUSH("asynchronous")
EC_CLEANUP_END
}
```

请注意控制块的设置方式；首先将其清零，以确保任何依赖于实现的额外成员也被清零。每 8000 次读取（`FREQ` 之前已定义）后，程序发起一次 `aio_read` 调用，之后在 `aio_suspend` 中等待，直到控制块就绪才发起下一次调用。在 `aio_read` 处理期间，程序继续读取文件，在接下来的 8000 次读取中不再挂起。这次的用户 CPU 时间变得更差了——0.18 秒——因为有更多的工作要做。系统时间大致相同（0.70 秒），但总耗时缩短了：180.58 秒。

使用 AIO 并不总能带来如此显著的收益，有时你甚至能看到比这个示例更好的改进。关键在于：

- 程序在 I/O 异步处理期间必须有一些有用的工作要做。
- 收益必须超过增加的管理开销（bookkeeping costs）和增加的系统调用次数。你还应考虑增加的编程复杂度以及 AIO 并非在所有系统上都受支持这一事实。

### 3.9.9 `lio_listio`

控制块列表还有另一种用途：将 I/O 请求批量处理，并通过单次调用启动它们：

lio_listio——列表驱动的 I/O

```
#include <aio.h>

int lio_listio(
    int mode,                    /* LIO_WAIT or LIO_NOWAIT */
    struct aiocb *const list[],  /* array of control blocks */
    int ncnt,                    /* number of elements in array */
    struct sigevent *sig         /* NULL or signal to generate */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

与 `aio_suspend` 类似，`lio_listio` 接受一个由 `cbcnt` 个控制块组成的列表，忽略 *list* 中的 NULL 元素。它以非特定顺序发起请求。每个操作由控制块的 `aio_lio_opcode` 成员指定：

- `LIO_READ`    相当于调用 `aio_read` 或 `pread`。
- `LIO_WRITE`   相当于调用 `aio_write` 或 `pwrite`。
- `LIO_NOP`     空操作；忽略该控制块。

*mode* 参数决定由 `lio_listio` 发起的 I/O 是同步还是异步，如表 3.6 所示，该表类似于表 3.5（参见 3.9.1 节）。

**表 3.6** 同步与异步的 `lio_listio` 对比

|                | 同步                                     | 异步                                     |
| -------------- | ----------------------------------------- | ------------------------------------------- |
| 非同步化         | `LIO_WAIT; O_SYNC` 和 `O_DSYNC` 未设置     | `LIO_NOWAIT; O_SYNC` 和 `O_DSYNC` 未设置     |
| 同步化          | `LIO_WAIT; O_SYNC` 或 `O_DSYNC` 已设置      | `LIO_NOWAIT; O_SYNC` 或 `O_DSYNC` 已设置      |

因此，`lio_listio` 并不像“aio”系统调用那样仅用于异步 I/O——只要你想批量处理 I/O 调用，就可以使用它。

对于异步的 `lio_listio`，若 mode 为 `LIO_NOWAIT`，你可以像使用控制块的

aio_sigevent 成员一样，通过 *sig* 参数请求通过信号或线程启动进行通知。但在这里，通知意味着列表中的所有请求都已完成。你仍可通过各个控制块的 aio_sigevent 成员接收完成通知。

对于 LIO_WAIT，sig 参数不被使用。

与其他一些 AIO 调用一样，`lio_listio` 的成功返回仅意味着该调用本身正常结束。它并未说明 I/O 操作的状态，你需要使用 `aio_error` 来测试。

## 练习

- 3.1. 按照该节最后一段的建议，修改 3.2.2 节中的程序。
- 3.2. 编写标准的 clc 命令。
- 3.3. 按照 3.6.2 节最后一段的建议，修改 aupls 命令。
- 3.4. 修改 3.6.4 节中的 getcwdx 函数，使其绝不更改当前目录。
- 3.5. 修复在 3.6.5 节开头描述的问题 2。
- 3.6. 修改 3.6.5 节中的 aupls 命令，使其按名称对列表进行排序。
- 3.7. 修改 3.6.5 节中的 aupls 命令，使其接受 –t 选项以按修改时间和名称排序。
- 3.8. 修改 3.6.5 节中的 aupls 命令，使其接受额外的标准选项（由你选择）。
- 3.9. 编写一个程序来复制整个目录和文件树。它应该有两个参数：树的根目录（例如，/usr/marc/book）和副本的根目录（例如，/usr/marc/backup/book）。无需处理符号链接或硬链接（即，允许多份拷贝），也无需保留所有权、权限或时间。
- 3.10. 与练习 3.9 相同，但在可能的范围内保留所有权、权限和时间。使“可能的范围”取决于命令是否以超级用户身份运行。
- 3.11. 与练习 3.10 相同，但保留符号链接和硬链接的结构。
- 3.12. 为什么没有 lchmod 系统调用？
- 3.13. 将 access 编写为一个函数。你可以使用任何系统调用，除了 access 之外。
- 3.14. 使用 lio_listio 实现 readv 和 writev（第 2.15 节）。以这种方式实现有任何优势吗？有什么缺点？
- 3.15. 你能对 read, write, pread, pwrite, fsync, fdatasync, aio\_read, aio\_write, 和 aio\_fsync 执行练习 3.14 吗？如果可以，请执行。有什么优势？有什么缺点？
- 3.16. 列出使用 aio\_suspend、信号、线程启动或使用 aio\_error 轮询来检查 AIO 完成情况的优缺点。（需要第 5 章和第 9 章中的信息。）

# 终端 I/O

## 4.1 引言

终端 I/O 非常复杂，需要独占大部分章节内容来描述。问题不在于正常的终端 I/O，我将以此开始介绍——它甚至比文件 I/O 更简单。使情况复杂化的是终端属性的众多变化。在本章中，我还会解释终端与会话和进程组之间的关系。然后，我将展示如何设置伪终端，这允许一个进程控制另一个为终端编写的进程。

UNIX 上的终端 I/O 将终端视为老式的硬拷贝电传打字机（Teletype），即那种带有巨大键盘箱、运行时发出巨大噪音并在博物馆或老电影中才能见到的型号。内核中没有对屏幕（字符或图形）、功能键或鼠标及其他指向设备的具体支持。其中一些较现代的设备可以通过调用标准设备驱动的库来处理。对于字符显示，最著名的此类软件包是 Curses，它现在是 [SUS2002] 的一部分。所谓的 UNIX 图形用户界面（GUI）应用程序通常构建为运行在 X Window System 上，可能使用其工具包之一，如 Motif、Qt、KDE 或 Gnome。

由于本章的主题主要是关于设备驱动，而不是像文件系统这样的内核固有部分，因此具体功能在不同 UNIX 版本之间通常比平时差异更大。有时甚至单个 UNIX 站点也会修改终端设备驱动程序。请记住，并非所有终端 I/O 的特性都是由 UNIX 本身造成的：随着智能终端、局域网和前端处理器的使用越来越多，字符流在 UNIX 内核看到它以及将其发送之后，都会经历大量的处理。这些预处理和后处理的细节差异太大，无法在此详述。一如既往，我将关注终端 I/O 的标准化属性。以此为背景，你应该能够根据自己的手册弄清楚自己的系统。

