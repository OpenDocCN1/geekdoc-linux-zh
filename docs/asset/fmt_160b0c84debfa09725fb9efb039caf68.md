
# 第 18 章 ✨ 运行 Linux 防火墙/路由器

## 11. 设置拨出连接

接下来的几个问题与设置拨出连接有关。调制解调器连接的设备（`COM1` 使用 `ttyS0`，`COM2` 使用 `tty1`，以此此类推）。端口速度是指计算机与调制解调器通信的速度（默认值为 `11520` 即可）。`ATZ` 是初始化调制解调器的正常脚本（如果需要其他，请查看你的调制解调器手册）。输入代表你 `ISP` 的任何名称（无空格）。输入用于获取互联网的电话号码。最后，输入 `ISP` 为你的互联网账户提供的用户名和密码。

输入调制调器的 `tty` 设备名称 (`ttySO`, 等)`[ttySO]`: `ttySO`

输入 `ttySO` 的端口速度 (`115200`, `57600`, 等)`[115200]`: `115200`

输入调制调器初始化字符串 (回车 = `ATZ`): `ATZ`

输入 `ISP` 名称（无空格)`[isp]`: `att`

输入拨号电话: `5551212`

用户名: `jmsit`

输入密码: `tkn0st`

## 12. 密码传输选项

输入 `n` 以在登录时不发送明文密码。如果你的 `ISP` 要求 `CHAP` 或 `PAP` 认证，你可能需要将其更改 `y`。

如果你启用了此项，你的密码将以明文形式通过线路发送。尽管已经验证了一切，仍然无法连接到 `ISP`。

在聊天期间登录？`[y/n]`: `n`

## 13. DHCP 服务器配置

因为此防火墙将为你局域网（`LAN`）上的其他计算机提供 `IP` 地址，因此它需要分配一个 `DHCP` 服务器 (`y`)。然后是它可以分配给这些计算机的地址范围。如果你计划在局域网上有 `100` 台或更少的计算机，此示例中的地址范围适用于你：

想要使用 `coyote DHCP` 服务器吗？`[y/n]`: `y`

输入 `DHCP` 起 `IP` `[192.168.0.100]`: `192.168.0.100`

输入 `DHCP` 结束 `IP` `[192.168.0.200]`: `192.168.0.200`

## 14. DMZ 配置

如果你想让同一个防火墙保护 `Web` 服务器，`DMZ` 是一种让你的本地网络免受外界影响的方法。在这种情况下，你可以为防火墙添加另一个网卡，将其连接到 `Web` 服务器，然后允许 `Web` 服务的传入请求通过服务器。这允许你阻止所有进入局域网桌面系统的流量。我直接选择了 `N`。

如果你不知道什么是 `DMZ`，只需回答 `NO`

你想配置非军事区（`DMZ`）吗？`[Y/N]`: `N`

## 15. 域名与 DNS 配置

设置与防火墙关联的域名，并输入解析地址所需的 `DNS` 服务器 `IP` 地址（可能由你的 `ISP` 提供，除非你正在运行自己的 `DNS` 服务器）：

输入域名: `example.com`

输入 `DNS` 服务器 `1`: `123.45.68.799`

输入 `DNS` 服务器 `2`（可选）： `123.45.68.800`

如果你在局域网上有一个让 `Coyote` 发送 `syslog` 数据的 `syslog` 服务器，你可以在这里指定地址。

如果不确定或没有 `syslog` 服务器，请留空此项。

# 480 第三部分 选择并安装 Linux 发行版

## 16. 远程日志

你可以让 `Coyote` 将活动记录到网络上的另一台服务器。这非常有用，因为可以从防火墙中移除日志（防止他人篡改），并允许你集中管理网络上的日志。在使用此功能之前，你需要在你的计算机上配置对远程日志的支持。为此，我建议在大多数 `Linux` 系统上使用 `syslog` 守护进程 (`syslogd`)。查找“Support for Remote Logging”部分。要禁用它（如示例所示），只需按回车继续。

`Syslog` 服务器地址：

## 17. 网卡模块配置

`Coyote Linux` 支持多种以太网网卡。你必须知道防火墙上每个网卡的以太网驱动模块名称并输入它。（如果你遵循了本节开头的注意事项，你应该已经拥有这些信息。）对于 `ISA` 卡（除非是非常老旧的，否则可能没有），你需要添加 `IO` 和 `IRQ` 信息。

```
输入你的本地网卡的模块名称: 8139too
输入 IO 地址（PCI 卡留空）：
输入 IRQ（PCI 卡留空）：
```

```
Checking module dependencies...
8139too deps = mii
```

`Coyote Web` 管理员界面的默认语言是英语。你想配置不同的语言吗？`[Y/N]`: `N`

## 18. 语言与镜像构建

要为 `Coyote Web` 管理员配置英语以外的语言，请选择 `Y`。从十多种可用语言中选择。随后 `Coyote` 设置程序将构建软磁盘镜像：

```
Building package: etc
Building package: local
Building package: modules
Building package: root
Building package: dhcpd
Building package: webadmin
```

## 19. 软盘构建

向软驱驱动器中插入一张空白软盘并按回车构建你的软磁盘 `Coyote Linux` 发行版：

确保该系统的第一个软驱驱动器中插入了软盘，并按回车继续...

```
Formatting /dev/fd01440
Double-sided 80 tracks 18 sec/track. Total capacity 1440 kB
Formatting ... done
Verifying ... done
bin/mkdosfs 2.2 (06 Jul 1999)
```

# 第 18 章 ✦ 运行 Linux 防火墙/路由器

```
Installing boot loader...
Copying files...\cp: omitting directory 'floppy/config'
'floppy/dhcpd.tgz' -> mnt/dhcpd.tgz
'floppy/etc.tgz' -> mnt/etc.tgz
'floppy/linux' -> mnt/linux
'floppy/local.tgz' -> mnt/local.tgz
'floppy/modules.tgz' -> mnt/modules.tgz
'floppy/root.tgz' -> mnt/root.tgz
'floppy/syslinux.cfg' -> mnt/syslinux.cfg
'floppy/SYSLINUX.cfg' -> mnt/SYSLINUX.cfg
'floppy/coyote.cfg' -> mnt/config/coyote.cfg
'floppy/fireiroc.cfg' -> mnt/config/fireiroc.cfg
'floppy/firewall.cfg' -> mnt/config/firewall.cfg
'floppy/hosts.dns' -> mnt/config/hosts.dns
'floppy/port.cfg' -> mnt/config/port.cfg
'floppy/portfw.cfg' -> mnt/config/portfw.cfg
'floppy/qosfilt.cfg' -> mnt/config/qosfilt.cfg
'floppy/reserve.cfg' -> mnt/config/reserve.cfg
```

## 20. 磁盘副本

软盘创建后，系统会询问是否想要创建另一个软磁盘。如果想要，请插入另一个磁盘进行创建。输入 `n` 即可：

想要创建此磁盘的副本吗 `[y/n]`: `n`

现在你准备好尝试你的 `Coyote Linux` 磁盘了。

# 运行 Coyote 磁盘

要启动防火墙，只需将软盘插入计算机并重启。防火墙将按照你配置的方式启动。防火墙的控制台没有直接界面，事实上，你不需要监控防火墙，因为你看不到登录提示。对防火墙的所有管理都应在局域网内完成。如果你配置了它，你的防火墙现在：

- 使用 `DHCP` 为局域网上的计算机提供地址。
- 一旦局域网内任何人尝试访问互联网，就从防火墙启动拨号连接。
- 允许从局域网到互联网的流量。
- 为局域网提供登录 (`sshd`) 和 `Web` 管理服务。

如果防火墙的行为不符合你的预期，请进入下一节进行调优。

# 管理 Coyote Linux 软磁盘

防火墙启动并运行后，你肯定想进一步管理它。你有几种方法可以访问防火墙以便通过 `Web` 界面或远程登录更改其配置。在使用远程登录之前，你必须更改系统（`root` 用户）密码，这只能通过 `Web` 界面完成。

## 使用 Web 界面

`Coyote Web` 管理员可以在局域网的任何浏览器上运行，以查看和更改防火墙配置。它位于端口 `8180`。要访问示例中配置的站点，请在浏览器中输入位置：`http://192.168.0.1:8180`。

你想做的第一件事是点击主菜单中的“System Password”按钮，为 `root` 用户添加密码。图 18-3 显示了在前节中设置的拨号连接。

![](img/a295d7eab32ca5b89b2baf8aa70_513_0.png)

图 18-3：从 浏览器管理 `Coyote Linux`。

## 使用远程登录

防火墙软盘配置为在 `ssh` 守护进程下运行，允许通过局域网（使用 `ssh` 命令）登录并管理 `Coyote Linux` 防火墙。例如，你可以输入：

```
# ssh -l root 192.168.0.1
root@192.168.0.1's password: ********
```
