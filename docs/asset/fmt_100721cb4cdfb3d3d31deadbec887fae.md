
按下回车后，你将看到如图 13.10 所示的对话框。使用 `Tab` 键导航到启用或禁用防火墙。你还可以自定义防火墙设置，允许特定协议通过端口，并在安装了多个网卡时指定一个以太网接口作为防火墙。注意，你也可以在 X 会话期间运行 `gnome-lokkit` 客户端使用 lokkit 的图形界面版本。

**图 13.10** Red Hat 的 lokkit 命令为 Linux 在内存中快速生成防火墙规则。

使用 `redhat-config-securitylevel` 是实现简单包过滤规则集的快速简方法，其过滤规则用于接受或拒绝流经主机以太网或指定设备（如 `eth0` 或 `ppp0`）的 TCP 和 UDP 数据包。规则是动态创建的并使用 `iptables` 立即在内存中实现。

从系统设置菜单中的“安全级别”菜单启动 `redhat-config-securitylevel`。系统会提示你输入 root 密码，然后会出现客户端窗口。图 13.11 显示了 `eth0` 以太网设备已启用防火墙，允许入站的安全 shell 和 HTTP 请求。

**图 13.11** Red Hat 的 `redhat-config-securitylevel` 客户端也可用于为 Linux 快速生成并实施标准或简单的自定义防火墙规则。

### Fedora 与防火墙

Fedora 还支持较旧但仍在使用的 `ipchains` 包过滤软件，我们用它在 Linux 防火墙、网关、服务器和工作站上构建有效的防火墙规则。Linux 还支持功能更强大的 `iptables` NetFilter 系统，它为构建规则集或过滤指令提供了额外的控制和日志功能。

遗憾的是，Fedora 没有包含任何命令行或图形界面供你构建、保存和测试以 shell 脚本实现的复杂 `iptables` 规则集。如果你想控制出站和入站数据包，就需要这样做。不过，你可以使用 `vi` 等文本编辑器编写自己的规则。许多经验丰富的 Linux 用户会针对网络环境中的特定应用（如路由规则开发）手动调优规则集。

有关使用 `iptables` 用于各种防火墙系统的概述和细节，请阅读 Robert L. Ziegler 的经典著作《Linux Firewalls, Second Edition》（New Riders 出）。你也可以访问他的网站 `http://linux.firewall-tools.com/linux/firewall/index.html`，该网站提供了一个基于 Web 的图形化防火墙设计构建工具，你可以用它快速构建基于 `ipchains` 的自定义规则集。

你可以使用 Fedora 创建自定义防火墙，通过使用 `ipchains` 或 `iptables` 可能支持 IP 伪装（也称为 NAT）。在 `/usr/share/doc/rp-pppoe/configs` 目录下你会找到三个示例脚本，它们用于使用数字用户线路（DSL）连接互联网时。

### 密码与物理安全

通向更好安全的下一步是保护网络上的密码并确保用户良好地使用，尤其是 root 密码。如果仅某一台机器的 root 密码被破解，整个网络都会陷入麻烦。为了获得一定的物理安全性，你可以强制要求 LILO 或 GRUB 引导加载程序使用密码，移除软盘和 CD-ROM 驱等可移动设备，或为 Fedora 配置网络启动服务器。这种方法在本文时尚未得到良好支持或记录；你可以在 Brieuc Jehomme 的《Network Book and Exotic Route HOWTO》中了解如何操作，该书地址为 `http://www.tldp.org/HOWTO/Network-book/`。你可以在第 24 章“内核与模块管理”中阅读关于 GRUB 和 LILO 的内容。

此外，请记住，研究显示 90% 的网络入侵是现任或前任员工造成的。如果某人不再需要访问网络，请立即锁定访问。良好的安全策略还规定对与账户相关的数据进行备份。在确保密码安全后，检查你的服务使用。虽然 NFS 可能很有帮助，但通过网络共享整个文件系统是不安全的。某些存在漏洞的服务包括 Web 服务、`telnet`、`FTP`（尤其是匿名 FTP）以及登录、`rcp` 等远程服务。

### 保护你的网络

最后，注意物理安全。如果潜在攻击者可以获得系统的物理访问权限，获取完全访问将轻而易举。将所有服务器锁在房间内，并确保只有授权人员访问客户端。

### 保护 TCP/IP

要让 TCP/IP 更安全并没有很难做，这是标准。只需确保用户无法访问他不应访问的网络部分，遵循良好的子网实践。使用 `nmap` 等工具扫描网络中的漏洞端口。许多网络管理员（在许可的情况下）会从家里 PC 尝试破解业务网络以测试安全性，这并不是坏主意。

### 配置与使用 Tripwire

Tripwire 是一种安全工具，它可以检查系统二进制文件的完整性并通过 `syslog` 或电子邮件报告任何更改。Tripwire 是确保二进制文件未被木马程序替换的良好工具。木马是无意中安装的与分发程序文件名相同的恶意程序，它们会对被入侵的系统造成破坏。Fedora 不包含免费版的 Tripwire，但可以使用它可以监控系统。要首次设置 Tripwire，请访问 `http://www.tripwire.org`，然后下载并安装开源版本。安装后，以 root 身份运行位于 `/etc/tripwire` 下的 `twinstall.sh` 脚本：

```
# /etc/tripwire/twinstall.sh
```

Tripwire 位和本地密码用于签名多种文件，例如配置、策略和数据库文件。

密码应至少为 8 个字符，并包含字母和数字。

更多信息请参阅 Tripwire 手册。

正在创建密钥...

（在选择密码时，请记住良好的密码通常包含大小写字母、数字和标点符号，且至少为 8 个字符。）

输入站点密钥文件密码：

# 第 13 章 网络连接

随后，你需要输入一个至少八个字符的密码（最好是一串随机乱码，例如 `5fwkc4ln`），至少输入两次。脚本将为你的系统（主机）生成密钥，然后要求你输入一个密码（两次）供本地使用。你会被要求再次输入新密码。按照提示操作后，（相当详细的）默认配置和策略文件（`tw.cfg` 和 `tw.pol`）将被加密。然后，你应该备份并删除由 Fedora RPM 软件包安装的原始文本文件。

要初始化 Tripwire，请像下面一样使用其 `--init` 选项：

```
# tripwire --init

Please enter your local passphrase:

Parsing policy file: /etc/tripwire/tw.pol

Generating the database...

*** Processing Unix File System ***
```

已写入数据库文件: `/var/lib/tripwire/shuttle2.twd`
数据库生成成功。

请注意，所有输出都显示在这里。在 Tripwire 创建其数据库（你的文件系统的快照）后，它将使用此基线以及 `/etc/tripwire` 目录下的加密配置和策略来监控系统的状态。然后你应该使用所需的选项在完整性检查模式下启动 Tripwire。（详情请参阅 tripwire 手册。）例如，你可以让 Tripwire 在命令行中检查你的系统并生成报告，如下：

```
# tripwire -m c
```

这里不显示输出，但在本示例中将显示一个报告。输出可以重定向到文件，但报告将保存为 `/var/lib/tripwire/report/hostname-YYYYMMDD.twr`（换句话说，使用你的主机名、年、月、日、时、分、秒）。可以使用 `tripprint` 工具读取此报告，如下：

```
# tripprint-report -r | \
/var/lib/tripwire/report/shuttle2-20020919-181049.twr | less
```
