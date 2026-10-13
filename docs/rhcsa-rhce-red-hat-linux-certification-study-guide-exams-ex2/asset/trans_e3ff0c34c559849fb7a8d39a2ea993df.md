
检查 nfsd、rpc.mountd 和 rpc.rquotad 服务是否正在运行。除非系统是 Kerberos 客户端，否则不必担心 nfs 状态命令输出中出现以下信息：

```
rpc.svcgssd is stopped
```

共享 NFS 目录的广告依赖于 RPC。而这始于由 /etc/init.d/rpcbind 脚本控制的 rpc.statd 服务。如果所有这些服务都在运行，还需要检查的一件事是 rpcinfo -p 命令的输出。如图 16-1 所示，它列出了许多服务和端口。

对于 NFSv2 和 NFSv3，如果端口未按 /etc/sysconfig/nfs 固定，则无法设置基于 iptables 的防火墙来支持通过这些端口的通信。如果图 16-1 中显示的服务并非全部出现在本地系统上，可能缺少某些内容。

现在要将此目录挂载到本地，需要一个空的本地目录。创建类似 /remotemnt 的目录。然后你可以使用以下命令从类似 192.168.122.50 的系统挂载共享目录：

```
# mount.nfs4 192.168.122.50:/mnt /remotemnt
```

此命令将该 IP 地址上的计算机上的 NFS 共享 /mnt 目录挂载。如果需要，可以用 mount -t nfs4 命令替换 mount.nfs4。成功后，你将能够像访问本地目录一样访问远程 /mnt 目录中的文件。

## Configure NFS in /etc/fstab

你也可以配置 NFS 客户端在启动过程中挂载远程 NFS 目录，如 /etc/fstab 中所定义。例如，客户端 /etc/fstab 中的以下条目基于 NFSv4，将名为 nfssrv 的计算机上的 /home nfs 共享挂载到本地 /nfs/home 目录：

```
nfssrv:/home nfs /nfs/home nfs4 soft,timeo=100 0 0
```

> 考试提示
> 
> 可以在 nfs 手册页中找到也可以在 /etc/fstab 中使用的 mount 命令的 NFS 特定选项。

soft 和 timeo 选项是多种专用 NFS 挂载选项的一部分。如下所示的此类选项也可以用于自定义在 /etc/fstab 文件中启动过程中如何进行挂载。有关这些及相关选项的更多信息，请参阅可通过 man nfs 命令获得的 nfs 手册页。

另外，可以使用 automounter 根据客户端计算机的需求动态挂载 NFS 文件系统。automounter 在一段时间内无活动后也可以卸载这些远程文件系统。有关管理 autofs 服务的更多信息，请参阅第 6 章。

如果没有超时，通过 /etc/fstab 进行的 NFS 挂载可能会出现问题。例如，如果网络或 NFS 服务器宕机，缺乏超时可能会导致客户端挂起。（我在本章前面更详细地讨论了这个问题。）如果在启动过程中发生挂起，这是一个大问题，因为启动可能永远无法完成，你将不得不通过启动到未启动网络的某个运行级别（如 1 或单用户）来恢复系统。

## Diskless Clients

NFS 支持无盘客户端，即不将操作系统存储在本地的计算机。无盘客户端可能使用启动软盘或启动可编程只读存储器（PROM）芯片来启动。然后嵌入式命令可以挂载适当的根（/）目录，设置交换空间，将 /usr 目录设为只读，并将其他共享目录（如 /home）配置为读写模式。如果你的计算机使用启动 PROM，你还需要访问 DHCP 和 TFTP 服务器以获取网络和内核信息。

Red Hat Enterprise Linux 包含支持无盘客户端的功能。虽然它们未列为当前 Red Hat 考试要求或相关课程大纲的一部分，但我不会对未来出现此类要求感到惊讶。有关该主题的开源 Red Hat 项目的更多信息，请参阅 https://fedorahosted.org/cobbler/ 上的 Cobbler 项目。

## Soft Mounting

挂载 NFS 文件系统时请考虑使用 soft 选项。当 NFS 服务器失败时，以 soft 方式挂载的 NFS 文件系统会失败而不是挂起。然而，这会因临时网络中断而导致长时间运行的进程失败的风险。

此外，你可以使用 timeo 选项设置超时间隔，以十分之一秒为单位。例如，以下命令将以 30 秒的超时挂载 /nfs/home（timeo 使用十分之一秒）：

```
# mount -o soft,timeo=300 myserver:/home /nfs/home
```

## Current NFS Status

NFS 服务的当前状态主要记录在两个目录中：/var/lib/nfs 和 /proc/fs/nfsd。如果 NFS 出现问题，请查看这些目录中的一些文件。一次处理一个目录。首先，/var/lib/nfs 目录中有两个关键文件：

- **etab** 包含导出的目录的完整描述，包括默认选项。
- **rmtab** 指定当前已挂载的共享目录的状态。

查看 /proc/fs/nfsd 目录的内容。作为虚拟目录，/proc 目录树中的文件大小为零。然而，作为动态文件，它们可能包含有价值的信息。也许基本操作的关键选项是名为 versions 的文件。该文件的内容指定了当前识别的 NFS 版本。

该文件的正常内容有点晦涩，表明当前 NFS 服务器可以使用 NFSv2、NFSv3 和 NFSv4 进行通信，但不能使用 NFS 版本 4.1。

```
+2 +3 +4 -4.1
```

因此，当我在 /etc/sysconfig/nfs 文件中意外激活了 #RPCNFSDARGS="-N 4" 选项时，versions 文件的内容变为

```
+2 +3 -4 -4.1
```

区别很微妙，但告诉我本地 NFS 服务器当前不识别 NFSv4 连接。当然，鉴于 NFSv4 相关的优势，你不应激活 RPCNFSDARGS="-N 4" 选项。

## CERTIFICATION OBJECTIVE 16.03

## The Very Secure FTP Server

文件传输协议是使用 TCP/IP 协议套件开发的原始网络应用程序之一。它遵循网络服务的标准模型，因为 FTP 需要客户端和服务器。lftp 命令行客户端可以从同名软件包轻松安装。FTP Server 软件包组包含默认的 Red Hat FTP 服务器，即非常安全的 FTP（vsFTP）守护进程。本节重点介绍 FTP 服务器的配置。你将使用第 2 章中描述的 lftp 客户端测试结果。虽然 Linux 还有许多其他优秀的 FTP 服务器，但 vsFTP 是 RHEL 6 上唯一受支持的服务器。

## Basic vsFTP Configuration

使用以下命令安装 vsFTP 及其依赖项是最简单的方法：

```
# yum install vsftpd
```

当然，如果你在生产环境或考试期间安装 vsFTP，运行以下类似命令很重要：

```
# /etc/init.d/vsftpd start
# chkconfig vsftpd on
```

如第 11 章所述，这些命令启动了指定的服务，并确保系统下次重新启动时服务也会启动。安装后，相关配置文件可以在 /etc/vsftpd 目录中找到。在 /etc/pam.d 目录中还有一个额外的配置文件 vsftpd。使用 ldd 和 strings 命令检查 /usr/sbin 目录中的 vsftpd 守护进程，确认 vsFTP 可以使用第 10 章中描述的 TCP Wrappers 文件进行保护。然而，在 vsFTP 可以使用 TCP Wrappers 保护之前，你需要确保在 vsftpd.conf 配置文件的末尾保留一个关键选项。

vsftpd.conf 配置文件的主页列出了所有可用指令的完整列表，分为三个类别：

- boolean 类似于 SELinux 选项，可以设置为 yes 或 no。
- numeric 可以设置为特定数值。
- string 与诸如文件名之类的值相关联。

## The Main vsFTP Configuration File

主要的 vsFTP 配置文件是 /etc/vsftpd 目录中的 vsftpd.conf。通常情况下，它相当安全。但如果配置不正确，你可能会为使用普通用户账户连接的用户提供访问顶级根目录的权限。要开始保护 vsFTP 服务器，可以配置 vsFTP 禁止普通
