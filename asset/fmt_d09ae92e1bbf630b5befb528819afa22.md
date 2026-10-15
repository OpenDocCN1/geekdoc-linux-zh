
# 嗅探器与电子窃听
## 第 7 章

修改为：

`OSNAME= BSD`
`#LIBS= -lkvm -lelf -lnsl -lsocket`

完成这些更改后，保存 `Makefile`，退出文本编辑器并输入 `make`。`ifstatus` 应该就能无问题地构建。

在此示例中，我在本地主机启动了 `linux_sniffer` 并调用了 `ifstatus`。以下是 `ifstatus` 的输出：

`WARNING: LINUX2.SAMSHACKER.NET INTERFACE eth0 IS IN PROMISCUOUS MODE.`

你找不到比这更简单或更清晰的了：

所以，`ifconfig` 和 `ifstatus` 足够检测本地主机上的嗅探器。但如果你有一个大型子网呢？除了逐一检查每台机器外，你需要一个能够检测跨子网嗅探器的工具。专门为此目的设计的工具中，最近的是 `NEPED`。

## NEPED: 网络混杂以太网检测器

`NEPED` 可以检测子网上的嗅探活动。

应用程序：`C`, `IP` 头部
需要：`IP` 头部, `Linux 2.0.x+`, `libc5` 和 `glibc`
配置文件：无

位置：`http://metalab.unc.edu/pub/Linux/distributions/trinux/src/netmap/NEPED.c`

安全历史：`NEPED` 没有重大的安全历史。然而，独立报告表明 `NEPED` 可能会被欺骗。

备注：`NEPED` 仅在 `2.0.36` 之前的 `Linux` 内核上工作。

`NEPED` 会扫描你的子网，寻找处于混杂模式的接口。在 `2.0.36` 之前的 `Linux` 内核中，`NEPED` 利用 `Linux` 实现 `arp.c` 中的缺陷来找出这些接口（你可以在 `http://llr.linux.no/source/ipv4/arp.c` 的 `LXR` 引擎中找到它）。`NEPED` 发送 `arp` 请求并引导嗅探工作站响应。巧妙。

遗憾的是，`NEPED` 有局限性。首先，在后后的内核中，`Linux` 的 `arp` 实现被修复了，因此嗅探工作站将不再响应异常的 `arp` 请求。此外，独立研究员 `Seth M. McGann` 指出你可以配置系统忽略 `arp` 请求，在这种状态下，它将溜过 `NEPED` 扫描。除去这些因素，`NEPED` 仍然是一个非常有用的工具。

# 针对嗅探器的其他通用防御方法

在你的网络上发现嗅探器是最坏的情况；如果它存在那里，你的网络已经已经被攻陷了。但你不需要等到这种情况发生才去反击嗅探攻击。事实上，你可以在建立网络之初就采取一种非常有效的预防措施：采用加密。

加密会话极大地降低了你的风险。与其担心数据被嗅探，你只需将其扰乱到无法识别的。这种方法的优点是显而易见的：即使攻击者嗅探了数据，对他来说也是没用的。然而，这种方法也有缺点。

你的用户可能会抵抗使用加密。他们可能觉得这太麻烦了。例如，让用户每次登录服务器时使用 `SKey`（或其他一次性密码系统）是很的。你可能需要找到一个折中方案：既支持强双向加密又提供某种用户友好性的应用程序。更多信息，请查阅第 10 章“传输中的数据保护”。

## 延伸阅读

以下在线文档提供了更多信息。

- `Sniffers and You`, `Dave Dittrich`, 盛顿大学。此文档是重大攻击后的建议。除了逐一检查每台机器外，你需要一个能够检测跨子网嗅探器的工具。专门为此目的设计的工具中，最近的是 `NEPED`。`http://weber.edu/misc/`
- `Sniffers and Security`, `Christopher Klaus`. 此文档提供了关于嗅探器的概述。
- `Privacy and Security`, `Dave Dittrich`, 盛顿大学。此文档是重大攻击后的建议。除了逐一检查每台机器外，你需要一个能够检测跨子网嗅探器的工具。专门为此目的设计的工具中，最近的是 `NEPED`。`http://zdnet.com/`
- `Sniffers and Security`, `Sun Microsystems SunOS 5.5 (Solaris 2.5)`. 此文档提供了对嗅探器的罕见视角。`http://sunmic.com/`
- `Sniffers and You`, `Dave Dittrich`, 盛顿大学。此文档是重大攻击后的建议。除了逐一检查每台机器外，你需要一个能够检测跨子网嗅探器的工具。专门为此目的设计的工具中，最近的是 `NEPED`。`http://weber.edu/`
- `Password Report`, `Widman, M.D.`, 德克萨斯大学医疗中心，圣安东尼奥。此文档提供了关于嗅探器的威胁。`security/`
- `Password Report`, `Internet Systems`. 此文档提供了关于嗅探器的通用介绍。`security/`
- `Gobbler: An Sniffer`, `Tirza Rijn and Jan Oorscholt`, 代尔夫特理工大学，工程学院。此文档描述了 `Gobbler` 的设计和测试。`computercraft.com/`
- `Gobbler: An Sniffer`, `Tirza Rijn and Jan Oorscholt`, 代尔夫特理工大学，工程学院。此文档描述了 `Gobbler` 的设计和测试。`computercraft.com/progs/gobbler.zip`.

## 扫描器剖析

系统扫描器会扫描你的本地主机，寻找明显的（以及不明显的）安全漏洞。这些漏洞通常源于疏忽、小瑕疵以及配置问题，即使是老手有时也会漏掉这些问题。示例包括：

- 疏松或错误的文件权限
- 默认账户
- 错误或重复的 `UID` 条目

为了更好地理解系统扫描器如何工作，请使用“计算机神谕与密码系统”（`COPS`）运行接下来的示例。

## COPS—计算机神谕与密码系统

应用：`COPS` 由 `Dan Farmer` 开发（另参 `SATAN`）
需要：`C`, `Perl`（版本 `3.44+`）以及 `cracklib`

配置文件：`is_able.1`（用于指定需要检查可写权限的文件和目录）和 `crc_1`（用于指定你想要维护 `CRC` 值的文件和目录）。

位置：`http://metalab.unc.edu/pub/linux/system/security/cops_104_linux.tgz`
安全历史：`COPS` 没有显著的安全历史。
备注：`COPS` 是一个较旧但仍然非常有用的工具。

`COPS` 会分析你的系统，寻找 `UNIX` 系统中仍然存在（或可能出现）的常见配置问题、缺陷和警告，包括：

- 无效或错误的文件、目录和设备权限
- 弱密码
- 密码和组文件安全设置应用不当
- 文件上的 `SUID/SGID` 位不当
- 文件校验和的疑疑更改

`COPS` 还会将现有文件日期与 `CERT` 安全公告的已知日期进行对比。（这非常有用，因为 `COPS` 可以识别出本应该打补丁但未被修复的文件。）

## 解包、制作、安装和运行旧版 COPS

下载 `COPS` 后，解压缩压缩包，如下：

```
$ gunzip cops_104_linux.tgz
```

接下来，解压 `COPS` 的 `tar` 归包，如下：

```
$ tar -xvf cops_104_linux.tar
```

![](img/238ef1f85709de12ba67e71734ee1e37_248_0.png)

## Linux 网络安全
### 第三部分

`COPS` 将扩展到 `cops_104/`。将你的工作目录更改到 `cops_104/` (`cd cops_104/`) 并运行 `reconfig` 脚本，如下：

```
$ ./reconfig
```

最后，运行 `make`：

```
$ make
```

> 注意
> 你不应该在 `make` 上遇到任何问题。但是，你必须安装 `cracklib`。如果没有安装，`COPS` 将在编译期间崩溃，并在 `src/pass.c` 处因错误退出。（你可以在 `Linux` 刻录光盘中找到 `cracklib`。）

现在你准备好测试该程序了。最快的方法是执行此命令：

```
$ ./cops -v -s -b cops.err
```

（注意：需要句号）。

发生的情况取决于主机的配置。分析可能只需要几秒钟，也可能需要几分钟。当 `COPS` 完成分析时，它会将结果写入一个以你的主机命名的目录下的一个命日日期文件中。例如，对于以下示例扫描，`COPS` 将结果写入 `GNSS/1999_May_24` 和 `linux2/1999_May_24`。

以下是对 `SGI IRIX 6.2`（一个可能存在多个漏洞的旧操作系统）进行 `COPS` 扫描的结果：

注意：
安全报告，时间 1999年5月24日 星期一 07:05:22 PDT
来自主机 GNSS

```
****.root.chk****

****dev.chk****

警告！NFS 文件系统导出时没有任何限制！

警告！NFS 文件系统导出时没有任何限制！

警告！NFS 文件系统 / 导出时没有任何限制！

警告！NFS 文件系统 /home/jsfs31 导出时没有任何限制！

警告！NFS 文件系统 / 导出时没有任何限制！

警告！NFS 文件系统 /usr/local 导出时没有任何限制！

****is_able.chk****

警告！/.ptriv 是可写的！
```
