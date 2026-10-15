
## 区分进程：`exec()`

进程可以使用 `exec` 系列系统调用之一用另一个可执行文件替换其当前的代码、数据和栈。当进程执行 `exec()` 时，其 `PID` 和 `PPID` 保持不变——只有进程正在执行的代码发生了变化。`exec()` 的工作原理如图 13.38 所示。图中列出的 `exec()` 成员并不是真正的系统调用；它们是调用 `execve()` 系统调用的 C 函数。`execve()` 很少直接使用，因为它包含一些很少使用的选项。

```c
Library Routine: int exec(const char* path, const char* arg0, const char* arg1..., char* argn, NULL);
int execv(const char* path, const char* argv[]);
int execl(const char* path, const char* arg0, const char* arg1..., char* argn, NULL);
int execvp(const char* path, const char* argv[]);
```

`exec()` 系列系统调用替换当前的进程映像为新映像。`exec()` 的工作原理如图 13.38 所示。图中列出的 `exec()` 成员并不是真正的系统调用；它们是调用 `execve()` 系统调用的 C 函数。`execve()` 很少直接使用，因为它包含一些很少使用的选项。

## 修改目录：`chdir()`

进程可以使用 `chdir()` 系统调用更改其当前工作目录。当程序需要在其启动时所在的目录之外操作时，这特别有用。

```c
int chdir(const char *path);
```

## 修改优先级：`nice()`

每个进程都有一个优先级值，影响分配给它的 CPU 时间。通常情况下，值越小，进程运行越快。进程可以使用 `nice()` 系统调用更改其优先级。

```c
int nice(int delta);
```

`nice()` 将 `delta` 加到进程的优先级值。只有超级用户可以指定导致负优先级的 `delta`。有效的优先级值范围是 -20 到 +19。如果指定的 `delta` 优先级值超出限制，则该值将被截断为限制值。

### 进程管理 483

```
PID TT STAT TIME COMMAND
15099 p2 S 0:00 -sh (sh)
15206 p2 S N 0:00 a.out
15211 p2 S N 0:00 -c ps
15212 p2 R N 0:00 ps
$_
```

注意，进程的优先级值变为非零，它在 `ps` 中被标记为 `N`，同时由于系统 `()` 库调用而创建的 `sh` 和 `ps` 命令也是如此。

## 访问用户 ID 和组 ID

图 13.41 显示允许你读取进程真实（real）和有效（effective）标识符的系统调用。图 13.42 显示允许你设置进程真实 ID 和有效 ID 的系统调用。

```
System Call: uid_t getuid ()

uid_t getuid ()

gid_t getgid ()

gid_t getegid ()
```

`getuid()` 和 `geteuid()` 分别返回调用进程的真实用户 ID 和有效用户 ID。`getgid()` 和 `getegid()` 分别返回调用进程的真实组 ID 和有效组 ID。这些 ID 数字对应于 `/etc/passwd` 和 `/etc/group` 文件中列出的用户 ID 和组 ID。

调用总是成功的。

图 13.41

`setuid()`、`getuid()`、`getgid()` 和 `getegid()` 系统调用描述。

```
Library Routine: int setuid (uid_t id)

int setuid (uid_t id)
int setgid (gid_t id)

int setegid (gid_t id)
```

`setuid()` 和 `seteuid()` 设置调用进程的有效用户（组）ID。`setuid()` 和 `setgid()` 将调用进程的有效和真实用户（组）ID 设置为指定值。

只有由超级用户执行或者 `id` 是调用进程的真实或有效用户（组）ID 时，调用才会成功。成功时返回 0；否则返回 -1。

图 13.42

`setuid()`、`seteuid()`、`setgid()` 和 `setegid()` 库例程描述。

## 第 13 章 系统编程

## 示例程序：后台处理

接下来，我们将检查一个利用 `fork()` 和 `exec()` 在后台执行程序的示例程序。原始进程会创建一个子进程来执行指定的可执行文件，然后终止。孤儿进程会自动被 `init` 接管。以下是代码：

```
$ cat background.c
#include <stdio.h>
main (argc, argv)
int argc;
char* argv[];
{
    if (fork () == 0) /* 子进程 * */
        execvp(argv[1], &argv[1]); /* 执行其他程序 */
        printf(stderr, "Could not execute %s\n", argv[1]);
}
$ background cc mywait.c ...运行程序。
$ ps ...确认 "cc" 在后台运行。
PID TT STAT TIME COMMAND
13664 p S 0:00 -csh (csh)
13716 p R 0:00 ps
13717 p D 0:00 cc mywait.c
$_
```

我是如何巧妙地通过将 `&argv[1]` 作为 `execvp()` 的第二个参数，将参数从 `main (1)` 列表传递给 `execvp()` 的。注意，我还使用了 `exec()` 而不是 `execvp()`，这样程序可以使用 `PATH` 来查找可执行文件。

## 示例程序：磁盘使用

下一个编程示例使用了一种新技术来计算层次结构中非目录文件的数量。当程序启动时，其第一个参数必须是要搜索的目录名称。程序遍历目录中的每个条目，为每个条目创建一个新进程。如果子进程关联的文件是非空文件，则以 1 退出，否则重复该过程，累加其子进程的退出码并返回总和。这种技术很有趣但很愚蠢：它不仅创建了大量进程（这并不高效），而且由于它使用终止码返回，因此被限制为8 位计数。代码如下：

```
$ cat count.c ...列出程序。
#include <stdio.h>
#include <fcntl.h>
#include <sys/dirent.h>
#include <sys/stat.h>
long processFile();
```

### 进程管理 485
