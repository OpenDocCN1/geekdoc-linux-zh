
`ftp://sunsite.nc.edu/pub/Linux/docs/HOWTO <http://sunsite.nc.edu/pub/Linux/docs/HOWTO>`

此外，你通常应该能够通过以下 Linux 文档页面找到本文：

`http://sunsite.nc.edu/LDP/ <http://sunsite.nc.edu/LDP/>`

最后，本文的最新版本也应该多种格式可用：

`ftp://ftp.sn.no.us/user/egilk/ISP-Hookup-HOWTO.txt <http://ftp.sn.no.us/user/egilk/ISP-Hookup-HOWTO.txt>`

`ftp://ftp.sn.no.us/user/egilk/ISP-Hookup-HOWTO.ps.gz <http://ftp.sn.no.us/user/egilk/ISP-Hookup-HOWTO.ps.gz>`

`ftp://ftp.sn.no.us/user/egilk/ISP-Hookup-HOWTO.tar.gz <http://ftp.sn.no.us/user/egilk/ISP-Hookup-HOWTO.tar.gz>`

# 我如何连接到世界其他地方？

## 1.2 反馈

所有的意见、错误报告、额外信息和各种批评都应发送至：`egil@kvaleberg.no <mailto:egil@kvaleberg.no>` `http://home.sn.no/home/egilk/ <http://home.sn.no/home/egilk/>`

## 1.3 免责声明

不对这些文档的内容承担任何责任。请自行风险使用这些概念、示例和其他内容。此外，这是一个早期版本，存在许多不准确和错误的可能性。

本文将描述多种可能的设置之一。在 Linux 世界中，通常有多种方法实现目标。包含替代方案提示的段落用 `ALT:` 标记。请注意，本文文档版权所有 (c)1996 Egil Kvaleberg，并按照以下条款分发：

- Linux HOWTO 文档可以全部或部分复制并分发（无论是物理还是电子格式），只要在所有副本上保留此版权声明即可。允许并鼓励商业重新分发；作者希望获知此类分发。
- 所有包含 Linux HOWTO 文档的翻译、衍生作品或汇总作品必须受本版权声明保护。也就是说，你不能从 HOWTO 产生衍生作品并对其分发施加额外限制。在某些条件下可以授予这些规则的例外；请联系下方的 Linux HOWTO 协调员。
- 如果你有任何问题，请联系 Linux HOWTO 协调员 Greg Hankins，地址如下所示：`gregh@unsite.nc.edu <mailto:gregh@unsite.nc.edu>` 查询电话号码和电子邮箱地址。

## 1.4 版权信息

我们将假设我们已经安装了基本的网络软件模块（例如 Slackware N 系列的核心部分），并且你已经设置了使用哪个串口端口作为 `/dev/modem`。

默认配置通常允许 `root` 用户直接访问 `/dev/modem`。为了直接连接到 ISP 的 Shell 账户并尝试连接序列，你可以使用 `minicom` 程序。它使用起来非常直观。

## 2.1 基本配置

用于联网的机器配置应以 `root` 用户身份进行。在继续后续之前，请确保 `/etc/hosts.deny` 文件包含以下行：

```
ALL: ALL
```

你通常会希望允许自己访问，因此在 `/etc/hosts.allow` 中添加以下行：

```
ALL: LOCAL
```

或者如果你坚持的话：

```
ALL: 127.0.0.1
```

对于以下内容，请注意它是适用于通过 PPP 连接并使用动态 IP 地址的用户。如果你拥有固定连接，将会会有所不同。

为机器连接一个名称是很好的，这个名称是动态 IP 用户完全根据自己的意愿选择的。将该名称放入 `/etc/HOSTNAME`：

```
roderick
```

下一步是在 `/etc/resolv.conf` 中设置域名服务器：

```
search .
nameserver 193.212.1.0
```

域名服务器必须通过数字 IP 地址进行指定，且不同的 ISP 之间会有不同。如果需要，你可以设置最多三个服务器，每个服务器占一行。它们将按照列出的顺序被请求。

如果你想使用 `somemachine` 作为 `somemachine.acme.net` 的缩写，你必须将第一行替换为：

```
search acme.net
```

`/etc/hosts` 也需要最少配置。大多数用户可以使用：

```
127.0.0.1 localhost
0.0.0.0 roderick
```

拥有固定 IP 地址的用户显然会将其 `0.0.0.0` 替换为该地址。
同样，`/etc/networks` 的最小配置为：

```
loopback 127.0.0.0
localnet 0.0.0.0
```

你还应该在 `/etc/mailname` 中设置你的外部邮件域：

```
acme.net
```

ISP 处的用户名和密码必须在 `/etc/ppp/pap-secrets` 中指定

## 我如何连接到世界其他部分？

`dirk` • `PrettySecret`

对于这些使用 CHAP 而不是 PAP 的 ISP，文件名为 `/etc/ppp/chap-secrets`。

最后，在启动 PPP 之前，必须指定连接过程本身的具体细节。这是在 `/etc/ppp/chatscript` 中完成的

```
TIMEOUT 5

" ATZ

OK ATDT12345678

ABORT "NO CARRIER"

ABORT BUSY

ABORT "NO DIALTONE"

ABORT WAITING

TIMEOUT 45

"\CONNECT

TIMEOUT 5

"name": ppp
```

这里的细节需要进行某种微调。第三行的电话号码必须根据需要设置。某些用户可能需要将 `ATZ` 方法字符串替换为适用于所用调制解调器的内容。最后一行指定了期望的提示 `name:`，并且在收到响应时应为 `ppp`。其他系统可能有其他的登录程序。

要实际启动拨号，可以通过执行以下命令启动 PPP 协议：

```
exec ppp connect \
  'chat -v -f /etc/ppp/chatscript' \
  -detach crtscts modem defaultroute \
  user dir \
  /dev/modem 38400
```

我们应该处于在线状态，并一直保持到输入 `Ctrl-C` 杀死程序为止。任何关于连接的消息将附加到系统日志中。要读取它们，请尝试：

```
tail /var/adm/messages
```

只要 PPP 运行，你就可以直接访问互联网，并可以使用 `ftp`、`nctfp`、`login`、`telnet`、`finger` 等程序。所有这些程序应该是网络包的一部分。

关于 PPP 的更多信息可以从这里获得：

```
/usr/lib/ppp/README.linux <file:/usr/lib/ppp/README.linux>
/usr/lib/ppp/README.linux-chat <file:/usr/lib/ppp/README.linux-chat>
```

最后，关于安全的补充说明。你拥有的 `/etc/inetd.conf` 文件将不允许外部访问。对于需要的人，必须在 `/etc/hosts.allow` 中显式允许所有访问。本地流量可以通过以下允许：

```
ALL: LOCAL
```
