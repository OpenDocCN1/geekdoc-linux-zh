
## 如何配置 NIS 客户端？

你还可以通过使用 SAM 或手动操作来配置 NIS 客户端。同样，《安装和管理 NFS 服务》手册提供了配置客户端的出色逐步操作指南。

要通过 SAM 进行配置，请选择 *网络/通信*，然后选择 NIS。首先系统会提示你指定 NIS 域名。之后，你可以继续进入 *启用 NIS 客户端* 菜单。

无论哪种方式，我有两点额外的建议。首先，HP 提供了以下 `/etc/nsswitch.compat` 文件作为模板，供你复制到 `/etc/nsswitch.conf`。这允许你在 `/etc/passwd` 和 `/etc/group` 中使用“+”和“-”语法：

```
# /etc/nsswitch.compat:
# An example file that could be copied over to
# /etc/nsswitch.conf; it
# uses NIS (YP) in conjunction with files. #

passwd:		compat
group:		compat
hosts:		nis [NOTFOUND=return] files
networks:		nis [NOTFOUND=return] files
protocols:		nis [NOTFOUND=return] files
rpc:		nis [NOTFOUND=return] files
publickey:		nis [NOTFOUND=return] files
netgroup:		nis [NOTFOUND=return] files
automount:		files nis
aliases:		files nis
services:		files nis
```

其次，你可能更倾向于使用 DNS 而非 NIS 来管理主机数据库，并在 `/etc/nsswitch.conf` 中使用以下“hosts”条目：

```
hosts:		files [NOTFOUND=continue] dns ...
```

或者

```
hosts:		dns	[NOTFOUND=continue,UNAVAILABLE=continue]
			files [NOTFOUND=continue,UNAVAILABLE=continue] nis
```

## 如何维护我的 NIS 环境？

最常见的用户操作是更改用户密码。用户可以使用 **passwd -r nis** 或 **yppasswd** 命令来执行此操作。这将提示输入旧的 NIS 密码、新密码，在 NIS 服务器上执行更改，并且默认情况下会重新制作 NIS 映射并将其推送到所有从服务器（Slave Servers）。

系统管理员可以通过 SAM、shell 脚本或命令（如 `passwd -r nis <username>` 或 `yppasswd <username>`）来更改用户密码。你还可以使用 SAM 添加新用户，或者通过 shell 脚本或命令来完成此操作。

通常，当用户通过 **vi** 编辑修改数据库文件时，如果需要将更改编译到 NIS 映射中（称为“制作”映射），并且“make”操作未自动完成此任务，则还需将映射推送到从服务器。例如，在修改了 `/etc/passwd.nis` 中某些用户的主目录后，系统管理员需要：

1. `cd /var/yp` # 切换到 NIS Makefile 所在目录
2. `make passwd` # “制作”或编译 passwd 映射
3. `yppush passwd` (如果步骤 #2 未推送到 NIS 从服务器)

这里有一个适用于 HP-UX 及任何 NIS 厂商实现（涉及分组文件）的技巧。有时用户属于多个组，导致 `/etc/group` 中的行长度超过 NIS 每行 1024 个字符的限制。为了绕过此限制，请使用不同的组名来表示相同的 GID，例如：

```
102 support:brian,sam,charlie
102 support1:bill,julie,maria
```

请注意，你不需要在 `/etc/group` 中指定用户的主要组成员资格，因为这在 `/etc/passwd` 中已通过其 GID 指定。如果用户属于多个组，你只需在 `/etc/group` 条目中将其用户名添加到他们的次要组中即可。

NIS 提供了一种集中式数据库方案，用于管理用户密码和组信息。用于 NIS 设置和管理的行政管理技术文档齐全，已集成到 SAM 中，并且通常与其他 NIS 实现具有互操作性。

## 第 7 章

## 备份

### 虚拟分区备份

虚拟分区（Virtual Partitions, vPar）的备份方式与非 vPar 系统几乎相同。主要区别在于，你不需要在物理系统上运行一次备份，而是必须对物理系统上存在的每个虚拟分区运行备份。你还必须对每个虚拟分区运行 **make_net_recovery**。这将为该虚拟分区创建一个可引导的恢复存档。这在 Ignite/UX 第 10 章中进行了介绍。

我们将对系统中第一个 vPar 执行备份，该系统的磁带驱动器已配置为其组件之一（这是备份到本地磁带驱动器）。然后，我们将对同一台计算机上的第二个 vPar 执行备份，目标是配置在第一个 vPar 上的磁带驱动器（这是备份到远程磁带驱动器）。磁带驱动器对于第二个 vPar 来说是远程的，因为它未将磁带驱动器配置为其 I/O 组件之一。由于两个 vPar 是独立且不同的系统，第一个 vPar 上的磁带驱动器对于第二个 vPar 来说是远程的。

![](img/eff8b9287a5f38c5adf538f24aacf29e_412_0.png)

### 备份到本地虚拟分区上的磁带驱动器

现在让我们将名为 *cable1* 的 vPar 备份到位于路径 *0.0.1.0.3.0* 的本地 DDS 驱动器。这是将 vPar 备份到本地磁带驱动器，意味着磁带驱动器资源与执行备份的 vPar 绑定。下面的 **vparstatus** 显示位于 *0.0* 的本地总线适配器（LBA）专门分配给 *cable1*：

```
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:	cable1
State:		Up
Attributes:	Dynamic,Manual
Kernel Path:	/stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:	1/3
Bound by User [Path]:
Bound by Monitor [Path]:	33
Unbound [Path]:	97

[IO Details]
						<-- path of Core I/O card
0.0.0.0
	0.0.1.2.0	BOOT
0.0.4.0	CONSOLE

[Memory Details]
Specified [Base	/Range]:
		(bytes)	(MB)
Total Memory (MB):	1024
#
```

虽然位于 *0.0.1.0.3.0* 的磁带驱动器未在此 **vparstatus -v** 输出中显示，但磁带驱动器连接到位于 *0.0* 的核心 *I/O* 卡，因此 *cable1* 可以访问它并将其用作备份设备。

顺便提一下，如果磁带接口不在专用于 *cable1* 的核心 *I/O* 卡上，我们可以将接口从 *cable1* 移动到同一台计算机上名为 *cable2* 的第二个 vPar，确认驱动程序在 `/stand/system` 中，然后备份 *cable2*。

由于你可能想要在系统中运行的 vPar 之间移动许多设备，因此务必确保你的内核中包含了支持这些设备所需的所有设备驱动程序。

现在让我们运行 **fbackup**，使用 `-u` 更新备份数据库，`-O` 执行完整备份，`-f` 指定我们要写入备份的目标文件，`-g` 指定我们的图文件，`-I` 指定索引文件的名称，最后，我们将消息重定向到一个包含备份日志的文件。我们将把日期和时间附加到索引文件和备份日志文件的末尾。

以下示例显示了发出的 **fbackup** 命令：

```
fbackup -Ou -f /dev/rmt/0m -g /tmp/backupgraph -I
    /tmp/backupindex.`date '+%y%m%d.%H:%M'` 2>
    /tmp/backuplog.`date '+%y%m%d.%H:%M'`
```

图文件用于指定要包含在备份中的文件。索引文件包含作为备份一部分生成的文件列表。图文件包含我们希望作为备份一部分包含（i）或排除（e）的文件。在我们的情况下，该文件仅包含以下行：

```
i /var/tmp
```

现在让我们看看发出此命令后生成了哪些文件。首先查看备份索引和备份日志文件：

```
# ls -l /tmp/backup*
-rw-rw-rw- 1 root sys   11 Aug 29 14:45 backupgraph
-rw------- 1 root sys  778 Aug 29 15:08 backupindex.010829.15:08
-rw-rw-rw- 1 root sys  521 Aug 29 15:08 backuplog.010829.15:08
#
```

```
# cat /tmp/backupindex.010829.15:08
1024      1 /var
1024      1 /var/tmp
1024      1 /var/tmp/aaaa04686
108       1 /var/tmp/ems_inittab.old
1241      1 /var/tmp/election2
28        1 /var/tmp/envd.action5
4106      1 /var/tmp/inetd.conf.old
96        1 /var/tmp/ntp
0         1 /var/tmp/rdsKUBAA02185
0         1 /var/tmp/rdsKWWAA01840
310       1 /var/tmp/sh1649.1
343       1 /var/tmp/sh1649.2
166       1 /var/tmp/sh1649.3
440       1 /var/tmp/sh1649.4
611       1 /var/tmp/swagent.log
0         1 /var/tmp/sysstat_em.fmt
22734848  1 /var/tmp/vmunix.noreloc
#
```

```
# cat /tmp/backupgraph
i /var/tmp
#
```

```
# cat /tmp/backuplog.010829.15:08
fbackup(1417): cannot open the dates file /var/adm/fbackupfiles/dates
for reading
fbackup(1004): session begins on Wed Aug 29 15:08:10 2001
fbackup(3203): volume 1 has been used 1 time(s)
fbackup(3024): writing volume 1 to the output file /dev/rmt/0m
fbackup(1423): WARNING: could not open the dates file /var/adm/fbackup-
files/dates for writing
fbackup(1030): warnings encountered during backup
fbackup(3055): total file blocks read for backup: 44432
#
```

这两个在文件名末尾附加了日期 *(2001年8月29日 15:08)* 的文件是由之前发出的 **fbackup** 命令生成的。附加在文件末尾的日期有助于备份文件的组织。我们可以使用 **frestore** 恢复其中任意或所有文件。

将 vPar *cable1* 备份到本地磁带驱动器，这是对主机名为 *cvhdcn3* 的系统的备份。在此系统上运行的另一个 vPar *cable2* 未包含在备份中，因为其主机 *cvhdcn4* 被视为一个独立的系统。在下一节中，我们将看到如何备份 *cable2* 到专门分配给 *cable1* 的磁带驱动器。

### 备份到不同本地虚拟分区上的磁带驱动器

上一节中的磁带驱动器连接到 *cable1* 并用于备份 *cable1*。现在让我们使用 *cable1* 虚拟分区中的磁带驱动器来备份 *cable2*。请记住，具有主机名...

