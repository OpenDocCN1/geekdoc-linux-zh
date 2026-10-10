

## 保持同步

与 Linux 相比，FreeBSD 更加“以源码为中心”；由于实际上只有一个“发行版”，整个安装过程在源码形式下直接可用。Linux 世界在这方面做得并不那么有效。每个发行版都有自己独特的结构和软件选择。Linux 内核本身是你唯一能确定与另一个 Linux 用户相同源码子树的地方。不同的发行版对于提供其余源码树的自动下载、同步和构建有着不同的理念。FreeBSD 提供了这些工具。

这意味着，为了保持与最新开发代码同步，在 FreeBSD 中你所要做的就是像第 17 章描述的那样使用 CVSup 跟踪源码。安全补丁和热修复（在 Linux 中以 RPM、源码补丁或二进制补丁等不同形式提供）在 FreeBSD 中既以源码补丁形式分发，也通过向中心源码树检入修复内容来分发。你可以通过遵循公告中的逐行补丁说明，或者简单地确保你的源码树已同步到修复完成后的某个时间点，然后重建系统的相应部分，来响应安全公告更新你的系统。

> **注意**
>
> 在不重建整个操作系统的情况下修补系统组件通常是一种有效的方法（尤其是对于系统中较小且非关键的元素），但并不总是如此。组件对系统操作越 fundamental（基础），你就越有可能需要执行完整的 `make world` 才能正确升级。这些基础区域通常包括中央库（`/usr/lib` 中的项目）或头文件（位于 `/usr/include`）。风险较低的区域是支持二进制文件，位于 `/usr/bin` 和 `/usr/sbin`。

## 处理主密码文件

Linux 和 FreeBSD 都使用影子密码（shadow passwords），这是一种将加密的密码字符串存储在仅 root 可读的文件中的方法（参见第 9 章中的“/etc/passwd 和 /etc/master.passwd 文件”）。然而，FreeBSD 维护一个包含所有用户数据的 `/etc/master.passwd` 文件，而 `/etc/passwd` 仅仅是一个子集（不包含实际密码字符串）；Linux 的做法略有不同。Linux 的 `/etc/shadow` 文件除了用户名和哈希密码外，不包含任何其他有用信息。

结合 Linux 系统中的 `/etc/passwd` 和 `/etc/shadow` 文件，你可以拼凑出一个 `master.passwd` 文件，并将其安装到你的 FreeBSD 机器中，从而保留所有用户的登录数据。这可以通过 Perl 脚本完成（随附 CD-ROM 中提供，名为 `mkpasswd.pl`），如清单 19.1 所示。

**清单 19.1 将 Linux 用户数据库转换为 FreeBSD 使用的示例 Perl 脚本**

```perl
#!/usr/bin/perl
# Set this to the location of bash on your FreeBSD machine (if installed),
# or to /bin/csh to switch /bin/bash users to csh
$nshshell = "/bin/csh";

open (PASSWD, "/etc/passwd");
@passwd = <PASSWD>;            # Read in the /etc/passwd file
close (PASSWD);
open (SHADOW, "/etc/shadow");
@shadow = <SHADOW>;            # Read in the /etc/shadow file
close (SHADOW);

foreach $user (@shadow) {
    @sdata = split(/:/,$user);
    $passhash{$sdata[0]} = $sdata[1]; # Make a lookup table based on usernames
}
foreach $user (@passwd) {
    @pdata = split(/:/,$user);
    $pdata[6] = $nshshell."\n" if ($pdata[6] eq "/bin/bash\n");
    $pdata[1] = $passhash{$pdata[0]}; # Replace the "x" with the password hash
    splice @pdata,4,0,undef,"0","0"; # Splice in extra blank fields
    foreach ($pdata) {             # Print the combined output line
        print "$_";
        print ":" unless ($_ == /\n/);
    }
}
```

确保此脚本具有可执行权限；然后，登录到 Linux 机器，使用 `su` 获得超级用户权限，并运行脚本将输出发送到文件：

```sh
% ./mkpasswd.pl > new.master.passwd
```

将此 `new.master.passwd` 文件传输到你的 FreeBSD 机器并放入 `/etc`（`pwd_mkdb` 不喜欢输入文件和目的地位于不同文件系统上的情况）。在文本编辑器中打开该文件，然后在另一个窗口中打开 FreeBSD 的 `/etc/master.passwd`。你需要修改前大约 15 个用户名（例如 `daemon`、`bin`、`news` 以及在 Linux 和 FreeBSD 中 UID 不同的其他系统伪用户）的第一部分。只需从 FreeBSD 的 `/etc/master.passwd` 中复制这块用户内容到 `new.master.passwd` 文件中，替换新文件中对应的部分。

通过创建副本来备份现有的 `/etc/master.passwd`。最后，运行 `pwd_mkdb` 以生成新的密码文件和哈希数据库：

```
# pwd_mkdb -p /etc/new.master.passwd
```

如果该命令在没有错误的情况下完成，请勿立即注销——你需要在仍具有超级用户（root）权限时测试此操作，以便你可以修复可能存在的任何问题。此外，测试以确定你是否可以通过新的终端会话以普通用户身份登录。如果不能，请再次在之前创建的备份文件上运行 `pwd_mkdb`，数据库将恢复到其先前状态。

## 技术玄学

Linux 和 FreeBSD 之间有许多额外的琐碎差异。以下是一些最显而易见的差异列表：

-   FreeBSD 中的设备名称不如 Linux 中通用，但更具描述性。换句话说，Linux 中所有以太网卡都是 `eth0`、`eth1` 等，因此你可以轻松识别出它们是以太网卡，但无法立即区分不同的制造商或型号。FreeBSD 为每个卡制造商和型号都有特定的驱动程序，其名称大致对应制造商名称（`rl` 代表 RealTek，`sf` 代表 Adaptec Starfire 等）。类似地，Linux 中的硬盘是 `hda`、`hdb` 等；FreeBSD 中的驱动器，取决于它们是 IDE/ATA 还是 SCSI，是 `ad0` 和 `ad1` 或 `da0` 和 `da1`。这些名称告诉你更多关于你拥有设备具体类型的信息；但如果你只是试图找到哪个设备对应你的以太网卡或硬盘，它们可能比 Linux 中更令人困惑。
-   FreeBSD 没有 `System.map` 文件。Linux 使用此表来查找常用内核符号的跳转向量。FreeBSD 将这些符号构建到内核中，因此你无需担心它们。
-   FreeBSD 的默认 shell 是 `tcsh`，而不是 `bash`。`tcsh` 和 `csh` 彼此硬链接，因此 `csh` 等同于 `tcsh`。如果你想要 `bash`，你需要从 ports 或 packages 中安装它。
-   Linux 二进制兼容性包（你应该在有此机会时安装它）创建了一个 `/compat/linux` 树，其中包含基本 Linux 二进制文件和库结构，供真正需要它们的 Linux 打包程序使用。它还创建了一个 `linux.ko` 内核模块（你可以使用 `kldstat` 检查其状态）。这些结构主要透明地处理 Linux 可执行文件；可能会出现一些异常情况，但大部分时候处理是无缝的。不过，如果你可以从 packages 或 ports 安装 FreeBSD 原生版本，你肯定希望尽可能这样去做，如果可用的话。
-   除非你修改 `/etc/ttys` 文件，否则 FreeBSD 不允许你远程以 root 身份登录（详见第 10 章“用户和组介绍”中的说明）。如果你在任何程度上关心安全性，你将希望不要动 `/etc/ttys`，并使用 `su` 来处理超级用户任务。
-   从 5.0 版本开始，FreeBSD 使用 DEVFS 设备文件系统，而不是填充有“特殊”文件的标准 `/dev` 目录。有关如何使用 DEVFS 和设备提示的更多信息，请参见第 17 章。
-   FreeBSD 中 PCI 总线上的设备按顺序编号，从主板上的设备零开始，然后随着它们沿着 PCI 链远离主板而增加。在 Linux 中，主板上的设备通常编号最高，且随着距离主板的距离增加，编号减小。这意味着，在拥有两个以太网卡的机器上，Linux 下的 `eth0` 和 `eth1` 在 FreeBSD 下可能分别变成 `fxp0` 和 `fxp1`。
-   在撰写本文时，由于市场渗透率不完整，将你的 Tux T 恤和豆袋换成 Daemon 风格的可能会让人有些沮丧。

然而，除了适应这些微小的差异外，从 Linux 过渡到 FreeBSD 应该会相当顺利。

## 应该做和不应该做（常见陷阱）

每个操作系统都有许多陷阱等待捕捉不小心的人。这些陷阱在系统新安装时似乎特别危险。本节列出了一些最常犯的错误和一些对于有效 FreeBSD 管理最有价值的建议。

**应该做：**

-   使用 ports 和 packages 安装软件。虽然可以直接从开发人员那里获取特定程序的源码并使用其内置脚本进行编译，但这只是污染了你的核心系统用户空间。如果该程序没有作为 port 提供，请发帖到 freebsd-ports@freebsd.org 邮件列表请求提供，或者你甚至可以学习移植过程并成为维护者。
-   关注每日、每周和每月的 periodic 输出消息。任何 `suid` 可执行文件差异都会在安全报告中被标记。这些消息还会提醒你文件系统使用率、被拒绝的邮件主机，以及许多其他形式的可见性，这些是对抗入侵者的有效“闭路电视”。
-   熟悉 CVSup。CVSup 是你的朋友。它不仅可以在所有时候保持你的源码和 ports 同步，还可以作为一种有效的镜像解决方案，正如本章稍后“镜像”部分所述。

