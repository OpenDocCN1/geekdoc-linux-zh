

# 使用标准 CHAP 认证链接到 ISP，因为这将要求
# ISP 机器向你的机器进行自我认证（而它通常无法做到）。
#+chap

# 不要同意使用 CHAP 进行认证。
#-chap

# 禁用 Van Jacobson 风格的 IP 头压缩协商
#（使用默认值，即不压缩）。
#-vj

# 增加调试级别（等同于 -d）。如果提供此选项，
# pppd 将以可读形式记录所有发送或接收的控制报文的
# 内容。这些报文通过 syslog 记录，设施为 daemon，
# 级别为 debug。通过适当设置 /etc/syslog.conf，
# 可以将此信息重定向到一个文件中（参见
# syslog.conf(5)）。（如果 pppd 在编译时启用了
# 额外调试功能，它将使用 facility local2 而不是
# daemon 来记录消息）。
#.debug

# 为了认证目的，将域名 <d> 附加到本地主机名。
# 例如，如果 gethostname() 返回
# 名称 porsche，但完全限定域名是
# porsche.Quotron.COM，你将使用 domain 选项将
# 域名设置为 Quotron.COM。
#.domain <d>

# 启用内核级 PPP 驱动中的调试代码。参数
# n 是以下数值的总和：1 用于启用
# 通用调试消息，2 用于请求打印
# 接收报文的内容，4 用于请求打印
# 发送报文的内容。
#.kdebug n

# 将 MTU [最大传输单元] 值设置为 <n>。除非对等方
# 通过 MRU 协商请求较小的值，否则 pppd 将请求
# 内核网络代码通过 PPP 网络接口发送不超过 n
# 字节的数据报文。
#.mtu <n>

# 将用于认证目的的本地系统名称设置
# 为 <n>。如果你正在使用 PAP/CHAP，
# 这可能需要设置为你 ISP 的用户名。
#.name <n>

![](img/a3584dae761d2e3abed8bf40d7637389_344_0.png)

# 将使用 PAP 与对等方认证此机器时使用的
# 用户名设置为 <u>。
# 如果你上面使用了 'name'，请勿使用此选项！
#user <u>

# 强制使用主机名作为本地系统的
# 认证名称（覆盖 name 选项）。
#usehostname

# 将用于认证目的的远程系统假定
# 名称设置为 <n>。
#remotename <n>

# 在此系统的 ARP [地址解析协议]
# 表中添加一个条目，包含对等方的 IP 地址和
# 此系统的以太网地址。
#proxyarp

# 使用系统密码数据库来使用
# PAP 认证对等方。
#login

# 如果提供此选项，pppd 将每隔 n 秒
# 向对等方发送一个 LCP echo-request 帧。在 Linux 下，当没有
# 从对等方接收到报文 n 秒时，将发送 echo-request。
# 通常，对等方应通过发送
# echo-reply 来响应 echo-request。此选项可以配合
# lcp-echo-failure
# 选项使用，以检测对等方是否不再连接。
#lcp-echo-interval <n>

# 如果提供此选项，pppd 将假定对等方已死，
# 如果发送了 n 次 LCP echo-requests 而未收到有效的 LCP
# echo-reply。如果发生这种情况，pppd 将终止连接。
# 使用此选项要求 lcp-echo-
# interval 参数具有非零值。此选项可用于
# 使 pppd 在物理连接断开后（例如，
# 调制解调器已挂断）终止连接，特别是在没有硬件调制解调器控制
# 线的情况下。
#lcp-echo-failure <n>

# 将 LCP 重启间隔（重传超时）设置为 <n>
# 秒（默认 3）。
#lcp-restart <n>

# 将 LCP terminate-request 传输的最大次数设置
# 为 <n>（默认 3）。
#lcp-max-terminate <n>

## PPP

# 将 LCP configure-request 传输的最大次数设置
# 为 `<n>`（默认 10）。
# 一些 PPP 服务器启动很慢。如果你不断收到 'serial line looped back' 错误，并且你
# 确定你已经正确登录且 PPP 应该在服务器上
# 启动，你可能需要增加此值。
#lcp-max-configure `<n>`

# 将 LCP configure-NAK 在开始发送 configure-Rejects 之前
# 返回的最大次数设置为 `<n>`（默认 10）。
#lcp-max-failure `<n>`

# 将 IPCP 重启间隔（重传超时）设置为 `<n>`
# 秒（默认 3）。
#ipcp-restart `<n>`

# 将 IPCP terminate-request 传输的最大次数设置
# 为 `<n>`（默认 3）。
#ipcp-max-terminate `<n>`

# 将 IPCP configure-request 传输的最大次数设置
# 为 `<n>`（默认 10）。
#ipcp-max-configure `<n>`

# 将 IPCP configure-NAK 在开始发送 configure-Rejects 之前
# 返回的最大次数设置为 `<n>`（默认 10）。
#ipcp-max-failure `<n>`

# 将 PAP 重启间隔（重传超时）设置为 `<n>`
# 秒（默认 3）。
#pap-restart `<n>`

# 将 PAP authenticate-request 传输的最大次数设置
# 为 `<n>`（默认 10）。
#pap-max-authreq `<n>`

# 将 CHAP 重启间隔（挑战的重传超时）设置为 `<n>`
# 秒（默认 3）。
#chap-restart `<n>`

# 将 CHAP 挑战传输的最大次数设置为 `<n>`
#（默认 10）。
#chap-max-challenge

# 如果提供此选项，pppd 将每隔 `<n>`
# 秒重新挑战对等方。
#chap-interval <n>
# 使用此选项时，pppd 将接受对等方关于我们本地 IP
# 地址的看法，即使本地 IP 地址是在选项中指定的。
#ipcp-accept-local
# 使用此选项时，pppd 将接受对等方关于其（远程）
# IP 地址的看法，即使远程 IP 地址是在
# 选项中指定的。
#ipcp-accept-remote

第三部分

### 我应使用哪些选项？（无 PAP/CHAP）

嗯，像所有事情一样，这取决于具体情况（叹气）。这里指定的选项应该能与大多数服务器配合工作。

然而，如果不起作用，请阅读模板文件（/etc/ppp/ options.tpl）和 pppd 手册页，并与运行你要连接的服务器的那些系统管理员/用户支持人员交流。

你还应注意，这里提供的连接脚本也使用了一些针对 pppd 的命令行选项，以使更改变得更加容易。

```
# /etc/ppp/options (NO PAP/CHAP)
#
# Prevent pppd from forking into the background
# -detach
#
# use the modem control lines
modem
#
# use uucp style locks to ensure exclusive access to the serial
device
lock
#
# use hardware flow control
crcts
#
# create a default route for this connection in the routing table
defaultroute
#
# do NOT set up any 'escaped' control sequences
asyncmap 0
#
# use a maximum transmission packet size of 552 bytes
mtu 552
#
# use a maximum receive packet size of 552 bytes
mru 552
#
#------END OF SAMPLE /etc/ppp/options (no PAP/CHAP)
```

### 如果你的 PPP 服务器使用 PAP（密码认证协议）

如果你连接的服务器要求 PAP 或 CHAP 认证，你需要多做一点工作。

在上述选项文件中，添加以下行：

```
#
#	force pppd to use your ISP user name as your 'host name'
#	during the authentication process
name <your ISP user name>	# you need to edit this line
#
#	If you are running a PPP *server* and need to force PAP or
#	CHAP uncomment the appropriate one of the following lines.
#	Do NOT use these if you are a client connecting to a PPP
#	server (even if it uses PAP or CHAP) as this tells the
#	SERVER to authenticate itself to your machine (which almost
#	certainly can't do - and the link will fail).
#-chap
#+pap
#
#	If you are using ENCRYPTED secrets in the /etc/ppp/pap-secrets
#	file, then uncomment the following line.
#	Note: this is NOT the same as using MS encrypted passwords as
#	can be set up in MS RAS on Windows NT.
#+papcrypt
```

### 使用 MSCHAP

Microsoft Windows NT RAS 可以设置为使用 CHAP（挑战/握手认证协议）的一种变体。在你的 PPP 源码压缩包中，你会发现一个名为 READM E .MSCHAP80 的文件，其中讨论了这一点。

你可以通过启用 pppd 的调试功能来确定服务器是否正在请求使用此协议进行认证。如果服务器正在请求 MS CHAP 认证，你将看到类似以下的行：

```
rcvd [LCP ConfReq id=0x2 <asyncmap 0x0> <auth chap 80> _<magic 0x46a3>]"
```

这里的关键信息是 *auth chap 80*。

