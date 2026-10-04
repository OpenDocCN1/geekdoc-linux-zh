
## 15.6.2 目录访问

由于目录在文件系统层次结构中的特殊重要性，访问其内容需要特殊的系统调用。要打开一个目录，需要使用 opendir() 系统调用，其原型为：

```
#include <dirent.h>

DIR *opendir(char *pathname);
```

此调用打开指定的目录，如果成功则返回目录指针，否则在出错时返回零。目录指针传递给相关的系统调用，主要的有 readdir() 和 closedir()。

readdir() 系统调用的原型为：

```
#include <dirent.h>

struct dirent *readdir(DIR *dirptr);
```

此调用返回指向 struct dirent 的指针，其中包含指定目录中下一个链接的详细信息。链接中文件名称存储在结构体的 d_name 元素中，它是一个字符数组。重复调用 readdir() 将导致按顺序遍历目录中的链接。当没有更多链接可读时，返回零值。

使用完目录后，可以使用 closedir() 系统调用将其关闭。此调用的原型为：

```
#include <dirent.h>

int closedir(DIR *dirptr);
```

## 15.6.3 link 和 unlink 系统调用

文件的目录项称为链接。当文件首次创建时，会根据其给定的路径名自动生成指向该文件的链接。此后，可以通过 link() 系统调用生成指向该文件的额外链接：

```
#include <unistd.h>

int link(char *pathname1, char *pathname2);
```

创建一个新的目录链接，称为 pathname2，指向现有文件 pathname1。为了使 link() 调用正常工作，pathname1 和 pathname2 必须位于同一文件系统上，并且调用进程必须具有向目标目录写入的适当权限。普通文件链接可以用 unlink() 系统调用删除。

```
#include <unistd.h>

int unlink(char *pathname)
```

此调用删除指定的目录链接，并递减其 inode 中文件链接计数。之后，如果链接计数变为零，则 inode 和文件的数据块全部释放回系统。如果某个进程在文件被安排删除时恰好打开了该文件，则 inode 和数据块的回收将被延迟，直到该进程终止，尽管目录链接仍将被删除，这样就不会有其他进程可以 open() 该文件并进一步延长其生命周期。

## 练习

- 1. 编写 ls 命令的简化版本，它仅将单个目录的名称作为唯一的命令行参数，并列出目录中所有文件的文件名，每行一个。如果不尝试对名称列表进行排序会更简单。
- 2. 编写一个程序，获取与终端关联的 struct termios 的副本，并以合理的人类可读形式显示其找到的设置值。
- 3. 编写一个 C 程序，提示用户输入姓名和密码，并根据提示从用户处获取字符串值。确保在输入密码时抑制字符回显，并在之后恢复回显，然后在程序打印获取的值并终止之前。
- 4. 编写一个简单的重命名命令，允许您重命名当前目录中您拥有的任何文件。命令的格式应为：

```
$ rename <oldname> <newname>
```

## 答案

1. 下面代码非常简单，部分原因是它没有执行通常需要进行的任何检查，以验证命令行参数的正确数量和类型，也没有验证所进行的系统调用的正确操作。然而，它确实使代码非常易于阅读：

```
#include <stdio.h>
#include <dirent.h>
```

```
main(int argc, char **argv)
{
    DIR *dp;
    struct dirent *link;

    dp = opendir(argv[1]);

    while ((link = readdir(dp))!=0)
        printf("%s\n", link->d_name);

    closedir(dp);
}
```

2. 解决此问题的方法是使用 ioctl() 或 tcgetattr() 来获取与终端关联的结构的内容。关于结构中每个标志和字节的含义和值的所需信息包含在头文件 /usr/include/linux/termios.h 中，stty 命令的手册页中还有一些额外信息。根据这些信息，很容易判断哪些标志被设置和重置以及它们的效果。然后可以以任何适当的形式显示。

3. 下面的 shell 脚本执行了所需的任务，并且可以很好地作为伪代码程序，供您在 C 中解决问题时参考：

```
echo -n "enter name: "
read name
stty -echo
echo -n "enter password: "
read password
stty echo
echo
echo name: $name
echo password: $password
```

4. 此问题的伪代码解决方案看起来像：

```
main(argc, argv)
    if argc!=3
        give error and usage message and exit
    if argv[1] or argv[2] outside current directory
        i.e. if they contain a '/', give error and exit
    if argv[1] not in current directory
        give error and exit
    link(argv[1], argv[2])
    unlink(argv[1])
```

您的 C 解决方案应遵循此基本模式。尽量使其尽可能防错，尝试处理您能找到的尽可能多的错误条件，包括检查系统调用的错误返回。

## 进程控制

Linux 是一个真正多任务操作系统。如果您有一个需要多个进程并发协作的应用程序，那么 Linux 可以安排它们并发运行，并在为您处理所有调度和进程管理。事实上，您已经看到这是如此。每次您使用 shell 运行管道时，例如：

```
$ ls | wc -w
```

它涉及多个命令（在此示例中为 ls 和 wc）并发运行，并且它们之间有一个通信通道，以便它们可以协作执行单个任务。当 shell 代表您安排运行并发进程时，它仅使用普通用户设施，您也可以在自己的程序中使用这些设施。它是这些设施构成本章的主题。

## 16.1 进程标识号

在 Linux 下运行的每个进程都有一个唯一的进程 ID 号（PID），系统据此识别它。从进程 1（init）开始的每个进程都有一个父进程，其进程 ID 也可以访问。

每个进程还属于一个进程组，其进程组 ID 只是进程组领导者的进程 ID。

当确定进程访问各种文件的权限时，进程使用另一组四个 ID。这些被称为真实用户和组 ID 以及有效用户和组 ID。进程的真实 ID 只是进程运行的用户 UID 和 GID。有效 ID 通常与真实 ID 相同，除非程序设置了其 setuid 或 setgid 位。如果设置了其中一个或两个位，则相应的有效用户或组 ID 将设置为与进程运行的程序文件关联的文件所有者 ID 或文件组 ID。

这听起来很复杂，所以举个例子。假设一个 UID 为 200 且 GID 为 20 的用户运行程序 /usr/bin/passwd。该程序的文件所有者 ID 为 0（root），文件组 ID 为 1（bin），并且还设置了其 setuid 位。

当运行 passwd 程序时，相关进程将具有真实用户 ID 200、真实组 ID 20、有效用户 ID 0（因为设置了 setuid 位），以及有效组 ID 20。

真实 ID 用于确定进程运行的用户身份。有效 ID 用于根据以下算法（从规则 1 开始）确定进程访问文件时的特权和权限：

- **规则 1** 如果进程的有效用户 ID 为 0（root），则大多数情况下自动授予权限。如果不是，转到规则 2
- **规则 2** 如果进程的有效用户 ID 与文件用户 ID 相同，则根据文件上的所有者权限位授予对文件的访问权限。如果不是，转到规则 3。
- **规则 3** 如果进程的有效组 ID 与文件组 ID 相同，则根据文件上的组权限位授予对文件的访问权限。如果不是，转到规则 4。
- **规则 4** 根据文件上的世界权限位授予对文件的访问权限。

与进程关联的各种 ID 都可以通过一组‘get ID’系统调用访问：

```
uid_t getuid(void)        /* get real user ID */
uid_t getgid(void)        /* get real group ID */
uid_t geteuid(void)       /* get effective user ID */
uid_t getegid(void)       /* get effective group ID */
pid_t getpid(void)        /* get process ID */
pid_t getppid(void)       /* get parent process ID */
pid_t getpgrp(void)       /* get process group ID */
```

## 16.2 使用 fork 创建进程

为了本次讨论的目的，我们将认为进程由三个独立的部分组成，如图 16.1 所示。

文本段保存要执行的机器代码指令。该段是只读的（因此您不能在此编写自修改代码），这使得系统上运行相同程序的两个或多个进程之间可以共享该段成为可能。例如，如果多个用户都以 bash 作为其 shell 运行，则内存中只需要一份程序指令的副本，他们都可以共享。
