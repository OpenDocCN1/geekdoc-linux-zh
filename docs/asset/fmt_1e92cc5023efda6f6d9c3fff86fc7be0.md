
# 4.2 stat 函数

三者返回：`0` 表示成功，错误时返回。

给定路径名，`stat` 函数返回关于文件的信息结构。`lstat` 函数与 `stat` 类似，但当命名文件是符号链接时。然而，当命名文件是符号链接时，`lstat` 返回符号链接本身的信息而不是引的文件。（我们在 4.21 遍历目录时需要 `lstat`。我们在 4.16 中详细描述符号链接）

第二个参数指向我们必须满足的结构指针。结构字段由 `buf` 填充。结构的定义在实现之间可能不同，但可能如下

```c
struct {
  mode_t st_mode;      /* 文件类型和权限 */
  ino_t st_ino;       /* 节点号（序列号） */
  dev_t st_dev;       /* 设备号（文件系统） */
  dev_t st_rdev;      /* 特殊文件的设备号 */
  nlink_t st_nlink;   /* 链接数 */
  uid_t st_uid;       /* 所有者用户 ID */
  gid_t st_gid;       /* 所有者组 ID */
  off_t st_size;      /* 字节大小，针对普通文件 */
  time_t st_atime;    /* 最后访问时间 */
  time_t st_mtime;    /* 最后修改时间 */
  time_t st_ctime;    /* 最后状态更改时间 */
  blkize_t st_blksize;  /* 最佳 I/O 块大小 */
  blkcnt_t st_blocks;  /* 分配的磁盘块数 */
};
```

请注意，每个成员都由一种基本系统数据类型标识（见第 2.8 节）。我们将遍历该结构体的每个成员，以检查文件的属性。

`stat` 函数最大的用户可能是 `ls -l` 命令，它用于获取文件的所有信息。

## 4.3. 文件类型

到为止，我们讨论了不同类型的的文件：普通文件和目录。UNIX 系统上的大多数文件都是普通文件或目录，但还有其他类型的文件。这些类型包括：

-   普通文件（Regular file）：最常见的文件类型，包含某种形式的数据。UNIX 内核不区分这些数据是文本还是二进制。对普通文件内容的任何解释都交给处理该文件的应用程序。
-   二进制可执行文件：这是一个例外。为了执行一个程序，内核必须理解其格式。任何二进制可执行文件都符合内核用于识别在何处加载程序文本和数据的格式。
-   目录文件（Directory file）：包含其他文件名和指向信息的指针的文件。任何对目录文件具有读权限的进程都可以读取目录内容，但只有内核可以写入目录文件。进程必须使用本章定义的函数对其进行更改。
-   块特殊设备文件（Block special）：一种为磁盘等设备提供固定大小单位的缓冲 I/O 访问的文件类型。
-   字符特殊设备文件（Character special）：一种提供变长度单位的非缓冲 I/O 访问的文件类型。系统上的所有设备要么是块特殊文件，要么是字符文件。
-   FIFO：一种用于进程间通信的文件类型。它有时被称为命名管道（named pipe）。我们在第 15.5 节中描述 FIFO。
-   套接字（Socket）：一种用于进程间网络通信的文件类型。套接字也可用于单主机进程间的非网络通信。我们在第 6 章中使用套接字进行进程间通信。
-   符号链接（Symbolic link）：指向另一个文件的文件类型。我们在第 4.16 节中详细讨论符号链接。

文件类型编码在 `stat` 结构的 `st_mode` 成员中。我们可以通过图 4.1 所示的宏确定文件类型。每个宏的参数都是 `stat` 结构中的 `st_mode` 成员。

### 图 4.1. `<sys/stat.h>` 中的文件类型宏

| 宏 | 文件类型 |
|---|---|
| `S_ISREG()` | 普通文件 |
| `S_ISDIR()` | 目录文件 |
| `S_ISCHR()` | 字符特殊文件 |
| `S_ISBLK()` | 块特殊文件 |
| `S_ISFIFO()` | 管道或 FIFO |
| `S_ISLNK()` | 符号链接 |
| `S_ISSOCK()` | 套接字 |

POSIX.1 允许实现表示进程间通信 (IPC) 对象（如消息队列和信号量）以及文件。图 4.2 所示的宏允许我们从 `stat` 结构确定 IPC 对象的类型。以 `st_mode` 成员作为参数，每个宏与图 4.1 中的宏不同之处在于它们的参数是指向 `stat` 结构的指针。

### 图 4.2. `<sys/stat.h>` 中的 IPC 类型宏

| 宏 | 对象类型 |
|---|---|
| `S_ISISMQ()` | 消息队列 |
| `S_TYPESSEM()` | 信号量 |
| `S_TYPESHM()` | 共享内存对象 |

消息队列、信号量共享内存对象将在第 15 章中讨论。然而，本书中讨论的 UNIX 系统实现没有一个是将这些对象表示为文件。

### 示例

图 4.3 中的程序打印每个命令行参数的文件类型。

图 4.3 的示例输出如下：

```
$ /a.out /etc/passwd /etc /dev/initcl /dev/log/dev/tty \
> /dev/scsi/host0/bus0/target/lun0/cd /dev/cdrom
/etc/passwd: regular
/etc: directory
/dev/initcl: fifo
/dev/log: socket
/dev/tty: character special
/dev/scsi/host0/bus0/target/lun0/cd: block special
/dev/cdrom: symbolic link
```

（在这里，我们在第一个命令的末尾显式输入了反斜杠，告诉 shell 我们想在另一行继续输入命令。shell 在下一行用其次级提示符 `>` 提示我们）我们特意使用了 `stat` 函数而不是 `lstat` 函数来检测符号链接。如果我们使用 `stat` 函数，将永远看不到符号链接。

要在 Linux 系统上编译此程序，我们必须定义 `GNU_SOURCE` 以包含 `S_ISSOCK` 宏的定义。

### 图 4.3. 打印每个命令行参数的文件类型

```c
#include "apue.h"

int
main(int argc, char *argv[])
{
    int i;
    struct stat buf;
    char *ptr;
    int err_ret;

    for (i = 1; i < argc; i++) {
        if ((err_ret = lstat(argv[i], &buf)) < 0) {
            perror(argv[i]);
            continue;
        }
        if (S_ISREG(buf.st_mode)) {
            ptr = "regular";
        } else if (S_ISDIR(buf.st_mode)) {
            ptr = "directory";
        } else if (S_ISCHR(buf.st_mode)) {
            ptr = "character special";
        } else if (S_ISBLK(buf.st_mode)) {
            ptr = "block special";
        } else if (S_ISFIFO(buf.st_mode)) {
            ptr = "fifo";
        } else if (S_ISLNK(buf.st_mode)) {
            ptr = "symbolic link";
        } else if (S_ISSOCK(buf.st_mode)) {
            ptr = "socket";
        } else {
            ptr = "unknown";
        }
        printf("%s: %s\n", argv[i], ptr);
    }
    exit(0);
}
```

## 4.4. 文件所有者和组

仅允许超级用户（superuser）执行。因为运行设置 set-user-ID 为其他用户的进程假设了额外的权限，因此必须小心编写。我们将在第 8 章中详细讨论这些类型的程序。

回到 `stat` 函数，set-user-ID 位和 set-group-ID 位包含在文件的 `st_mode` 值中。这两个位可以与常量 `S_ISUID` 和 `S_ISGID` 进行测试。

## 4.5. 文件访问权限

`st_mode` 值还包含文件的访问权限位。当我们说这些时，指的是我们之前描述的任何文件类型。所有文件类型、字符设备文件等都有权限。许多人认为只有普通文件才有访问权限。

每个文件有九个权限位，分为三类。如图 4.6 所示。

### 图 4.6. 来自 `<sys/stat.h>` 的九个文件访问权限位

| `st_mode` | 意义 |
| --- | --- |
| `S_IRUSR` | 用户读 |
| `S_IWUSR` | 用户写 |
| `S_IXUSR` | 用户执行 |
| `S_IRGRP` | 组读 |
| `S_IWGRP` | 组写 |
| `S_IXGRP` | 组执行 |
| `S_IROTH` | 其他读 |
| `S_IWOTH` | 其他写 |
| `S_IXOTH` | 其他执行 |

图 4.6 中前三行的“user”指的是文件的所有者。`chmod(1)` 命令通常用于修改这些权限位，它允许我们使用 `u` 代表所有者，`g` 代表组，`o` 代表其他。有些书籍将这三者称为所有者、组和世界；然而，`chmod` 命令使用 `o` 来表示其他。我们将使用 `user`、`group` 和 `other` 以与 `chmod` 命令保持一致。

图 4.6 中的三类（读、写、执行）被不同的函数以各种方式读取。我们在这里对它们进行总结，并在执行实际函数时再回到它们。

- 第一条规则是，每当我们通过名称打开任何文件时，必须在名称中提到的每个目录中（包括当前目录，如果可能）执行权限。这就是为什么目录的执行权限位通常被称为搜索位（search bit）。

例如，为了打开 `/usr/include/stat.h`，我们需要在 `/` 目录具有执行权限，`/usr` 目录具有执行权限以及 `/usr/include` 目录具有执行权限。然后，我们需要文件本身的访问权限，这取决于我们尝试如何读取它：只读、读写等。

如果当前目录是 `/usr/include`，那么我们需要在当前目录具有执行权限以打开文件 `stdio.h`。这是一个打开未特意提及的当前目录的例子。它与打开文件 `/stdio.h` 是相同的。

注意，目录的读权限和目录的执行权限意味着不同的含义。读权限允许我们读取目录，获取其中所有文件名的列表。执行权限允许我们在当该目录作为我们尝试访问的路径的组成部分时，通过该目录。（我们需要搜索目录以查找特定的文件名）。

另一个隐式目录权限的例子是，如果在第 8.10 节描述的 `PATH` 环境变量指定了一个没有启用执行权限的目录。在这种情况下，shell永远无法在那里找到可执行文件。

- 文件的读权限决定了我们是否可以只读打开文件：`open` 函数的 `O_RDONLY` 和 `O_RDWR` 标志。

- 文件的写权限决定了我们是否可以写打开文件：`open` 函数的 `O_WRONLY` 和 `O_RDWR` 标志。

- 我们必须拥有文件的权限才能在 `open` 函数中指定 `O_TRUNC` 标志。

- 除非我们在包含它的目录下具有写权限和执行权限，否则我们无法在该目录下创建新文件。

- 如果我们想使用任何 `exec` 函数（第 8.10 节）执行文件，则该文件的执行权限必须开启。该文件也必须是一个普通文件。

内核在每次进程打开、创建或删除文件时执行的文件访问测试取决于文件的所有者（`st_uid` 和 `st_gid`）、进程的有效 ID（有效用户 ID 和有效组 ID）以及进程的补充组 ID。这两个 ID 是文件的属性，而进程的有效 ID 和补充组 ID 是进程的属性。内核执行的测试如下：

1. 如果进程的有效用户 ID 为 0（超级用户），则允许访问。这使得超级用户可以自由访问整个系统文件。

2. 如果进程的有效用户 ID 等于文件的所有者 ID（即进程拥有该文件），如果设置了适当的访问权限位，则允许访问。否则拒绝权限。适当的访问权限位是指：如果进程正在读取文件，则用户读位必须开启；如果进程正在写打开文件，则用户写位必须开启；如果进程正在执行文件，则用户执行位必须开启。

3. 如果进程的有效组 ID 或进程的某个补充组 ID 等于文件的组 ID，如果设置了适当的组访问权限位，则允许访问。否则拒绝权限。

4. 如果设置了其他用户权限位，则允许访问。否则拒绝权限。

## 4.6. 新文件和目录的所有权

当我们在第 3 章描述创建文件时，我们提到了用户 ID 和组 ID 是如何分配的。我们将在第 20 节查看创建目录。目录的所有权规则与新文件相同。

1. 文件的用户 ID 是进程的有效 ID。

2. 文件的组 ID 取决于它所在的目录。（FreeBSD 5.2.1 和 Mac OS 10.3 始终使用进程的组 ID）。

3. 在 Linux ext2 和 ext3 文件系统中，组 ID 被设置为目录的组 ID。该所有权将从该点向下传播。这在 Linux 的 `/var/spool/mail` 目录中就有应用。

4. 在 Linux 2.4.22 和 Solaris 9 下，我们必须启用组位，且 `mkdir` 函数会自动传播组 ID。

## 4.7. access 函数

正如我们之前描述，当我们打开文件时，内核根据有效用户和组 ID 执行其访问测试。有时进程需要根据真实用户和组 ID 测试访问性。当某人使用一个 set-user-ID 或 set-group-ID 进程被设置为 root 时，它仍然可以验证真实用户是否可以访问给定文件。`access` 函数基于真实用户和组 ID 进行测试。（将第 4.5 节末尾四个步骤中的“effective”替换为“real”）

```c
#include <unistd.h>
access(const char *pathname, int mode);
```

返回值：成功返回 0，错误时返回 1

`mode` 是图 4.7 所示任意常量的位或结果。

### 图 4.7. `access` 函数的模式常量，来自 `<unistd.h>`

| `mode` | 描述 |
| --- | --- |
| `R_OK` | 测试读权限 |
| `W_OK` | 测试写权限 |
| `X_OK` | 测试执行权限 |
| `F_OK` | 测试文件是否存在 |

### 示例

图 4.8 显示了 `access` 函数的使用。

以下是该程序的示例会话：

```
$ ls -l a.out
-rwxr-xr-x 1 15945 Nov 30 12:10 a.out
$ /a.out a.out
read access OK
open for reading OK
$ ls -l /etc/shadow
-rw------- 1 1315 Jul 17 2002 /etc/shadow
$ /a.out /etc/shadow
access error for /etc/shadow: Permission denied
open error for /etc/shadow: Permission denied
$ su
enter superuser password
Password:
# chmod u+a /etc/shadow
# /a.out /etc/shadow
read access OK
open for reading OK
# exit
$ /a.out /etc/shadow
access error for /etc/shadow: Permission denied
open for reading OK
```

在这个示例中，set-user-ID 程序演示了真实用户通常无法读取该文件，即使 `open` 操作会成功。

### 图 4.8. `access` 函数示例

```c
#include "apue.h"
#include <fcntl.h>

int
main(int argc, char *argv[])
{
    if (argc != 2)
        err_quit("usage: %s <pathname>", argv[0]);

    if (access(argv[1], R_OK) < 0)
        err_ret("access error for %s", argv[1]);
    else
        printf("read access OK\n");

    if (open(argv[1], O_RDONLY) < 0)
        err_ret("open error for %s", argv[1]);
    else
        printf("open for reading OK\n");

    exit(0);
}
```
