
# 第三部分 选择和安装 Linux 发行版

## 获取 iptables 脚本

与其手动输入所有的防火墙规则，互联网上有很多可用脚本（基于 GPL 许可），你可以根据自己的需求对其进行修改。在这些脚本的开头部分，你可以添加 IP 地址、端口号以及其他特定于你防火墙设置的其他信息。

一组展示了如何使用 iptables 的优秀脚本源自 iptables 教程的作者 Oskar Andreasson。你可以在 http://iptables-tutorial.frozentux.net/scripts/ 找到这些脚本。其中，`rc.firewall.txt` 是一个非常适合逐步学习的文件。

## 了解更多关于 iptables 的信息

到为止，你已经了解了 iptables的功能概述并对它的作用有了基本的理解。创建复杂的防火墙需要更深入 iptables 知识。我建议从这里开始，会有很多人尝试破解，这需要更丰富的知识。请参考以下内容：

- iptables 教程 (http://iptables-tutorial.frozentux.net) —— 这份由 Oskar Andreasson 编写的教程是衡量其他 iptables 信息的标准。
- filter 项目 (www.netfilter.org) —— 获取关于 iptables 开发、补丁、安全问题、邮件列表和新闻的最新信息。
- LinuxGuru (www.linuxguruz.com/iptables) —— 该网站提供了丰富的 iptables 常见问题解答、脚本、聊天室、HOWTO、教程、工具、安全网站和邮件列表的链接。

## 制作一个 Coyote Linux 启动软盘防火墙

仅需一张 1.4MB 的磁盘，你就能拥有一个可以很好保护你的局域网免受互联网意外访问的防火墙。通过光驱（CD），你实际上可以添加数百种工具来管理你的防火墙并保持网络顺畅运行。

现在有许多可启动的 Linux 发版。本章的其余部分将引导你完成 Coyote Linux (www.coyelinux.com) 的设置，并描述其他你可能感兴趣的发行版。

> 注意：这里将 Coyote Linux 描述为实用的 Linux 系统可以多小的演示。如果你愿意，甚至可以从 CD (http://rzero.com/coyote/bootcd.html) 使用 Coyote Linux。然而，如果你计划用于防火墙的电脑带有光驱，请考虑使用功能更丰富、更及新的防火墙发行版，例如 Devil Linux (www.devil-linux.com)。

## 创建 Coyote Linux 防火墙

通过一个简单简单的脚本，Coyote Linux 让你能够创建一个可以放在软盘上的启动 Linux 防火墙。当你安装并启动 Coyote Linux 时，可以从局域网内的另一台电脑上管理它。你可以使用 Web 界面或通过 `ssh` 登录并在 Linux shell 中管理 Coyote Linux。

对于对于如此狭小的空间来说，Coyote Linux 包含了一系列令人惊叹的功能。启动你创建的 Coyote Linux 启动软盘后，你将获得一个可以执行以下操作防火墙：

- 在局域网和互联网之间路由数据包。
- 为以太网局域网（TCP 或 PPPoE）或拨号（PPP）网络连接提供网络接口。
- 创建 iptables 支持的防火墙规则。（它从几条基本规则开始，但你可以添加自己的规则，包括 IP 伪装和 NAT、端口转发、透明代理或许多其他 iptables 功能）
- 启用 DHCP 让 Linux 充当 DHCP 服务器，为局域网内的计算机提供 IP 地址和其他信息。
- 记录活动。除了创建防火墙上的活动日志外，还可以设置 Coyote 将这些日志传递到局域网内的另一台电脑。
- 监控网络活动。Coyote Linux 中有几个基础管理工具可以检查你的网络状态。这些工具包括 `traceroute` 和 `nslookup`。
- 远程登录 (`ssh`) 并绕过 shell。Coyote Linux 中的 `ssh` 守护允许你从局域网内的另一台电脑登录。`busybox` 实用 (www.busybox.net/) 提供了一组很好的基础 shell 工具。
- 打开 Coyote Linux 的 Web 界面。从局域网内的任何 Web 浏览器，你都可以通过输入 IP 地址和端口 8180 来打开 Coyote Linux Web 管理界面（例如，http://192.168.0.1:8180）。

下一节将展示如何创建一个 Coyote Linux 启动软盘防火墙/路由器。一旦 Coyote Linux 防火墙运行，你可以从局域网内的另一台电脑上通过 Web 浏览器或 shell (`SSH`) 连接到该电脑来更改防火墙设置。如果你熟悉 shell 和防火墙功能（在本章前面描述的内容），那么许多诸如路由、按需拨号和使用 DHCP 服务器等操作都可以这个小小的发行版完成。

> 注意：更多信息请参考 Vortech Consulting, LLC 的网站 (www.vortech.net)，该机构创建了 Coyote Linux 项目。像许多支持开源软件的公司一样，它也提供了与其开源项目相关的商业产品。如果你需要更高级的产品和支持，可以考虑购买其企业和小型办公防火墙产品。

## 构建 Coyote Linux 软盘

为了在你的 Coyote 防火墙软盘中获得你想要的内容，你需要自己构建它。这涉及以下步骤：

- **创建软盘** —— 你需要一台带有软盘驱动器的电脑，向其写入原始数据。该机器应该运行 Linux（如果你还没有安装 Linux，使用 `KNOPPIX` 效果会很好）。
- **运行软盘** —— 为此，你需要一台可以从软盘启动并具有两个网络接口的电脑。这台电脑性能可以低到是一台废弃的 486 机器。在示例中，防火墙电脑将有一个拨号调制调器用于连接互联网，以及一个以太网卡用于连接局域网。在你的 Coyote 防火墙软盘中获得你想要的内容，你需要自己构建它。这涉及以下步骤：

- **创建软盘** —— 你需要一台带有软盘驱动器的电脑，向其写入原始数据。该机器应该运行 Linux（如果你还没有安装 Linux，使用 `KNOPPIX` 效果会很好）。
- **运行软盘** —— 为此，你需要一台可以从软盘启动并具有两个网络接口的电脑。这台电脑性能可以低到是一台废弃的 486 机器。在示例中，防火墙电脑将有一个拨号调制调器用于连接互联网，以及一个以太网卡用于连接局域网。

在运行创建软盘的程序之前，你需要知道以太网卡的 Linux 驱动名称。如果可能，最好使用宽带或其他以太网接口连接互联网，因为拨号调制调器需要额外的配置，提供的连接较慢，并且让你一直保持连接。本节旨在说明如何使用极简硬件使用 Linux。图 18-2 显示了你创建的防火墙配置示例。

要创建一个 Linux 防火墙，请遵循以下步骤：

- 1. 在一台带有光驱和软盘驱动器的电脑上，将书中附带的 Coyote 目录复制到电脑硬盘上。然后打开终端窗口（或其他 shell）并切换到该目录。（Coyote 在 CD 中的位置参见附录 A。）
- 2. 输入以下命令解压并提取 Coyote Linux 文件：

```bash
tar xvfz coyote*tar.gz
```

- 3. 进入刚创建的 `coyote` 目录并启动 `makefloppy.sh` 批脚本构建 Coyote Linux 软盘，如下：

```
@ cd coyote
@ ./makefloppy.sh
Coyote 软盘构建脚本 v2.9

请选择创建的软盘所需的容量：

1) 1.4MB（最安全可靠但可能缺少某些选项所需的空间）

2) 1.68MB（可靠性且有额外空间）——推荐

3) 1.72MB（最大空间可能在所有系统或所有软盘上有效）
```
