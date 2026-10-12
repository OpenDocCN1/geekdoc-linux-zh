
在这种情况下，基于控制台的红帽防火墙工具比 `redhat-config-securitylevel-tui` 更灵活。你可以使用 `redhat-config-securitylevel-tui` 命令启动此控制台工具。这将打开图 17.6 中的菜单。

图 17.6

灵活的 `redhat-config-securitylevel-tui` 工具。

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_542_0.png)

`redhat-config-securitylevel-tui` 工具是 `lokkit` 的继者。目前，`lokkit` 处于静态状态，但红帽正在将启动其所有工具的命令更改为 `redhat-config-*` 格式。

如你所见，你可以启用（Enable）或禁用（Disable）防火墙。对于本次练习，请启用防火墙并选择自定义（Customize）。你将被带到图 17.7 中的“防火墙配置 - 自定义”菜单，在其中你可以允许与 GUI 工具相同的标准服务相同的入站数据。你还可以启用其他端口的访问，例如安全 HTTP 服务。

在图中，我启用了通过 Samba 连接所需的端口的通信。你可以在图 17.8 中看到结果，这是 `iptables -L` 命令的输出。有关大多数 TCP/IP 端口号的更多信息，请参阅 `/etc/services` 文件。该列表并非 100% 完整；官方列表保留在 www.iana.org/assignments/port-numbers 中。

## 图 17.7

自定义防火墙

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_543_0.png)

## 图 17.8

防火墙规则列表

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_543_1.png)

## 重建防火墙

如果你对防火墙进行了更改并犯了错，可以重新开始。如果你直接通过命令行界面重启 `iptables` 来做出更改，可以恢复原始的防火墙服务：

```
# service iptables restart
```

如果你使用红帽工具之一更改了防火墙，可以将你的原始防火墙设置还原到 `/etc/sysconfig/iptables`。然后你可以重启 `iptables` 服务。

## 设置 IP 伪装（IP Masquerading）

IP 伪装允许你隐藏局域网（LAN）上计算机的 IP 地址。它将这些 IP 地址替换为网关计算机上的公共 IP 地址。这有助于保护局域网内的计算机免受直接攻击。

注意：IP 伪装是网络地址转换（NAT）的一种。实现 NAT 的另一种方法是使用代理服务器。

IP 伪装和防火墙通常在与局域网相同的同一台计算机上配置，最常见的是该局域网与外部网络（如互联网）之间的网关。因此，`iptables` 的开发者包含了使用该命令来配置伪装的选项。

自然地，局域网的网关计算机充当在网络之间路由消息的设备。为了使之工作，你需要按照第 16 章所述启用 IP 转发（IP Forwarding）。

你无法使用红帽防火墙工具配置伪装。一旦设置好，你就想要存储该命令。

## 功能

正如第 16 章所述，局域网的网关计算机充当在网络之间路由消息的设备。为了使之工作，你需要启用 IP 转发（IP Forwarding）。

你无法使用红帽防火墙工具配置伪装。一旦设置好，你就想要存储该命令。

`Tripwire` 是检查文件完整性的一个重要工具。在编写时，该软件既有开源版本也有商业版本。遗憾的是，开源版本未包含在 Red Hat Enterprise Linux（红帽企业 Linux）的安装 RPM 中。你可以在 www.tripwire.org 下载阅读文档；商业版本作为 Psionic Technologies (www.psionic.com) 提供的 TripSentry 套件的一部分可用。

`Tripwire` 设计用于检查系统上配置文件的完整性。为了让该工具生效，你应该尽快安装它；在破解者破入并修改了系统上的关键文件后，它无法检测到这些意外更改。

注意 `Tripwire` 未包含在 Red Hat Enterprise Linux 中，且不受 Red Hat 的支持。

由于 Red Hat Enterprise Linux 中未包含 `Tripwire`，你需要从其他来源安装它。我是从 Red Hat Linux 9 RPM 包安装的。Fedora 核心版也有相同的基础包，因此我怀疑它未来可能会被包含在 Red Hat Enterprise 中。

一旦安装了 `Tripwire`，你就需要对其进行设置并创建数据库。然后，`Tripwire` RPM 附带的 cron 任务就可以每天检查你的文件（奇怪的是，该 cron 任务的名为 `tripwire-check`）。

# 设置 TRIPWIRE

使用 `Tripwire` 非常简单。只需运行安装脚本 `/etc/tripwire/twinstall.sh` 即可。该脚本是文本格式；你甚至可以使用文本编辑器修改安装文件的位置。它包含了 `Tripwire` 许可副本，即 GPL。

当你运行默认脚本时，系统会提示你添加本地和站点密码口令（passphrases）。在设置过程中，`twinstall.sh` 脚本会在 `/etc/tripwire` 目录下创建一个配置和策略文件。

接下来，使用 `tripwire --init` 命令初始化 `Tripwire` 数据库。如果你使用其策略文件 `twpol.db` 构建初始数据库，该命令可能需要几分钟时间。在搜索可能未安装的文件时，可能会列出一些错误。

你可以通过编辑 `/etc/tripwire/twpol.txt` 来更新 `Tripwire` 策略。例如，如果你没有安装 "Z" 壳，你可以删除对 `/bin/z` 的引用。一旦完成更改，你可以使用以下命令更新 `Tripwire` 策略：

```
# tripwire --update-policy /etc/tripwire/twpol.txt
```

一旦安装，`Tripwire` 是防御你系统的重要工具。破解者可能会尝试通过更改各种 `tripwire` 文件来隐藏踪迹。你可以使用一些安全或只读介质来防止这一点；例如，某些管理员会将 `Tripwire` 文件写入只读 CD 中。

# TRIPWIRE 的实际运行

假设你已经安装了 `Tripwire`，数据库每天都会被检查。事实上，`/etc/cron.daily` 目录下有一个 `tripwire-check` 脚本。正如第 13 节所述，该脚本通过 `/etc/crontab` 默认在每天早上 4:02 运行。

你可能想编辑此文件以保存输出；例如，你可以将 `tripwire` 命令的输出重定向到日志文件：

```
/usr/sbin/tripwire --check >> /var/log/tripwire
```

产生的输出很有意思。为了本书的内容，我在运行 `tripwire-check` 脚本之前临时更改了 `/sbin/halt` 文件的名称。在 `/var/log/tripwire` 中，这导致了大量的输出，包括以下行：

```
Rule Name: User binaries (/sbin)
Security Level: 66
```

Added:

"/sbin/halt.bak"

Modified:

"/sbin"

```
Rule Name: System Administration Programs(/sbin/halt)
Security Level: 100
```

Removed:

"/sbin/halt"
