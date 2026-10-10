
/* Found a directory, but ignore . and .. */

if (strcmp(".", entry->d_name) == 0 ||
    strcmp("..", entry->d_name) == 0)
    continue;

printf("%s\n", entry->d_name);

/* Recurse at a new indent level */
printdir(entry->d_name, depth+4);

} else printf("%*s%s\n", depth, entry->d_name);

}

chdir("..");
}

现在让我们移动到主函数：

```c
int main()
{
    printf("Directory scan of /home:\n");
    printdir("/home",0);
    printf("done.\n");
    exit(0);
}
```

程序产生的输出如下所示（为了简洁起见进行了编辑）：

```
$ printdir
Directory scan of /home:
iel/
.Xdefaults
.Xmodmap
.Xresources
.bash_history
.bashrc
.kde/
share/
apps/
konqueror/
dirtree/
public_html.desktop
toolbar/
bookmarks.xml
kong_history
kdisplay/
color-schemes/
BLP3/
Gnu_Public_License
chapter04/
argopt.c
args.c
chapter03/
file.out
mmap.c
printdir
done.
```

## 第 3 章

### 工作原理

大部分操作都在 `printdir` 函数中完成，我们将重点这里。在通过 `opendir` 进行目录是否存在存在的初始错误检查后，`printdir` 会调用 `chdir` 进入指定的目录。如果 `readdir` 返回的项不为空，程序将检查该项是否为目录。如果不是目录，它将带有缩进深度地打印该文件项。

如果该项是一个目录，我们就会遇到一点点递归。在忽略了 `.` 和 `..`（当前目录和父目录）后，`printdir` 函数会通过相同的过程再次调用自己。它是如何退出这些循环的？一旦 `while` 循环结束，`chdir("..")` 调用将将它带回目录树的上一层，之前的列表操作就可以继续。调用 `closedir(dp)` 可以确保打开的流数量不会超过所需的范围。

为了在第 4 章对 Linux 环境进行简要讨论，让我们来看看如何让该程序更具通用性。该程序目前是局限的，因为它是针对 `/home/neil` 目录的。通过以下更改，我们可以将其转换为更有实用的目录浏览器：

```c
int main(int argc, char* argv[]) {
    char *topdir = ".";
    if (argc >= 2)
        topdir=argv[1];
    printf("Directory scan of %s\n",topdir);
    printdir(topdir,0);
    printf("done.\n");
    exit(0);
}
```

### 操作文件

我们修改了三行并增加了五行，但现在它是一个带有可选目录名称参数的通用工具，该参数默认为当前目录。你可以使用以下命令运行它：

```bash
$ printdir2 /usr/local | more
```

输出将分页显示，以便用户翻阅输出。因此，用户就拥有了一个方便的小型通用目录树浏览器。只需花费极少精力，你就可以添加空间使用统计、限制显示深度等功能。

### 错误

正如我们看到的，本章描述的许多系统调用和函数可能会因为多种原因而失败。当它们失败时，会通过设置外部变量 `errno` 的值来指示失败的原因。许多不同的库使用此变量作为报告问题的标准方式。必须重复强调，程序必须在出现问题的函数之后立即检查 `errno` 变量，因为即使该函数本身没有失败，也可能被下一个调用的函数覆盖。

错误的值和含义列在头文件 `errno.h` 中。它们包括：

- `EPERM`: 操作不允许许可
- `ENOENT`: 无此类文件或目录
- `EINTR`: 系统调用被中断
- `EIO`: I/O 错误
- `EBUSY`: 设备或资源忙忙
- `EEXIST`: 文件存在
- `EINVAL`: 无效参数
- `EMPFILE`: 打开的文件太多了
- `ENODEV`: 无此类设备
- `EISDIR`: 是目录
- `ENOTDIR`: 不是目录

有两个在错误发生时报告错误的很有用函数：`strerror` 和 `perror`。

### `strerror`

`strerror` 函数将错误号映射为描述发生的错误类型的字符串。这对于记录错误情况很有用。

语法如下：

```c
#include <string.h>
char *strerror(int errnum);
```

### `perror`

错误函数也将当前报告的错误映射为字符串，并将其打印到标准错误流。该字符串前面是消息，后面跟着冒号。语法如下：

```c
#include <stdio.h>
void perror(const char *s);
```

例如：

```c
perror("program");
```

### `/proc` 文件系统

在本章早些时候我们提到 Linux 将许多内容视为文件。`/proc` 目录中的项用于访问硬件。许多驱动程序可以在此处配置。例如，硬盘控制器可能在此配置。网络卡可能在此报告状态。系统调用可以在此处获取信息。应用程序可以读取这些文件以获取参数。`/proc` 目录中的项包含了内核的各种信息。`/proc` 目录中的文件通常是动态生成的。在许多情况下，文件可以直接读取并提供状态信息。例如，`/proc/cpuinfo` 提供了可用处理器的详情。

同样，`/proc/meminfo` 和 `/proc/version` 分别提供内存使用和内核版本的信息。

# 第3章

MemFree: 279804 kB
MemShared: 0 kB
Buffers: 8136 kB
Cached: 130864 kB
SwapCached: 0 kB
Active: 101208 kB
Inactive: 106056 kB
HighTotal: 0 kB
HighFree: 0 kB
LowTotal: 279804 kB
SwapTotal: 136512 kB
SwapFree: 136512 kB
BigFree: 0 kB

```bash
$ cat /proc/version
Linux version 2.4.19-4GB (root@Pentium.sude) (gcc version 3.2) #1 Wed Nov 27
00:56:40 UTC 2002
```

文件提供的信息是在读取该文件时生成的。稍后重新读取 mininfo 文件将获得数秒级的结果。

关于特定内核函数的更多信息可以在 `/proc` 的子目录中找到。例如，你可以从 `/proc/net/socketstat` 获取网络套接使用统计信息：

```bash
$ cat /proc/net/socketstat
sockets: used 246
TCP: inuse 200 orphan 0 tw 0 alloc 22 mem 11
UDP: inuse 3
RAW: inuse 0
FRAG: inuse 0 memory 0
```

某些 `/proc` 条目既可以读取也可以写入。例如，正在运行的程序同时可以打开的文件总数是一个 Linux 内核参数。可以在 `/proc/sys/fs/file-max` 读取当前值：

```bash
$ cat /proc/sys/fs/file-max
52428
```

在这里，该值设置为 52,428。如果我们需要增加此值，可以通过向同一个文件写入来实现。如果我们正在运行某些特殊应用程序，例如使用许多表的数据库系统——这些系统需要同时打开许多文件——我们可能需要这样做。

> 写入 `/proc` 文件需要超级用户权限。在写入 `/proc` 文件时需要小心；写入不适当的值可能会导致严重问题。

要将系统范围的文件句柄限制增加到 60,000，我们只需将新限制写入 `file-max` 文件即可：

```bash
# echo 60000 > /proc/sys/fs/file-max
```

### 操作文件

现在，当我们重新读取文件时，我们看到了新值：

```bash
$ cat /proc/sys/fs/file-max
60000
```
