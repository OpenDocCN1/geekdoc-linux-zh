
# 第 18 章 ♦ 设置文件服务器 645

在 Samba 的最新版本中支持浏览。在 Samba 中，浏览通过以下选项配置并由 `nmb` 守护进程实现。如果你在单局域网内的工作组中使用 Samba，你可能不需要担心浏览选项。然而，如果你在跨局域网中使用 Samba，你可能需要关注浏览选项。

- `Hosts Allow`（允许的主机） — 添加你想要访问此文件系统的计算机的名称。你可以使用逗号、空格或制表符来分隔主机名。输入主机名的有效方法有以下几种：

  - `localhost` — 访问本地主机。
  - `192.168.74.18` — IP 地址。输入单个 IP 地址。
  - `192.168.74.` — 输入网络地址以包含网络上的所有主机。
  - `maple, pine` — 通过名称启用对单个主机的访问。

- `EXCEPT host`（排除主机） — 如果你正允许对一组主机的访问（例如通过输入网络地址），使用 `EXCEPT` 特异地拒绝该组中某一个主机的访问。

- `Hosts Deny`（拒绝的主机） — 通过在此处放置名称来拒绝对特定计算机的访问。默认情况下，不排除任何特定计算机。以与 `Hosts Allow` 相同的格式输入主机。

- `Browseable`（可浏览） — 表明你是否可以在共享目录列表中查看此目录。默认开启（Yes）。（参见“查看可用的 Samba 文件系统”以了解如何查看共享文件系统。）

- `Available`（可用） — 允许你保持此条目不变，但关闭服务。如果你想临时访问目录，这非常有用。默认开启（Yes）。选择 No 将关闭。

4. 选择 `Commit Changes`（提交更改）。

此时，共享文件系统应该对能够访问你的 Linux Samba 服务器的 Samba 客户端（Windows 95、Windows NT、OS/2、Linux 等）可用。不过，在尝试之前，你可以对你的 Samba 配置进行几项检查。

## 使用 SWAT 检查你的 Samba 设置

在 SWAT 窗口中，选择 `Status`（状态）。从此窗口，你可以重启 `smbd` 和 `nmbd` 进程。同样，你可以看到活动连接、活动共享和打开文件的列表。

## 测试你的 Samba 权限

你可以从 shell 运行多个命令来操作 Samba。其中之一 `testparam` 命令。使用 `testparam` 命令检查你设置的访问权限。它列出了已设置的全局参数，以及任何共享目录或打印机。

## 检查共享文件系统的状态

可以使用 `smbtstatus` 命令查看谁正在使用从你的 Red Hat Linux 系统提供的 Samba 共享资源。以下是 `smbtstatus` 的输出示例：

```
Samba version 2.0.7 pid machine
Service uid gid  
Temp nobody nobody 2943 snowbird(10.0.0.12) Mon May 24 10:52:22 1999

Locked files:
Pid DenyMode R/W Oplock Name
2943 DENY_NONE RDNLY EXCLUSIVE+BATCH /tmp/install.log Mon Oct 23 11:17:04 2000
```

共享内存使用（字节）：

1048360(99%) free + 136(0%) used + 80(0%) overhead = 1048576(100%) total

此输出显示，对于你的 Red Hat Linux Samba 服务器，Temp 服务（`/directory` 的共享）目前正被名为 `snowbird` 的计算机打开。正在使用 `nobody` 用户和组来访问该资源。PID (2943) 是 Red Hat Linux 服务器上处理该服务的 `smbd` 守护进程的进程号。唯一打开的文件是 `/tmp/install` 文件。该文件以只读 (`RDONLY`) 方式可用。

## 为 Windows 系统设置 Samba 客户端

为了通过网络从你的 Red Hat Linux 系统向 Windows 95/98 客户端共享 Samba 文件系统，需要对客户端进行一些配置。在 Windows 95/98 和类似系统中，大部分配置是在 `Network`（网络）窗口中完成的。在 Windows 95/98 等系统中：

1. 点击 `Control Panel`（控制面板）。
2. 从控制面板双击 `Network`。

在网络窗口中，你可以看到组件（协议、客户端、适配器和服务）。Samba 依赖 TCP/IP 网络，因此你可能已经在 LAN 上设置了 TCP/IP（见第 15 章）。为了使用 Samba，你还需要配置以下内容：

- `Client for Microsoft Networks`（微软网络客户端） — 该客户端允许文件共享。如果不在列表中，可以通过 `Settings: Add: Microsoft: Client for Microsoft Networks` 添加。
- `NetBEUI protocol` — 用于 MS Windows 以及其他系统之间执行文件和打印的协议。如果不在列表中，可以通过 `Add > Protocol: Add > Microsoft > NetBEUI`。（NetBEUI 是一种原始 NetBIOS 协议。如果你的计算机运行 NetBIOS over TCP 则无需它。）
- `Network Adapter`（网络适配器） — 代表实际连接计算机的网络介质。例如以太网卡。
- `TCP/IP protocol` — 如果网络适配器尚未添加 TCP/IP，点击 `Add > Protocol: Add > Microsoft > TCP/IP`。然后点击 `OK`。点击网络窗口中的 TCP/IP 项，点击 `Properties`。在 `bindings` 选项卡上确保勾选 `Client for Windows`。在 `WINS` 选项卡输入服务器名称，点击 `OK`。

> 如果你经常使用该目录，可能想为它分配一个驱动器号。右键点击文件夹，选择 `Map Network Drive`。从列表中选择驱动器，如果需要，选择 `Reconnect at logon` 以在登录时可用。点击 `OK`。

> 如果你要的服务器没有出现在网络窗口中，可以尝试搜索。点击 `Start > Find > Computer`。输入要搜索的计算机名称，点击 `Find Now`。如果计算机名称出现，双击它。应该打开一个窗口，显示共享目录和打印机。

> 图 18-3：查看网络

![](img/176fafece2d30daee750bc078e898ee4_678_0.png)

## 第四部分 网络与设置

## 在 Red Hat Linux 中设置 NetWare 服务器

NetWare 曾经是 LAN 中 PC 之间共享文件和打印机最流行的软件。NetWare 被称为网络操作系统。这意味着 NetWare 接管了整个计算机并管理其资源。NetWare 不像你放在办公桌上像 Windows 95/98 那样用于文字处理的客户端操作系统，它是一个高效的文件和打印机服务器。

在 Linux 中，有软件可以从你的 Linux 系统中模拟 NetWare 服务器。Red Hat Linux 自带了一个名为 Martin Stovers NetWare 模拟器（`mars_nwe` 软件包）。虽然 `mars_nwe` 无法实现 NetWare 服务器的所有功能，但它作为一个基础文件和打印服务器表现良好。以下是 `mars_nwe` 包含的特性：

- 文件服务 — 你可以使用 NetWare 模拟器从 Linux 共享目录结构（称为卷）。
- 打印服务 — 你可以使用 NetWare 模拟器共享与 NetWare 服务关联的打印机。
- RIP/SAP 守护进程 — 这允许你的 Red Hat Linux 计算机充当 IPX 路由器。（IPX 是用于 NetWare 系统之间通信的网络协议。）

另一个提供 NetWare 文件服务器模拟的包是 `lwared` 软件包（LinWare Daemon 的缩写）。该包也提供 NetWare 文件和打印服务。然而，它与 Windows 95 或 Windows 客户端兼容性不好。（`lwared` 包未包含在 Red Hat Linux 中，且在本节中未讨论）

在客户端，`ncpfs` 包是一个额外的软件包，如果你想让你的 Red Hat Linux 计算机利用 NetWare 服务器，就需要安装它。该包提供了全套访问 NetWare 服务的客户端命令。这些命令允许你挂载 NetWare 卷、显示可用服务的信息以及处理 NetWare bindery 对象。

## 创建 NetWare 文件服务器

要从你的 Red Hat Linux 服务器共享 NetWare 服务，你需要使用 IPX 协议通过物理网络与 NetWare 客户端通信。一种常见的情况是在以太网局域网中使用 IPX（这在本节所描述的内容）。

请参第 15 章有关设置以太网局域网的信息。
