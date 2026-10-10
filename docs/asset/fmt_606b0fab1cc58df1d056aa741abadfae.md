
与其使用 `iwconfig` 直接设置参数，你可以在无线设备的配置文件中指定它们。无线设备配置文件位于 `/etc/sysconfig/network-scripts` 目录下，并根据设备名称命名为 `ifcfg-eth0`。此文件已包含了许多 `iwconfig` 设置。可以通过像此处所示将 `iwconfig` 值分配给 IWCONFIG 参数来完成进一步的设置：

```
iwconfig--rate 11M
```

## iwpriv

`iwpriv` 命令与 `iwconfig` 配合使用，允许你设置针对特定类型无线设备的选项。通过 `iwpriv`，你还可以开启漫游或选择要使用的端口。使用 `private-command` 参数来输入设备特定的选项。以下示例开启了漫游：

```
iwpriv eth0 roam on
```

# 第五章：网络配置

## iwspy

你的无线设备可以检查与其接收数据的另一个无线设备连接情况，报告传输的质量、信号强度和噪声水平。你的设备可以维护一个与其可能接收数据的不同设备的地址列表。使用 `iwspy` 工具设置或添加你需要的地址。你可以列出 IP 地址或硬件设备。使用 `+` 符号将添加地址，而不是替换整个列表：

```
iwspy eth0 +192.168.2.25
```

要显示连接的质量、信号和噪声水平，你只需带上设备名称使用 `iwspy` 命令：

```
iwspy eth0
```

## iwlist

要获取有关无线设备的更详细信息（例如所有可用的频率或通道），你可以使用 `iwlist` 工具。通过设备名称配合特定参数，可以获取有关设备的特定信息，包括频率、接入点、速率、电源功能、重试限制和加密密钥。你可以使用 `iwlist` 获取有关故障连接的信息。以下示例将列出 eth0 无线设备上使用的频率：

```
iwlist eth0 freq
```

## linux-wlan

linux-wlan 项目 (www.linux-wlan.org) 为支持新的 802.11 标准的基于 Prism 的无线卡开发了一套独立的无线驱动程序。linux-drivers 目前未包含在 Fedora 中；你必须下载驱动程序。源码包可以从 linux-wlan 网站 www.linux-wlan.org 获取。目前的包是 linux-wlan-ng。你需要按照上一章中关于源码软件包的说明对驱动程序进行解包和编译。

驱动程序将安装 WLAN 设备，设备配置位于 `/etc/sysconfig/network-scripts` 目录下。例如，第一个 WLAN 设备的配置将位于 `ifcfg-wlan0` 脚本中。通用选项位于 `/etc/wlan.conf` 文件中。

## 设置你的防火墙：system-config-securitylevel

要设置防火墙，请在系统中运行 `system-config-securitylevel`（系统管理窗口和菜单中的安全级别）。在 1.8 版本中，你可以使用启用和禁用按钮来开启防火墙（见图 5-5）。你可以在直接连接互联网的独立系统上运行防火墙，也可以在连接局域网到互联网的网关交换机上运行。大多数小型网络现在使用专用路由器访问互联网，这些路由器带有自己的防火墙。system-securitylevel 的 1.7 版本还包含一个启用和禁用 SELinux 的面板（也可以通过 system-config-selinux 完成）。其他防火墙端口没有单独的面板。

### 第一部分：入门指南

图 5-5

system-config-

security-level 工具，

版本号 1.8。

![](img/af27012edddcf42a8b40fad81183c10b_171_0.png)

自定义规则（Custom Rules）面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 `system-config-security-level`。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level`。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

自定义规则面板允许你加载包含自定义防火墙规则的 IP-tables 文件。与其选择使用 `system-config-security-level` 还是在 IP-tables 文件中创建整套规则，你可以使用 system-config-security-level。

### 第一部分：入门指南

Linux 系统还可以为本地网络运行邮件服务器和打印服务器，以及 Web 和 FTP 服务。此类服务设计旨在与任何 DNS 或防火墙服务配合工作，而不仅仅是 Linux 版本。你可以使用 Linux 设置打印机服务器，而让你的专用路由器来处理防火墙和 DNS 服务。

下表列出了本地网络中常用的网络服务：

| 服务名称 | 服务程序 |
| --- | --- |
| 域名系统服务 (DNS) (第 36 章) | named |
| 网络连接 (第 37 章) | network |
| 防火墙 ( (第 20 章) | iptables |
| Squid 代理服务 (第 24 章) | squid |
| Samba Windows 网络客户端 (第 39 章) | smb |
| Apache Web 服务器 (第 23 章) | httpd |
