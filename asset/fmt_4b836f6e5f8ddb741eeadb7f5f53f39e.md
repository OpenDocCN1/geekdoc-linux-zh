
![](img/a123b4f2456cac935474ae2401b95b01_508_0.png)

# 478 第三部分 ♦ 选择并安装 Linux 发行版

6. 你只需输入 `N` 接受默认 IP 地址（子网掩码、广播、网络）。如果你在为局域网创建一组新地址，请输入 `y`。

你想更改这些设置吗？`[Y/N]: N`

7. 空闲时间（网络上发送数据时）后后掉线的秒数。默认是 `180`（三分钟）。我将其更改为 `600`（十分钟）。

`Enter number of seconds for idle disconnect [180]: 600`

8. 要使用特定的 IP 地址（由 ISP 分配）连接互联网，请输入 `y` 然后按要求添加 IP 地址。大多数情况下，只需输入 `n` 让 ISP 分配 IP 地址。

`Did your ISP assign you static IP ADDRESS? [y/n]: n`

设置动态 PPP

9. 需要一个初始 IP 来启动 PPP 接口。如前所述，你应该使用一个位于局域网网络的 IP 地址。

`Press enter for [192.168.0.3]: 192.168.0.3`

10. 接下来的几个问题与设置拨出连接有关。`tty` 设备是调制器连接的端口（`tty0` 对应 `COM1`，`tty1` 对应 `COM2`，以此类推）。端口速度是指计算机与调制解调器通信的速度（默认的 `115200` 即可）。`ATZ` 是初始化调制解调器的脚本（如果需要其他内容，请查看调制解调器手册）。输入代表你 ISP 的任何名称（无空格）。输入获取互联网连接的电话号码。最后，输入 ISP 为你的互联网账户提供的用户名和密码。

# 第 18 章 ✦ 运行 Linux 防火墙/路由器 479

```
调制调器的 tty 设备名称 (ttySO, 等)[ttySO]: ttySO
输入 ttySO 的端口速度 (115200, 57600, 等)[115200]: 115200
输入调制调器初始化字符串 (Enter = ATZ): ATZ
输入 ISP 名称（不包含空格)[isp]: att
输入拨号号码: 5551212
输入用户名: jmsmit
输入密码: tkN0st
```

12. 输入 `n` 以便在登录时不发送明文密码。如果你的 ISP 请求 `CHAP` 或 `PAP` 认证，你可能需要将其改为 `y`。

如果你启用了此项，你的密码将以明文形式通过线路发送。如果在验证了一切后仍然无法连接到 ISP，请在此处说明。

```
在对话期间登录？[y/n]: n
```

13. 因为此防火墙将为局域网上的其他计算机提供 IP 地址，因此它需要作为一个 DHCP 服务器 (`y`)。然后列出它可以分配给这些计算机的地址。如果你计划在局域网上有 100 台或更少的计算机，示例中的地址范围应该适用于你：

```
你想要 coyote chat DHCP 服务器吗？[y/n]: y
输入 DHCP 起始 IP [192.168.0.100]: 192.168.0.100
输入 DHCP 结束 IP [192.168.0.200]: 192.168.0.200
```

14. 如果你希望由同一个防火墙保护 Web 服务器，那么 DMZ 是一种将你的本地网络从外部世界进一步隔离开的方法。在这种情况下，你可以为防火墙添加另一块网卡，将其连接到 Web 服务器，然后允许 Web 服务的入站请求通过 Web 服务器。这允许你阻止所有进入局域网桌面系统的入站流量。例如，只需选择 `N`。

如果你不知道什么是 DMZ，直接回答 `NO`

```
你想要配置非军事区吗？[Y/N]: N
```

15. 设置与此防火墙关联的域名，并输入将解析地址的 DNS 服务器 IP 地址（可能由你的 ISP 提供，除非你正在运行自己的 DNS 服务器）：

```
输入域名: example.com
输入 DNS 服务器 1: 123.45.68.799
输入 DNS 服务器 2（可选): 123.45.68.800
```

如果你在局域网上有一个想让 Coyote 发送 syslog 数据的 syslog 服务器，你可以在此处指定地址。
如果不确定或没有 syslog 服务器，请留空此项。

# 480 第三部分 ♦ 选择和安装 Linux 发行版

16. 你可以让 Coyote 在网络上的另一台服务器上记录其活动。这非常有用，因为可以将日志从防火墙中移除（这样别人就无法篡改），并允许你对网络上的日志进行集中管理。在使用此功能之前，你需要在你的日志计算机上配置远程日志支持。为此，我建议使用大多数 Linux 系统上的 syslog 守护进程 (`syslogd`)。查找“Support for Remote Logging”部分。要禁用它（如示例所示），只需按 Enter 继续。

```
Syslog 服务器地址：
```

17. Coyote Linux 支持一系列以太网卡。你必须知道防火墙上每块以太网卡的驱动程序模块名称并输入它（如果你遵循了本节开头的注意事项，你应该已经有了这些信息）。对于 ISA 卡（由于是一台非常老旧机器，可能没有这些信息），你需要添加 `IO` 和 `IRQ`。

```
输入你本地网卡的模块名称: 8139to
输入 IO 地址（PCI 卡留空）：
输入 IRQ（PCI 卡留空）：
```

```
Checking module dependencies...
8139too = mi
```

Coyote Web 管理员的默认语言是英语。你喜欢配置不同的语言吗？`[Y/N]: N`

18. 若要为英语以外的语言配置 Coyote Web 管理员，请选择 `Y`。从多个可用语言中进行选择。然后 Coyote 设置脚本将构建软磁盘镜像：

```
Building package: etc
Building package: local
Building package: modules
Building package: root
Building package: dhcpd
Building package: webadmin
```

19. 向软驱驱动器插入一张空白软盘并按回车以构建你的软磁盘 Coyote Linux 发行版：

确保此系统的第一个软驱驱动器中有一张软盘并按键继续...

```
Formatting /dev/fddu1440
Double-sided 80 tracks 18 sec/track. Total capacity 1440 kB
Formatting ... done
Verifying ... done
bin/mkdosfs 2.2 (06 Jul 1999)
```

# 第 18 章 ✦ 运行 Linux 防火墙/路由器 481

```
Installing boot loader...
Copying files...
cp: omitting directory 'floppy/config'
'floppy/dhcpd.tgz' -> mnt/dhcpd.tgz'
'floppy/etc.tgz' -> mnt/etc.tgz'
'floppy/linux' -> mnt/linux'
'floppy/local.tgz' -> mnt/local.tgz'
'floppy/modules.tgz' -> mnt/modules.tgz'
'floppy/root.tgz' -> mnt/root.tgz'
'floppy/syslinux.cfg' -> mnt/syslinux.cfg'
'floppy/SYSLINUX.cfg' -> mnt/SYSLINUX.cfg
'floppy/webadmin.cfg' -> mnt/webadmin.cfg
'floppy/coyote.cfg' -> mnt/coyote.cfg'
'floppy/fireloc.cfg' -> mnt/fireloc.cfg'
'floppy/firewall.cfg' -> mnt/firewall.cfg'
'floppy/hosts.dns' -> mnt/hosts.dns'
'floppy/portfw.cfg' -> mnt/portfw.cfg'
'floppy/qosfilt.cfg' -> mnt/qosfilt.cfg'
```
