
在前面的示例和第 8 章中，我们有时会切换到超级用户，以演示其工作原理。如果你在一个多用户系统上没有超级用户权限，你将无法完全复制这些示例。

![](img/902515e97eef28cac8083866e00a6f4c_158_0.png)

![](img/902515e97eef28cac8083866e00a6f4c_158_1.png)

## 4.8 `umask` 函数

现在我们已经描述了与每个文件相关的权限位，我们可以描述与每个进程相关的创建创建掩码（file creation mask）。

`umask` 函数设置进程的文件创建掩码并返回上一个值。（这是少数几个没有错误返回值的函数之一）。

```c
#include <sys/stat.h>

mode_t umask(mode_t cmask);
```

返回：之前的文件创建掩码

`cmask` 参数是由图 4.6 中的九个常量中的任意一个进行位或形成的，如 `S_IRUSR`、`S_IWUSR` 等。

每当进程创建新文件或目录时，就会使用文件创建掩码。（请回想第 3.3 节和 3.4 节关于 `open` 和 `create` 函数的描述。它们都接受一个指定新文件访问权限位的 `mode` 参数。）我们在第 4.20 节中描述了如何创建一个新目录。文件创建掩码中开启的任何位在文件的模式中都会关闭。

### 示例

图 4.9 中的程序创建了两个文件，一个 `umask` 为 0，另一个 `umask` 禁用了组权限和其他权限位。

如果我们运行这个程序，就可以看到权限位是如何被设置的。

```bash
$ umask      首次打印当前的文件创建掩码
002
./a.out
$ ls -l foo
-rw------- 1 sar      0 Dec 7 21:20 bar
-rw-rw-rw- 1 sar      0 Dec 7 21:20 foo
$ umask      查看文件创建掩码是否发生了变化
002
```

# 图 4.9. `umask` 函数示例

```c
#include "apue.h"
#include <fcntl.h>

#define RWRWRWR (S_IRUSR|S_IWUSR|S_IRGRP|S_IWGRP|S_IROTH|S_IOWTH)

int
main(void)
{
    umask(0);
    if (create("foo", RWRWRWR) < 0)
        err_sys("create error for foo");
    umask(S_IRGRP | S_IWGRP | S_IROTH | S_IOWTH);
    if (create("bar", RWRWRWR) < 0)
        err_sys("create error for bar");
    exit(0);
}
```

大多数 UNIX 用户从不处理 `umask` 值。它通常在登录时由 shell 的启动文件设置一次，并且永远从不更改。在编写创建文件的程序时，如果我们想确保特定的访问权限位被启用，我们必须在进程运行时修改 `umask` 值。如果我们想确保任何人都能读取某个文件，我们应该将 `umask` 设置为 0。否则，在我们进程运行期间生效的 `umask` 值可能会导致权限位被关闭。

在这个示例中，我们使用 shell 的 `umask` 命令在运行程序前后打印文件创建掩码。这显示了更改进程的文件创建创建不会影响父进程的掩码。所有的 shell 都有内置的 `umask` 命令，我们可以用来设置或打印当前的文件创建掩码。用户可以使用 `umask` 值来控制他们创建的文件的默认权限。该值以八进制表示，其中一个位表示被掩码的权限，如图 4.10 所示。可以通过设置相应的位来拒绝权限。一些常见的 `umask` 值如 `002` 防止组成员写入文件，`022` 防止组成员和其他写入文件，`027` 防止组成员读取、写入或执行文件。

# 图 4.10. `umask` 权限位

| 掩码位 | 含义 |
|---|---|
| `400` | 用户读取 |
| `200` | 用户写入 |
| `100` | 用户执行 |
| `040` | 组读取 |
| `020` | 组写入 |
| `010` | 组执行 |
| `004` | 其他读取 |
| `002` | 其他写入 |
| `001` | 其他执行 |

Single UNIX 规范要求 shell 支持 `umask` 命令的符号格式。与八进制格式不同，符号格式指定哪些权限是被允许的（即在文件创建掩码中清除），而不是哪些是被拒绝的（即在文件创建掩码中设置）。比较命令的两种形式：

- `umask 002`：首次打印当前的文件创建掩码
- `umask -S`：打印符号格式
- `umask 027`：更改文件创建掩码
- `umask -S`：打印符号格式

![](img/902515e97eef28cac8083866e00a6f4c_158_0.png)

![](img/902515e97eef28cac8083866e00a6f4c_158_1.png)

## 4.9. `chmod` 和 `fchmod` 函数

这两个函数允许我们更改现有文件的访问权限。

```c
#include <sys/stat.h>

int chmod(const char *pathname, mode_t mode);
int fchmod(int file, mode_t mode);
```

成功返回 `0`，错误返回 `1`。`chmod` 函数作用于指定的文件，而 `fchmod` 函数作用于已经打开的文件。要更改文件的权限位，进程的有效用户 ID 必须等于文件的者 ID，或者进程必须具有超级用户权限。`mode` 指定为图 4.11 常量的位或。

# 图 4.11. 来自 `<sys/stat.h>` 的 `chmod` 函数常量

| mode | 描述 |
|---|---|
| `S_ISUID` | 执行时设置用户 ID |
| `S_ISGID` | 执行时设置组 ID |
| `S_ISVTX` | 滞留位 (sticky bit) |
| `S_IRWXU` | 用户（所有者）读、写、执行 |
| `S_IRUSR` | 用户（所有者）读取 |
| `S_IWUSR` | 用户（所有者）写入 |
| `S_IXUSR` | 用户（所有者）执行 |
| `S_IRWXG` | 组读、写、执行 |
| `S_IRGRP` | 组读取 |
| `S_IWGRP` | 组写入 |
| `S_IXGRP` | 组执行 |
| `S_IRWXO` | 其他（世界）读、写、执行 |
| `S_IROTH` | 其他（世界）读取 |
| `S_IWOTH` | 其他写入 |
| `S_IXOTH` | 其他（执行） |

注意图 4.11 中的九项内容是图 4.6 中的文件访问权限位。我们添加了设置 ID 常量（`S_ISUID` 和 `S_ISGID`）。滞留位 `S_ISVTX` 不属于 POSIX.1。它在 Single UNIX 规范中定义为 XSI 扩展。下一节将描述其用途。

### 示例

回想编写图 4.9 程序演示 `umask` 函数时 `foo` 和 `bar` 文件的最终状态：

```bash
$ ls -l foo bar
-rw-r--r-- 1 sar 0 Dec 7 21:20 bar
-rw-rw-rw- 1 sar 0 Dec 7 21:20 foo
```

图 4.12 中的程序修改了这两个文件的模式。运行图 4.12 后，我们看到两个文件的最终状态为：

```bash
$ ls -l bar
-rw-r--r-- 1 sar 0 Dec 7 21:20 bar
```

在这个示例中，我们将文件的权限设置为了绝对值，而不考虑权限位。对于该文件，我们将权限设置为其当前状态。为了做到，我们首先调用 `stat` 获取当前权限，然后对其进行修改。我们显式地开启了组 ID 位并关闭了组执行位。在 Solaris 上，`ls` 命令显示 `I` 而不是 `S`，表示文件锁定已启用。这仅适用于普通文件，我们将在第 14.3 节中进行讨论。最后，当我们运行 `i-node` 时，`ls` 列出的时间和日期没有变化。我们见图 4.12。

# 图 4.12. `chmod` 函数示例

```c
#include "apue.h"

int
main(void)
{
    struct stat stat;
    /* 开启组-ID 并关闭组-执行 */
    if (stat("foo", &stat) < 0)
        err_sys("stat error for foo");
    if (chmod("foo", stat.st_mode & ~S_IXGRP | S_ISGID) < 0)
        err_sys("chmod error for foo");
    /* 设置绝对模式为 "rw-r--r-" */
    if (chmod("bar", S_IRUSG | S_IWUSG | S_IRGRP | S_IROTH) < 0)
        err_sys("chmod error for bar");
    exit(0);
}
```

- 新创建的文件的组 ID（group ID）可能是调用进程并不所属的组。回想第 4.6 节，新文件的组 ID 有可能是父目录的组 ID。如果新文件的组 ID 不等于进程的有效组 ID（effective group ID）或该进程的附加 ID（supplementary IDs）之一，且该进程没有超级用户权限，那么设置组 ID（set-group ID）将自动关闭。这防止了用户创建一个由其不所属的组拥有的设置组 ID 文件。

`FreeBSD 5.2.1`、`Linux 2.4.22`、`Mac OS X 10.3` 和 `Solaris 9` 增加了另一项安全特性，试图防止某些保护位被误用。如果进程在没有超级用户权限的情况下写入文件，则设置用户 ID（set-user-ID）位和设置组 ID（set-group-ID）位将自动关闭。恶意用户即使发现了一个他们可以写入的设置组 ID 或设置用户 ID 的文件，尽管他们可以修改该文件，但他们也会失去该文件的特殊权限。

![](img/902515e97eef28cac8083866e00a6f4c_166_0.png)

## 4.10. 粘滞位 (Sticky Bit)

`S_ISVTX` 位有一个有趣的历史。在早于需求分页的 UNIX 系统版本中，该位被称为粘滞位（sticky bit）。如果对一个可执行程序文件设置了该位，那么在程序第一次执行时，当进程终止，程序的文本副本会被保存到交换区（swap area）中。（文本部分是机器指令。）这使得程序在下次执行时加载到内存的速度更快，因为交换区被处理为一个连续文件，而普通的 UNIX 系统中的数据块是随机分布的。粘滞位通常设置在常用应用程序上，例如编辑器和 C 语言编译器。交换区耗尽时，能够包含的粘滞文件数量是有限制的，但这是一种实用的技术。“粘滞”（sticky）这个名字的由来是因为在系统重启之前无法删除该文件。后来的 UNIX 系统版本将其称为“保存文本位”（saved-text bit）；对于如今的 UNIX 系统，大多数系统拥有虚拟内存系统和更快的文件系统，这种技术的性已经消失了。

在现代系统中，粘滞位的使用被扩展了。单 Unix 规范（Single Unix Specification）允许对目录设置该位。如果对目录设置了该位，只有当用户对该目录具有写权限并满足以下条件时，才能删除或重命名目录中的文件：

- 拥有该文件
- 拥有该目录
- 是超级用户

目录 `/tmp` 和 `/var/spool/ucpublic` 是粘滞位目录的典型候选，任何用户通常可以在其中创建文件。这两个目录的权限通常对所有人（用户、组和其他）都是读、写、执行权限。但用户不应该删除或重命名他人拥有的文件。

> 保存文本位（saved-text bit）不是 POSIX.1 的一部分。它是对单 Unix 规范定义的定义的 POSIX.1 功能的 OSI 扩展，并被 `FreeBSD 5.2.1`、`Linux 2.4.22`、`Mac OS X 10.3` 和 `Solaris 9` 支持。

`Solaris 9` 在普通文件上设置粘滞位时，赋予了其特殊含义。在这种情况下，如果没有设置任何执行位，操作系统将不会缓存文件的内容。

## 4.11. `chown`, `fchown`, `lchown` 函数

`chown` 函数允许更改文件的用户 ID（user ID）和组 ID（group ID）。

```c
#include <unistd.h>

int chown(const char *pathname, uid_t owner, gid_t group);
int fchown(int fd, uid_t owner, gid_t group);
int lchown(const char *pathname, uid_t owner, gid_t group);
```

所有函数返回：`0` 表示成功，`1` 表示错误

这三个函数的操作相似，除非引用的函数是符号链接。在这种情况下，`lchown` 修改的是符号链接的所有者，而不是符号链接指向的文件。

> `lchown` 函数是单 Unix 规范中定义的 POSIX.1 功能的 XS 扩展。因此，所有的 Unix 实现都扩展提供了该函数。

如果参数或组中的任意一个为 `-1`，则对应的 ID 保持不变。

从历史上看，基于 BSD 的系统执行只有超级用户才能更改文件所有权的限制。这是为了防止用户通过赠送文件来规避任何磁盘配额限制。然而，System V 允许任何用户更改任何文件的所有权。

POSIX.1 允许这两种形式的操作，取决于 `_POSIX_CHOWN_RESTRICTED` 的值。

在 `Solaris 9` 中，这是一个配置选项，其默认执行该限制。`FreeBSD 5.2.1`、`Linux 2.4.22` 和 `OS X 10.3` 允许这种操作。

回想第 2.6 节，`_POSIX_CHOWN_RESTRICTED` 常量可以在头文件 `<unistd.h>` 中可选定义，并且可以使用 `pathconf` 函数或 `fpathconf` 函数随时查询。此调用也可以定义在引用的文件上；它可以根据文件系统来启用或禁用。我们将使用短语 "_POSIX_CHOWN_RESTRICTED 生效”来表示它适用于我们正在讨论的特定文件，无论该常量是否启用。

`wc(1)` 命令配合 `-c` 选项用于统计文件中字符（字节）的数量。

如果我们使用 `cat(1)` 等工具对该文件进行复制，所有的空洞都将被写入为实际的 0 字节：

```bash
$ cat core > core.copy
-rw-r--r-- 1 sar 8483248 Nov 18 12:18:core
-rw-r--r-- 1 sar 8483248 Nov 18 12:27:core.copy
$ du -s core
272 core
16592 core.copy
```

在这里，新文件实际使用的字节数是 8,495,104 (512 x 16,592)。此大小与 `ls` 报告的大小之间的差异在于文件系统用于存储指向实际数据块指针所占用的块数。

感兴趣的读者可以参阅 [1986] 的第 4.2 节，McKusik 等人 [1996] 的第 7.2 节和 7.3 节（或 McKusik 和 Neville-Neil [2005] 的第 8.2 节和 8.3 节），以及 Mauro 和 McDououghall [2001] 的第 14.2 节，获取关于文件物理布局的更多细节。

![](img/902515e97eef28cac8083866e00a6f4c_172_0.png)

![](img/902515e97eef28cac8083866e00a6f4c_172_1.png)

## 4.13. 文件截断

有时我们需要通过切掉文件末尾的数据来截断文件。清空文件（可以通过打开文件时使用 `O_TRUNC` 标志来实现）是截断的一种特殊情况。

```c
#include <unistd.h>

int truncate(const char *pathname, off_t length);
int truncate(int fd, off_t length);
```
