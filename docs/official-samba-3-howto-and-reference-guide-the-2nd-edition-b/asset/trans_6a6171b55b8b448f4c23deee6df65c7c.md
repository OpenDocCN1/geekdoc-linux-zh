
## 分析和解决 Samba 问题

有大量信息来源，包括邮件列表、RFC（请求评论）和文档。Samba 发行版附带的文档对通用 SMB 主题（如浏览功能）提供了很好的解释。

### 38.1 诊断工具

在使用 SMB 网络时，某些问题的原因往往并不显而易见。Samba 本身提供了相当有用的信息，但在某些情况下，你可能不得不退回使用抓包工具（sniffer）。抓包工具是一种在局域网（LAN）上监听、分析并显示屏幕数据的程序。

#### 38.1.1 使用 Samba 自身进行调试

用于调试问题的最佳诊断工具之一是 Samba 本身。你可以使用 `smbd` 和 `nmbd` 的 `-d` 选项来指定运行时的调试级别。有关调试选项的更多信息，请参阅 `smbd`、`nmbd` 和 `smb.conf` 的手册页。调试级别（日志级别）可以从 1（默认值）到 10（用于调试密码时为 100）不等。

另一种有用的调试方法是使用 gcc `-g` 标志编译 Samba。这将在二进制文件中包含调试信息，并允许你将 gdb 附加到正在运行的 smbd/nmbd 进程。要将 gdb 附加到 NT 工作站的 smbd 过程，首先需要让工作站建立连接。按下 ctrl-alt-delete 并导航到域框就足够了（至少在你第一次加入域时），这将生成一个 LsaEnumTrustedDomains。此后，工作站会保持连接打开状态，并且会有一个正在运行的 smbd 进程（假设你未设置 `--real-smbd idle-timeout`）。因此，在按下 ctrl-alt-delete 和实际输入密码之间，你可以附加 gdb 并继续执行。

一些值得研究的有用的 Samba 命令包括：

```
$ tetharn 1 more
$ smbclient -L ///(服务器 netbios 名称)
```

#### 38.1.2 Tcpdump

Tcpdump 是第一个支持 SMB 的 UNIX 抓包工具。它是一个命令行实用工具，现在其 SMB 支持功能比 **ethereal** 和 **tethereal** 稍显落后。

#### 38.1.3 Ethereal

Ethereal 是一种图形化抓包工具，适用于 UNIX（Gtk）和 Windows 平台。Ethereal 对 SMB 的支持相当好。有关 **ethereal** 使用方法的详细信息，请阅读编写精良的 Ethereal 用户指南。

![](img/86d74c6cc862465e3a42e6dc3c90935a_647_0.png)

监听端口 137、138、139 和 445 上的数据。例如，使用过滤器 `port 137`、`port 138`、`port 139` 或 `port 445`，如图 38.1 的快照所示。

Ethereal 也有一个控制台版本，称为 tethereal。

# 图 38.2 Ethereal 主数据窗口。

![](img/86d74c6cc862465e3a42e6dc3c90935a_648_0.png)

#### 38.1.4 Windows 网络监视器

为了在 Microsoft Windows NT 上跟踪事务，可以使用网络监视器（又称 Netmon），它随附在 Microsoft 开发网络（MSDN）光盘、Windows NT 服务器安装光盘以及 SMS 光盘中。随 SMS 提供的 Netmon 版本允许在任意两台计算机之间转储数据包（即将网络接口设置为混杂模式）。NT 服务器安装光盘上的版本仅允许监控指向本地 NT 主机的网络流量以及本地子网上的广播流量。请注意，Ethereal 可以读取和写入 Netmon 格式的文件。

##### 38.1.4.1 在 NT 工作站上安装网络监视器

在 NT 工作站上安装 Netmon 需要几个步骤。以下是关于安装随附 Microsoft Windows NT Server 4.0 的 Netmon V4.00.349 到 Microsoft Windows NT Workstation 4.0 的说明。对于 Netmon 的其他 Windows NT 版本，过程应该类似。你需要同时具备 Microsoft Windows NT Server 4.0 安装光盘和工作站 4.0 安装光盘。

首先，你需要在 NT 服务器上安装网络监视器工具（Network Monitor Tools）和代理（Agent），具体步骤如下：

- 进入 **开始** -> 设置 -> 控制面板 -> 网络 -> 服务 -> 添加。
- 选择 **网络监视器工具和代理（Network Monitor Tools and Agent）** 并点击 **确定**。
- 在网络控制面板上点击 **确定**。
- 当系统提示时，插入 Windows NT Server 4.0 安装光盘。

此时，Netmon 文件应存在于 `%SYSTEMROOT%\System32\netmon\*.*` 中。还有两个子目录存在：`parsers`，其中包含解析 Netmon 数据包转储所需的 DLL；以及 `captures`。

要在 NT 工作站上安装 Netmon 工具，首先需要从工作站安装光盘安装网络监视器代理（Network Monitor Agent）。

- 进入 **开始 -> 设置 -> 控制面板 -> 网络 -> 服务 -> 添加**。
- 选择 **网络监视器代理（Network Monitor Agent）**，点击 **确定**。
- 在网络控制面板中点击 **确定**。
- 当系统提示时，插入 Windows NT Workstation 4.0 安装光盘。

现在，将 NT 服务器上 `%SYSTEMROOT%\System32\netmon` 中的文件复制到工作站上的 `%SYSTEMROOT%\System32\netmon`，并根据你的站点情况设置适当的权限。你将在 NT 主机上运行 Netmon 时需要管理员权限。

##### 38.1.4.2 在 Windows 9x/Me 上安装网络监视器

要在 Windows 9x/Me 上安装 Netmon，请从 Windows 9x/Me 光盘（`<admin\nettools\netmon>`）安装网络监视器代理。光盘中的 Netmon 驱动文件附带一个 readme 文件，如果你需要了解如何操作，可以参考该文件。请从一个正常工作的 Netmon 安装中复制文件。

### 38.2 有用的网址

- 查看 Scott Merrill 如何在 `http://www.skippy.net/linux/smb-howto.html` 上模拟 BDC 行为。
- 旧版 SMB 规范的 FTP 站点：`ftp://ftp.microsoft.com/developr/drg/CIFS/`

### 38.3 获取邮件列表帮助

有一些与 Samba 相关的邮件列表。前往 `<http://samba.org>`，点击最近的镜像站，然后点击 **支持（Support）**。接下来，点击 **Samba 相关邮件列表（Samba-related mailing lists）**。

对于涉及 Samba TNG 的问题，请前往 <http://www.samba-tng.org/>。已被要求不要将关于 Samba-TNG 的问题发布到主流 Samba 列表中。

如果你确实要向某个列表发布消息，请遵守以下准则：

- 永远记住开发人员是志愿者；他们不收取费用，也从不保证在特定时间开发特定功能。任何时间表都只是“最佳猜测”，仅此而已。
- 始终提及你使用的 Samba 版本以及其运行的操作系统。你应该列出 smb.conf 文件的相关部分，至少是 [global] 部分中影响 PDC 支持的选项。
- 除了版本外，如果你通过 CVS 获取了 Samba，请提及你最后一次检出的日期。
- 尽量让你的问题清晰且简短。许多冗长、复杂的问题在完全阅读之前就被删除了！不要发布 HTML 编码的消息。邮件列表上的大多数人会直接删除这些消息。
- 如果你设置了那些巧妙的“我在度假”自动回复功能，请确保其配置为不回复邮件列表流量。邮件列表的自动回复真的会让那些不得不处理这种糟糕网络礼仪行为的成千上万人感到恼火。
- 不要交叉发布。确定最适合发布的列表，看看会发生什么。不要同时向 samba-ntdom 和 samba-technical 发布消息。许多在列表中活跃的人订阅了一个以上的列表，看到同一条消息两次或更多次时会感到恼火。通常，如果某人认为消息在另一个列表中处理得更好，他们会为你转发该消息。
- 你可能需要包含在日志级别设置为 20 或更低时编写的部分日志文件。请不要发送整个日志，只需提供足够的上下文来解释错误消息即可。
- 如果你有一个完整的 Netmon 跟踪记录（从管道打开到错误），你也可以发送 \*.CAP 文件。
- 在附件文件中添加文档前请仔细考虑。考虑将相关部分粘贴到消息正文中。Samba 邮件列表发送人数众多。难道每个人都需要一份你 smb.conf 的副本放在他们的附件目录中吗？

### 38.4 如何退订邮件列表

要从 Samba 邮件列表中移除你的名字，请前往你订阅它的那个地方，即 http://lists.samba.org，点击最近的镜像站，点击 支持（Support），然后点击 Samba 相关邮件列表。

请不要向列表发布请求移除的消息。你只会被告之上述地址（除非该过程以某种方式失败了）。

![](img/86d74c6cc862465e3a42e6dc3c90935a_650_0.png)

