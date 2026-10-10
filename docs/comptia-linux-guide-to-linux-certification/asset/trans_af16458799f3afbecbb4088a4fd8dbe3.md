
## 命令输入与输出

`|` 元字符两侧无需留有空格；命令 `ls -l /etc | less` 和 `ls -l /etc|less` 是等效的。

管道的一个常见用途是减少在终端屏幕上显示的信息量，特别是当命令显示的信息过多时。以 `mount` 命令的以下输出为例：

```bash
[root@server1 ~]# mount
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=1015268k,
 nr_inodes=253817,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,
noexec,relatime)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts
(rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs
(rw,nosuid,nodev,noexec,relatime,seclabel, mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup
(rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/
systemd-cgroups-agent,name=systemd)
psstore on /sys/fs/psstore type psstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/cpuset type cgroup
(rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup
(rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
cgroup on /sys/fs/cgroup/memory type cgroup
(rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/devices type cgroup
(rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/freezer type cgroup
(rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls type cgroup
(rw,nosuid,nodev,noexec,relatime,net_cls)
cgroup on /sys/fs/cgroup/blkio type cgroup
(rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/perf_event type cgroup
(rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/hugetlb type cgroup
(rw,nosuid,nodev,noexec,relatime,hugetlb)
/dev/sda3 on / type ext4 (rw,relatime,seclabel,data=ordered)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs
(rw,relatime,fd=35,
pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
configfs on /sys/kernel/config type configfs (rw,relatime)
hugetlfs on /dev/hugepages type hugetlfs (rw,relatime,seclabel)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
tmpfs on /tmp type tmpfs (rw,seclabel)
/dev/sda1 on /boot type ext4 (rw,relatime,seclabel,data=ordered)
[root@server1 ~]#
```

若要仅查看与 ext4 文件系统相关的行，可以将 `mount` 命令的标准输出作为标准输入发送给 `grep` 命令，如下面的输出所示：

```bash
[root@server1 ~]# mount | grep ext4
/dev/sda3 on / type ext4 (rw,relatime,seclabel,data=ordered)
/dev/sda1 on /boot type ext4 (rw,relatime,seclabel,data=ordered)
[root@server1 ~]#
```

前面输出中的 `grep` 命令接收来自 `mount` 命令的完整输出，然后只显示包含 ext4 的行。`grep` 命令通常接受两个参数；第一个指定要搜索的文本，第二个指定要搜索的文件名。前面输出中使用的 `grep` 命令不需要第二个参数，因为要搜索的材料来自标准输入（即 `mount` 命令），而不是来自文件。

此外，你可以在命令行上使用多个 `|` 管道元字符，将一个命令的信息管道传输到另一个命令，其运作方式与工厂中的流水线非常相似。通常，流水线会经过几个部门，每个部门都擅长执行特定的任务。例如，一个部门可能负责组装产品，另一个部门可能负责喷漆，还有一个部门可能负责包装。每个产品都必须经过每个部门才能完成。

你可以以同样的方式使用处理数据的 Linux 命令，通过管道将它们连接成一条流水线。信息由一个命令进行处理，然后处理过的信息被发送到另一个命令进行进一步处理。这个过程持续进行，直到信息达到用户所需的格式。管道传输过程如图 7-3 所示。

![](img/c27875544958897d817484d558c208c8_335_0.png)

**图 7-3 管道传输多个命令**

任何能够接收标准输入并将其转换为标准输出的命令都称为过滤命令。需要注意的是，像 `ls` 和 `mount` 这样的命令不是过滤命令，因为它们不接收来自其他命令的标准输入，而是从系统读取信息并显示给用户。因此，这些命令必须位于管道的开头。其他命令，如 `vi`，是交互式的，因此不能存在于两个管道符号之间，因为它们无法从标准输入接收数据并输出到标准输出。

Linux 用户可以使用数百种过滤命令。表 7-2 列出了本书中常用的一些命令。

| 命令 | 描述 |
| :--- | :--- |
| sort | 按字母数字顺序对文件中的行进行排序 |
| sort -r | 按字母数字顺序对文件中的行进行反向排序 |
| wc | 统计文件中的行数、单词数和字符数 |
| wc -l | 统计文件中的行数 |
| wc -w | 统计文件中的单词数 |
| wc -c | 统计文件中的字符数 |
| pr | 格式化文件以便打印，提供多个选项；它在每页顶部放置日期和页码 |
| pr -d | 以双倍行距格式化文件 |
| tr | 替换文件文本中的字符 |
| grep | 显示文件中匹配正则表达式的行 |
| nl | 为文件中的行编号 |
| awk | 使用模式-动作语句提取、处理和格式化文本 |
| sed | 使用查找和替换表达式处理文本 |
| split | 将输入拆分为多个文件 |
| unexpand | 将空格字符转换为制表符 |
| uniq | 省略重复的行 |
| xargs | 将输入列表转换为可与命令一起使用的参数 |

**表 7-2 管道中常用的命令**

例如，以莎士比亚《罗密欧与朱丽叶》的序言为例：

```bash
[root@server1 ~]# cat prologue
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
```

现在假设你想将上述文件中的所有小写字母 “a” 替换为大写字母 “A”，按每行第一个字符对内容进行排序，输出双倍行距，并逐页查看结果。要完成这些任务，可以使用以下管道：

```bash
[root@server1 ~]# cat prologue | tr a A | sort | pr -d | less
2015-08-20 08:06
Page 1
A pair of star-cross’d lovers take their life;
And the continuance of their parents’ rage;
Do with their death bury their parents’ strife.
From ancient grudge break to new mutiny,
From forth the fatal loins of these two foes
In fair Verona, where we lay our scene,
Is now the two hours’ traffic of our stage;
The fearful passage of their death-mark’d love,
Which if you with patient ears attend,
Two households, both alike in dignity,
What here shall miss, our toil shall strive to mend.
Where civil blood makes civil hands unclean.
Which, but their children’s end, nought could remove,
Whole misadventured piteous overthrows
```

前面示例中使用的命令通过 **less** 命令将最终标准输出显示在终端屏幕上。在许多情况下，你可能希望在显示管道结果的同时，将副本保存到硬驱动中的文件中。完成此任务的过滤命令是 **tee** 命令，它从标准输入接收信息，并将该信息发送到文件以及标准输出。

为了在通过 **less** 命令将处理后的序言显示到终端屏幕之前保存一份副本，可以使用以下命令：

```bash
[root@server1 ~]# cat prologue | tr a A | sort | pr -d | tee newfile | less
2015-08-20 08:06
Page 1
A pair of star-cross’d lovers take their life;
And the continuance of their parents’ rage;
Do with their death bury their parents’ strife.
```
