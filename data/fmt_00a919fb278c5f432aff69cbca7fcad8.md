
```
 fixed-address 192.168.0.3;

 }

}
```

`host` 声明也可以放置在子网声明中，以提供该子网中特定主机的信息。

固定地址的常见候选项是网络的 DNS 服务器。通常，您会希望 DNS 服务器位于相同的 IP 地址，以便可以直接访问它。然后，DHCP 服务器可以将此 IP 地址提供给其客户端。

# 第 38 章：NFS、NIS 和 GFS

Linux 提供了多种用于访问连接网络的远程系统上文件的工具。网络文件系统（NFS）允许您连接并直接访问驻留在另一台机器上的资源，例如文件或像 CD-ROM 这样的设备。新版本 NFS4 提供了更高的安全性，访问受您的防火墙控制。网络信息服务（NIS）维护网络中所有系统的配置文件。使用 GFS，您可以设置网络文件系统，通过网络访问磁盘空间。

## 网络文件系统：NFS 和 `/etc/exports`

NFS 允许您将远程计算机上的文件系统挂载起来，就像它是您自己系统的本地文件系统一样。然后，您可以直接访问该远程文件系统上的任何文件。这具有让网络中不同系统直接访问相同文件的优点，而无需每个系统保留自己的副本。远程文件系统上只会有一个副本，每个计算机都可以访问它。您可以在其网站 nfs.sourceforge.net 上了解有关 NFS 的更多信息。

> **注意** 基于 BSD Unix 的用于 Macintosh 计算机的 Mac OS X 现在支持用于文件共享的 NFS。要访问使用旧版 Apple 操作系统的 Apple 文件系统和打印机，您可以使用 Netatalk。Netatalk 在 Unix 和 Linux 系统上实现了经典的 AppleTalk 和 AppleShare IP 网络协议。当前的 Netatalk 网站是 netatalk.sourceforge.net，其中包含 FAQ 和 HOW-TO 部分的链接。

### NFSv4

NFS 版本 4 是 NFS 协议的一个新版本，具有增强的功能，例如更高的安全性、可靠性和速度，目前受 Fedora 和 Red Hat Linux 支持。大多数命令相同，但有一些更改。例如，当您挂载 NFSv4 文件系统时，需要指定 `nfs4` 文件类型。此外，对于 NFSv4，在 `/etc/exports` 文件中，您可以使用 `fsid=0` 选项来指定根导出位置。

```text
/home/richlp      *(fsid=0,ro,sync)
```

前面的条目允许您将文件系统挂载到 `/home/richlp` 目录，而无需在挂载操作中进行指定。

```text
# mount -t nfs4 rabbit.mytrek.com:/ /home/dylan/projects
```

## NFS 守护进程

NFS 在 TCP/IP 网络上运行。持有文件系统的远程计算机使其可供网络上的其他计算机使用。它通过导出文件系统来实现这一点，这涉及在名为 `/etc/exports` 的 NFS 配置文件中创建条目，并运行多个守护进程以支持其他系统的访问。这些包括 `rpc.mountd`、`rpc.nfsd` 和 `rpc.portmapper`。对您的 NFS 服务器的访问可以通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件进行控制。NFS 守护进程列举如下：

- `rpc.nfsd` 接收来自远程系统的 NFS 请求，并将它们转换为对本地系统的请求。
- `rpc.mountd` 执行请求的挂载和卸载操作。
- `rpc.portmapper` 将远程请求映射到适当的 NFS 守护进程。
- `rpc.rquotad` 提供用户磁盘配额管理。
- `rpc.statd` 在远程主机重启时提供锁定服务。
- `rpc.lockd` 处理已宕机系统的锁恢复。

> **注意** 建议仅在本地安全网络上使用 NFS。如果在互联网上使用，NFS 将使您的系统暴露于不安全的访问。NFS4 确实提供了保护。

## 启动和停止 NFS

您可以使用 `/etc/rc.d/init.d/nfs` 服务来启动和关闭 NFS 守护进程，您可以通过 `service` 命令调用它，`service nfs start`。要使 NFS 自动启动，您可以使用 `chkconfig` 或 `system-config-services` 工具来指定它将运行的运行级别。以下示例将使 NFS 在运行级别 3 和 5 自动启动：

```text
chkconfig -level 35 nfs on
```

`nfs` 脚本将启动 `portmapper`、`nfsd`、`mountd` 和 `rquotad` 守护进程。要启用 NFS 锁定，请使用 `nfslock` 脚本。这将启动 `statd` 和 `lockd` 守护进程。NFS 锁定为因远程主机系统崩溃而可能发生的被中断操作提供更好的恢复能力。

要查看 NFS 是否实际正在运行，您可以使用带有 `-p` 选项的 `rpcinfo` 命令。您应该看到 `mountd` 和 `nfs` 的条目。如果没有，则 NFS 未运行。

## 使用 NFS 配置工具配置 NFS

代替手动挂载和配置 NFS 目录，您可以使用 NFS 配置工具（`system-config-nfs`）。从 System | Administration | Server Settings 菜单中选择 NFS 条目。这将打开 NFS 服务器配置工具窗口。请确保您的

NFS 服务器软件已安装（`system-config-packages`），且 NFS 服务器正在运行（`system-config-services`）。

若要添加一个共享目录，请点击“添加”按钮打开“添加 NFS 共享”对话框。您可以在“目录”框中浏览或输入要共享的目录。然后列出主机所在位置，并指定访问权限。在“常规选项”选项卡中，您可以设置基本安全和更新功能，例如不可靠的文件锁定或立即同步写操作。默认情况下，已设置“请求时同步写操作”选项。在“用户访问”选项卡中，您可以将用户视为本地 root 用户，或视为具有特定用户或组 ID 的匿名用户。

点击“确定”后，该条目将列在“NFS 服务器配置”窗口中。更改在您点击“应用”之前不会生效。这将创建 `/etc/exports` 文件中的一个条目，用于共享目录。您随后可以通过选择该条目并点击“属性”来打开“编辑”对话框，从而更改这些设置中的任意一项。若要保存您的设置，请单击“应用”。如果防火墙需要使用特定端口来访问 NFS 目录，您可以在“服务器设置”窗口中指定这些端口。

以下示例具有与下一节中描述的 `/etc/exports` 文件中使用的相同条目。此处显示了使用此示例由 NFS 服务器配置工具生成的 `/etc/exports` 文件：

```console
/home/foodstuff/    lizard.mytrek.com(rw, sync)
/media/cdrom       rabbit.mytrek.com(ro, sync)
/home/richlp     *(ro, sync)
/pub        *(ro, insecure, sync, all_squash)
```

在“基本”、“常规选项”和“用户访问”面板中设置的选项将作为列出的每个条目中的选项显示。例如，只读访问是 `ro`，读写访问是 `rw`。请查看 NFS 服务器配置帮助文档以获取完整列表。选项列表见表 38-1。

## NFS 配置：`/etc/exports`

`/etc/exports` 文件中的一个条目指定要导出的文件系统以及可以访问该文件系统的网络主机。对于文件系统，请输入其挂载点，即该文件系统在主系统上被挂载的目录。随后列出可以访问此文件系统的主机列表以及控制访问的选项。每个主机后面可能跟有一个放在括号内的、由逗号分隔的导出选项列表。例如，您可能希望向一个主机授予只读访问权限，而向另一个主机授予读写访问权限。如果选项前带有 * 符号，则它们适用于任何主机。选项列表见表 38-1。`/etc/exports` 文件中条目的格式如下所示：

`directory-pathname host-designation(options)`

## NFS 主机条目

您可以为同一目录设置多个主机条目，每个条目都可以访问该目录：

`directory-pathname host(options) host(options) host(options)`

在指定主机时，您有很大的灵活性。对于您域内的主机，您可以直接使用主机名；而对于域外主机，则需要使用完全限定域名。您也可以仅使用主机的 IP 地址。除了单个主机，您还可以引用特定域内的所有主机，从而允许整个网络访问。一种简单的方法是使用 * 作为主机段，后接网络的域名，例如 `*.mytrek.com` 表示 mytrek.com 网络中的所有主机。您也可以使用 CIDR 格式的 IP 网络地址代替域名，其中指定网络掩码以表示 IP 地址范围。您还可以使用 NIS 网络组名称来引用一组主机。NIS 网络组名称前带有 @ 符号。

```
directory     host(options)
directory     *(options)
directory     *.domain(options)
```
