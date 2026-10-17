
```
user = root

server = /usr/bin/rsync

server_args = --daemon

log_on_failure += USERID
}
```

注意，此示例的第一行将服务标识为 `rsync`。这与 `/etc/xinetd` 文件中列出的服务名称完全匹配，导致该服务监听 TCP 和 UDP 协议的端口 `873`。你可以看到该服务默认是关闭的 `disable = yes`。要启用 `rsync` 服务，请将该行改为：

```
disable = no
```

> 提示：如果你的机器是 FTP 服务器，那么开启 `rsync` 服务是一个很棒的主意。它允许人们使用 `rsync` 客户端（包含校验和搜索算法）从你的服务器下载文件。有了该功能，用户可以重启中断的下载，而无需从头开始。

由于大多数服务默认都是关闭的，因此你的计算机的安全性完全取决于你如何设置。你可以通过确保 `/etc/xinetd.d/login` 和 `rsh` 文件中的 `disabled = yes` 来双重检查如 `login` 和 `rsh`（包含在 `rsh-server` 包中）等服务也是关闭的。

> 提示：你可以激活远程登录服务，但禁用对 `/etc/host.equiv` 和 `.hosts` 文件的使用，要求登录时始终提示密码。与其禁用服务，不如在 `rsh` 文件中找到该行 `server = /usr/sbin/in.rsh`，并在末尾添加一个空格和 `-L`。当然，这并没有改变你的密码和数据仍将通过网络以加密方式传输的事实。

你现在需要向 `xinetd` 进程发送一个信号，告诉它重新加载配置文件。最快的方法是重新加载 `xinetd` 服务。作为 root 用户，在 shell 中输入以下命令：

```
# service xinetd reload

Reloading configuration:      [ OK ]
```

就是这样——你已经启用了 `rsync` 服务。只要你已正确配置了邮件服务器（参见第 19 章），客户端现在应该能够通过 `rsync` 协议从你的计算机下载文件。

# 第三部分：管理 Fedora 和 RHEL

## 4. 我收到了消息并使用我的私钥对其进行解密。

# 安全套接层 Secure Sockets Layer

公钥加密的一种经典实现是使用安全套接层 `SSL` 通信。这项技术允许你安全地向在线商户提交信用卡信息。`SSL` 加密会话的元素如下：

- 启用了 `SSL` 的 浏览器 `Firefox`、`Mozilla`、`Internet Explorer`、`Opera`、`Konquerer` 等
- 启用了 `SSL` 的 Web 服务器 `Apache`
- `SSL` 证书

要启动 `SSL` 会话，Web 浏览器首先连接到端口 `443` 上的 Web 服务器，该端口也称为 `HTTPS`（安全超文本传输协议）。在两台机器之间建立套接连接后，会发生以下情况：

1. 服务器向浏览器发送其 `SSL` 证书。
2. 浏览器通过 `SSL` 证书验证服务器的身份。
3. 浏览器生成一个对称加密密钥。
4. 浏览器使用 `SSL` 证书加密该对称密钥。
5. 浏览器将加密后的密钥发送给服务器。
6. 服务器使用与其公钥 `SSL` 证书对应的私钥解密对称密钥。
7. 浏览器和服务器现在可以基于对称密钥的共同知识加密和解密流量。

现在可以进行安全的数据交换。

## 创建 SSL 证书

为了使用 `SSL` 证书进行安全的 HTTP 数据交换，你必须拥有一个支持 `SSL` 的 Web 服务器 `Apache` Web 包，它随 Fedora 和 RHEL 一起提供并支持 `SSL` 能力。以下是你为 Apache Web 服务器创建自己的 `SSL` 证书时需要的一些文件：

- `/etc/httpd/httpd.conf` — Web 服务器配置文件
- `/etc/pki/tls/certs/Makefile` — 证书构建脚本
- `/etc/httpd/conf.ssl.conf` — 主要 Web 服务器配置文件

既然你已经熟悉了基本组件，请看一眼用于创建 `SSL` 证书的工具：

```
# cd /etc/pki/tls/certs

# make
```
