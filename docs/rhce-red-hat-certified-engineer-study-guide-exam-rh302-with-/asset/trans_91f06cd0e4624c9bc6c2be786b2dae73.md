

# 582 第 23 章 • 理解二级网络服务

电子邮件地址：bmccarty@azuspacific.com

注释：
你选择了此 USER-ID：
"Bill McCarty <bmccarty@apu.edu>"

更改(N)ame、注释(C)oment、邮件(E)mail 或 确认(O)kay/退出(Q)uit
你需要一个密码短（Passphrase）来保护你的密钥。

thisisatest
我们需要生成大量的随机字节。在生成质数期间，执行一些其他操作（在另一个窗口中、移动鼠标、利用网络和磁盘）是一个好主意；这能让随机数生成器有更好的机会获得足够的熵。

++++++++++++ +++++++++++++ ++++++
+++++, ++++++, +++++++++++++, ++++++
+++++, ++++++, +++++++++++++, ++++++
+++++, ++++++, ++++++, ++++++

已创建并签名了公钥和私钥。

你还必须下载并安装 Red Hat, Inc. 用于签名 RPM 包的公钥。该密钥可以在 www.redhat.com/about/contact.html 获取。将密钥下载到文件 redhat2.asc 中，然后通过执行命令进行安装

```
gpg --import redhat2.asc
```

命令输出将显示以下内容：
gpg (GNUPG) 0.4.0; Copyright (C) 1998 Free Software
Foundation, Inc.
本程序不带任何**绝对**的保证。
这是一款免费软件，欢迎在某些条件下进行重新分发。详情请参阅 COPYING 文件。

```
gpg:redhat2.asc: key DB42A60E: public key imported
```

要验证 RPM 包的签名，请执行如下格式的命令：
rpm -K package_file
例如，你可以执行以下命令来验证 basesystem 包的签名：
rpm -K basesystem-6.0-4.noarch.rpm

如果签名匹配，输出将如下所示：

basesystem-6.0-4.noarch.rpm: md5 gpg 0K
\欲了解更多关于 GNUPG 信息，请参阅 GNUPG 网站：
www.gnupg.org。

# 总结

在本章中，你学习了二级网络服务。涵盖的最重要主题是：

- **动态主机配置协议 (DHCP)** DHCP 允许配置客户端在系统启动时获取其网络配置信息。DHCP 配置文件为 /etc/dhcpcd.conf。可以配置 DHCP 服务器为给定的主机提供固定信息，服务器通过主机的媒体访问控制（MAC）地址识别该主机。或者，DHCP 服务器也可以从池中提供可用的配置。

- **DHCP 客户端** Linux DHCP 客户端名为 pump。使用 linuxconf 或 netconf，你可以配置 Linux 系统在启动时通过 pump 获取其网络配置。

- **IPX 协议** IPX 协议是 Novell NetWare 系统的原生协议。Red Hat Linux 的 mars-nwe 包文件和打印机共享与 Novell 的 IPX 协议兼容的。

- **远程打印机访问** Red Hat Linux 远程打印机访问由 lpd 服务提供。要定义远程打印机，你可以使用 printtool 修改 /etc/printcap 文件。要为远程主机启用打印机，请在 /etc/hosts.lpd 或 /etc/hosts.equiv 文件列出远程主机。

- **互联网新闻** 互联网新闻由 ip 包提供。互联网新闻的配置相对困难，并且需要大量的计算资源，特别是磁盘。

- **时间同步** 你可以使用 rdate 或 xntp3 同步系统时间。xntp3 设施使用网络时间协议 (NTP)，是两个设施中更复杂的一个，并提供更精确的时间同步。该设施的主配置文件为 /etc/ntp.conf。

# 第 23 章 • 二级网络服务

在本章中，你学习了二级网络服务。最重要的主题是：

