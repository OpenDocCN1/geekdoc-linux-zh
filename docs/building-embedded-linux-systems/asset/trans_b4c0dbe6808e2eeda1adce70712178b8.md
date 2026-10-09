

该方法假设设备在运行期间，将内核及其他关键系统软件保留在临时内存中，如前文“将文件系统保留在 RAM 中”所述。在启动过程中，引导加载程序会从根文件系统将系统软件复制到 RAM。因此，要安装新软件，只需使用新版本重写存储软件的压缩 CPIO 归档文件，然后重启系统即可。

只要在向存储设备写入新软件的关键时刻不失去电源，并且新软件功能正常，系统就能良好运行。然而，如果在升级循环期间断电，或者加载了损坏或仅存在 bug 的映像，可能会将一个 200 美元的电子产品变成一块毫无价值的塑料砖。换句话说，你需要具备最低限度的功能性软件才能升级系统。

## rsync

另一种升级方法涉及在根文件系统联机状态下更新单个文件。这种方法仅适用于软件直接从可写的持久性根文件系统运行的情况，如前文“使用在线可写持久存储”所述。

rsync 是一种远程更新实用工具，允许你将本地目录树与远程服务器同步。其算法通过仅传输本地文件和远程文件之间的差异来优化传输。使用适当的选项运行 rsync 时，它可以保留文件权限、文件所有权、符号链接、访问时间戳以及设备条目。它可以采用 rsh 或 ssh 与远程服务器进行通信。所有这些特性使 rsync 成为更新网络启用嵌入式系统的良好候选者。

rsync 可在其项目网站 http://samba.anu.edu.au/rsync 上获取。该网站还托管其文档和邮件列表。Michael Holve 撰写的良好入门教程可在 http://everylinux.org/rsync 获取。

要使用 rsync，你必须在服务器上以守护进程形式运行 rsync 可执行文件，并且必须在嵌入式系统上将可执行文件作为客户端调用。由于上述教程和 rsync 文档已很好地涵盖了服务器安装和客户端使用的细节，因此我们将不详细讨论这些内容。我们仅解释如何交叉编译并安装 rsync 以供目标使用。本节中的示例安装的是 rsync 版本 2.6.9。

首先，下载并解压 rsync 软件包副本到你的 `${PRJROOT}/sysapps` 目录。解压软件包后，在后续步骤中移动到其目录：

```
$ cd ${PRJROOT}/sysapps/rsync-2.6.9/
```

现在，配置并编译该软件包：

```
$ CC=arm-linux-gcc ./configure --host=$TARGET --prefix=${TARGET_PREFIX}
$ make
```

编译完成后，在目标根文件系统上安装 `rsync` 二进制文件并进行 strip 处理：

```
$ cp rsync ${PRJROOT}/rootfs/bin
$ arm-linux-strip ${PRJROOT}/rootfs/bin/rsync
```

经过 strip 处理的二进制文件在动态链接 glibc 时大小为 291 KB，在动态链接 uClibc 时大小为 286 KB。

同一二进制文件可用于命令行和作为守护进程。在服务器上运行时，请包含 `--daemon` 选项。我们将仅在命令行上使用 `rsync`。

要使用 `rsync`，你需要在目标上安装 `rsh` 或 `ssh`。`rsh` 作为 netkit-rsh 软件包的一部分，可在 <http://ftp.uk.linux.org/pub/linux/Networking/netkit> 获取。`ssh` 作为 OpenSSH 软件包的一部分提供，第 10 章将深入讨论该软件包。尽管该讨论集中在由 Dropbear 生成的 SSH 守护进程（`sshd`）的使用上，但在编译 Dropbear 软件包期间也可以生成 SSH 客户端（`ssh`）。以下步骤假设你使用的是 `ssh` 而不是 `rsh`，因为 `ssh` 提供安全的传输通道，因此被大多数管理员认为更优越。

一旦在目标上安装了 `rsync`，你就可以在目标上使用如下命令来更新其根文件系统：

```
# rsync -e "ssh -i root" -r -l -p -t -D -v --progress \
> 192.168.172.50:/home/karim/contro1-project/user-interface/rootfs/* /
root@192.168.172.50’s password: Enter your password
receiving file list ... done
bin/
dev/
etc/
lib/
sbin/
tmp/
usr/bin/
usr/sbin/
bin/busybox
750756 (100%)
bin/tinylogin
39528 (100%)
etc/inittab
377 (100%)
etc/profile
58 (100%)
lib/ld-2.2.1.so
111160 (100%)
lib/libc-2.2.1.so
1242208 (100%)
sbin/nft1_format
8288 (100%)
sbin/nftldump
7308 (100%)
sbin/unlock
3648 (100%)
bin/
dev/
etc/
lib/
sbin/
wrote 32540 bytes read 2144597 bytes 150147.38 bytes/sec
total size is 3478029 speedup is 1.60
```

该命令从 IP 地址为 192.168.172.50 的主机上的 root/5 目录复制用户界面模块项目的内容到目标的根目录。要使该命令成功运行，主机必须同时运行 sshd 和 rsync 守护进程。

以下是你需要使用的选项：

- -e：将用于连接远程服务器的应用程序名称传递给 rsync。（在此情况下，我们使用 `ssh -l root` 以 root 身份连接到服务器。你可以将 root 替换为任何适当的用户名。如果未提供用户名，ssh 将尝试使用与会话所有者相同的用户名进行连接。）
- -r：递归复制目录。
- -l：保留符号链接。
- -p：保留文件权限。
- -t：保留时间戳。
- -D：保留设备节点。
- -v：提供详细输出。
- --progress：报告传输进度。

运行期间，rsync 会提供每个复制或目录的列表，并维护一个计数器，显示已完成的传输百分比。完成后，rsync 会在本地复制远程目录，目标的根文件系统将与服务器上的最新目录同步。

如果你想检查哪些文件将被更新而不执行实际更新，你可以使用 -n 选项对 rsync 进行“试运行”：

```
# rsync -e "ssh -i root" -r -l -p -t -D -v --progress -n \
> 192.168.172.50:/home/karim/contro1-project/user-interface/rootfs/* /
root@192.168.172.50's password:
receiving file list ... done
bin/busybox
bin/tinylogin
etc/inittab
etc/profile
lib/lib-2.2.1.so
lib/lib-2.2.1.so
sbin/nft1_format
sbin/nftldump
sbin/nflock
wrote 376 bytes read 5198 bytes 716.53 bytes/sec
total size is 3478029 speedup is 647.20
```

有关 rsync 作为客户端和服务器使用的更多信息，请查阅该命令的手册页以及项目网站上可用的文档。

通过 rsync 升级文件面临与前一节中描述的单个文件更新相同的可靠性问题。升级期间的停电可能导致系统不可用，尽管故障模式会略有不同：中断的更新可能已更新了一个文件，但未能更新其依赖的其他文件。例如，如果升级过程已将系统中的可执行文件升级到更新版本，但未能更新该可执行文件所需的动态共享库，那么在电源恢复时系统甚至可能无法启动。

涉及多个文件的更新方法留下了另一个不那么明显的问题来源。支持人员和专业服务可能在处理日常问题时更新特定文件以向用户提供“热修复”，从而在现场留下任意数量的略有不同的软件版本。

只有明确陈述的政策和组织纪律才能保护你免受维护那些你并不完全了解的系统的痛苦。必须仔细记录所有系统何时以及如何更新，因为在事后很难确切知道哪些文件已被替换。下一节中的技术也可以帮助你避免多个版本造成的混乱。

## 包管理工具

像上一节中使用 rsync 那样同时更新构成根文件系统的所有软件包，并不总是可能或可取的。此外，正如我们已所述，进行跟踪非常困难。有时，最好的方法是使用包管理系统单独升级每个包，例如工作站和服务器发行版中常用的那些。例如，如果你在工作站上使用 Linux，你很可能已经熟悉用于 Linux 的两大主要包管理系统之一，即 RPM 包管理器（RPM）或 Debian 包（dpkg），具体取决于你的发行版基于哪个系统。由于这些系统在帮助用户和系统管理员维护其系统方面有着良好的记录

