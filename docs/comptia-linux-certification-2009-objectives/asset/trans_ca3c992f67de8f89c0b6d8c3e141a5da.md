

## 活动 14-6

### 实现安全审计

**开始之前：**
1. 在 *srvA* 上，你已在 CLI 中以 root 身份登录。
2. 显示第一个 CLI 终端。
3. 输入 `cd /root` 以导航到根目录。
4. 输入 `clear` 以清屏。

**场景：**
你需要在网络上实施安全审计。你决定将 iptables 防火墙丢弃的数据包输出到日志文件中，以便对其进行审查，查看是否存在潜在的入侵尝试。

| 你做什么 | 你如何操作 |
| :--- | :--- |
| 1. 设置 iptables 将可能的入侵发送到日志文件。 | a. 输入 `iptables -N LOG_DROP` 以创建名为 LOG_DROP 的链。<br><br>b. 输入 `iptables -A LOG_DROP -j LOG --log-tcp-options --log-level 3 --log-ip-options --log-prefix "[Dropped Packet] :"` 以在 LOG_DROP 链中添加一条新规则。<br><br>c. 输入 `iptables -L` 以查看规则。<br><br>d. 观察 LOG_DROP 链的规则列表中列出了 LOG 规则。<br><br>e. 输入 `iptables -A LOG_DROP -j DROP` 以在 LOG_DROP 链中添加一条新规则。<br><br>f. 输入 `iptables -L` 以查看规则。<br><br>g. 观察 LOG_DROP 链的规则列表中列出了 DROP 规则。<br><br>h. 输入 `service iptables save` 以保存 iptables 规则。 |

i. 输入 **vi /etc/syslog.conf** 以打开 syslog.conf 文件。

j. 按 **Shift+G** 前往文件末尾。

k. 按 **O** 切换到插入模式并移至新行。

l. 输入 `#Log iptables results to iptables log` 以指定关于将 iptables 结果重定向到日志文件的描述。

m. 输入 `kern.3`，然后按 **Tab** 键，接着输入 `/var/log/iptables` 以将结果重定向到日志文件。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_726_0.png)

n. 按 **Esc** 并输入 `:wq` 以保存并关闭文件。

o. 输入 `touch /var/log/iptables` 以创建 /var/log/iptables 文件。

p. 输入 `service syslog restart` 以重启 syslog 服务。

## 主题 E

### 检测入侵

你已实施安全审计。为了保护包含机密数据的文件，你需要持续监控网络。在本主题中，你将实施一个入侵检测系统。

如果你的网络连接到公共网络，入侵者可能会追踪网络上的数据包并滥用系统中的服务。作为 Linux+ 管理员，你需要在网络上实施一项服务，以监控传入和传出的数据包，并如果任何文件或服务被破坏或篡改则发送警报。

### 网络监控实用工具

![](img/477ccb2f05b6ba1b2d563ea74f18c197_727_0.png)

有各种实用工具可用于监控网络设备及其连接的系统。

| 工具 | 用于 |
| :------ | :------ |
| nmap | 扫描整个网络的各种端口及其上运行的服务及其状态。nmap 实用工具也可以使用 nmapfe 命令作为 GUI 前端运行。此实用工具主要用于监控远程网络连接。nmap 实用工具有许多选项。这些选项有助于用户获取有关网络的特定信息。nmap 实用工具的语法为 `nmap [scan type] [options] [target specification]`。 |
| tcpdump | 从发送到网络接口的查询字符串中获取数据包信息。如果数据包头部与查询中的表达式匹配，则数据包将返回给用户。tcpdump 实用工具的语法为 `tcpdump [option] [expression]`。 |
| wireshark | 获取数据包信息。它是一个基于 GUI 的实用工具。运行 wireshark 命令时，将显示 Wireshark 网络分析器工具。其功能与 tcpdump 实用工具相似。 |

### 入侵检测系统

**定义：**
*入侵检测系统 (IDS)* 是一种保护门户、网络和文件免受黑客攻击的安全传感器。IDS 监控系统文件、日志文件和通过网络传输的数据包。它还检查网络数据流以查找未授权的签名和攻击。IDS 软件还可以分析数据并向管理员发出潜在安全问题的警报。IDS 可以包含各种硬件传感器、入侵检测软件和 IDS 管理软件。每种实现都是独特的，具体取决于安全需求和所选组件。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_728_0.png)

**示例：Snort**
Snort 是一种监控网络上每个数据包的 IDS。如果检测到可疑数据包，它会将警报传递给 syslog 文件。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_728_1.png)

*图 14-17：IDS 保护网络免受黑客攻击。*

### 被动式和主动式 IDS

IDS 可以是被动式的或主动式的。*被动式 IDS* 检测潜在的安全漏洞，记录活动，并提醒安全人员。*主动式 IDS* 同样执行这些操作，然后采取适当措施阻止用户进行可疑活动。有些人认为主动式 IDS 是一种入侵预防系统，而不是独立的预防系统。

### Tripwire

**定义：**
*Tripwire* 是一种入侵检测工具，它将文件或目录的内容与包含该文件或目录位置及修改日期的数据库进行比较。它还监控文件的属性，例如二进制签名、大小或预期大小变化。如果文件已更改，则 Tripwire 工具会通过电子邮件向管理员发出警报。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_728_2.png)

示例：

![](img/477ccb2f05b6ba1b2d563ea74f18c197_729_0.png)

*图 14-18：Tripwire 通过比较文件内容并监控其属性来检测入侵。*

### Tripwire 数据库

*Tripwire 数据库* 包含基线，即在特定时间记录的文件和目录的快照。当使用变得异常时，通过将最新文件和目录与早期快照进行比较，可以轻松检测问题。安装并配置 Tripwire 后，应初始化数据库。要初始化 Tripwire 数据库，请执行以下命令：`/usr/sbin/tripwire --init`。在初始化数据库期间，Tripwire 根据策略文件中提到的特定规范创建一组文件系统对象。初始化数据库后，应执行完整性检查。要查看整个数据库，请输入命令 `/usr/sbin/twprint -md --print-dbfile | less`。

### tw.cfg 文件

tw.cfg 文件是 Tripwire 配置文件。在生成 tw.cfg 文件之前，你可以修改 tw.cfg.txt 文件中的配置选项以满足你的需求。下表列出了部分配置选项。

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| POLFILE | 修改策略文件 tw.pol 的位置。 |
| DBFILE | 修改数据库文件 [hostname].twd 的位置。 |
| REPORTFILE | 修改报告文件 [hostname].[date].twr 的位置。 |
| SITEKEYFILE | 修改站点密钥文件的位置。 |
| LOCALKEYFILE | 修改本地密钥文件的位置。 |
| EDITOR | 指定当数据库更新时由 Tripwire 调用的编辑器。 |
| MAILPROGRAM | 指定由 Tripwire 使用的邮件程序。 |
| MAILMETHOD | 指定由 Tripwire 使用的邮件协议。 |

如果 Tripwire 文件位置未在 tw.cfg.txt 文件中正确指定，则无法创建 tw.cfg 文件。

### Snort

**定义：**
Snort 是一种监控网络流量的网络 IDS。Snort 监控网络上的每个数据包。如果检测到可疑数据包，它会将警报传递给 syslog 文件，并通过电子邮件或弹出窗口通知管理员。它检测各种网络攻击方法，包括 CGI 攻击、拒绝服务、缓冲区溢出和 SMB 探测。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_730_0.png)

示例：

![](img/477ccb2f05b6ba1b2d563ea74f18c197_730_1.png)

#### Snort 选项

下表列出了 snort 命令的一些常用选项。

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-v` | 以详细模式运行 Snort。 |
| `-i interface` | 监听特定接口上的数据包。 |
| `-l directory` | 指定输出日志目录。 |
| `-n number of packets` | 指定退出前要处理的数据包数量。 |
| `-D` | 以守护进程模式运行 Snort，并在 /var/log/snort/alert 目录中记录所有消息。 |

