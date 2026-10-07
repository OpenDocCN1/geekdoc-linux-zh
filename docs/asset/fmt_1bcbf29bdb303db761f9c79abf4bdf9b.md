
```
echo stream tcp nowait root internal
echo echo udp wait root internal
ftp stream nowait root /usr/sbin/in.ftpd in.ftpd -l -a
telnet stream nowait root /usr/sbin/in.telnetd in.telnetd
imap stream tcp nowait root /usr/sbin/imapd imapd
finger stream tcp nowait nobody /usr/local/sbin/my_safe.fingerd in.fingerd
```

此配置文件仅在针对 TCP 协议的内部服务上运行四个外部服务。在对其运行 `xconv.pl` 之后，我们得到了示例 11.6 所示的 `xinetd.conf` 文件。

### 示例 11.6 转换后的 xinetd.conf

```
service ftp
{
    flags = REUSE
    socket_type = stream
    protocol = tcp
    wait = no
    user = root
    server = /usr/sbin/in.ftpd
    server_args = in.ftpd -l -a
}
service telnet
{
    flags = REUSE
    socket_type = stream
    protocol = tcp
    wait = no
    user = root
    server = /usr/sbin/in.telnetd
    server_args = in.telnetd
}
service imap
{
    flags = REUSE
    socket_type = stream
    protocol = tcp
    wait = no
    user = root
    server = /usr/sbin/imapd
    server_args = imapd
}
service finger
{
    flags = REUSE
    socket_type = stream
    protocol = tcp
    wait = no
    user = nobody
    server = /usr/local/sbin/my_safe.fingerd
    server_args = in.fingerd
}
defaults
{
    flags = REUSE
    socket_type = stream
    protocol = tcp
    wait = no
    user = root
}
```

此配置文件仅在针对 TCP 协议的内部服务上运行四个外部服务。在对其运行 `xconv.pl` 之后，我们得到了示例 11.6 所示的 `xinetd.conf` 文件。

## 第 11 章 安全工具

此配置文件并没有实现我们想要的所有，因此我们将对其进行一些更改。首先，我们只允许 1 个 ftp 连接。其次，我们只允许来自内部主机的 telnet 会话（其地址为 `192.168.1.0/24`）。我们将记录所有的 finger 连接并将它们连接到 `/usr/local/my_safe.fingerd`。由于我们没有在此主机上运行 imap，我们将所有 imap 会话重定向到位于 `192.168.1.10` 的 imap 服务器上。

限制 ftp 连接非常简单。我们将修改 ftp 部分使其像示例 11.7 所示。

### 示例 11.7 定义 ftp

```
service ftp
{
    flags = REUSE
    socket_type = stream
    protocol = tcp
    wait = no
    user = root
    server = /usr/sbin/in.ftpd
    server_args = in.ftpd -l -a
    instances = 1
}
```

控制访问也很简单。我们将修改 telnet 会话以匹配示例 11.8。

### 示例 11.8 为 telnet 定义访问控制

```
service telnet
{
    flags = REUSE
    socket_type = stream
    protocol = tcp
    wait = no
    user = root
    server = /usr/sbin/in.telnetd
    server_args = in.telnetd
    only_from = 192.168.1.0/24
}
```

如果我们想在非工作时间断开来自本地子网主机的连接呢？可以在该部分的末尾（`only_from` 行之后）添加以下行：

```
access_time = 08:00-18:00
```

同样地，你可以通过添加以下规则来永久禁止某些连接：

```
# 这个家伙伙是个麻烦制造者
no_access = 192.168.1.20
```

我们默认会记录日志，但我们将尝试捕获关于 finger 用户的额外信息。示例 11.9 显示了如何操作。

### 示例 11.9 捕获 finger 数据

```
service finger
{
    flags = REUSE NAMEINARGS
    socket_type = stream
    protocol = tcp
    wait = no
    user = nobody
    server = /usr/local/sbin/my_safe.fingerd
    server_args = my_safe.fingerd
    log_on_success = PID HOST USERID
}
```

最后，为了将 imap 用户重定向到正确的地方，我们将进行示例 11.10 所示的更改。

### 示例 11.10 重定向 imap 用户

```
service imap
{
    flags = REUSE NAMEINARGS
    socket_type = stream
    protocol = tcp
    wait = no
    user = root
    redirect = 192.168.1.10 143
}
```

## 如果我遇到了问题怎么办？

如果在安装、设置或使用 Xinetd 时遇到问题，你应该订阅邮件列表并寻求帮助。你可以通过向 `majordomo@synack.net` 发送邮件，正文内容为“subscribe xinetd”来订阅。

## 第 202 页 11 章 安全工具

## 如果要订阅

当问题出现时，请尽量编写一份良好的 bug 报告。要具体，包含所有相关信息，并保持礼貌！记住，回答你问题的人只是在利用自己的时间。如果你不懒于写一段体面的说明来描述你的问题、你已经做了，并表明你至少尝试读过文档，他们会感到厌烦，并可能完全忽略你。

## tcp wrappers

`tcp wrappers` 是一种用于保护由类似守护进程启动的网络服务的访问的安全工具。通过调用 `tcpd` 而不是服务的标准守护进程，可以按主机和按服务来实施访问控制。`tcp wrappers` 可以与 Xinetd 结合使用（有关 Xinetd 的更多信息请参见上上一节），以提供更高水平的安全性。

大多数现代 Linux 发行版默认安装了 `tcp wrappers`。但它们并没有配置为提供任何实际保护。在本节的剩余部分，我们将研究 `tcp wrappers` 以让你的系统（或系统）更加安全。为了做到这一点，我们需要回顾 `inetd` 是如何工作的，然后通过引入 `tcpd` 来修改该系统。

Unix 和 Linux 并不是为主机提供的每个服务运行单独的守护进程，而是运行一个名为 `inetd` 的“超级交换机守护进程”。该守护进程监听许多端口，当它在给定端口上接收到请求时，会启动相应的守护进程来处理该请求。它监听的端口列表以及与端口相关的守护进程在 `/etc/inetd.conf` 中给出，并使用以下语法（提供了语法和示例）：

```
# <service_name> <service_type> <flags> <user> <server_path> <args>
echo stream tcp nowait root internal
```

在例例中，`echo` 服务（TCP 和 UDP 协议栈的内置服务）被定义为 TCP。`inetd` 将在 `/etc/inetd.services` 文件查找 `echo` 的端口号：

```
echo 7/tcp
```

然后，每当在 TCP 端口 7 上接收到 TCP 连接请求时，`inetd` 将把请求交给 TCP 协议栈内置的 echo 服务器。`/etc/inetd.conf` 中列出的每个服务都遵循相同的模型。

通过将 `/etc/inetd.conf` 条目中的 `<server_path>` 部分替换为 `/usr/sbin/tcpd` 来使用 `tcp wrappers`。`telnet` 服务将如下所示通过 `tcp wrappers` 运行：

```
telnet stream tcp nowait /usr/sbin/tcpd in.telnet
```

## tcp wrappers 原理

`tcp wrappers` 将根据其允许和拒绝主机的规则列表对连接客户端的 IP 地址进行检查。首先检查允许的主机规则，然后是拒绝的主机规则。检查在匹配到第一个规则时停止。如果处理了所有规则但连接未被显式允许或拒绝，则将允许连接。

正如你可能从名称猜出的那样，`tcp wrappers` 仅适用于保护基于 TCP的服务。因为 UDP 不创建会话，`tcp wrappers` 不用于控制单个守护进程的启动。如果你想控制对 UDP 访问，应该参考“iptables”部分获取有关如何设置数据包过滤规则的详细信息。

## tcp wrappers 的工作

为了让 `tcp wrappers` 运转起来，我们将查看可能使用其策略的地方，为主机创建一个策略，并转换 `/etc/inetd.conf` 以使用 `tcp wrappers` 实现它。

`tcp wrappers` 是为位于复杂的防火墙后的组主机提供安全的良好解决方案，或者为间歇连接到互联网的单个主机提供保护。在后一种情况下，应该考虑数据包过滤工具以及（或代替）`tcp wrappers`。如果你正在使用 `tcp wrappers` 保护多个主机，请记住你必须在每个主机上对其进行配置和维护。

在我们的示例中，我们将查看一个已经位于防火墙后的单个主机。它是 IS LAN (`192.168.1.0/24`) 的一部分，应该只向 IS LAN (`192.168.1.0/24`) 提供 talk 和 echo 服务。它应该通过 `inetd` 使用 finger。这见示例 11.1。

### 示例 11.1 无 tcp wrappers

```
# inetd.conf
echo stream nowait root
talk stream nowait root
finger stream nowait root
```

此时，真正的工作开始了：你需要让使用 OPIE 的用户运行 `opiepassword` 来生成初始密码。

OPIE 服务端是在执行安装的 `make install` 步骤时生成的。每个用户必须单独添加到 OPIE 数据库中。这是通过 `opiepasswd` 命令完成的，如示例 11.2 所示。

## OPIE

动态密码（OPIE）提供了一个更安全的环境，而无需在主机之间传输加密流量。它基于在贝尔实验室设计的系统，并在海军研究实验室编写。

## 获取和安装 OPIE

OPIE 可以从 `http://www.inner.net` 获取。截至写作时的最新版本是 2.32。下载后，构建 OPIE 是一个三步骤：

```
# ./configure
# make
# make install
```

## 配置 OPIE

安装并配置 OPIE 后，有趣的事情开始了。当你 `telnet` 到 OPIE 机器时，将通过示例 11.3 所示的过程。

### 示例 11.2 使用 opiepassword

```
[pate@cherry sgml]$ opiepassword -n 497 -c
Updating pate:
Reminder - 仅从控制台使用此方法;
切勿从远程使用。如果你在使用 telnet、xterm 或拨号，输入 "C" 现在退出或无密码。
然后运行不带 -c 参数的 opiepassword。
使用 MD5 计算响应。
输入旧口令：
输入新口令：
再次输入新口令：

ID date pate OPIE key is 497 cr1997
PHI CLAY MOOD VOID ELI BIRD
```

### 11.3 使用 OPIE 连接远程主机

```
[pate@cherry sgml]$ telnet 192.168.1.20
Trying 192.168.1.20...
Connected to 192.168.1.20.
Escape character is '^'.
Red Hat Linux release 6.2 (Zoot)
Kernel 2.2.14-5.0 on an i586
patelogin:
login: pate
otp-md5 497 cr1997 ext
```

## 206 第 11 章 安全工具

示例 11.14 续

```
Response: phi clay mood void eli bird
Last login: Fri Sep 1 05:27:20 from crashtestdummy
```

```
[pate@crashtestdummy pate]$
```

由 `otp-md56` 程序生成的实际响应见示例 11.15。

### 示例 11.15 在你的本地主机上使用 otp5

```
[pate@cherry]$$ otp5 497 cr1997
Using the MD5 algorithm to compute response.
Reminder: Don't use opiekey from telnet or dial-in sessions
Enter secret pass phrase:
PHI CLAY MOOD VOID ELI BIRD
[pate@cherry]$
```

此输出中显示的提示非常重要。OPI 不对你的流量进行任何加密，如果你使用 `opiekey`（无论其名称为何），你将向向任何能够看到你所发送的数据包的人泄露你的密码短。事实上，如果我尝试从我的 telnet 会话连接到 `crashtestdummy`，它将失败并报错，提示我不在安全终端上。

## 尾注

- 1. 这组规则并不是你在现实生活中想要使用的，它仅旨在帮助你练习工具的安装。
- 2. 好了，无论如何你都应该订阅邮件列表。现在就去吧。它会在这里等你的。
- 3. `inetd` 有几种替代方案，包括 `Xinetd`，将在本章的“Xinetd”节中讨论。
- 4. 这并不完全正确；`tcp wrappers` 可用于控制基于 UDP 的服务的初始访问。大多数服务要求守护进程在最后一次连接后继续运行短段时间。这意味着只有需要启动守护进程的连接会被记录并接受测试。
- 5. 这不是子网掩码。我正在使用 CIDR 风格表示法来指示 IS 和数据中心 LAN 使用的地址范围。
- 6. `otp-md5` 实际上是 `opiekey` 的另一个名称。使用这种使用 md5 风格加密从密码短语生成响应。

## RFC-1122

网络工作组—互联网工程任务组

意见征求：1122 R. Braden, 编辑

1989年10月

## 互联网主机主机—通信层

### 本备忘录状态

此 RFC 是互联网社区的官方规范。它通过引用、修改、纠正和补充与主机相关的主要的协议标准。本文档的分发不受限制。

### 摘要

这是定义和讨论互联网主机软件要求的的一对 RFC 之一。此 RFC 涵盖了通信协议层：链路层、IP 层和传输层；其同伴的 RFC-1123 涵盖了应用层和支持协议。

## 目录

- 1. 引言
- 1.1 互联网体系
- 1.1.1 互联网主机
- 1.1.2 体系假设
- 1.1.3 互联网协议族
- 1.1.4 嵌入式网关代码
- 1.2 通用考虑
- 1.2.1 持续的互联网演进
- 1.2.2 稳健性原则
- 1.2.3 错误日志
- 1.2.4 配置
- 1.3 阅读本文档
- 1.3.1 结构
- 1.3.2 要求
- 1.3.3 术语
- 1.4 致谢
- 2. 链路层
- 2.1 引言
- 2.2 协议演练
- 2.3 具体问题
- 2.3.1 尾部协议协商
- 2.3.2 地址解析协议—ARP
- 2.3.2.1 ARP 缓存验证
- 2.3.2.2 ARP 数据包队列
- 2.3.3 以太网和 IEEE 802 封装
- 2.4 链路/网络层接口
- 2.5 链路层要求总结
- 3. 网络层协议
- 3.1 引言
- 3.2 协议演练
- 3.2.1 互联网协议—IP
- 3.2.1.1 版本号
- 3.2.1.2 校验和
- 3.2.1.3 寻址
- 3.2.1.4 分段与重组
- 3.2.1.5 标识
- 3.2.1.6 服务类型
- 3.2.1.7 生存时间
- 3.2.1.8 选项
- 3.2.2 互联网控制协议—ICMP
- 3.2.2.1 目的不可达
- 3.2.2.2 重定向
- 3.2.2.3 源洪塞
- 3.2.2.4 超时
- 3.2.2.5 参数问题
- 3.2.2.6 回显请求/响应
- 3.2.2.7 信息请求/响应
- 3.2.2.8 时间戳和时间戳响应
- 3.2.2.9 地址掩码请求/响应
- 3.2.3 互联网组管理协议 IGMP
- 3.3 具体问题
- 3.3.1 出站数据报
- 3.3.1.1 本地/远程决策
- 3.3.1.2 网关选择
- 3.3.1.3 路由缓存
- 3.3.1.4 网关检测
- 3.3.1.5 新网关选择
- 3.3.1.6 初始化
- 3.3.2 重组
- 3.3.3 分段
