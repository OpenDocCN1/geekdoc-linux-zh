

/EVERY:date[,...]

重复任务通过日期（星期一、星期二，等等）或月中的某一天（1-31）来安排。

/NEXT:date[,...]

使用此选项在日期下一次发生时安排任务。指定一个或多个日期（星期一、星期二，等等）或月中的某一天（1-31）。

“command”

要执行的命令。

我们现在可以将之前的 **NTBACKUP** 命令与 AT 结合使用，以执行计划备份。通过将之前的 **NTBACKUP** 命令放入 **backup** 文件中，我们可以发出以下命令：

```
C:\ AT 03:00 /every:Monday,Tuesday,Wednesday,Thursday,Friday "backup"
```

# 第 20 章

# Samba

## Samba 概述

Samba 是一个应用程序，允许 UNIX 主机作为 Windows 系统的文件服务器。Windows 系统可以使用其原生的 Windows 网络访问 UNIX 文件系统和打印机。

本章的目标是概述 Samba 的设置，并展示其功能的一个子集。我们将仅关注文件服务器功能。我们将在远程 UNIX 系统上设置共享，这些共享在 Windows 系统上将显示为驱动器字母和图标。由于 Samba 随本书中使用的 Red Hat Linux 软件一起提供，我们将在 Linux 系统上设置并运行 Samba。Samba 可用于大多数 UNIX 变体。

Samba 使用服务器消息块（SMB）协议提供此文件共享功能。SMB 运行在 TCP/IP 之上。在本章的示例中，Windows 系统和 UNIX 系统都在运行 TCP/IP 和 SMB。这些提供了在两个系统之间建立文件共享所需的所有技术。

第 16 章介绍了在 Windows 系统上运行并访问 UNIX 系统上文件的网络文件系统（NFS）。此功能与本章我们将介绍的 Samba 功能类似。除了文件共享功能外，Samba 还提供打印机共享和额外的用户访问控制功能。我们将在本章中不重点介绍这些功能；但是，Samba 确实在这些方面提供了一些高级功能。

在撰写本章时，Samba 包含上述提到的功能：文件共享、打印机共享以及文件的高级用户访问控制。许多基于 GNU 通用公共许可证（GPL）作为自由软件提供的 Samba 和其他软件正在不断进行改进。由于软件是免费的，许多人可以访问它并花时间增强软件。因此，您可能会发现 Samba 和其他此类软件中包含了额外的功能。Samba 有许多计划中的增强功能，包括管理工具和其他在本章撰写时尚未可用的改进。本章末尾提供了有关获取 Samba 和其他自由软件的更多信息。

## 设置

由于 Samba 包含在 Red Hat Linux CD-ROM 中，我们将使用 Red Hat Linux 通过一个简单的 Samba 设置过程进行讲解。在安装 Red Hat Linux 时，您可以选择希望加载的软件包，这与其他大多数 UNIX 变体一样。如果您在最初安装操作系统时未加载 Samba，可以使用 *GNOME RPM* 工具或命令行中的 **rpm** 来加载 Samba 或其他任何软件。这些工具在系统管理章节中简要介绍过。

使用 *linuxconf*，我们将执行一些简单的任务来设置 Samba。图 20-1 显示了 *linuxconf* 窗口下 *Samba 文件服务器* 中的 *磁盘共享*，其中包含我们在此示例中将使用的三个磁盘共享。

![](img/75f39fc91296b889c0653851accdfd46_1364_0.png)

**图 20-1** Linuxconf 中的共享信息

我们的 Linux 系统上有三个共享名称，我们将这些共享提供给其他运行 SMB 的系统。图 20-2 显示了名为 home 的中间共享的更详细信息。

![](img/75f39fc91296b889c0653851accdfd46_1365_0.png)

**图 20-2** Linuxconf 中的 /home 共享信息

此共享用于 linux1 上的 /home 目录。请注意图中与权限相关的四个选项。我们已在此共享上授予公共访问、可写和可浏览权限。我们未将其限制为仅访客访问。在此共享上，我们在授予的权限方面没有限制。在您分配这些权限时，希望仔细考虑这些权限。请记住，为了保持示例简单，我们在示例中没有使用任何用户身份验证。然而，在实际操作中，您将确保为共享分配适当的权限。

分配完三个共享后，我们将使用 *Linuxconf* 启动 *smb*。我们通过启用 *控制服务活动* 中的 *smb* 来实现这一点，如图 20-3 所示。

![](img/75f39fc91296b889c0653851accdfd46_1366_0.png)

**图 20-3** 在 *Linuxconf* 的 *控制服务活动* 中启动 *smb*

*smb* 已启用，以便服务在系统启动时开始运行。

在我们开始使用 SMB 之前，让我们对使用 *Linuxconf* 进行的工作进行几次快速检查。我们本可以手动完成所有使用 *Linuxconf* 所做的操作。

第一个检查是查看文件 */etc/smb.conf*。此文件包含我们所有的 SMB 配置信息。暂时，让我们直接进入“共享定义”部分，以确认我们在 *Linuxconf* 中配置的三个共享在 */etc/smb.conf* 中有正确的条目：

```text
#===================== Share Definitions ======================
[homes]
comment = Home Directories
browseable = no
writable = yes

# Un-comment the following and create the netlogon directory for
Domain Logons
; [netlogon]
; comment = Network Logon Service
; path = /home/netlogon
; guest ok = yes
; writable = no
; share modes = no

# Un-comment the following to provide a specific roving profile
share
# the default is to use the user's home directory
;[Profiles]
; path = /home/profiles
; browseable = no
; guest ok = yes

# NOTE: If you have a BSD-style print system there is no need to
# specifically define each individual printer
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
# Set public = yes to allow user 'guest account' to print
   guest ok = no
   writable = no
   printable = yes

[root]
comment = root dir on linuxl
available = yes
path = /
public = yes
guest only = no
writable = yes
browseable = yes
only user = no

[home]
comment = home on linuxl
available = yes
path = /home
public = yes
guest only = no
writable = yes
browseable = yes
only user = no

[/home/martyp]
comment = /home/martyp on linuxl
available = yes
path = /home/martyp
public = yes
guest only = no
writable = yes
browseable = yes
only user = no
```

确实在 /etc/smb.conf 中为我们配置在 Linuxconf 中的三个共享设有条目，权限也是我们设置的。这些条目显示在列表的末尾附近。接下来我们将运行一个名为 testparm 的 Samba 实用工具。此工具将检查我们的 /etc/smb.conf 文件是否存在错误。此工具会产生非常长的输出，我不会在此处包含，但您应该运行它并检查它产生的任何警告或错误。

对于我们的 /etc/smb.conf 文件，testparm 仅在文件的最开头产生了一个警告，如下所示：

```text
# testparm smb.conf
Load smb config files from /etc/smb.conf
Processing section "[homes]"
Processing section "[printers]"
Processing section "[root]"
Processing section "[home]"
Processing section "[/home/martyp]"
Loaded services file OK.
WARNING: You have some share names that are longer than 8 chars
These may give errors while browsing or may not be accessible to some older clients
Press enter to see a dump of your service definitions
```

**testparm** 为长共享名称产生了警告，并且还列出了我们的三个共享，看起来顺序正常。我们不会处理长共享名称警告，因为示例中使用的 Windows 系统可以处理长名称。然而，如果我们使用的是 DOS 系统，那么该名称将存在问题。我们稍后将看到 Linux 如何处理这些潜在的名称不兼容性。

我们要执行的下一个检查是查看 Samba 的守护进程 **smbd** 是否确实在运行，如下所示：

![](img/75f39fc91296b889c0653851accdfd46_1369_0.png)

```text
# ps -efl | grep smbd

140  S  root   490   1  0  60   0 -   553 do_sel Sep28 ? 00:00:00 [smbd]
140  S  root  1493  490  0  60  0 -   896 do_sel Sep29 ? 00:00:00 smbd -D
000  S  root  1976 1951  0  70  0 -   288 pipe_r 09:09 pts/1 00:00:00 grep smbd
```

此 **ps** 输出表明 **smbd** 正在运行。接下来，让我们检查 **netbios-ssn** 服务是否处于“LISTEN”状态，如下例所示：

![](img/75f39fc91296b889c0653851accdfd46_1369_1.png)

![](img/75f39fc91296b889c0653851accdfd46_1369_2.png)

```text
# netstat -a | grep netbios

tcp   0  0 linux1:netbios-ssn   f4457mf2:1047        ESTABLISHED
tcp   0  0 :netbios-ssn   *:                 LISTEN
udp   0  0 linux1:netbios-dgm   *:*
udp   0  0 linux1:netbios-ns   *:*
udp   0  0 :netbios-dgm   *:*
udp   0  0 :netbios-ns   *:*
```

