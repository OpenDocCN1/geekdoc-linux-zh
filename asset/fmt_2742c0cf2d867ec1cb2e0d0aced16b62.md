
```
$ kali@kali:~$ chmod 777 kali.txt
$ kali@kali:~$ ls -l
total 40
drwxrxr-r-x 2 kali 4096 Jun 22 04:43 kali
-rw-rw-x 1 kali 4096 Jun 22 04:51 kali.txt
drwxrxr-r-x 2 kali 4096 Jun 22 03:18 Desktop
drwxrxr-r-x 2 kali 4096 Jun 22 03:18 Documents
drwxrxr-r-x 2 kali 4096 Jun 22 04:53 Downloads
--rw-r--r-- 1 kali 0 Jun 22 04:54 example.txt
drwxrxr-r-x 2 kali 4096 Jun 22 03:18 Music
drwxrxr-r-x 2 kali 4096 Jun 22 03:18 Pictures
drwxrxr-r-x 2 kali 4096 Jun 22 03:18 Public
drwxrxr-r-x 2 kali 4096 Jun 22 03:18 Templates
drwxrxr-r-x 2 kali 4096 Jun 22 03:18 Videos
```

图 2 `ls -l` 命令

`[root@localhost ~]# chmod 777`

再次点击回车键输入 `-l`

八进制表示 所有者 组 其他

| r w x | r w x | r w x |
| :--- | :--- | :--- |
| 4 2 1 | 4 2 1 | 4 2 1 |

### 2.3.15 `hostname`

主机名是赋予连接到网络的计算机的名称，用于在网络上唯一标识该计算机，并允许在不使用 IP 地址的情况下对其访问。`hostname` 命令用于查看系统主机名和 DNS（域名服务器）。使用此命令可以更改主机名。

语法：`hostname [options] [new_host_name]`

## 2.4 安装软件

在 Windows 中，通过运行 `setup.exe` 文件来安装程序。安装包包含了程序本身以及正确运行软件所需的许多依赖组件。

对于 Linux / UNIX，安装文件以包的形式分发。但该包只包含程序本身。任何通常以包形式提供的依赖组件必须单独安装。你可以使用 `sudo apt update` 使用 `apt` 命令来安装、删除或更新系统中所有已安装的包。

```
kali@kali:~$ sudo apt-get update
```

## 总结

- Linux 是基于内核的开源操作系统。通常，Linux 同时为桌面版和服务器发行版打包。Linux 内核是操作系统的基础部分。

- 命令行是一个基于文本的界面，帮助执行命令并显示输出。图形界面（GUI）是内部的命令解释器。

## 章节复习

1. Kali 正在用于 Linux 托管。哪个文件夹包含了所有的配置？

A. `/bin`

B. `/usr`

C. `/home`

D. `/etc`

2. 哪个目录包含所有用户共享、下载和创建的文件？

A. `/home`

B. `/media`

C. `/etc`

D. `/var`

3. Linux 功能所需的所有库文件在哪里？

A. `/bin`

B. `/media`

C. `/lib`

D. `/var`

4. Daniel 将一个 USB 盘插入了 Kali Linux 机器，并想知道设备的路径。这些设备挂载在哪里？

A. `/bin`

B. `/var`

C. `/opt`

D. `/media`

5. Kali 正在为防火墙和磁盘管理配置系统。

A. `/bin`

B. `/var`

C. `/opt`

D. `/media` (此处原文题目不完整，按原意翻译)

# 第 3 章 配置 Kali

## 3.1 配置网络

虚拟网络由 3 种类型组成：

- NAT

- Bridge

- NAT 网络

这些是我们在任何虚拟机上配置的 3 种主要类型。那么，它们是什么？这些类型提供什么？

`NAT`：在启动操作系统时自动虚拟机分配子网 IP 地址的网络类型。

`Bridge`：如果这种网络由路由器本身分配 IP 地址，虚拟机将被视为主机网络中的设备，即虚拟机将从同一个子网获取 IP 地址。

桥接网络

```
kali@~$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
      inet 192.168.1.12 netmask 255.255.255.0 broadcast 192.168.1.255
      inet6 2401:4900:1f26:51e4:76f5:a18f:9600:cb2 prefixlen 64 scopeid 0x
```

图 24 桥接网络

`NAT` 网络

```
kali@~$ sudo ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
      inet 10.0.2.15 netmask 255.255.255.0 broadcast 10.0.2.255
      inet6 2401:4900:1f26:51e4:76f5:a18f:9600:cb2 prefixlen 64 scopeid 0x
```

图 25 `NAT` 网络

# Secbay 出版

`NAT 网络`：当您创建了一个网络，在虚拟框内配置了网络地址掩码和网络 IP，并在虚拟机启动时为 VM 分配相同的子网 IP 地址。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_82_0.png)

图 26 `NAT` 网络

### 3.1.1 带有 Network Manager 的桌面环境

Network Manager 在默认桌面安装期间，已通过 GNOME 的控制中心进行了预安装和配置。配置的配置依赖于动态主机配置协议（DHCP）来获取 DNS 服务器、网关和 IP 地址。

在诸如 SSH、OpenVPN、Cisco 的 VPNPC 等插件的支持下，可以使用 Network Manager 管理所有形式的网络连接，如 WAN、使用 PPP 的路由器以及 VPN。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_82_1.png)

图 27 带有 Network Manager 的桌面

©Secbay Press * 83 | 页

### 3.1.2 使用 Ifupdown 的命令行

使用预安装的 `ifupdown` 软件包，用户可以使用命令行配置 Network Manager。这些工具在 `/etc/network/interfaces` 目录下有配置文件，并在 `/etc/init.d/networking` 目录下有一个在启动时配置网络的脚本文件。

网络设备的配置和管理都是通过使用 `ifupdown` 命令完成的。有两个选项：

1. 正如名称所示，`auto` 网络设备在适用时自动配置网络接口。
2. 根据提供的接口配置 `inet / inet6` 网络设备 `iface`。
3. 无线连接默认可以使用 `wpa_supplicant` 软件包。最常用的替代方案是 `wpa-psk` 和 `wpa-ssid`。

### 3.1.3 使用 systemd-networkd 的命令行

一个值得了解的新工具是 `Systemd-networkd`。它并不特定于基于 Debian 的发行版（与 `ifupdown` 不同），并且被设计得非常小，如果你使用 `system unit` 文件的语法，配置起来相对简单。在考虑到 `NetworkManager` 臃肿且难以配置时，这是一个特别有吸引力的替代方案。

通过将网络文件放置在 `/etc/systemd/network/` 目录下，我们可以配置 `systemnetwork`。`Match` 部分描述了配置所引用的网络接口。你可以以多种方式定义接口，包括地址或系统形式的访问控制（MAC）。`Network` 部分定义了网络的配置。要在基于 Debian 的访问中使用任何预安装的功能，也应以类似的方式启用，`systemd-networkd` 是预安装的，但应该开启对其的访问。

`Systemd-networkd` 的集成使得管理各种虚拟网络和其他场景变得简单。

```
root@kali:~~$ systemctl status systemd-networkd
● systemd-networkd.service - Network Service
   Loaded: loaded (/lib/systemd/system/systemd-networkd.service; disabled; >
   Active: inactive (dead)
   TriggeredBy: ● systemd-networkd.socket
   Docs: man:systemd-networkd.service(8)
lines 1-5/5 (END)
```

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_83_0.png)
