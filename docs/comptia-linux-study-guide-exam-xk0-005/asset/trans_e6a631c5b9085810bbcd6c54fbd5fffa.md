

- `sudo`：`sudo` 命令是 *substitute user do*（替代用户执行）的缩写。它允许标准用户账户以其他用户账户（包括 `root` 用户账户）的身份运行任何命令。`sudo` 命令会提示用户输入自己的密码以验证其身份。
- `sudoedit`：`sudoedit` 命令允许标准用户以其他用户账户（包括 `root` 用户账户）的权限在文本编辑器中打开文件。`sudoedit` 命令同样会提示用户输入自己的密码以验证其身份。

虽然 `su` 命令的含义比较直观，但 `sudo` 和 `sudoedit` 命令可能稍显复杂。通过提供自己的用户密码以管理员权限运行命令，听起来似乎有点奇怪。

每个 Linux 系统都使用一个文件来定义哪些用户被允许运行 `sudo` 命令，该文件通常位于 `/etc/sudoers`。`sudoers` 文件不仅包含用户账户列表，还包含允许其用户拥有管理员权限的组列表。有两个常用的用户组用于授予这些权限。基于 Debian 的发行版使用 `sudo` 组，而基于 Red Hat 的发行版使用 `wheel` 组（*big wheel* 的缩写）。

> **警告**
>
> 切勿使用标准编辑器打开 `sudoers` 文件。如果多个用户同时打开 `sudoers` 文件，可能会发生异常情况并导致文件损坏。`visudo` 命令可以安全地在编辑器中打开该文件，以便您进行修改。

## 限制用户和文件

最后，有两个命令需要了解，它们与文件所有权或权限没有直接关系，而是与用户和文件的限制有关。`ulimit` 命令有助于限制每个用户账户对系统资源的访问。列表 15.8 展示了运行带有 `-a` 选项的 `ulimit` 命令的输出，该选项显示用户账户的设置。

### 列表 15.8：`ulimit` 命令输出

```
$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority         (-e) 0
file size               (blocks, -f) unlimited
pending signals             (-i) 19567
max locked memory       (kbytes, -l) 16384
max memory size         (kbytes, -m) unlimited
open files                (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues (bytes, -q) 819200
real-time priority (-r) 0
stack size (kbytes, -s) 8192
cpu time (seconds, -t) unlimited
max user processes (-u) 19567
virtual memory (kbytes, -v) unlimited
file locks (-x) unlimited
$  
```

随着用户账户消耗系统资源，它会对系统造成负载，但主要体现在 CPU 时间和内存方面。如果您在多用户 Linux 环境中工作，可能需要限制每个用户账户可以消耗的资源数量。这正是 `ulimit` 命令发挥作用的地方。表 15.3 列出了您可以用于限制用户账户特定资源的命令行选项。

**表 15.3 ulimit 命令选项**

| 选项 | 描述 |
| --- | --- |
| -a | 列出当前用户账户的限制 |
| -b | 设置最大套接字缓冲区大小 |
| -c | 设置最大核心文件大小 |
| -d | 设置进程的最大数据段大小 |
| -e | 设置允许的最大调度优先级 |
| -f | 设置允许写入的最大文件大小 |
| -i | 设置最大待处理信号数 |
| -k | 设置可分配的最大队列数 |
| -l | 设置可锁定的最大内存大小 |
| -m | 设置最大常驻集大小 |
| -n | 设置最大打开文件描述符数 |
| -p | 设置以 512k 块为单位的最大管道大小 |
| -r | 设置最大实时调度优先级值 |
| -s | 设置最大堆栈大小 |
| -t | 设置允许用户账户使用的最大 CPU 时间 |
| -u | 设置用户可同时运行的最大进程数 |
| -v | 设置用户可用的最大虚拟内存量 |
| -x | 设置最大文件锁数量 |
| -P | 设置用户账户可登录的最大伪终端数量 |
| -T | 设置用户可拥有的最大线程数 |

正如表 15.3 所示，通过 `ulimit` 命令，Linux 管理员可以对单个用户账户在系统上能做什么实施相当严格的限制。

您还可以设置关于用户可以对文件和目录做什么或不能做什么的限制。文件和目录属性定义了文件系统允许或阻止对该文件或目录执行的操作。

`chattr` 命令用于修改分配给文件或目录的属性。`chattr` 命令的格式为：
`chattr [ mode ] files...`

`mode` 选项定义了要设置或取消设置的属性。表 15.4 定义了 Linux 中可用的不同属性。

**表 15.4 Linux 文件和目录属性**

| 属性 | 描述 |
|---|---|
| a | 写入时只能以追加模式打开。 |
| A | 当文件打开时，文件的访问时间不会被修改。 |
| c | 自动压缩磁盘上的文件。 |
| C | 对于日志文件系统，文件写入时不会自动进行复制。 |
| d | 不要使用 dump 程序备份该文件。 |
| D | 所有更改都同步写入磁盘，不经过缓存（仅适用于目录）。 |
| e | Linux 使用扩展（extents）来映射磁盘上的块。 |
| E | 文件由文件系统加密。 |
| F | 应用于目录时，目录中的所有路径查找均不区分大小写。 |
| i | 文件不能被修改或删除。 |
| I | 使用哈希树对目录进行索引。 |
| j | 如果文件系统支持日志记录，则写入文件的数据在写入文件之前会先写入日志。 |
| N | 文件包含存储在 inode 表本身中的数据。 |
| P | 应用于目录时，目录中的文件继承目录的项目 ID。 |
| s | 如果文件被删除，其块会被清零并写回磁盘。 |
| S | 对文件的更改同步写入磁盘，而不是存储在缓冲区中。 |
| t | 如果文件末尾包含部分块碎片，它不会与其他文件合并。 |
| T | 目录被视为目录层级的顶部（用于存储目的）。 |
| U | 删除文件时保存其内容，以便启用 undelete（撤销删除）功能。 |
| V | 对文件应用文件认证。 |

要为文件或目录分配某个属性，请在该属性前加一个加号：

```
$ sudo chattr +i test1.txt
$ rm test1.txt
rm: cannot remove 'test1.txt': Operation not permitted
$ 
```

此示例为文件设置了不可变属性（i），使得无法删除该文件。这个特定属性只能由 root 用户账户设置，因此需要使用 `sudo` 命令。设置属性后，文件将不再可以被删除。

要显示当前应用于文件或目录的属性，请使用 `lsattr` 命令：

```
$ lsattr test1.txt
---i---------- test1.txt
$ 
```

要移除属性，请在 `chattr` 命令中使用减号：

```
$ sudo chattr -i test1.txt
$ lsattr test1.txt
----------- test1.txt
$ rm test1.txt
$ 
```

![](img/c0a399aca0d18f8822d714ad0a173123_528_0.png)

并非所有文件系统都支持所有文件和目录属性。您需要查阅特定文件系统的文档，以确定哪些文件和目录属性可供您使用。

练习 15.1 将介绍如何设置一个简单的共享目录，使多个用户账户都可以对文件进行读写访问。

## 练习 15.1 创建共享目录

本练习展示了如何使用 GUID 位创建允许多个用户既读又写文件的目录。

- 1. 登录您的 Linux 系统并打开一个新的命令提示符。
- 2. 使用命令 `sudo useradd -m test1` 创建第一个测试用户账户。使用命令 `sudo passwd test1` 为该测试账户分配密码。
- 3. 使用命令 `sudo useradd -m test2` 创建第二个测试用户账户。使用命令 `sudo passwd test2` 为该测试账户分配密码。
- 4. 使用命令 `sudo groupadd sales` 创建一个名为 sales 的新组。
- 5. 使用命令 `sudo usermod -G sales test1` 和 `sudo usermod -G sales test2` 将两个测试用户账户都添加到 sales 组中。您可以使用命令 `cat /etc/group | grep sales` 检查组文件以验证您的工作。您应该看到 test1 和 test2 用户账户都列为该组的成员。
- 6. 使用命令 `sudo mkdir /sales` 创建一个新的共享目录。使用命令 `sudo chgrp sales /sales` 更改分配给该目录的默认组。使用命令 `sudo chmod g+w /sales` 授予 sales 组成员对 /sales 目录的写权限。使用命令 `sudo chmod g+s /sales` 为 /sales 目录设置 GUID 位。这确保在 /sales 目录中创建的任何文件都被分配给 sales 组。

