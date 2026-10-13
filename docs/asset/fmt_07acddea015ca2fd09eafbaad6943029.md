
在此示例中，第一个 IP 地址分配给主机计算机，而第二个 IP 地址将分配给远程用户。有关配置 Linux 下 PPP 的详细信息，请阅读 ppp 手册页或 `/usr/share/doc/pppd/` 目录下的文档。如果你是 Linux 开发者，请浏览 `/usr/src/linux/drivers/network` 下的 `ppp_async.c`、`ppp_deflate.c`、`ppp_generic.c` 和 `ppp_synctty.c` 文件。

# 相关 Red Hat 和 Linux 命令

以下是用于 Red Hat Linux 中管理 Internet 连接的一些最实用命令：

- `internet-druid`：Red Hat 图形化 Internet 连接向导的命令行名称（也是 `redhat-config-network` 客户端的符号链接）。
- `mgetty`：一种高级的串口监控工具，支持在 Linux 下进行数据和调制解调器操作。
- `neat`：Red Hat 图形化网络配置工具的命令行名称。
- `redhat-config-network`：Red Hat 图形化网络配置工具的命令行名称。
- `redhat-control-network`：Red Hat 图形化网络设备控制工具的命令行名称。

## 参考

- http://www.tldp.org/HOWTO/Modem-HOWTO.html—Linux 调调器 HOWTO 提供了丰富的信息：第 8 节涉及定位你的调调器；第 17 节提供了故障排除建议。
- http://www.roaringpenguin.com/ppoe/—强大的 rab-ppoe 软件包页面，让 DSL 用户能够使用 Linux 连接互联网。这是 Red Hat Linux 和 DSL 用户的“必选”软件包。
- http://www.redhat.com/support/resources/web_ftp/ppp.html—与 Red Hat Linux 使用 PPP 的确定性链接。
- http://www.redhat.com/support/resources/tips/Dialup-Tips/Dialup-Tips.html—如何使用 Red Hat 拨号连接到 ISP。
- http://www.redhat.com/support/resources/tips/Dialup-Tips/ppp_server_tips.html—如何使用 Red Hat Linux 和 `mgetty+sendfix` 软件包设置拨拨入服务器。
- http://axion.physics.ubc.ca/ppp-linux.html—W.G. Unruh 的详尽网页，描述了如何使用 PPP 和 Linux 连接到 ISP。
- http://www.tldp.org/HOWTO/PPP-HOWTO—开始学习 PPP 和 Linux 的绝佳之地包含了配置各种客户端、链接局域网和设置 PPP 服务器的指导。
- http://www.tldp.org/DSL-HOWTO—关于 DSL 和 Linux 的最新信息，包含 DSL 硬件、设置网络、使用 USB 模块、DSL 使用和安全以及其他有用提示。强烈推荐任何考虑 DSL 服务的 Red Hat 用户阅读。
- http://www.knowledge.org/ppp.html—5 分钟 Linux PPP HOWTO。一份关于手动设置 PPP 的简明指南。
- http://www.tldp.org/FAQ-Linux/index.html—Linux 常见问题解答。第 8.8.9 节“我如何让拨号 PPP 工作？”非常用。第 27 节有对常见通用问题的回答。
- http://www.tldp.org/Serial-HOWTO.html—串口 HOWTO 涵盖了调调器所使用的串口的所有方面。
- http://www.tld.org/HOWTO/PCMCIA-HOWTO.html—Linux PCMCIA HOWTO 涵盖了笔记本电脑使用的 PCMCIA 调调器。
- http://www.tld.org/HOWTO/PPP-HOWTO/index.html—Linux PPP HOWTO 是 PPP 的权威参考。
- http://www.tld.org/FAQ/PPP-FAQ.html—FAQ 补充了 HOWTO 并详细探讨了调调器的故障排除。
- http://www.maximumhoyot.com/cabal/killerppp.html—幽默风格的 PPP 教程的第一部分，侧重于配置。
- http://www.maximumhoyot.com/cabal/killerpart2.html—教程的第二部分，侧重于故障排除。
- http://www.walbran.org/sean/linux/linmodem-howto.html—Linmodem HOWTO 帮助处理软件调调器。
- http://www.idir.net/-gromitkc/winmodem.html—大量的软件调调器信息集。
- http://www.pcquest.com/content/linux/handson/102082101.asp—Winmodems 与 Linux：软件调调器概述。

## 安装 Apache 服务器

### 安装 Apache 服务器 505

服务器构建时间：2002年9月4日 17:20:34
服务器模块编号：20020628:0

架构：32位
服务器编译自：....

输出将显示版本号、构建日期和时间、平台以及在构建期间使用的各种选项。Red Hat Linux 包含了 Apache 2.0.40 版本。

你可以通过 RPM 包安装 Apache，也可以从源代码自行进行编译。Apache 源代码可以在任何类 Unix 操作系统和 Win32 系统上进行编译。

如果你正准备安装新版本的 Apache，关闭旧服务器可能是一个好主意。尽管旧服务器不太可能干扰安装过程，但关闭它可以确保不会出现任何问题。如果你不知道如何停止 Apache，请参阅本章后文的“启动和停止 Apache”部分。

### 从 RPM 安装

你可以在 Red Hat 安装介质、Red Hat FTP 服务器或其许多镜像站点之一找到 Apache RPM。你应该尽可能地检查 `updates.redhat.com` FTP 站点（或其中一个镜像），以便在更新发布时及时下载。在与你的 Red Hat 版本对应的目录中，你偶尔会发现 Apache 的更新。更新后的 RPM 文件通常包含修复漏洞或安全漏洞的重要更新。当新版本发布时，请尽快安装以确保安全。

> 注意
> 请检查 Red Hat 的错误说明/更正页面（errata page）以获取 Apache 的漏洞和安全修复，或使用 Red Hat 的邮件公告列表以保持最新状态。访问 http://www.redhat.com/apps/support/errata/index.html 获取更新链接。在 http://www.redhat.com/mailing-lists/ 订阅支持列表（例如 `linux-security`）。

> 如果你想获得最新的、实验性的 Apache 版本进行测试，请检查 Red Hat Rawhide 发行版，该版本也可以在 Red Hat FTP 服务器（`ftp://ftp.redhat.com/pub/redhat/rawhide/`）上找到。该发行版是实验性的，始终包含所有 RPM 的最新版本。但请注意，Apache 包 (`httpd`) 可能依赖 Rawhide 发行版中其他 RPM 的新功能。因此，你可能需要从 Rawhide 安装许多新的 RPM。如果你想使用 Rawhide 发行版的 Apache 版本进行测试，更好的选项可能是下载源代码 (`SRPM`)。这样，你就可以避免对其他新包的依赖。（请参考第 8 章“管理软件和系统资源”中的“处理源 RPM 文件”，以获取有关从 RPM 文件构建和安装包的信息）。

![](img/446debe023486a07fde575245cf7a3ff_540_0.png)

#### 警告

你应该警惕安装实验性软件包，且绝不要在*生产*服务器（即在“现实生活中”使用的服务器）上安装。请先在未连接网络的主机上非常地测试这些软件包！

获取 Apache RPM 后，你可以通过命令行 `rpm` 工具并输入以下命令进行安装：

```
rpm -Uvh latest_apache.rpm
```
