
`ls -l fifo1 greeting` 命令的输出显示两者都是空的。`du fifo1 greeting` 命令的输出显示两者都使用一个磁盘块。我们在 `greeting` 文件以及 `fifo1` 中放入了 "Hello, world!"（14 字节）。第二次 `ls -l fifo1 greeting` 命令的输出显示 `fifo1` 仍然是空的，但 `greeting` 包含 14 字节。`du fifo1 greeting` 命令的输出显示 `fifo1` 仍然使用一个磁盘块，而 `greeting` 文件使用五个磁盘块。即使我们使用 `cat fifo1` 命令清空 `fifo1`，`fifo1` 的磁盘使用量也保持不变。此会话表明，当我们向 `fifo1` 中放入数据时，数据不会进入与其关联的磁盘对象，而是进入与 `fifo1` 关联的内存缓冲区（管道）。

```
% mkfifo fifo1
% touch greeting
% ls -i fifo1 greeting
4933 fifo1  4934 greeting
% ls -l fifo1 greeting
prw-r--r-- 1 sarwar faculty 0 Apr 18 17:29 fifo1
-rw-r--r-- 1 sarwar faculty 0 Apr 18 17:29 greeting
% du fifo1 greeting
1       fifo1
1       greeting
% cat > greeting
Hello, world!
% cat greeting > fifo1 &
[1] 68928
% ls -l fifo1 greeting
prw-r--r-- 1 sarwar faculty 0 Apr 18 17:29 fifo1
-rw-r--r-- 1 sarwar faculty 14 Apr 18 17:31 greeting
% du fifo1 greeting
1       fifo1
5       greeting
% cat fifo1
Hello, world!
[1]  + Done                    cat greeting > fifo1
% du fifo1 greeting
1       fifo1
5       greeting
%
```

以下会话是在 Solaris 机器上捕获的，以显示 FIFO 在 Solaris 上也是以相同方式工作的。唯一的区别是，在 BSD 系统上空 FIFO 使用一个磁盘块，而在 Solaris 上它不使用任何磁盘空间，如 `du fifo1 greeting` 命令的输出所示。

```
$ mkfifo fifo1
$ touch greeting
$ ls -i fifo1 greeting
$ ls -l fifo1 greeting
prw-r--r-- 1 sarwar faculty 0 Apr 18 17:42 fifo1
-rw-r--r-- 1 sarwar faculty 0 Apr 18 17:42 greeting
$ du fifo1 greeting
0 fifo1
1 greeting
$ cat > greeting
Hello, world!
$ cat greeting > fifo1 &
[1] 10044
$ ls -l fifo1 greeting
prw-r--r-- 1 sarwar faculty 0 Apr 18 17:42 fifo1
-rw-r--r-- 1 sarwar faculty 14 Apr 18 17:43 greeting
$ du fifo1 greeting
0 fifo1
9 greeting
$ cat fifo1
Hello, world!
[1]+ Done cat greeting > fifo1
$ du fifo1 greeting
0 fifo1
9 greeting
$
```

## EXERCISE 20.2

在你的 UNIX 系统上重现这些 shell 会话。它们产生相同的结果吗？如果不是，列出我们会话结果与你的会话结果之间的差异。

你可以使用 `mknod()`、`mknodat()`、`mkfifo()` 或 `mkfifoat()` 系统调用来创建 FIFO。然而，`mknod()` 和 `mknodat()` 系统调用需要超级用户权限。这些系统调用的主要目的是创建特殊文件，但也可以用来创建 FIFO。`mkfifo()` 和 `mkfifoat()` 调用最终会调用 `mknod()` 系统调用。一旦创建了 FIFO，你可以使用 `open()`、`read()`、`write()` 和 `close()` 系统调用通过多个读取器和写入器进程对其进行 I/O。最后一个使用 FIFO 的进程，通常是读取器进程，关闭 FIFO 并使用 `unlink()` 系统调用将其从文件系统中删除。因为多个进程可以写入 FIFO，所以 UNIX 内核确保每个进程写入的最多 `PIPE_BUF` 字节的数据是原子写入的并且不会交错。`PIPE_BUF` 在 Solaris 上定义在 `/usr/include/sys/param.h` 中为 5120 字节，在 BSD 上定义在 `/usr/include/sys/syslimits.h` 中为 512 字节。

通道。我们主要在示例程序中使用 `mkfifo()` 调用。以下是 `mkfifo()` 和 `mkfifoat()` 系统调用的简要说明。

```
#include <sys/types.h>
#include <sys/stat.h>
int mkfifo(const char *path, mode_t mode);
int mkfifoat(int fd, const char *path, mode_t mode);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

`mkfifo()` 创建一个名为 `path` 参数指定的 FIFO，其访问权限由 `mode` 参数指定。与其他类型的文件一样，访问权限受当前 `umask` 限制。在 `mkfifoat()` 系统调用中，`path` 参数相对于与文件描述符 `fd` 关联的目录，而不是用户的当前工作目录。如果 `fd` 参数为 `AT_FDCWD`，则 `mkfifoat()` 调用的行为与 `mkfifo()` 调用相同。

`mkfifo()` 和 `mkfifoat()` 调用可能失败的原因大多与 `creat()` 和 `open()` 系统调用可能失败的原因相同，如第 18.8.1 节所述并列于表 18.4 中。这些调用失败的几个额外原因列于表 20.7 中。

未完全打开用于 I/O 的 FIFO 的行为与处于相同条件下的管道相似。对没有进程打开用于读取的 FIFO 的写入会导致写入进程收到 `SIGPIPE` 信号。当最后一个写入 FIFO 的进程关闭它时，会向读取进程发送 `eof`。

我们现在讨论一个示例客户端-服务器模型，以说明 FIFO 用于同一台机器上不相关进程之间 IPC 的使用。图 20.6 显示了客户端和服务器进程的算法。

以下是实现此客户端-服务器模型的 `fifo.h`、`client.c` 和 `server.c` 文件。

```
% cat fifo.h
#include <string.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <sys/errno.h>
```

### TABLE 20.7 Reasons for the mkfifo() and mkfifoat() System Calls to Fail

| 失败原因 | errno 值 |
|---|---|
| 要创建 FIFO 的目录没有写权限，或路径前缀中的某个组件目录不可搜索 | `EACCES` |
| `path` 中命名的 FIFO 已存在 | `EEXIST` |
| 对于 `mkfifoat()` 调用，`fd` 参数既不是 `AT_FDCWD` 也不是用于搜索的有效描述符且 `path` 参数不是绝对路径名 | `EBADF` |
| 对于 `mkfifoat()` 调用，`fd` 参数既不是 `AT_FDCWD` 也不是用于目录的有效描述符且 `path` 参数不是绝对路径名 | `ENOTDIR` |

# 服务器进程

# 客户端进程

| Server process | Client process |
|---|---|
| 1. 创建两个 FIFO，`FIFO1` 和 `FIFO2` | 1. 打开 `FIFO1` 用于写入，`FIFO2` 用于读取 |
| 2. 打开 `FIFO1` 用于读取，`FIFO2` 用于写入 | 2. 通过 `FIFO1` 向服务器写入 "Hello, world!" |
| 3. 通过 `FIFO1` 从客户端读取 "Hello, world!" | 3. 读取 `FIFO2` 中来自服务器的消息 |
| 4. 通过写入标准输出将此消息显示在屏幕上 | 4. 通过写入标准输出将此消息 "Hello, class!" 显示在屏幕上 |
| 5. 通过 `FIFO2` 向客户端写入 "Hello, class!" | 5. 关闭 `FIFO1` 和 `FIFO2` |
