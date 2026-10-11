

在 GNU/Linux 上，`remove()` 使用 `unlink()` 系统调用删除文件，并使用 `rmdir()` 系统调用（本章稍后讨论）删除目录。（在较旧的、不使用 glibc 的 GNU/Linux 系统上，`remove()` 是 `unlink()` 的别名；这在目录上会失败。如果你有这类系统，最好升级它。）

## 5.1.6 符号链接

本章从讨论分区、文件系统和 inode 开始。我们还看到目录条目将名称与 inode 号关联起来。由于目录条目不包含其他信息，硬链接仅限于同一*文件系统*内的文件。这是必须的；没有办法区分一个文件系统中的 inode 2341 和另一个文件系统中的 inode 2341。以下是我们尝试时会发生的情况：

```bash
$ mount                                   *Show file systems in use*
/dev/hda2 on / type ext3 (rw)
/dev/hda5 on /d type ext3 (rw)
...
$ ls -li /tmp/message                   *Earlier example was on file system for /d*
228708 -rw-r--r-- 2 arnold  devel  19 May  4 15:51 /tmp/message
$ cat /tmp/message
Hi, how ya doin' ?
$ ls /bin/pwd                            *Current directory is on a different file system*
/d/home/arnold
$ ln /tmp/message .
Attempt the link
ln: creating hard link `./message' to `/tmp/message': Invalid cross-device link
```

大型系统通常有许多分区，既包括物理连接在本地磁盘上的分区，也包括远程挂载的网络文件系统。硬链接限于同一文件系统的这一限制带来不便，例如，如果某些文件或目录必须移到新位置，但旧软件使用了针对旧位置的硬编码文件名。

为了绕过这一限制，4.2 BSD 引入了*符号链接*。符号链接（也称为*软链接*）是一种特殊类型的文件（就像目录是一种特殊类型的文件一样）。文件的内容是被“指向”的文件的*路径名*。所有现代 Unix 系统，包括 Linux，都提供符号链接；事实上，它们现在是 POSIX 的一部分。

符号链接可以指向系统中的任何文件。它们也可以指向目录。这使得在地点之间移动目录变得很容易，只需在原始位置留下一个指向新位置的符号链接即可。

当处理文件名时，系统会注意到符号链接，并改为对目标文件或目录执行操作。使用 `ln` 的 `-s` 选项创建符号链接：

```bash
$ /bin/pwd
/home/arnold
$ ln -s /tmp/message ./.hello
$ cat .hello
Hi, how ya doin’ ?
$ ls -l hello
lrwxrwxrwx 1 arnold    12 May 4 16:41 hello -> /tmp/message
```

链接指向的文件不一定需要存在。系统会在运行时检测这种情况并做出相应的处理：

```bash
$ rm /tmp/message
$ cat .hello
cat: ./.hello: No such file or directory
$ echo hi again > hello
$ ls -l
-rw-r--r-    1 arnold    9 May 4 16:45 /tmp/message
$ cat /tmp/message
hi again
```

使用 `symlink( )` 系统调用创建符号链接：

```c
#include <unistd.h>
int symlink(const char *oldpath, const char *newpath);
```

`oldpath` 参数指定被指向的文件或目录的名称，而 `newpath` 是要创建的符号链接的名称。成功时返回值为 0，出错时为 -1；请参阅 `symlink(2)` 的手册页了解可能的 `errno` 值。

符号链接有其缺点：

- 它们占用额外的磁盘空间，需要单独的 inode 和数据块。硬链接只占用一个目录槽位。
- 它们增加了开销。内核需要更努力地解析包含符号链接的路径名。
- 它们可能会引入“循环”。考虑以下情况：

```bash
$ rm -f a b
$ ln -s a b
$ ln -s b a
$ cat a
cat: a: Too many levels of symbolic links
```

内核必须能够检测这种情况并产生错误消息。

- 它们很容易失效。如果你将目标文件移动到不同的位置或重命名它，符号链接就不再有效了。硬链接不会发生这种情况。

## 5.2 创建和删除目录

创建和删除目录很简单。不出所料，这两个系统调用分别是 `mkdir()` 和 `rmdir()`：

```c
#include <sys/types.h>          POSIX
#include <sys/stat.h>

int mkdir(const char *pathname, mode_t mode);
```

```c
#include <unistd.h>             POSIX

int rmdir(const char *pathname);
```

两者在成功时都返回 0，出错时返回 −1，并适当设置 `errno`。对于 `mkdir()`，`mode` 参数代表应用于目录的权限。它与第 4.6 节“创建文件”第 106 页中讨论的 `creat()` 和 `open()` 的 `mode` 参数完全类似。

两个函数都处理正在创建或删除目录中的 `.` 和 `..`。在目录可以被删除之前，它必须是空的；如果目录不为空，`errno` 会被设置为 ENOTEMPTY。（在这种情况下，“空”意味着目录仅包含 `.` 和 `..`。）

新目录，像所有文件一样，都会被分配一个组 ID 号。不幸的是，这如何工作很复杂。我们将讨论推迟到第 11.5.1 节“新文件和目录的默认组”，第 412 页。

两个函数*一次只处理一个目录级别*。如果 `/somedir` 存在且 `/somedir/sub1` 不存在，则 `mkdir("/somedir/sub1/sub2")` 会失败。长路径名中的每个组件都必须单独创建（因此 `mkdir` 有 −p 选项，参见 `mkdir(1)`）。

此外，如果 pathname 以 / 字符结尾，`mkdir()` 和 `rmdir()` 在某些系统上会失败，而在其他系统上会成功。下面的程序 `ch05-trymkdir.c` 演示了这两个方面。

```c
/* ch05-mkdir.c ---  Demonstrate mkdir() behavior.
    Courtesy of Nelson H.F. Beebe. */

#include <stdio.h>
#include <stdlib.h>
#include <errno.h>

#ifndef EXIT_SUCCESS
#define EXIT_SUCCESS 0
#endif

void do_test(const char *path)
{
    int retcode;

    errno = 0;
    retcode = mkdir(path, 0755);
    printf("mkdir(\"%s\") returns %d: errno = %d [%s]\n",
        path, retcode, errno, strerror(errno) );
}

int main(void)
{
    do_test("/tmp/t1/t2/t3/t4");
    do_test("/tmp/t1/t2/t3");
    do_test("/tmp/t1/t2");
    do_test("/tmp/t1");

    do_test("/tmp/u1");
    do_test("/tmp/u1/u2");
    do_test("/tmp/u1/u2/u3");
    do_test("/tmp/u1/u2/u3/u4");

    do_test("/tmp/v1/");
    do_test("/tmp/v1/v2/");
    do_test("/tmp/v1/v2/v3/");
    do_test("/tmp/v1/v2/v3/v4/");

    return (EXIT_SUCCESS);
}
```

以下是 GNU/Linux 下的结果：

```bash
$ ch05+mkdir
mkdir("/tmp/t1/t2/t3/t4") returns -1: errno = 2 [No such file or directory]
mkdir("/tmp/t1/t2/t3") returns -1: errno = 2 [No such file or directory]
mkdir("/tmp/t1/t2") returns -1: errno = 2 [No such file or directory]
mkdir("/tmp/t1") returns 0: errno = 0 [Success]
mkdir("/tmp/u1") returns 0: errno = 0 [Success]
mkdir("/tmp/u1/u2") returns 0: errno = 0 [Success]
mkdir("/tmp/u1/u2/u3") returns 0: errno = 0 [Success]
mkdir("/tmp/u1/u2/u3/u4") returns 0: errno = 0 [Success]
mkdir("/tmp/v1/") returns 0: errno = 0 [Success]
mkdir("/tmp/v1/v2/") returns 0: errno = 0 [Success]
mkdir("/tmp/v1/v2/v3/") returns 0: errno = 0 [Success]
mkdir("/tmp/v1/v2/v3/v4/") returns 0: errno = 0 [Success]
```

注意 GNU/Linux 接受尾部斜杠。并非所有系统都这样。

## 5.3 读取目录

在原始的 Unix 系统上，读取目录内容很容易。程序使用 `open()` 打开目录并直接读取二进制的 struct direct 结构，每次 16 个字节。以下代码片段来自 V7 `rmdir` 程序⁵的第 60–74 行。它展示了检查目录是否为空的逻辑。

```c
60	if (fd = open(name,0)) < 0) {
61		fprintf(stderr, "rmdir: %s unreadable\n", name);
62		++Errors;
63		return;
64	}
65	while(read(fd, (char *)&dir, sizeof dir) == sizeof dir) {
66		if(dir.d_ino == 0) continue;
67		if(!strcmp(dir.d_name, ".") || !strcmp(dir.d_name, ".."))
68			continue;
69		fprintf(stderr, "rmdir: %s not empty\n", name);
70		++Errors;
71	close(fd);
72		return;
73	}
74	close(fd);
```

第 60 行以只读方式打开目录（第二个参数为 0，等同于 O_RDONLY）。第 65 行读取 struct direct。第 66 行检查空的目录槽位；即 inode 号为 0 的槽位。第 67 行和第 68 行检查 `.` 和 `..`。到达第 69 行时，我们知道已经看到了其他文件名，因此，该目录不为空。

> （测试 `!strcmp(s1, s2)` 是 `strcmp(s1, s2) == 0` 的简写形式；即测试字符串是否相等。值得注意的是，我们认为 `!strcmp(s1, s2)` 的形式是不良风格。正如 Henry Spencer 曾经说过的：“`strcmp()` 不是布尔值！”）

