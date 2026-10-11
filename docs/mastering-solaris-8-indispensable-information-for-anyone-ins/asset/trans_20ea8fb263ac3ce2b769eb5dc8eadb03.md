

（DNS、NIS 或 NIS+），hosts 数据库是名称服务为主机信息分配数据库的一部分。hosts 数据库条目的格式如下：

`<IP4 address>  <hostname> <nicknames>  <comment>`

当 Solaris 首次创建 *etc/inet/hosts* 文件时，它包含两个条目，一个用于环回，一个用于本地计算机。环回地址是一个私有地址，允许本地系统向自身发送消息以测试其 TCP/IP 栈或与你不希望在外部接口上可用的 IP 服务进行通信。如果你有一台双宿主机（dual-homed machine），你会看到类似下面第三行的条目：

`127.0.0.1  localhost  loghost`  
`192.168.1.1  sunrise #The local system’s host name`  
`192.168.2.1  sunrise2 #This is the interface to the second network for a router`

当使用本地文件作为名称服务时，每个系统都会查询其 *etc/inet/hosts* 文件以获取网络上系统的主机名和 IP 地址。在这种情况下，*hosts* 文件至少必须包含环回地址、本地系统的 IP 地址和主机名、所有网络接口的 IP 地址和主机名、系统上主机和路由器的 IP 地址和主机名，以及你的本地系统希望通过其主机名来标识的系统的 IP 地址。

**ipnodes 数据库** ipnodes 数据库包含网络上系统的 IPv6 地址和主机名。对于名称服务，ipnodes 数据库作为服务中主机表的一部分进行管理。

**netmask 数据库（可选）** netmask 数据库仅在你的网络包含子网时使用。该数据库是网络及其关联子网掩码的列表。子网划分允许你将较大的网络划分为较小的网络，以便出于管理和性能原因进行管理。

## 动态主机配置协议（DHCP）

动态主机配置协议（DHCP）用于在系统启动时自动为系统提供 TCP/IP 地址作为服务。DHCP 服务器管理寻址信息，从地址池中提供地址，为系统可以保持特定地址分配租约或生命周期，并从 DHCP 向客户端提供其他服务。正确配置的 DHCP 解决了两个棘手的问题：首先，它减轻了网络管理员在数据库或文本文件中手动分配、跟踪和编辑地址的繁重任务；其次，通过向出现的系统分配地址，它有助于缓解网络上可分配的 IP 地址有限的问题。

Solaris DHCP 还提供支持 BOOTP（BOOTSTRAP Protocol）客户端的额外好处，因为 BOOTP 服务器和 DHCP 服务器都可以监听并使用相同的消息结构响应客户端的请求。DHCP 可以提供 BOOTP 客户端请求的 IP 地址。BOOTP 可以发送从一个网络到另一个网络的消息。由于使用相同的消息结构，DHCP 请求也可以被中继到路由器，并且无法与 BOOTP 请求区分开来。

客户端从 Solaris DHCP 获得的另一项功能是网络服务器启动所需的信息。这可以取代使用反向地址解析协议（RARP）和 bootparams。DHCP 服务器提供客户端正确启动所需的 IP 地址、启动服务器和网络配置信息。由于请求可以在子网之间中继，DHCP 在服务启动请求方面比其他系统更高效。

DHCP 是一个强大的网络功能，如果设置正确，它可以为你节省大量的时间和精力。由于在本出版物中无法解释 DHCP 的各个方面，强烈建议购买专门介绍 DHCP 主题的多本书之一，或链接到 www.dhcp.org 等网站以获取更全面的信息。

要在服务器上启动和停止 DHCP 服务，请使用 DHCP Manager 或命令行实用工具。通常，DHCP 设置为在服务器启动时自动启动，并在服务器关闭时服务变得不可用。因此，DHCP 服务器通常保持运行或由冗余系统备份。

DHCP 服务器将其数据存储在 dhcpdtab 文件和一组 DHCP 网络表中，每个表的文件名都是网络的编号。因此，地址为 192.168.1.1 的网络将其 DHCP 信息存储在名为 192_168_1_1 的表中。

DHCP Manager 是一个 GUI 实用工具，你可以使用它在服务器上配置、启动、停止、禁用和启用 DHCP 服务。你还可以使用此工具自定义你的 DHCP 服务器设置。DHCP 让你选择要管理哪些 IP 地址，使用网络配置宏，并修改非标准网络配置选项。你将发现 DHCP Manager 提供了详尽的帮助系统。

要启动 DHCP Manager，请执行以下操作：

- 1. 在本地系统上，使用以下命令以超级用户身份登录：
  ```bash
  # xhost <servername>
  ```
  
  在远程 DHCP 服务器上，输入以下内容：
  
  `# Display=localhost; export display`
  
  `# /usr/sbin/dhcpmgr &`
- 2. 在 DHCP Manager 窗口中进行更改。
- 3. 从文件菜单中选择退出命令。

以下是四个 DHCP 命令行实用工具（这四个命令中的每一个都在 man 页面中有文档）：

- **in.dhcpd**：此命令允许你控制 DHCP 守护程序。
- **dhcpconfig**：这是一个 shell 脚本，允许你使用基于文本的菜单系统中呈现的命令来配置 DHCP 服务器。
- **dhtadm**：此命令允许你更改 DHCP 客户端的配置选项和宏。
- **pntadm**：此命令允许你修改 DHCP 网络表。

Solaris DHCP 客户端是接受来自服务器的 IP 地址的系统。在 Solaris 中，它是作为守护程序（dhcpagent）运行的软件程序。Solaris 在安装操作系统时自动安装 DHCP 客户端。你不需要启用此客户端，因为它已经启用。

## 网络文件系统

网络文件系统（NFS）允许你在远程计算机磁盘上存储的文件上本地工作，但看起来就像它们存在于你自己的计算机上。远程系统充当文件服务器，本地系统充当客户端并查询文件服务器。

**注意** 第 5 章广泛介绍了文件系统。你可能需要回顾该章节以获取有关 NFS 的更详细讨论。

系统管理员配置 NFS 的方式与配置 NIS 的方式相同。如果你正在处理文件，你可能不会意识到文件物理存储在哪里。这是分布式计算的又一个完美示例。由于大多数中央文件服务器都配备了大容量磁盘驱动器以及使数据备份副本的设备，一些 Solaris 系统可能是无磁盘的。可以使用软盘启动 Solaris 并从网络上的另一台机器加载系统软件。Solaris 还产生无数据系统，该系统仅存储系统软件和操作系统，而应用程序保存在磁盘上。

使用 df 实用工具显示系统上可用的文件系统列表（你可以使用带 -k 选项的 df 以千字节而不是块来显示）。它还将显示空闲的磁盘空间以及已使用的空间。带有主机名前缀的文件系统名称对你可用。

所有标准 Solaris 实用程序处理 NFS 远程文件的方式与处理本地存储的文件的方式相同。文件的物理位置并不重要，除非你通过停机或暂时不可用而失去对文件的访问权限。如果 NFS 服务器无法响应，你很可能会收到错误消息。当文件再次可用时，它会给你一个 OK 消息。

分布式计算的优势之一是你可以在网络上的任何机器上登录，你所有的文件都可用，包括你的启动脚本。你的主目录始终可以在网络上的任何机器上访问。

## 共享文件系统

与其他机器共享本地文件有许多优势。它节省磁盘空间，这是一个主要优势，但它还让你有一个单一的地方来更改数据，而不是必须在不同的位置更改几次。共享文件系统通常存储在 /export 或 /usr/export 目录下（尽管你可以共享系统中的任何文件系统或目录），每个子目录容纳一个共享文件系统。共享文件可以保留在任何目录中。

要共享文件系统，你必须通过编辑 /etc/dfs/dfstab 来启用 NFS。此文件在系统进入运行级别 3 时由 /etc/rc3.d/$15nfs.server 脚本运行。语法如下：

```bash
$ cat /etc/dfs/dfstab
# place share (1M) commands here for automatic execution on
#     entering init state 3.

#Issue the command '/etc/init.d/nfs.server start' to run the
#   NFS daemon processes and the share commands, after adding
#   the very first entry to this file.

#Share [-F fstype] [-o options] [-d "<text>"] <pathname>
#  [resource],e.g.,
share -F nfs -o rw-engineering -d "home dirs" /export/home2
share -nfs -o ro-huey, rw=dewey:louie, root=dewey -d 'home \
  directories' /export/home
```

