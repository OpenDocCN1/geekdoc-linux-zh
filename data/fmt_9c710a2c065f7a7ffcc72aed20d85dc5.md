
## 配置启动文件

在配置 NIS 时，您必须修改某些配置文件以确保 `ybind` 启动。在配置 NIS 后，在 `/etc/yp.conf` 中设置域名，见图 8-10。

![](img/d1fb1ff3244ecb66d002a5e633e6f729_236_0.png)

## 关键 NIS 客户端文件和命令

表 8-2 列出了 NIS 客户端文件和命令并简要描述了它们的用途。

| 文件/命令 | 描述 |
| --- | --- |
| `ypwwhich` | 显示 NIS 服务器名称 |
| `ypcat` | 输出 NIS 数据库中的条目 |
| `yppasswd` | 修改用户密码和信息 |
| `ypoll` | 显示 NIS 映射的服务器版本 |
| `ypmatch` | 输出 NIS 映射中一个或多个目的的值 |

表 8-2（续）

| 文件/命令 | 描述 |
|---|---|
| `/etc/yp.conf` | 配置 NIS 客户端绑定 |
| `/etc/nsswitch.conf` | 配置系统名称数据库 |
| `/etc/host.conf` | 配置主机名解析 |

## 测试您的配置

如果前面的配置步骤按预期工作（它们应该是这样的），您可以使用几个简单的命令来验证您的 NIS 配置。例如，按照本章所述配置的 NIS 客户端应该从服务器检索其密码信息。因此，在 NIS 客户端上执行以下命令应打印密码数据库：

```
# ypcat passwd

nfsnody::65534:65534:Anonymous NFS User:/var/lib/nfs/sbin/login

bubba:$1$F2EoTOW$32MNfobZbBIdG05B9mks:500:500:Bubba:/home/bubba:bash

maryue:$1$h0nMockLFSEARImgeFHXThu:501:5:0. Mary sue:/home/maryue:/bash
```

同样，您可以使用 `ypmatch` 命令打印特定的信息。例如，要打印任意用户的 NIS 密码条目，可以使用格式为 `ypmatch username passwd` 的 `ypmatch` 命令，其中 `username` 是您感兴趣的用户。因此，打印 `bubba` 的密码条目：

```
# ypmatch bubba passwd

bubba:$1$F2EoTOW$32MNfobZbBIdG05B9mks:500:500:Bubba:/home/bubba:/bin/bash
```

同样要显示 `maryue` 的组文件条目，正确的命令是

```
# ypmatch maryue group

maryue:501::
```

使用 `ypcat -x` 命令列出 NIS 服务器共享的映射列表，如下例所示：

```
# ypcat -x

Use "ethers"          for map "ethers.byname"

Use "aliases"        for map "mail.aliases"
```

对于映射 "services.byname" 使用 "services"
对于映射 "protocols.byname" 使用 "protocols"
对于映射 "hosts.byname" 使用 "hosts"
对于映射 "networks.byaddr" 使用 "networks"
对于映射 "group.byname" 使用 "group"
对于映射 "passwd.byname" 使用 "passwd"

# 第8章：网络信息系统

## 配置示例 NIS 客户端

本小节说明了如何配置 NIS 客户端，以使用本章早些配置的 NIS 服务器所提供的 NIS 服务。与之前一样，NIS 域名为 `kurtwerks`，运行在名为 `karta.Kurtwerks.com` 的服务器上，其 IP 地址为 `192.168.0.1`。

- 1. 设置 NIS 域名：
  `# nisdomainname kurtwerks`
  `# nisdomainname`
  `kurtwerks`

- 2. 编辑 `/etc/ypmap.conf` 以识别默认 NIS 服务器。完成后的配置文件如下（不包含注释）：
  `ypserver 192.168.0.1`

- 3. 确保 `portmapper` 正在运行：
  `# rpcinfo -p localhost`
  `program vers port`
  `100000 2 tcp 111 portmapper`
  `100000 2 udp 111 portmapper`

- 4. 启动主客户端守护 `ybind`：
  `# /etc/rc.d/init/ypbind start`
  正在绑定到 NIS 域：
  正在等待 NIS 域服务器。

- 5. 确认 `ybind` 正在运行：
  `# rpcinfo -u localhost ybind`
  `program 100007 version 1 ready and waiting`
  `program 100007 version 2 ready and waiting`

- 6. 编辑 `/etc/host.conf` 并将 NIS 添加到用于主机查找的服务中。完成后的文件看起来所示：
  `order hosts,nis.bind`

- 7. 编辑 `/etc/nswitchconf.conf`，更改类似于下方的条目：

```
passwd: files nisplus

shadow: files nisplus

group: files nisplus

hosts: files nisplus
```

修改这些条目使其看起来如下所示：

```
passwd: files nisplus

shadow: files nisplus

group: files nisplus

hosts: files nisplus
```

- 8. 使用前文介绍的服务配置工具，配置 `ybind` 在启动时运行。

- 9. 重启服务器以确保客户端守护进程启动。

## 增强 NIS 安全性

通常，在 NFS 中出现的类似安全问题也会给 NIS 带来麻烦。因为 NIS 使用 RPC，基于 `portmapper` 的漏洞可能会损害系统安全。此外，由于用户密码和其他身份验证信息是以明文传输的，除非使用 SSH 或其他 IP 隧道或封装方案对传输进行加密，否则不要在互联网上使用 NIS。如果可能或可行，你的 NIS 域名不应是与服务器 DNS 域名相关的名称，尽管这种方法是一种常用手段。选择不同 DNS 和 NIS 域名的原因是这样做让黑客更难从你的 NIS 服务器中获取密码数据库。在服务器端，主要的安全性考虑是使用本章服务器配置部分描述的 `/var/yp/securenets` 配置语法来限制对 NIS 映射的访问。

## 总结

在本章中，我们学习了如何在 Red Hat Linux 上配置 NIS 服务器和客户端服务。你首先学习了如何设置和测试 NIS 服务器，以及如何确保 NIS 服务器在系统重启后启动。你还学习了如何配置 NIS 客户端连接到 NIS 服务器获取身份验证信息。

# 第9章

# 连接到微软网络

本章内容

- 安装 Samba
- 配置 Samba 服务器
- 使用 Swat
- 配置 Samba 客户端
- 从 Linux 计算机使用 Windows 打印机
- 测试 Samba 服务器

在本章中，你将学习如何将 Red Hat Linux 网络连接到微软网络。运行 Windows 95 或更高版本的计算机使用一种名为 Server Message Block (`SMB`) 的协议进行通信，并共享文件和打印共享等服务。通过使用名为 `Samba` 的程序，你可以模拟 `SMB` 协议并将 Red Hat 网络连接到 Windows 网络，以共享文件和打印机。Linux PC 图标会出现在 Windows“我的网络”窗口中，可以使用 Windows 资源管理器浏览 Linux PC 上的文件。

## 安装 Samba

在使用 `Samba` 连接到 Windows 计算机之前，必须先在 Linux PC 上安装它。所有当前的 Linux 发行版都包含 `Samba`，但在系统安装期间可能尚未安装。即使已经安装，你也应该始终检查最新版本，确认最新发布是否修复了任何问题，并在必要时进行安装。要检查系统是否安装了 `Samba`，输入以下命令：

```
rpm q samba
```

如果未安装 `Samba`，命令将返回图 9-1 所示输出。
（图 9-1：RPM 查询显示未安装 Samba。）

如果已安装 `Samba`，RPM 查询将返回图 9-2 所示的版本号。
（图 9-2：RPM 查询显示当前的 Samba 版本。）

如果你需要下载最新版本的 `Samba`，可以在 `Samba` 官方网站（位于 `http://www.samba.org`）获取最新版本的 `Samba`（截至本文编写时，最新版本为 2.0.7）。按照网站上的说明下载适用于你发行版的 RPM 文件。下载 `Samba` 文件后，使用以下命令安装，其中“文件名”是你下载的版本号：

```
rpm -i samba(文件名)
```
