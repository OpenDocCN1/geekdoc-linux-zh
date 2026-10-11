
| `chmod a-rw sample` | 使 `sample` 的组权限与其用户（所有者）权限一致 |

| `chmod a+x sample` | 允许所有人执行 `sample` |

| `chmod go= sample` | 移除 `sample` 对组和其他人的所有访问权限 |

`chmod` 命令及其用途如表 5.3 所示。请记住，以下权限意味着对目录进行搜索。

```bash
$ cd
$ ls -l
drwxr-x---- 2 sarwar faculty 512 Apr 23 09:37 courses
-rwxrxr-wx 1 sarwar faculty 12 May 01 13:22 labs
```

## 基于访问权限的文件保护

```
-rwxr---- 1 sarwar faculty 163 May 05 23:13 temp
$ chmod 700 courses
$ ls -ld courses
drwx------ 2 sarwar faculty 512 Apr 23 09:37 courses
$ chmod g+rx courses
$ ls -ld courses
drxr-x-- 2 sarwar faculty 512 Apr 23 09:37 courses
$ chmod o+r courses
$ ls -ld courses
drwxr-xr-- 2 sarwar faculty 512 Apr 23 09:37 courses
$ chmod a-w *
$ ls -l
dr-xr-xr-x 2 sarwar faculty 512 Apr 23 09:37 courses
-r-xr-xr-x 1 sarwar faculty 12 May 01 13:22 labs
-r-xr-xr-x 1 sarwar faculty 163 May 05 23:13 temp
$ chmod 700 [1-t]*
$ ls -l
dr-xr-x-- 2 sarwar faculty 512 Apr 23 09:37 courses
-rwx------ 1 sarwar faculty 12 May 01 13:22 labs
-rwx------ 1 sarwar faculty 163 May 05 23:13 temp
$
```

可以使用带有 `-R` 选项的 `chmod` 命令设置一个或多个目录下的所有文件和目录的访问权限。以下命令将 `~MyWeb` 目录下所有文件和目录的访问权限递归设置为 `711`。为了让其他人能够浏览 `MyWeb`，用户需要允许所有人对用户可浏览页面对应的所有文件具有读取权限，即对这些文件设置 `755` 权限。

### $ chmod -R 711 MyWeb

```bash
$
```

如果你在 `chmod` 命令中使用单个数字指定访问权限，该命令将使用该数字来设置其他人的访问权限；用户和组的访问权限将被设置为 `0`（无访问权限）。如果你在 `chmod` 命令中指定两个数字，该命令将使用这两个数字来设置组和其他人的访问权限；用户的访问权限将被设置为 `0`（无权限）。在接下来的序列中，第一个 `chmod` 命令将目录的其他人访问权限设置为 `7` (`rwx`)。第二个 `chmod` 命令分别将个人目录的组和其他人的访问权限设置为 `7` (`rwx`) 和 `0` (`--`)。`ls -1` 命令显示这些命令的结果。

### $ chmod 7 courses

### $ chmod 70 personal

### $ ls -1 -l

```
d----rwx 2 sarwar faculty 512 Nov 10 09:43 courses
d---rwx-- 2 sarwar faculty 512 Nov 10 09:43 personal
drwxr-x-- 2 sarwar faculty 512 Nov 10 09:43 sample
```

现在让我们来看看读、写、执行权限对目录意味着什么。正如我们之前提到的，目录的读取权限允许你读取目录的内容。请记住，目录的内容是其中文件和目录的名称，写权限允许你在目录中创建文件或删除现有的文件或目录，而目录的执行权限是搜索该目录。在接下来的演示中，`courses` 目录的写权限已被关闭。因此你无法使用 `mkdir` 命令在该目录下创建子目录。同样，由于你没有 `personal` 目录的搜索权限，你无法使用 `cd` 命令进入（切换目录）。如果 `sample` 目录有一个开启了执行权限的子目录，你仍然无法进入，因为 `sample` 的搜索权限被关闭。最后，由于 `personal` 目录的读取权限被关闭，你无法使用 `ls -l` 命令显示其中的文件和目录。

```bash
$ chmod 600 sample
$ chmod 500 courses
$ chmod 300 personal
$ ls -1 -l
dr-x------ 2 sarwar faculty 512 Nov 10 09:43 courses
d-x------ 2 sarwar faculty 512 Nov 10 09:43 personal
drwxr-x-- 2 sarwar faculty 512 Nov 10 09:43 sample
```

```bash
$ mkdir courses/sample
mkdir: cannot create directory "courses/sample"; Permission denied
$ cd sample
cd: Permission denied
$ ls -1 -personal
ls: Permission denied
```

下面的演示进一步阐述了目录执行权限的含义，它允许你搜索目录但不读取其内容。`mkdir -p test1/test2/test3` 在当前目录创建一个层级结构，其中 `test1` 为父目录，`test2` 为子目录，`test3` 为孙目录。`test1` 目录具有执行权限但没有读取或写入权限，这意味着你无法读取其内容。`test2` 目录具有读、写和执行权限，因此你可以读取其内容、在其创建新文件（或目录）并进行搜索。因此 `ls` 命令产生了错误：

```bash
$ mkdir -p test1/test2/test3
$ chmod 100 test1
$ chmod 700 test2
$ ls test1
ls: Permission denied
$ ls test2
```

## 特殊权限位

除了本章常用的访问位（用户、组和其他人的读、写、执行权限），还有三个额外的位具有特殊意义。这些位被称为用户 ID (`SUID`)、组 ID (`SGID`) 位和粘滞位 (`sticky bit`)。

### 5.3.1 用户 ID (SUID) 位

我们之前已经过外部 shell 命令具有包含二进制代码或 shell 脚本的相关文件。这些文件中的程序在执行任务的能力方面并没有特殊之处。通常，当命令执行时，它是在发出命令的用户访问权限下运行的，这就是本章描述的访问权限工作原理。然而，许多 Linux 和 UNIX 命令需要写入那些对通常运行这些命令的用户保护的文件。此类文件的一个示例是 `/etc/passwd`，它是包含用户登录信息的文件（见第 2 章）。只有超级用户允许写入此文件以执行添加新登录和更改用户 ID 等任务。但是，Linux/Unix 用户通常允许执行 `password` 命令来更改密码。那么，当用户执行 `password` 命令时，该命令代表运行此的用户更改 `/etc/passwd` 文件中的用户密码。问题在于，我们希望用户能够更改自己的密码，但同时他们不能随意访问 `/etc/passwd` 文件，以防其他用户的信息被泄露。

正如我们所说，当命令执行时，它以运行命令的用户权限运行。相同内容的另一种说法是，当命令运行时，它以运行命令用户的“有效用户 ID”执行。Linux/Unix 拥有一种优雅的机制来解决上述问题和其他许多安全问题——通过允许命令以某种方式改变其执行权限，而不破坏系统的完整性。Linux/Unix 还有一个额外的权限位称为 `SUID` 位。如果该位设置在一个包含可执行程序的文件，则命令在执行时将获取文件所有者的权限。因此，如果一个文件的所有者是 `root` 并具有 `SUID` 位，则为 `password` 命令设置该位。那么，当你运行 `password` 命令时，它可以写入 `/etc/passwd` 文件（用新密码替换现有密码），即使你没有写入该文件的访问权限。

其他几个 Linux 和 UNIX 命令需要设置所有和 `SUID`，因为它们可以访问和更新普通用户可能没有权限的系统资源（文件、数据结构等）。这些命令包括 `lp`、`mail`、`mkdir`、`mv` 和 `ps`。`SUID` 位的另一个用途用于维护评分文件的软件。当此类软件设置了 `SUID` 位时，用户玩游戏时它可以更新评分，尽管同一个用户无法通过显式写入更新评分。

可以使用 `chmod` 命令使用八进制或符号模式设置 `SUID` 位，语法如下：

```bash
chmod 4xxx file-list
chmod u+s file-list
```
