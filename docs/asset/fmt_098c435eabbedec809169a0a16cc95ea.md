
你必须执行的第一件事是启用该服务。当你首次安装 `tftpd-hpa` 软件包时，`RUN_DAEMON` 默认值为 `"no"`。要启用它，你必须将默认的 `"no"` 改为 `"yes"`，如列表 12-4 所示。第二行定义了守护进程本身的命令行选项，通常为 `/usr/sbin/in.tftpd`。`-s` 告诉 `inftpd` 在启动时切换到指定的目录 (`/tftpboot`)，这使得该目录成为你 TFTP 服务器的根目录。`-c` 标志允许创建新文件。这对于从目标向服务器写入文件非常有用。`BDI-3000`（本书后部分将介绍）具有这种能力，如果没有 `-c` 它将无法工作。`-l` 参数指示 TFTP 守护进程在后台运行并在 TFTP 端口上监听传入的 TFTP 数据包。

一旦对此配置文件进行了更改，你必须重启 TFTP 服务器以便更改生效：

```bash
$ sudo /etc/init.d/tftpd-hpa restart
```

在任何情况下，请咨询随发行版附带的文档，了解如何在你的特定发行版上启用 TFTP 服务器的选项。

## 12.3.2 BOOT/DHCP 服务器

在你的开发主机上拥有 DHCP 服务器可以简化嵌入式目标的配置管理。我们已经确定了为什么在目标硬件上使用太网接口是一个好主意。当 Linux 在你的目标板上启动时，它需要配置以太网接口后该才能投入使用。此外，如果你在目标板上使用 NFS 根挂载配置，Linux 需要在启动过程完成之前配置你目标的以太网接口。我们在第 9 章“文件系统”中详细介绍了 NFS。

通常情况下，Linux 可以在启动期间使用两种方法初始化其以太网/IP 接口：

- 在 Linux 内核命令行或默认配置中硬编码以太网接口参数，例如静态 IP 配置。
- 配置内核在启动时自动检测网络设置。

出于明显的原因，第二种选择更灵活。DHCP 或 BOOTP 是你的目标和服务器用于完成自动检测网络设置的协议。有关 DHCP 和 BOOTP 协议的详情，请参见本章的最后节。

DHCP 服务器控制其已配置的 IP 子网的 IP 地址分配，以及配置为参与的 DHCP 或 BOOTP 客户端。DHCP 服务器列出来自 DHCP 客户端（例如你的目标）的请求，并在启动过程中将地址和其他相关信息分配给客户端。典型的 DHCP 交换（见列表 12-5）可以通过带有 `-d` 调试开关启动你的 DHCP 服务器，并观察目标机器请求配置时的输出来检查。

### 列表 12-5 典型的 DHCP 交换

```
tgt DHCPDISCOVER from 00:09:5b:65:1d:d5 via eth0
svr DHCPPOFFER on 192.168.0.9 to 00:09:5b:65:1d:d5 via eth0
tgt DHCPREQUEST for 192.168.0.1 (192.168.0.1) from \
  00:09:5b:65:1d:d5 via eth0
svr DHCPACK on 192.168.0.9 to 00:09:5b:65:1d:d5 via eth0
```

该序列从客户端（目标）发送广播帧以发现 DHCP 服务器开始。这通过 `DHCPDISCOVER` 消息显示。服务器（如果已配置并启用）通过为客户端提供一个 IP 地址来响应。客户端随后通过在本地测试此 IP 地址来响应。测试包括向 DHCP 服务器发送 `DHCPREQUEST` 包，如所示。最后，服务器通过确认向客户端分配 IP 地址来响应，完成目标配置。

有趣的是，配置适当的客户端会记住它上次由 DHCP 服务器分配的地址。下次它启动时，它将跳过 DHCP-DISCOVER 阶段直接进入 DHCPPREREQUEST 阶段，假设它可以重用服务器之前分配的相同 IP 地址。启动的 Linux 内核不具备这种能力，并且每次启动都会发出相同的序列。

配置你的主机的 DHCP 服务器并不困难。像往常一样，我们的建议是咨询随你的桌面 Linux 发行版提供的文档。在 Red Hat 或 Fedora 发行版上，单个目标的配置条目可能看起来列表 12-6。

### 列表 12-6 示例 DHCP 服务器配置

```
# Example DHCP Server configuration
allow bootp;

subnet 192.168.1.0 netmask 255.255.255.0 (
  default-lease-time 120960
  option routers 192.168.1.1
  option domain-name-servers 8.8.8.8;
  option range 192.168.1.100 192.168.1.200;
    host target {
      hardware 00:30:bd:2a:26:1f;
      fixed-address 192.168.1.68;
      filename "/home/sandbox/uImage";
    }
  }
}
```

这是一个简单的示例，仅用于展示你可以传递给目标的信息。除了固定地址外，你还可以向目标传递其他信息，如列表 12-6 所示。

## 12.3.3 NFS 服务器

为你的目标板使用 NFS 根挂载是一个非常强大的开发工具。这种配置对开发的某些优势如下：

- 你的根文件系统不受你开发板有限资源（如 Flash 内存）的大小限制。
- 开发期间对应用程序文件的更改将立即供你的目标使用。
- 你可以在开发和调试根文件系统之前调试并启动内核。

设置 NFS 服务器的步骤取决于你使用的哪个桌面 Linux 发行版。结合本章描述的其他服务，你必须咨询你的 Linux 发行版文档以获取适用于你配置的详细信息。NFS 服务必须从启动脚本、图形菜单或命令行启动。例如，对于 Fedora Core Linux 桌面从根命令行启动 NFS 服务的命令如下：

```bash
$ /etc/init.d/nfs start
```

或

```bash
$ /etc/init.d/nfs restart
```

## 12.3 托管目标板卡

请注意，在较新版本的 Ubuntu 和其他发行版中，此命令已更改为 `/etc/init.d/nfs-kernel-server`。你每次启动桌面 Linux 工作站时都必须执行此操作。（其他服务可以在启动时自动启动。请参阅你的桌面 Linux 发行版的文档。）除了启用服务外，你的内核必须编译了对 NFS 的支持。虽然 DHCP 和 TFTP 都是用户空间程序，但 NFS 需要内核支持。这在你的开发工作站和目标板上都是如此。图 12-2 显示了内核中 NFS 的配置选项。注意，同时存在 NFS 服务器和客户端支持的配置选项。还要注意“Root file system on NFS”（NFS 根文件系统）选项。你的目标内核必须配置此选项以进行 NFS 根挂载操作。

![](img/01fe6847ecb41916a11c291e01f06c00_352_0.png)

图 12-2 NFS 内核配置

NFS 服务器从位于开发工作站的 exports 文件获取指令。该文件通常位于 `/etc/exports`。列表 12-7 是一个简单的 exports 条目示例。

### 列表 12-7 简单的 exports 文件

```
$ /etc/exports
# /home/chris/sandbox/coyote-target \ *(rw,sync,no_root_squash,no_all_squash,no_subtree_check)
# /home/chris/sandbox/pdna-target \ *(rw,sync,no_root_squash,no_all_squash,no_subtree_check)
# /home/chris/workspace \ *(rw,sync,no_root_squash,no_all_squash,no_subtree_check)
```

这些条目允许客户端远程挂载所示的三个目录之一。目录规范后的属性指示 NFS 服务器允许来自任何 IP 地址 (*) 的连接，并使用给定的属性（读/写且带 `no_root_squash`）挂载相应的目录。后一个属性允许具有 root 权限的客户端在给目录上使用这些权限。在处理嵌入式系统时通常需要它，因为它们通常拥有 root 账户。

`no_all_squash` 属性确保传入的 NFS 请求的 uid 和 gid 得到尊重，而不是映射到默认的匿名账户。`no_subtree_check` 属性禁用了服务器上的子树检查。在某些情况下这可以提高性能和可靠性。详情请参考你的 NFS 服务器文档和描述 exports 文件的 man 页面。

你可以直接从工作站测试 NFS 配置。假设你已经启用了 NFS 服务（这需要 NFS 服务器和客户端组件都启用），你可以像挂载任何其他文件系统一样挂载本地导出：

```
# mount -t nfs localhost:/home/chris/workspace/mnt/remote
```

如果此命令执行成功且 .../workspace 中的文件在 `/mnt/remote` 上可用，则说明你的 NFS 服务器配置正常。
