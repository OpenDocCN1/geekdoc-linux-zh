

# 信息类命令

这些命令用于显示关于您的系统或其用户的信息。

## 计算机名称

`hostname` 命令用于显示计算机的名称。以下是在我的机器 shishi.skoll.ca 上运行的示例：

```
$ hostname
shishi.skoll.ca
$ hostname -a # (别名)
shishi
$ hostname -f # (全名)
shishi.skoll.ca
$ hostname -i # (IP 地址)
192.168.2.3
$ hostname -s # (短名称)
shishi
$ hostname -d # (域名)
skoll.ca
$ hostname newname # (设置名称 - 仅限 root)
```

`hostname` 还有更多选项；详情请参阅 `hostname(1)`。

`uname` 用于显示关于您计算机的信息。以下展示了 `uname` 的实际运行效果：

```
$ uname # (操作系统名称)
Linux
$ uname -m # (机器类型)
i686
$ uname -n # (节点名称)
shishi.skoll.ca
$ uname -r # (操作系统发行版)
2.2.5
$ uname -s # (操作系统名称)
Linux
$ uname -p # (主机处理器类型)
unknown
$ uname -v # (操作系统版本)
#1 Sat Apr 3 21:49:22 MST 1999
$ uname -a # (所有信息)
Linux shishi.skoll.ca 2.2.5 #1 Sat Apr 3 21:49:22 MST 1999 i686 unknown
```

## 我是谁？

许多命令可以告诉您您的身份信息。

```
$ logname # (我的登录名是什么？)
dfs
$ id # (我的用户和组 ID 是什么？)
uid=500(dfs) gid=500(dfs) groups=500(dfs),17(postgres)
$ whoami # (我的有效用户 ID 是什么？)
dfs
$ who am i # (我是谁？)
shishi.skoll.ca dfs tty0 Jun 28 09:09 (:0.0)
```

注意最后一个示例，`who am i`。它显示的身份信息如以下表格所示：

| 机器 | 用户 | 终端 | 登录时间 | 登录位置 |
| :--- | :--- | :--- | :--- | :--- |
| shishi.skoll.ca | dfs | tty0 | 6月 28日 09:09 | (:0.0) |

## 距离上次重启过去了多久？

命令 `uptime` 提供有关系统运行时间的信息：

```
$ uptime
3:31pm up 6:23, 2 users, load average: 0.11, 0.20, 0.13
```

`uptime` 命令告诉您当前的时间是下午 3:31，计算机在 6 小时 23 分钟前最后一次重启。当前有两名用户。过去 1、5 和 15 分钟的系统负载平均值分别为 0.11、0.20 和 0.13。（负载平均值是指在任意给定时刻处于可运行状态的平均进程数。）

## 谁已登录？

以下命令可以告诉您谁已登录：

```
$ w # (谁已登录以及他们正在做什么？)

3:32pm up 6:24, 2 users, load average: 0.11, 0.20, 0.13
USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
dfs ttyD :0.0 9:09am 0.00s 7:49 0.00s w
dfs tty3 shevy 3:36pm 5.00s 0.04s 0.00s -bash
```

输出的第一行与 `uptime` 相同。下一行是标题。对于每个在终端上登录的人，会生成一行输出。该行包含以下字段：

- **USER** 用户名称。
- **TTY** 用户登录到的终端设备。
- **FROM** 用户从哪个远程系统登录。在第一行中，显示为 `:0.0`，因为该终端是显示器 `:0.0` 中的 xterm。第二行显示 `dfs` 是从机器 `shevy` 远程登录的。
- **LOGIN@** 登录时间。
- **IDLE** 用户空闲了多久。
- **JCPU** 用户终端上所有作业的累计 CPU 时间。
- **PCPU** 当前正在运行的作业的 CPU 时间。
- **WHAT** 用户终端上的前台作业（当前正在运行的作业）。

`who` 提供的信息较少：

```
$ who # (谁已登录？)
dfs    :0    Jun 28 09:09
dfs    tty p3    Jun 28 15:36 (shevy.skoll.ca)
```

这里，字段包括 USER、TTY、LOGIN@ 以及 FROM（如果不是从本地机器登录）。

命令 `last` 显示某人最后登录的时间。其语法是

```
$ last [-n] [user]
```

例如，`last dfs` 显示用户 `dfs` 的登录历史。以下示例显示了 `dfs` 的最后四次登录记录：

```
$ last -4 dfs
dfs tty p3 shevy Mon Jun 28 15:36 still logged in
dfs :0          Mon Jun 28 09:09 still logged in
dfs :0          Sun Jun 27 12:23 - 22:43 (10:19)
dfs :0          Sun Jun 27 11:22 - 12:05 (00:43)
```

字段包括 USER、TTY、FROM（如果不是本地机器）、登录时间、注销时间以及总的登录时长。

`last` 有多个选项；详情请参阅 `last(1)`。

## 空闲内存

`free` 命令显示有关内存使用情况的统计信息：

```
$ free

          total     used free shared buffers cached
Mem:      128220   100163 28052 59756 4624 55472
-/+ buffers/cache: 40072 88148
Swap:     377516    388 377128
```

total 列显示可用内存的总量，单位为千字节。这台计算机拥有 128MB 的物理内存和大约 368MB 的交换空间。

used 列显示已使用的内存量，free 列显示空闲的内存量。shared 显示被多个进程共享的内存量。buffers 和 cached 显示文件系统缓冲区和缓存使用的内存量。Linux 会将磁盘文件缓存在内存中，但这些内存可以被正在运行的进程占用——它们具有更高的优先级。`-/+ buffers/cache` 这一行显示了实际上可供进程使用的内存量。磁盘缓存使用的内存会从已使用的内存中减去。

`free` 是 Linux 特有的；在其他 UNIX 系统中找不到。更多详情请参阅手册页 `free(1)`。

您还可以输入 `cat /proc/meminfo` 来查看内存统计信息。这会生成类似 `free` 的输出，但提供字节级别的内存统计信息。

# 磁盘空间

Linux 有两个命令用于确定空闲磁盘空间的数量以及文件和目录使用的磁盘空间量。

## 空闲空间

`df` 命令告诉您拥有多少磁盘空间：

```
$ df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda1 1554202 73090 1400049 5% /
/dev/hda2 3106103 1131281 1814172 38% /usr
/dev/hda3 4655757 220433 4194349 5% /home
```

各字段具有以下含义：

- **Filesystem** 对应于文件系统的块特殊文件。
- **1k-blocks** 文件系统中 1KB 块的总数。
- **Used** 已使用的块数。
- **Available** 可用的块数。请注意，Used 和 Available 的总和小于 1k-blocks，因为某些块保留给 root 专用。
- **Use%** 已使用的可用块百分比。
- **Mounted on** 文件系统的挂载点。

`df` 有许多选项；详情请参阅 `df(1)`。我最喜欢的是 `-h` 选项，它可以生成人类可读的输出：

```
$ df -h
Filesystem Size Used Avail Use% Mounted on
/dev/hda1 1.5G 71M 1.3G 5% /
/dev/hda2 3.0G 1.1G 1.7G 38% /usr
/dev/hda3 4.4G 215M 4.0G 5% /home
```

![](img/df365d352a104b50fea29e59a052de4d_994_0.png)

## 已用空间

`du` 命令计算文件和目录使用的磁盘空间量。

`du` 的调用方式如下所示：

```bash
$ du [options] [pathname,...]
```

对于每个 `pathname`，`du` 计算该文件或目录使用的磁盘空间。如果未提供 `pathname`，则假定为当前目录。

`du` 会递归进入作为参数给出的目录，并显示所有子树以及作为参数给出的目录所使用的空间。例如，

```bash
$ du DFClass
```

```
4	DFClass/.CVS
4	DFClass/src/.CVS
182	DFClass/src
4	DFClass/tests/.CVS
346	DFClass/tests
3	DFClass/include/.CVS
4	DFClass/include/df/.CVS
33	DFClass/include/df
37	DFClass/include
614	DFClass
```

显示了每个子树的磁盘使用情况。在最后一行，您会看到 `DFClass` 目录及其所有后代使用的总磁盘空间为 614KB。

`du` 有许多选项：

- `-s` 汇总磁盘空间。`du` 仅打印命令行中明确命名的项目的磁盘空间。例如，

```bash
$ du -s DFClass B1ge
```

```
614	DFClass
3855	B1ge
```

不显示详细信息。`-s` 开关对于查明谁在占用磁盘很有用：

```bash
# du -s /home/j/* > /DISKNOGS
```

- `-a` 显示所有详细信息，即使是普通文件也是如此。这会生成大量的输出。

- `-x` 仅统计与给定参数位于同一文件系统上的空间。这可以防止 `du` 递归进入不同的文件系统。

