
`chargen`           `19/tcp`            `ttytst` source

`chargen`           `19/udp`            `ttyst` source

`ftp-data`          `20/tcp`

`ftp-data`          `20/udp`

# 21 is registered to ftp, but also used by fsp

`ftp`               `21/tcp`

`ftp`               `21/udp`            `fsp` `fspd`

`ssh`               `22/tcp`            # SSH Remote Login Protocol

`ssh`               `22/udp`            # SSH Remote Login Protocol

`telnet`            `23/tcp`

`telnet`            `23/udp`

# 24 - private mail system

`smtp`             `25/tcp`            mail

在注释行之后，你将看到三列信息。左列包含每个服务的名称。中间列定义了该服务的端口和协议类型。最右侧的字段包含该服务的可选别名或别名列表。

例如，检查文件片段中的最后条目。它描述了 `SMTP`（简单邮件传输协议）服务，该服务用于在互联网上投送电子邮件。中间列包含文本 `25/tcp`，它告诉我们 `SMTP` 使用 `25` 端口，并使用传输控制协议（TCP）作为其协议。

端口号到底是什么？它是为特定的网络服务预留的唯一数字。它允许网络连接被正确路由到处理该服务的软件。例如，当电子邮件从其他计算机投递到你的 Linux 机器时，远程系统必须首先与你的系统建立网络连接。你的计算机接收连接请求，对其进行检查，并标记为端口 `25`，因此知道该连接应该交由处理电子邮件的程序（恰好是 `sendmail`）。

我提到过 `SMTP` 使用 `TCP` 协议。某些服务使用 `UDP`（用户数据报协议）。你真正需要了解 `TCP` 和 `UDP`（出于本次安全讨论的目的）的是，它们提供了通过网络连接发送信息的不同封装方式。`TCP` 连接提供了错误检测和丢失数据的重传。`UDP` 则不检查数据是否完整且无损地到达；它旨在作为一种发送非关键信息的快速方法。

## 禁用网络服务

尽管在你的 Fedora 或 Red Hat Enterprise Linux 系统上可能有数百种服务（列在 `/etc/services` 中）可用并可能易受到攻击，但现实中只有几十个被安装，且其中极少数是默认开启的。大多数网络服务是由 `xinetd` 服务或 `/etc/init.d` 目录下的启动脚本启动的。

`xinetd` 是一个在大量网络端口上监听的守护进程。当连接到特定端口号时，`xinetd` 会自动启动该服务的相应程序并处理该连接。`xinetd` 守护进程通过提供功能改进了其前身 `inetd`，包括更灵活的访问控制、日志设置和拒绝服务保护。

配置文件 `/etc/xinetd.conf` 为 `xinetd` 服务器提供了默认设置。`/etc/xinetd.d` 目录包含告知 `xinetd` 在哪些端口上监听以及启动哪些程序的文件。每个文件包含单个服务的配置信息，且该文件名通常以其配置的服务名命名。例如，要启用 `rsync` 服务，请编辑 `/etc/xinetd.d` 目录下的 `rsync` 文件，并寻找类似下面的部分：

```
service rsync

{

    disable = yes

    socket_type = stream

    wait = no

    user = root

    server = /usr/bin/rsync

    server_args = --daemon

    log_on_failure += USERID

}
```

此示例的第一行将服务标识为 `rsync`。这与 `/etc/services` 文件中列出的服务名称完全匹配，导致该服务在 TCP 和 UDP 协议的端口 `873` 上监听。你可以看到该服务默认是启用的（`disable = yes`）。要启用 `rsync`，将该行改为：

`disable = no.`

> 提示：如果你的机器是 FTP 服务器，`rsync` 服务是一个很好的开启的服务。它允许人们使用 `rsync` 客户端（包含校验和搜索算法）从你的服务器下载文件。有了该功能，用户可以重启中断的下载，而无需从头开始。

虽然 `AES` 算法也会受到暴力破解攻击，但破解它所需的计算能力比破解 `DES` 算法要高得多。

关于 `AES` 的更多信息，包括该算法的命令行实现，您可以访问 http://aescript.sourceforge.net/。

## 公钥加密

公钥加密不受密钥分发问题的困扰，这就是为什么它是安全互联网通信的首选加密方法。这种方法使用两个密钥：一个用于加密消息，另一个用于解密消息。用于加密消息的密钥称为公钥，因为它是所有人可见的。用于解密消息的密钥是私钥，它是被隐藏的。整个过程的工作原理如下：

假设你想使用公钥加密向我发送一条安全消息。我们需要：

- 1. 我必须拥有一对公钥和私钥。根据具体情况，我可能自己生成密钥（使用特殊软件），也可以从密钥机构获取密钥。
- 2. 你想向我发送一条消息，所以你首先查找我的公钥（更准确地说，是查找你查找公钥的软件）。
- 3. 你用公钥对消息进行加密。此时，消息只能用私钥解密（公钥不能用于解密消息）。
- 4. 我收到消息并使用我的私钥对其进行解密。

## 安全套层 (SSL)

公钥加密的一种经典实现是安全套层 (`SSL`) 通信。这项技术让你能够安全地向在线商家提交你的信用卡信息。`SSL` 加密会话的元素如下：

启用 `SSL` 的 Web 浏览器（Firefox、Mozilla、Internet Explorer、Opera、Konquerer 等）
- 启用 `SSL` 的 Web 服务器（Apache）
- `SSL` 证书

要启动 `SSL` 会话，Web 浏览器首先连接到端口 `443` 的 Web 服务器，也称为 `HTTPS`（安全超文本传输协议）。在两台机器之间建立套接连接后，会发生以下情况：

- 1. 服务器向浏览器发送其 `SSL` 证书。
- 2. 浏览器通过 `SSL` 证书验证服务器的身份。
- 3. 浏览器生成一个对称加密密钥。
- 4. 浏览器使用 `SSL` 证书加密该对称密钥。
- 5. 浏览器将加密后的密钥发送给服务器。
- 6. 服务器用与其 `SSL` 证书对应的私钥解密对称密钥。
- 7. 浏览器和服务器现在可以基于对对称密钥的共同认知对流量进行加密和解密。

现在可以进行安全的数据交换了。

## 创建 SSL 证书

为了进行安全的 HTTP 数据交换，你必须拥有一个支持 `SSL` 的 Web 服务器。来自 Fedora 和 RHEL 的 Apache Web 服务器（`httpd` 软件包）是支持 的。以下是为你为 Apache Web 服务器创建自己的 `SSL` 证书时需要的一些文件：

- `/etc/httpd/conf/httpd.conf` — Web 服务器配置文件
- `/etc/pki/tls/` — 证书构建脚本
- `/etc/httpd/conf/ssl.conf` — 主 Web 服务器 SSL 配置文件

现在你已经熟悉了基本组件，请看一眼用于创建 `SSL` 证书的工具：

```bash
# cd /etc/pki/tls/certs
# make
```

此 `Makefile` 允许你创建：
- 公钥/私钥对
- `SSL` 证书签名请求 (`CSRs`)
- 自签名 `SSL` 测试证书

要创建密钥对，运行 "`make SOMETHING.key`" 。要创建 `CSR`，运行 "`make SOMETHING.csr`" 。
要创建测试证书，运行 "`make SOMETHING.crt`" 。要在一个文件中创建一个密钥和一个测试证书，运行 "`make SOMETHING.pem`" 。

要创建一个用于 Apache 的密钥，运行 "`make genkey`" 。
要创建一个用于 Apache 的 `CSR`，运行 "`make certreq`" 。
要创建创建一个用于 Apache 的测试证书，运行 "`make testcert`" 。

要创建一个序列号不为 零的测试证书，请添加 `SERIAL=num`

示例：

```bash
make server.key
make server.csr
make server.crt
make stunnel.pem
make genkey
make certreq
make testcert
make server.crt SERIAL=1
make stunnel.pem SERIAL=2
make testcert SERIAL=3
```
