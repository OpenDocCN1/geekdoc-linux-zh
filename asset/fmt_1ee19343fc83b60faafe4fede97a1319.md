
# setup

# 第 9 章 — 构建专用的 SOHO 防火墙

在显示的 Devil-Linux 系统配置界面上，你可以看到图 9-5 所示的菜单选项。

![](img/1b8a24a162893627b8005ac678b79236_277_0.png)

图 9-5：Devil-Linux 设置菜单文本菜单

以下章节将帮助你根据需求配置防火墙系统。请参考图 9-1 并注意此防火墙/网关旨在：

- 在 `eth0` 上获取 DHCP IP 地址以连接宽带提供商
- 在你的内部 `eth1` 接口上提供 DHCP 服务
- 为你的内部网络运行 DNS (`BIND`)
- 在内部运行 `SSH`，以便你的管理员可以在内部管理防火墙
- 可能运行其他服务来协助监控防火墙流量 (`ntop`, `ntop`, `httpd`)

在执行以下任何设置程序期间，你都可以从主菜单（`Main Menu`）选择 `Config`（配置）来保存当前设置。通过这种方式，你可以在完成程序之前退出 Devil-Linux 设置（如果需要的话），而不会丢失已完成的工作。

## 基础

在主菜单界面上，你可以设置主机名、域名（如果你使用的是注册域名）以及你的时区。

| hostname example.com -- 如果使用真实域名则进行替换 | 域名 |
| :--- | :--- |
| TIMEZONE CST6CDT | |

> 如果你没有想要与机器关联的注册域名，你应该列出主机名和域名，以匹配宽带提供商提供给你防火墙 `eth0` 的 IP 地址的 FQDN（全主机名）。你可以通过登录防火墙（稍后）、运行 `ifconfig` 确定 `eth0` 的 IP，然后运行 `host <IP>` 来查看你的防火墙在互联网上的全名。然后你可以在先前的设置中使用它。

检查是否有任何你需要更改的内容（例如你的默认键盘或鼠标），并选择 `Back`（返回）继续进入下一个菜单。

## 服务

配置菜单的服务项控制防火墙启动时启动哪些服务。这些服务包括实际上启用 Devil-Linux 路由器/网关功能和防火墙功能的初始化脚本，以及常见的 SOHO 网关所需的服务，如 DNS (`named`)、网络时间同步工具 (`ntpd`) 和 `dhcp`。

- [x] `CRON` 周期性命令调度器
- [x] `IPV6_ROUTING` 启动时执行互联网协议防火墙脚本
- [x] `NAMED` Bind 命名服务 (`DNS`) 守护进程
- [x] `NTPD` 网络流量探测工具
- [x] `ROUTING` 启用路由（接口之间）
- [ ] `SHAREWALL` 替代防火墙创建/启动（目前不建议使用）
- [x] `SSH` 用于安全登录的安全 Shell | 文件传输
- [x] `THHTTP` 轻量、快速且安全的 Web 服务器（小心！）

`DHCP` 服务将在稍后配置内部局域网（LAN）布局时进行配置。接下来，在你选择了上述服务后，选择 `OK`，以便保存你的选择并继续进入下一个菜单。

> 我建议不要一开始就设置 `shorewall` 启动脚本。`Shorewall` 是一个非常强大的配置脚本工具，但你首先需要使用 `DHCP` 防火墙脚本让系统运行起来，或者从零开始自定义或优化你自己的防火墙脚本，或者使用如 `shorewall` 或 `fvbuilder` 类的脚本编写器。相信我——你可能不想同时排查 `DHCP`、`DNS` 和 `IPTables` 规则！关于 `shorewall` 的信息请查看 [www.shorewall.net/two-interface.html](http://www.shorewall.net/two-interface.html)，对于 `fvbuilder` 请查看：[www.linuxjournal.com/article/625 and how.linux.com](http://www.linuxjournal.com/article/625 and how.linux.com)。

## 网络

在 `NET` 菜单中，你可以配置宽带提供商提供给防火墙 `eth0` 的 IP 地址的 FQDN（全主机名）。你可以通过登录防火墙（稍后）、运行 `ifconfig` 确定 `eth0` 的 IP，然后运行 `host <IP>` 来查看你的防火墙在互联网上的全名。然后你可以在先前的设置中使用它。

检查是否有任何你需要更改的内容（例如你的默认键盘或鼠标），并选择 `Back`（返回）继续进入下一个菜单。

# 第9 章 — 构建专用的 SOHO 防火墙

直接在控制台或远程（使用 `ssh`）登录防火墙（从内部域网，使用 `ssh root@192.168.1.1`），并编辑位于 `/etc/dhcpcd.conf` 的 DHCP 守护进程配置文件（使用 `/etc/dhcpcd.conf`）。

如果你使用的是 Linux 系统，或者不仅仅是 Linux，可以使用 `pico` 或 `joe` 编辑器。
如果你不熟悉 `pico`，在用 `pico /etc/dhcpcd.conf` 打开配置文件后，只需按 `F1` 获取帮助，并按 `Ctrl+X` 保存并退出。附录 8 提供了文本编辑器的快速教程。

![](img/1b8a24a162893627b8005ac678b79236_281_0.png)

根据 DHCP 配置中提到的设置，你的 `/etc/dhcpcd.conf` 文件看起来如下：

```
# 在 Devil Linux 上重启 DNS:

# /etc/init.d/dhcpcd stop

# /etc/init.d/dhcpd start

#

######## 我的网络布局 ######

## 1      防火墙/网关

## 2-10    留给我们的机器

## 10-250  访/DHCP IP (wap)

## 251-254 特殊边缘设备

############################

authoritative;

default-lease 14400;

max-lease 14400;

lease-hostnames false;

use-host-decl-names on;

ndns-update-style none;

option domain-name="example.com"

option subnet-mask 255.255.255.0;

### 这是我的内部域网动态/访 IP 范围 ####

subnet 192.168.1.10 netmask 255.255.255.0

option domain-name-servers 192.168.1.2;

option routers 192.168.1.1;

option broadcast-address 192.168.1.255;

range 192.168.1.10 192.168.1.250;

}

### 这些是映射了 MAC 地址的静态 IP 的已知机器

host fileserver {

  hardware ethernet 00:e0:29:3d:a0:93;

  fixed-address 192.168.1.2;

}

host janice3 {

  hardware ethernet 00:08:54:d1:94:21;

  fixed-address 192.168.1.3;

}

host fixed4 {

  hardware ethernet 00:00:c0:a8:80:04;

  fixed-address 192.168.1.4;

}

host fixed6 {

  hardware ethernet 00:00:c0:a8:80:06;

  fixed-address 192.168.1.6;

}

host fixed7 {

  hardware ethernet 00:00:c0:a8:80:07;

  fixed-address 192.168.1.7;

}

host fixed8 {

  hardware ethernet 00:00:c0:a8:80:08;

  fixed-address 192.168.1.8;

}

host fixed9 {

  hardware ethernet 00:00:c0:a8:80:09;

  fixed-address 192.168.1.9;

}

#### 网络设备 ####

host wap {

  hardware ethernet 00:0c:66:0c:2f:14;

  fixed-address 192.168.1.254;

}
```
