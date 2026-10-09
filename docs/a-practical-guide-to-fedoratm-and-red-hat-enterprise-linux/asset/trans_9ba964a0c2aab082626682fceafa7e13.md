
## firewalld 服务

**firewalld** 服务（使用 **firewalld** 守护进程）正在取代 **iptables** 服务。与 **iptables** 服务相比，**firewalld** 服务无需在每次更改时重新加载；它可以在运行时接受防火墙的更改。频繁重新加载 **iptables** 服务会中断已建立的连接。在虚拟化环境中，这个问题尤为明显，因为每当虚拟机启动或关闭时，防火墙都会发生变化。**libvirt** 库（第 662 页）现在使用 **firewalld** 来按需调整防火墙。

在 **firewalld** 下设置的防火墙必须由 **firewalld** 守护进程直接管理，以便守护进程中的状态和内核中的状态保持同步。因此，你不能使用 **iptables** 命令向由 **firewalld** 控制的防火墙添加规则。

**firewalld** 守护进程引入了一层抽象，使防火墙的设置更简单、更直观。不像 **iptables** 那样编写防火墙规则，使用 **firewalld** 时，你使用 *firewall-config*（GUI）或 *firewall-cmd*（CLI）来设置防火墙。

**firewalld** 守护进程由 systemd（第 438 页）通过 **firewalld.service** 单元进行管理。它在网络启动之前启动，以便在网络启动时能够立即保护网络。

运行在*内核空间*（第 1257 页）中的 *netfilter* 是一组表，其中包含内核用于控制网络数据包过滤的规则。为了发挥作用，*netfilter* 需要一个前端。**firewalld** 前端运行在*用户空间*（第 1279 页），允许管理员设置防火墙（就像 **iptables** 那样）。

D-BUS（www.freedesktop.org/wiki/Software/DBus）是一种 IPC（进程间通信系统），也称为消息总线系统，它允许应用程序和进程相互通信并通过总线请求服务。**dbus** 服务（运行 **dbus-daemon**）会通知进程事件（例如，当添加新设备或用户登录时）。

**firewalld** 守护进程具有 D-BUS 接口，允许其与进程通信。应用程序、守护进程和管理员可以使用 D-BUS 启用/禁用 **firewalld** 功能。这些功能可以包括打开端口、转发端口或数据包，以及执行更高级的任务。

## firewalld 配置

本节描述了 **firewalld** 配置的某些方面。

### 运行时与永久配置

当你设置或更改 **firewalld** 功能时，可以在运行时配置中操作，这会使更改立即在运行中的系统上生效。或者，你可以在永久（持久）配置中进行更改，这在防火墙重新加载或系统重启时生效。

### 区域

（网络）区域定义了网络连接的信任级别。例如，你可能有一个用于 LAN 的区域和一个用于 Internet 的区域。在笔记本电脑上，区域可能会根据计算机是使用公共 Wi-Fi 网络还是使用办公有线连接而改变。表 25-1 列出了默认的区域集合。

public 区域 默认区域是 public，也是本章唯一讨论的区域。

**表 25-1 防火墙区域**

| 区域 | 功能 |
| :--- | :--- |
| drop | 丢弃传入数据包且不回复；允许传出连接 |
| block | 使用 icmp-host-prohibited (ipv4) 或 icmp6-admin-prohibited (ipv6) 拒绝传入连接；允许传出连接；有关 ICMP 的定义请参见第 1254 页 |
| public | 不信任其他系统不会伤害本地系统；接受 ssh、mdns 和 dhcpv6-client 服务（默认区域） |
| external | 不信任其他系统不会伤害本地系统；用于启用伪装的外部网络（尤其是路由器）；接受选定的传入连接 |
| dmz | 用于本地 DMZ（第 890 页）中对本地网络访问受限的公开可访问计算机；接受选定的传入连接 |
| work | 主要信任其他系统不会伤害本地系统；接受选定的传入连接 |
| home | 主要信任其他系统不会伤害本地系统；接受选定的传入连接 |
| internal | 主要信任其他系统不会伤害本地系统；接受选定的传入连接 |
| trusted | 完全信任其他系统不会伤害本地系统；接受所有连接 |

### 服务

服务是一个或多个端口和协议（TCP 或 UDP）的组合。例如，SSH 服务使用 TCP 端口 22。可选地，服务可以包括目标地址。

### 锁定白名单

防火墙使用的主要认证机制称为 polkit（www.freedesktop.org/wiki/Software/polkit）。默认情况下，防火墙锁定白名单是关闭的，并不影响什么或谁可以修改防火墙。当它开启时，防火墙除了使用 polkit 外，还使用此白名单，并且只有以锁定白名单中指定的 (SELinux) 上下文运行的应用程序，以及此列表中指定的命令和用户，才被允许修改防火墙。在初始设置中，只有 `NetworkManager`（第 637 页）、`libvirt`（第 662 页）以及以 root 权限运行的用户/进程在此白名单上。

### 用户界面

你可以使用两种接口之一来设置 `firewalld`：`firewall-config` GUI（见下文）或 `firewall-cmd` CLI（第 906 页）。其他进程使用 D-BUS 与 `firewalld` 通信。一些桌面还显示 `firewall-applet`（`firewal-applet` 包），你可以使用它与 `firewalld` 进行交互。截至本文撰写时，GNOME 3 未能正确显示此小部件，因此你无法在 GNOME 3 中使用 `firewall-applet`。

### 先决条件

安装以下软件包（两者均默认安装）：

- firewalld
- firewall-config

**检查 firewalld 是否正在运行**

新的 Fedora/RHEL 系统启动时，`firewalld` 已安装并正在运行。使用 `systemctl status` 命令确保服务正在运行。以下输出显示 `firewalld` 正常运行的状态。如果 `firewalld` 未运行，Active 行将显示 `inactive` (dead)。

```
$ systemctl status firewalld.service
Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled)
Active: active (running) since Thu 2013-08-15 14:33:00 PDT; 6 days ago
Main PID: 374 (firewalld)
CGroup: names+systemd/system/firewalld.service
└-374 /usr/bin/python /usr/sbin/firewalld --nofork --nopid
```

```
Aug 15 14:33 guava.example.com systemd[1]: Started firewalld -- dynamic firewall daemon
```

**重新加载和停止 `firewalld`**

在使用 `root` 权限操作时，你可以输入上述命令，将 `status` 替换为 `reload` 以使 `firewalld` 重新读取其配置文件，使用 `stop` 停止 `firewalld`，或在停止时使用 `start` 启动它。

**恐慌模式**

如果系统受到攻击，输入以下命令立即关闭网络。参见第 902 页的警告提示。

```
$ su -c "firewall-cmd --panic-on"
```

使用 `--panic-off` 选项将防火墙恢复到其先前状态。

### 快速入门：使用 `firewall-config` 构建防火墙

本节解释了如何使用图形化工具 `firewall-config` 来信任一个服务（打开一个端口）。按照这些说明在运行中的系统（运行时配置）和系统重启后（永久配置）中打开该端口。有关更多信息，请参见下一页的“*firewall-config：防火墙配置窗口*”。有关更复杂的防火墙，请参见 *firewall-cmd*（第 906 页）或 *iptables*（第 908 页）。

![](img/243613168ac865b539f12460d966088e_957_0.png)

### 防火墙默认已启用

> 安装 Fedora/RHEL 时，系统中会安装 *firewalld*。防火墙正在运行并阻止大多数入站流量。然而，*firewalld* 接受 TCP 端口 22 上的入站流量，允许远程系统连接到本地系统上的 *sshd* 守护进程。有关设置 OpenSSH 服务器的信息，请参见第 700 页。此外，*firewalld* 接受 mDNS（多播 DNS；www.multicastdns.org；仅适用于 Fedora）和 dhcpv6 客户端流量。

防火墙配置窗口（图 25.1）允许你构建简单的防火墙，或在紧急情况下将防火墙置于恐慌模式，从而切断所有网络通信。通过从“输入命令”窗口（ALT+F2）或终端模拟器输入命令 *firewall-config* 来打开此窗口。如果你不以 root 权限运行 *firewall-config*，它会显示一个认证窗口；输入请求的密码并点击 *Authenticate*。

### 将 firewalld 置于恐慌模式

在紧急情况下，例如系统受到攻击时，你可以将 *firewalld* 置于恐慌模式来阻止所有网络通信。在恐慌模式下，*firewalld* 丢弃所有传入和传出数据包，并允许活跃连接过期。恐慌模式仅影响 *firewalld* 的运行时配置：当系统重启时，防火墙将恢复到其永久配置。

