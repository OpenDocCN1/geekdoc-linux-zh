
输出的第一列（紧邻远程主机名称之前）包含“tally code”字符，该字符表示关联主机的状态，该状态是时钟选择过程的结果。* 表示服务器是当前时间源，系统时间与其进行比较；+ 表示主机是时钟合并算法的候选；- 表示主机被聚类算法丢弃。您可以在 ntpq 文档（/usr/share/doc/packages/xntp-doc/html/ntpq.html）中了解有关不同 tally codes 的更多信息。

### NOTE
为了提供容错能力，时间服务器通常与多个远程服务器一起运行。NTP 使用一组算法分别细化每个对等体的數據，并从多个来源选择和合并数据。首先，使用时钟选择过程创建“short list”时间源，该过程检查其合理性并为每个源计算置信度。通常，该集合的成员原则上可以提供正确的时间；然而，由于各种误差贡献，并非所有都能提供最准确和稳定的时间。此时调用的聚类算法的工作是选择幸存者中最好的子集，使其在组合系综平均值中的方差最小，与子集中每个成员单独的方差相比。您可以在 RFC 1305（http://www.ietf.org/rfc/rfc1305.txt）中找到有关 NTP 使用的各种算法的详细讨论，例如时钟选择、聚类确定和时钟合并程序。

以下内容总结了其余列的含义：

- **remote** 显示远程机器的主机名或 IP。（如果使用 `-n` 开关运行 `ntpq`，则会显示 IP 地址而不是 DNS 名称。）
- **refid** 标识远程机器同步到的时间源。如果显示 IP 地址或主机名，则该服务器正在与另一台 NTP 服务器同步。在前面的示例中，它显示 `tick.nrc.ca` 正在与 GPS 时钟同步。

### NOTE
在远程主机的层级（stratum）被识别之前（即不是 16），refid 列会显示一个称为 kiss code 的四字符字符串，以便帮助调试情况。一些常见的 kiss codes 是 INIT（即主机尚未首次同步）、AUTH（服务器身份验证失败并等待重试）和 DENY（远程主机拒绝访问）。您可以在 /usr/share/doc/packages/xntp-doc/html/debug.html 中找到 kiss codes 的详细列表。

- `st` 显示远程机器的层级。层级为 16 表示“未同步”，或无法确定状态。层级值为 0 最佳，但您永远不会在 `ntpq` 中看到它显示。

### NOTE
在 NTP 世界中，stratum 级别定义了与参考时钟的距离。stratum-0 时间源具有参考时钟，例如无线电时钟或其自身的铯钟。stratum-0 服务器不能在网络上使用。相反，它们直接连接到计算机，然后这些计算机作为 stratum-1 服务器运行。stratum-1 时间服务器的基本定义是它直接链接（不是通过网络路径）到可靠的 UTC 时间源（stratum-0 服务器）。反过来，stratum-1 时间服务器充当主要网络时间标准。

本质上，时间服务器距离 stratum-1 服务器越远，分配给该时间服务器的 stratum 级别越高。随着您通过不同层级进展，会涉及网络成本（传输延迟），这会降低 NTP 服务器相对于 UTC 的准确性。stratum-1 时间服务器通常与 UTC 相差不到一毫秒。在互联网上，由于网络延迟，stratum-2 时间服务器可能与 UTC 相差 10–100 ms，每个后续时间服务器将增加额外的 10–100 ms 的不准确性。对于大多数应用程序，从 stratum-2 服务器获取时间已经足够。

- `t` 显示使用的通信方法类型：`u` = unicast，`m` = multicast，`l` = local，`-` = unknown。
- `when` 显示自上次轮询远程机器以来经过的秒数。
- `poll` 给出轮询间隔（以秒为单位）。
- `reach` 显示八进制的“reachability register”，位从最低有效位（最右侧）开始进入。如果该寄存器中至少有一位设置为 1，则认为对等体可达。
- `delay` 显示与远程通信的时间延迟（以毫秒为单位）。
- `offset` 显示本地时间与远程时间之间的偏移量（以毫秒为单位）。

这是一个“rotating”寄存器，意味着它跟踪最后八次轮询请求。例如，十进制值 276（二进制模式 10110110）表示在最后八次轮询中，有两次（包括最近一次轮询尝试）未收到远程机器的响应。

- jitter 给出系统时钟与远程之间的观察到的时间误差（以毫秒为单位），作为 RMS（root mean square）时间差的平均值。（在 pre-NTPv4 中，此列称为 dispersion。）

NTP 发行版中包含的另一个方便的故障排除工具是 ntptrace。它确定给定的 NTP 服务器从何处获取时间，并跟随 NTP 服务器链一直追溯到其主时间源。如果不带参数运行 ntptrace，它将从 localhost 开始。以下是 ntptrace 输出的示例：

```
Athena:/home/admin # ntptrace
localhost: stratum 16, offset 0.000000, synch distance 0.000000
time.nrc.ca: stratum 2, offset 0.002815, synch distance 0.03061
toc.nrc.ca: stratum 1, offset 0.002153, synch distance 0.00156,
~refid 'PPS'
```

每行输出中的字段（从左到右）为：

- Host name
- Host stratum
- Time offset between that host and the local host as measured by ntptrace—this is why it is not always zero for localhost
- Host synchronization distance and (only for stratum-1 servers) the reference clock ID

所有时间均以秒为单位。

有关其他故障排除和调试提示，例如为 ntpd 启用调试和详细输出，请参阅 NTP 发行版的 HTML 文档，尤其是 /usr/share/doc/packages/xntp-doc/html/debug.html。

## Email Services
如果您熟悉 SunOS 或 BSD 等任何一种 Unix 发行版，您就会知道 Sendmail（http://www.sendmail.org/），多年来它是 Unix 平台的事实上的电子邮件应用程序。Sendmail 已移植到许多非 Unix 操作系统，包括 OpenVMS、Windows 和 Macintosh OS X。然而，这并不意味着 Sendmail 是理想的软件，因为它相当复杂，正确实现和配置都很困难。它依赖于在文本配置文件中调用的晦涩语法，这些文件通过宏处理器运行。它还与 Unix 惯例和标准紧密相连，需要在两者方面拥有大量的知识基础。

### TIP
如果您计划处理 Sendmail，您需要确保您有一个用于安装和配置服务器的良好资源。O'Reilly & Associates 出版的 sendmail 书籍（ISBN 1-56592-222-0），由 Sendmail 开发者 Eric Allman 合著，被认为是该主题的权威指南。

SLES 9 附带了多个邮件服务器，其中包括 Sendmail 和 Postfix。由 IBM Thomas J. Watson 研究中心（纽约州约克敦高地）的 Dr. Wietse Venema 开发，Postfix 试图成为 Sendmail 的快速、易于管理和安全的替代品。SLES 9 默认安装 Postfix，即使对于基本系统配置也是如此。因此，本节的讨论是关于 Postfix 的。

### NOTE
Linux/Unix 社区中另外两个备受喜爱的电子邮件服务器软件包（通常称为 Message Transfer Agents 或 MTAs）是 Qmail（http://www.qmail.org）和 Exim（http://www.exim.org）。然而，它们不随 SLES 提供。

### WARNING
Postfix 软件包与 Sendmail 和 Exim 的软件包冲突。因此，如果已安装 Postfix，则必须先卸载它，然后才能安装 Sendmail 或 Exim。（如果您例如通过 YaST 安装 Sendmail，依赖项检查会警告您冲突并允许您指定解决操作。）

Postfix 的一大优点是它可以快速轻松地设置，而不会牺牲安全性。以下步骤引导您进行 Postfix 快速入门：

- 1. 如果尚未安装，请安装 Postfix 软件包（使用 YaST 或 rpm）。您可以在 SLES CD1 上找到它，或从 http://www.postfix.org 下载最新版本。

### NOTE
如果您从源代码 tarball 安装 Postfix，您应该注意 INSTALL 文件和许多 readme 文件（在 README 文件目录中）使用退格字符来模拟粗体文本。根据您的终端设置，您可能会看到类似 Postfix 的文本，等等。如果您在文本
