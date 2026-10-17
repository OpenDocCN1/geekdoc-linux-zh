
这将启用 Samba 服务在级别 3、4 或 5 运行时自动启动。

此时，你可以从本地局域网的 Windows 桌面上为你刚刚设置的用户打开“网络邻域”图标。网络邻域窗口中会出现一个代表你所配置的 Linux 服务器的图标。当你打开服务器图标时，你应该看到一个代表用户主目录（`/home/user`）的图标，以及每个 Linux Samba 服务器可用的共享打印机的图标。

## 在 Red Hat Linux 中设置 NetWare 文件服务器

NetWare 曾经是连接到局域网的 PC 之间共享文件和打印机最流行的 NMB 软件。NetWare 被称为网络操作系统。这意味着 NetWare 控制了整台电脑并管理其资源。虽然 NetWare 不像客户端操作系统（如 Windows 9x）那样可以放在办公桌桌上进行文字处理，但它是一个非常高效的文件和打印服务器。

www.unlted.com 上的额外内容

在 Linux 中，有可用软件从你的系统模拟 NetWare 服务器。Red Hat Linux 附带的一个是 Martin Stovers NetWare 模拟器（`mars_nwe` 包）。虽然 `mars_nwe` 无法完成 NetWare 服务器能做的所有工作，但它作为文件和打印服务器表现良好。以下是 `mars_nwe` 包含的功能：

- 文件服务——你可以使用 NetWare 模拟器从 Linux 共享目录结构（称为卷）。
- 打印服务——你可以使用 NetWare 模拟器共享与 NetWare 服务关联的打印机。
- RIP/SAP 守护进程——这允许你的 Red Hat Linux 充当 IPX 路由器。IPX 是 NetWare 系统之间使用的原生协议。

另一个提供 NetWare 文件服务器模拟的包是 `Iward` 包（Linux Daemon 的缩写）。该包也提供 NetWare 文件和打印服务。然而，它与 Windows 客户端兼容性不佳。（`Iward` 包未包含在 Red Hat Linux 中，且在本节中不讨论。）

在客户端，如果你希望你的 Red Hat Linux 计算机能够利用 NetWare 服务器的服务，你需要安装名为 `neptcls` 的额外包。该包提供了一全套访问 NetWare 服务的客户端命令。这些命令允许你挂载 NetWare 卷、显示可用服务的信息，并与 NetWare 二进制对象进行操作。

### 创建 NetWare 文件服务器

为了从你的 Red Hat Linux 服务器共享 NetWare 服务，你需要使用 IPX 协议通过物理网络与 NetWare 客户端进行通信。一种通信方式是在以太网局域网上使用 IPX（本节描述的内容）。

请参考第 15 章有关设置以太网局域网的信息。

Linux 中 NetWare 服务器的大部分配置都在 `/etc/nwswerv.conf` 文件中完成。`mars_nwe` 提供的 `nwswerv.conf` 文件包含许多注释信息，描述了在 Red Hat Linux 中配置 NetWare 服务所需的内容。请参考注释文本获取有关在 Red Hat Linux 中配置 NetWare 服务器的不同方法的更多细节。

### 配置 `/etc/nwswerv.conf`

你需要添加到 `/etc/nwswerv.conf` 文件中的信息按章节组织。每个章节中的条目都以该章节的数字开头。以下是你为 Red Hat Linux 中的 NetWare 服务器需要修改的一些章节。（每个章节分配的数字在括号中。）

- Volumes（1）—— 你想要共享的卷（Red Hat 目录）的名称。
- Server Name（2）—— 你的服务器标识。
- Internal Network Number（3）—— 唯一标识你的服务器的数字。该地址必须是十六进制数或包含单词 `auto` 以使用你的 IP 地址作为内部网络号。
- IPX Devices（4）—— 包含了在 Red Hat Linux 中配置 NetWare 服务所需的 IPX 设备名称、类型以及网络号。一种通信方式是在以太网局域网上使用 IPX（本节描述的内容）。
- Password Handling（7）—— 决定是否以及如何加密 密码。
- Minimal UID/GID Rights（10）—— 授予 `nobody` 用户的最小权限。
- Supervisor Login（12）—— 授予 `root` 登录。默认情况下，其 权限为 99。
- 99 默认情况下，其组权限为 99。
- User Logins（13）—— 映射到 `root` 登录。
- Automatic Login（15）—— 决定是否自动映射 登录。
- Startup Tests（16）—— 在启动时运行检查。

### Red Hat Linux 默认服务器设置

www.unlted.com 上的额外内容

Red Hat Linux 网络和服务器设置

| 数字 | 章节 | 默认值 |
| :--- | :--- | :--- |
| 1 | SYS | `/var/nwe/sys` |
| 2 | CDROM | `/mnt/cdrom` |
| 4 | | `0x0` |
| 7 | | `1` |
| 10 | | `99` |
| 11 | | `99` |
| 12 | SUPERVISOR | `root` |
| 15 | | `maple` |

这些 `SYS`（`/var/nwe/sys` 目录）和 `CDROM`（`/mnt/cdrom`）卷被共享。服务器名称是自动分配的（`auto`）。Linux 内核可以选择一个网络号。网络接口是 `eth0`（第一个以太网网络），帧类型是 802.3。最小用户和组权限被授予 UID 99（`nobody`）。`SUPERVISOR` 权限被授予 `root`（带有初始密码 `secret`）。UID 99 的密码为 `top-secret`。

### 启动 NetWare 服务器守护进程

此时，你都必须启动 NetWare 服务器进程。你可以通过输入 `nwserv` 来执行。你的另一种选择（长期来看更好）是从系统初始化脚本启动服务器。`mars-nwe` 包提供了一个脚本，但它可能没有配置为自动启动。要自动启动 NetWare 服务器进程，请输入：

```
# cd /etc/rc3.d; mv K*mars-nwe S92-mars-nwe

# cd /etc/rc5.d; mv K*mars-nwe S92-mars-nwe
```
