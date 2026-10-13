
3. 重启后，您应该使用以下命令验证 Samba SELinux 设置的至少一项适当更改：

    # getsebool samba_enable_home_dirs

4. 此外，您还应确认适当目录已配置为 samba_share_t 文件类型，不仅在所注目录中使用 ls -Z 命令，还应在 /etc/selinux/targeted/contexts/files 目录中的 file_contexts.local 文件中进行确认。

![](img/9139201cfcaf4292284a0eed074928e5_873_0.png)

## 16

## 更多文件共享服务

## 认证目标

- 16.01 网络文件系统（NFS）服务器 ✔ 两分钟练习
- 16.02 测试 NFS 客户端 问答 自测
- 16.03 非常安全的 FTP 服务器

Linux 专为网络而设计。除了第 15 章中介绍的 Samba 之外，还有另外两个与在网络上共享文件相关的主要服务：NFS 和 FTP。Red Hat 未为这些服务提供 GUI 工具。即使 Red Hat 提供了此类工具，从命令行学习配置这些服务也最快。如果您了解这些服务，则可以直接编辑关键配置文件，从而在更短的时间内完成更多工作。

本章首先介绍网络文件系统（NFS），这是一种在服务器和工作站之间共享文件系统功能强大且多用途的方式。NFS 客户端功能包含在 RHEL 6 的默认安装中，并支持连接到 NFS 服务器的连接。

本章随后介绍非常安全的 FTP（vsFTP）守护进程，它提供基本和安全的 FTP 服务器服务。使用 vsFTP，您可以使用各种级别的访问控制来保护用户、目录、子目录和文件。

这些是您可能在 Red Hat 考试中配置和/或排除故障的另外两个网络服务。花时间了解与每个服务相关的配置文件，并练习在 Linux 计算机上使它们正常工作。在某些情况下，使用两台或三台运行 Linux 的计算机将有助于练习本章的课程。

## 考试内情

在 RHCE 目标中，NFS 的要求与 Samba 基本相同。当然，与 NFS 配置相关的要求与 Samba 的要求大不相同。因此，当您看到以下目标时：

- 向特定客户端提供网络共享
- 提供适合组协作的网络共享

您可以在设置 NFS 以实现这些目标时预期学习不同的技术。限制 NFS 对特定客户端的访问过程很简单。设置 NFS 网络共享的组协作过程更多地基于 NFS 服务器上配置的共享目录。本章还讨论了 FTP 服务。这是在 RHCSA 考试第 1 章中配置的同一 FTP 服务器，作为 RHEL 6 的安装服务器。RHCE 目标是

## 配置仅匿名下载

vsFTP 服务器的默认安装已支持仅匿名下载。但它实际上也支持常规用户访问其自己的本地帐户的访问。这仅由单个

SELinux 布尔值阻止。此外，vsFTP 和 NFS 为远程客户端提供服务的方式取决于对防火墙和 SELinux 选项所做的更改。这与适用于所有服务的标准 RHCE 目标相关，包括基于用户和基于主机的安全。

## 认证目标 16.01

## 网络文件系统（NFS）服务器

NFS 是在 Linux 和 Unix 计算机上共享目录中的文件和打印机的标准。它最初由 Sun Microsystems 于 1980 年代中期开发。Linux 多年来一直支持 NFS（作为客户端和服务器），并且 NFS 在使用 Unix 或 Linux 的网络的组织中仍然很受欢迎。

您可以通过编辑 /etc/exports 配置文件直接创建共享 NFS 目录。但了解 NFS 的工作原理可能会有所帮助，从最重要的 NFS 文件到设置 NFS 进行基本操作所需的内容。有了这些信息，您将了解要启动哪些服务，以及 NFS 如何通过网络通信。NFS 通信可以通过 /etc/sysconfig/nfs 文件中的正确设置在固定端口上进行配置。当然，如果没有对 SELinux 进行适当的更改，通过 NFS 共享的目录将无法工作。

NFS 安全可以通过多种方式增强，不仅可以通过基于 iptables 的防火墙的正确选项，还可以通过 TCP Wrappers 的帮助。

### RHEL 6 的 NFS 选项

虽然 NFS 版本 4（NFSv4）是 RHEL 6 的默认值，但 Linux NFS 软件也支持 NFS 版本 2（NFSv2）和 3（NFSv3）。区别包括客户端和服务器通信的方式、支持的文件大小以及对 Windows 风格访问控制列表（ACLs）的支持

由于默认支持 NFSv4，您不再需要使用 rpcbind 包设置远程过程调用（RPC）通信。尽管如此，它仍然可用于与其他 NFS 客户端进行通信。如果使用，您需要为 NFS 服务设置多个固定端口；一种方法基于 /etc/sysconfig/nfs 文件中可用的配置选项。NFSv4 支持 ACL。

NFSv3 的主要优点是支持 64 位文件大小，这有效地允许通过共享目录访问超过 2GB 的数据。NFSv4 保留了这些优点。

## 基本 NFS 安装

与 NFS 软件相关的主要组是“NFS 文件服务器”。换句话说，如果您运行以下命令，yum 将从该组安装强制性软件包，nfs-utils 和 nfs4-acl-tools：

```
# yum groupinstall "NFS file server"
```

但这些并不是 NFS 感兴趣的唯一软件包，尤其是对于需要 RPC 支持的较旧版本的 NFS（版本 2 和 3）。另外三个感兴趣的软件包包括

- **portreserve** 支持 portreserve 服务，是 NFS（和网络信息服务 [NIS]）通信中 portmap 的继任者。防止 NFS 占用其他服务所需的端口。
- **quota** 为共享 NFS 目录提供配额支持；并非绝对必需。
- **rpcbind** 包含不同 NFS 通道的 RPC 通信支持。

为了确保所有需要的软件包都已安装并运行，请运行以下命令：

```
# /etc/init.d/rpcbind start
# /etc/init.d/nfs start
```

## 基本 NFS 服务器配置

NFS 服务器相对容易配置。您需要做的就是导出文件系统，无论是一般还是针对特定主机，然后从远程客户端挂载该文件系统。当然，您还需要打开防火墙中的正确端口，并根据需要修改 SELinux 选项。NFS 由一系列脚本控制，与多个守护进程相关联。它还附带了广泛的控制命令。

## NFS 服务脚本

一旦安装了适当的软件包，它们可能会由 /etc/init.d 目录中的几个不同的服务脚本控制：

- /etc/init.d/nfs NFS 的控制脚本；引用 /etc/sysconfig/nfs 进行基本配置。可通过 rpc.nfsd 控制 NFS 服务，通过 rpc.rquotad 控制配额，通过 rpc.svcgssd 控制通用安全服务守护进程，通过 rpc.mountd 控制挂载。
- /etc/init.d/nfslock 用于锁文件和 statd 守护进程的控制脚本，该守护进程锁定并提供当前正在使用的文件的状态。
- /etc/init.d/portreserve portmap 脚本的替代品；用于为 RPC 服务设置端口。
- /etc/init.d/rpcbind RPC 程序号转换器。
- /etc/init.d/rpcgssd RPC 相关通用安全服务的控制脚本。
- /etc/init.d/rpcidmapd NFS 用户 ID 映射到 LDAP 和 Kerberos 系统的配置。
- /etc/init.d/rpcsvcgssd RPC 相关通用安全服务的服务器端控制脚本。

要配置 NFS 服务器，您需要确保所有这些脚本在适当的运行级别中处于活动状态。由于其中一些脚本可能尚未处于活动状态，请确保应用以下命令以启动每个脚本，并确保它们在重新启动后处于活动状态：

```
# /etc/init.d/script start
# chkconfig script on
```
