
这些 CA 通常是大型公司（如 `Thawte` 或 `Equifax`），它们会验证请求证书的公司是否有权获得该证书。这是通过各种带外手段实现的，例如在数据库中验证你的公司信息，或验证你的电话、地址、域名所有者以及他们收取费用的项目。在确定你是合法身份后，他们会对你的公钥进行签名并将证书返回给你。

## 公共 CA 并非完美

即便如此谨慎，公共 CA 并不总是能处理正确。例如，`Veris` 在 2001 年 1 月向一个完全与微软无关的人颁发了两个微软证书，直到六周后才注意到。在此期间，接收该证书的人可以使用它在提供网页服务或签署软件时伪装成微软。

获取第三方证书需要时间（通常为一到两周）以及填写信息的繁琐过程。它还需要费用。一个标准的网站证书大约花费 350 美元。

对于我们的目的来说，没有理由不简单地使用自签名证书，从而省去第三方证书带来的麻烦和成本。

### 自签名证书

任何公钥/私钥对都可以创建证书。CA 密钥并没有什么特殊之处，除了它们被预装在你的网页浏览器中。

避免 CA 的常用方法是使用自签名证书。在我们的 VPN 设置中，我们将为每个连接创建一个公钥/私钥对。客户端将验证服务器的证书。

如果我们使用第三方证书，我们将验证证书的完整性。只要你验证了证书，使用自签名证书和第三方证书在安全性上并没有区别。

### 如果你已经有了自己的 CA 怎么办？

如果你有自己的 CA，你可能想使用它。如果是这样，我们很惊讶你竟然在读这一节。

# 第 4 章 使用 SSL/TLS/PPP 构建 VPN

## 建立 SSL/TLS 连接

所有的 SSL/TLS 连接都从握手开始，允许两台机器进行安全通信。简而言之，SSL/TLS 握手如下：

客户端通过一个“client hello”包发起连接请求。服务器用“server hello”响应。这些消息建立了 SSL/TLS 协议版本、它们支持的加密算法以及一些随机数据。服务器发送其证书，客户端对其进行验证。如果需要，服务器可能会向客户端请求证书并同样进行验证。

然后，两台机器使用更改密文规范（这是一种独立于握手协议的 SSL 组件）来确定本次会话使用的加密算法，并约定使用的密钥。该密钥通过使用对方的公钥进行加密来防止被窥探。

在验证了远端的真实性、约定了加密算法并安全地传输了使用的密钥后，SSL/TLS 协商完成，每端都指示成功。此时，实际的应用程序数据将封装在 SSL/TLS 连接中发送。

这是对 SSL/TLS 设置的简要概述。如果你想了解 SSL/TLS 的细节，请阅读 `RFC-2246` 和位于 `http://home.netscape.com/eng/ssl13/` 的 SSL 规范。你不要相信，整个握手只需要四个数据包即可完成。

因此，当把协议（例如 HTTP）封装在 SSL/TLS 内部时，连接如下：

- 客户端连接到服务器端口 `443`（HTTPS）。
- 客户端和服务器协商并启用 SSL/TLS。
- HTTP 在加密连接上开始。

## 我们的示例网络

理论上是：从 VPN 客户端到 VPN 服务器建立 SSL/TLS 连接，并在两端运行 PPP 守护进程相互通信以创建我们的 VPN。我们将在 `Bears`（VPN 服务器）和 `Falcons`（VPN 客户端）之间创建一个 VPN，如图 4.1 所示。

`Bears` 和 `Falcons` 之间都有需要安全连接的网络。虚线表示在两个主机之间创建的虚拟网络。

![](img/ac8d70f99c3fa1e7029fbd036fc254da_123_0.png)

图 4.1 我们的 VPN 网络。

## 手动通过 SSL/TLS 设置 PPP

首先，我们将向你展示手动在两个主机之间创建 VPN 所需涉及的各种组件。这将为我们稍后的脚本奠定基础，并帮助你理解正在发生什么。如有必要，这有助于调试连接。

### 安装并验证 PPP

首先，确定你的 VPN 客户端和 VPN 服务器上都安装了 `ppp`。在 Debian 或其他基于 `dpkg` 的系统上，输入以下命令：

```
root@debian# dpkg -l ppp | grep ppp
ii ppp  2.3.11-4  Point-to-Point Protocol (PPP) daemon.
```

在 Red Hat 或其他基于 `rpm` 的系统上，你输入以下命令：

```
root@redhat# rpm -q ppp
ppp: 2.3.11-4
```

确保你安装的 `ppp` 版本为 `2.3.7` 或更高，因为这是第一个支持自动设置 `pty` 所需的 `pty` 参数的版本。

### 启用 Linux IP 转发

大多数 Linux 发行版默认不允许 IP 数据包转发，但我们必须启用它以便通过 PPP 接口路由 VPN 包。你可以通过修改适当的内核参数来更改 IP 转发的状态。虽然重新编译内核到默认设置，但最简单的方法是使用 `/proc` 文件系统。`/proc` 中的实际上不是文件，而是访问和/或修改内核参数的方法，你必须更改这些内容。因此，开启端口转发最简单的方法是运行以下命令：

```
root# echo 1 > /proc/sys/ipv4/ip_forward
```

这默认会自动开启所有接口的 IP 转发。如果你在制作主机到主机的 VPN，这足够了。如果你想创建网络到网络或主机到网络的 VPN，你可能只想对显式想要转发的接口开启 IP 转发。有关如何操作的示例，请参阅第 3 章“使用 SSH 和 PPP 构建 VPN”中的“启用 IP 转发”章节。

## 创建 VPN 用户

接下来，你必须在两端创建一个运行 VPN 命令的用户。我们假设两端都使用用户名 `sslvpn`，尽管你可以使用任何喜欢的用户名。虽然两台机器上的用户名不需要相同，但会让事情变得更简单。例如，你可以如下创建用户：

```
root# groupadd sslvpn
root# useradd -m -d /opt/ssl-vpn -c "SSL VPN User" -g sslvpn sslvpn
```

示例的 `/etc/shadow` 条目可能如下：

```
sslvpn::11429:0:99999:7::
```

`useradd` 默认创建带有锁定密码的用户，确保目前没有人可以登录这些账户，唯一的访问方法是使用 `root` 通过 `/bin/su`。我们为该用户使用的家目录传统是 `/opt/ssl-vpn`。

虽然我们可以在 `/home` 中创建家目录，但这个用户将更像一个软件产品一样使用。因此，安装在 `/opt`（或 `/usr` 等）更符合其功能。所以，此后我们将使用 `/opt/ssl-vpn`，尽管你可以使用任何喜欢的路径。

### 命名规范

为了区分我们的两个主机，我们将建立 VPN 客户端的机器称为 VPN 客户端，将另一台机器称为 VPN 服务器。VPN 客户端将与 VPN 服务器建立 SSL 连接。

我们还必须为我们的 VPN 起一个名字。在我们的示例中，我们将使用 `vpn1`。我们的脚本可以同时建立多个 VPN，这个名称有助于区分它们。

## 创建你的密钥和证书

我们希望我们的 SSL 连接在两端都经过身份验证，从而确保端点是合法的。为此，我们必须为客户端和服务器都创建密钥和证书。我们将让 VPN 服务器在两端都要求证书认证，这并不是 SSL 连接的默认设置。

由于我们追求偷懒，我们将创建自签名密钥。为了生成密钥，我们必须创建一个 OpenSSL 配置文件。Stunnel 分发版中已经为你提供了一个，名为 `stunnel.cnf`。你可以使用这个文件，也可以自己创建一个一个。以下是我们通常使用的配置文件：

```
[ req ]
default_bits = 1024
encrypt_key = yes
distinguished_name = req_dn
x509_extensions = cert_type
[ req_dn ]
countryName = Country Name (2 letter code)
countryName_default = US
stateProvinceName = State or Province Name (full name)
stateProvinceName_default = IL
localityName = Locality Name (eg, city)
localityName_default = Chicago
organizationName = Organization Name (eg, company)
organizationName_default = Building Linux VPNs
commonName = Common Name (FQDN of your server)
commonName_default = fictitious.example.com

[ cert_type ]
sCertType = server
```

我们需要将密钥和证书放在特定的目录中以便 Stunnel 找到它们。为了能够拥有具有不同密钥和证书的多个 VPN，我们将创建一个名为 `/opt/ssl-vpn/etc/vpnname/`（将 `vpnname` 替换为实际 VPN 名称）的目录，并在其中存储文件。无论使用哪个 VPN，OpenSSL 配置文件都是相同的，将该文件保存为 `/opt/ssl-vpn/etc/stunnel.cnf`。

为了在一个简单的命令中创建密钥并签名，我们将运行：

```
bears-server$ cd /opt/ssl-vpn/etc/vpn1
bears-server$ openssl req -new -x509 -days 365 -nodes \
  -config /opt/ssl-vpn/etc/stunnel.cnf \
  -out server.pem -keyout server.pem
```

在客户端，我们将运行：

```
falcons-client$ cd /opt/ssl-vpn/etc/vpn1
falcons-client$ openssl req -new -x509 -days 365 -nodes \
  -config /opt/ssl-vpn/etc/stunnel.cnf \
  -out client.pem -keyout client.pem
```

上述 `openssl` 参数含义：

- `-req -x509`: 生成新的 SSL 私钥和自签名证书。
- `-days 365`: 证书有效期为一年。
- `-nodes`: 不使用密码加密私钥。
- `-config`: 配置路径。
- `-out`: 保存证书的文件。
- `-keyout`: 保存私钥的文件。

### 无密码生成密钥

我们希望 VPN 能够在不需要管理员协助的情况下通过启动脚本、`cron` 任务等进行连接。为此，我们在创建密钥时使用 `-nodes` 选项，我们的 SSL 私钥可能不会被密码保护。如果你喜欢这种额外的安全性且不介意手动启动，请按回车接受默认值。

### 这些都相关吗？

Stunnel 不关心你指定的实际数据，因此两端可以使用相同的数据。但稍后我们会看到，该信息被 Stunnel 用于查找证书，因此你应该确保客户端和服务器证书使用独特的信息生成。信息不需要准确。

```
Using configuration from stunnel.cnf
Generating 1024 bit RSA private key......
```

将新私钥写入 'stunnel.pem'

将被要求输入用于证书请求的信息。你即将输入的内容被称为区别名称（DN）。有很多字段，但你可以留一些空白。某些字段会有默认值，如果你输入 '.'，该字段将留空。

Country Name (2 letter code) [US]:

StateProvince Name (full name) [IL]:

Locality Name (eg, city) [Chicago]:

Organization Name (eg, company) [Building Linux VPNs]:

Common Name (FQDN of your server) [fictitious.example.com]:

### 通用名称字段

SSL 浏览器识别证书的通用名称（CN）字段以匹配服务器的完全域名。因此，如果一台机器连接到 `www.example.com`，CN 也必须匹配 `www.example.com`。Stunnel 没有此要求，它将简单对照本地安装的有效证书列表检查提供的证书。

我们的密钥和证书已相应创建为 `server.pem` 或 `client.pem`。这以隐私增强邮件（PEM）格式保存，即数值数据的文本表示（base64 编码）。可以使用 OpenSSL 生成其他格式，但 Stunnel 只支持 PEM 格式。文件看起来如下：

```
--- BEGIN PRIVATE KEY ---
MIIXIQAAABBAQGC01HKMLLCUG02CZFN6X7bBC2gJWU7IOVAg2/pNAFAYJZT
X1wjVHLFTObBhtRbHtIG+OCfJp+A11ZknprKZCE
--- END PRIVATE KEY ---
--- BEGIN CERTIFICATE ---
MIIYCTCCacgAwIBAgIUIBANBgBgki9oBAQGFADBrMqswCQYDVQQGGEWJVULE
B0BCtMg4v41/B2UsdwSjNmHoLDKD4JR+EoI1joLBVBY==
--- END CERTIFICATE---
```

第一部分是密钥，第二部分是证书。Stunnel 要求它们位于同一个文件中。要查看与证书关联的信息，运行以下命令：

```
bears$ openssl x509 -subject -issuer -dates -fingerprint -noout -in server.pem
subject=C=US/ST=IL/Chicago=Building Linux VPNs/CN=fictitious.example.com
issuer=C=US/ST=IL/Chicago=Building Linux VPNs/CN=fictitious.example.com
notBefore=Sep 17 00:00:00 2001 GMT
After=Sep 17 00:00:00 2002 GMT
MD5 Fingerprint:74:8C:A2:B8:63:A6:FB:BA:7B:24:33:CD:9F:A0:19:C5
```

## 手动设置基于 SSL/TLS 的 PPP

### 使用第三方证书

如果你倾向于使用第三方证书，则应该使用以下命令生成你的密钥：

```bash
bears-server$ openssl req -x09 -newkey -x509 -days 365 -nodes \
-config /opt/ssl-vpn/etc/sslvpn.cnf \
-keyout server.pem
```

`server.pem` 中将保存一个私钥。屏幕上将输出一个证书请求，你应该让你的证书颁发机构（CA）对其进行签名。通常这涉及将证书请求的副本粘贴到 CA 的订单单中。当你收到他们的证书时，将其附加到 `server.pem` 文件中即可开始使用。使用与我们相同的方法来生成 `client.pem` 文件。

最后一步是创建一个不包含私钥的证书副本。虽然你可以直接从 `{server, client}.pem` 文件中剪切并粘贴证书，但使用 `openssl` 这样做会更快：

```bash
bears-server$ openssl x509 -in server.pem -out server.cert
falcons-client$ openssl x509 -in client.pem -out client.cert
```

这些文件现在仅包含证书，不包含私钥信息。由于我们在创建私钥时没有设置任何密码，因此务必将它们仅保留在本地机器上。

### 安装证书

我们现在必须将服务器证书复制到客户端用于验证，反之亦然。我们目前的目录结构如下：

```bash
bears-server$ ls /opt/ssl-vpn/etc/vpn1
server.cert server.pem
```

```bash
falcons-client$ ls /opt/ssl-vpn/etc/vpn1
client.cert client.pem
```

使用你喜欢的任何方法将证书文件拷贝到另一台机器——无论是 `scp`、`sftp`、剪切和粘贴，或者如果你运气好可以使用 `ftp`。这使得我们的目录如下：

```bash
bears-server$ ls /opt/ssl-vpn/etc/vpn1
client.cert server.cert server.pem
```

```bash
falcons-client$ ls /opt/ssl-vpn/etc/vpn1
client.cert client.pem server.cert
```

由于你的 VPN 的安全性基于对这些证书的验证，你应该检查并确保它们已正确传输。如果你极度多疑，可以进行视觉上的对比。然而，最简单的方法可能是对校验和值进行快速对比：

```bash
bears-server$ md5 /opt/ssl-vpn/etc/vpn/client.cert
3c97f58b0b4a0068fe3a0ca5c7a5d56
falcons-client$ md5 /opt/ssl-vpn/etc/vpn/client.cert
3c97f58b0b4a0068fe3a03ca5c7a5d56
```

`md5` 会生成文件内容的校验和值。如果文件相同，结果（以 `3c97f58...` 开头的数字）将是相同的。请确保在两台机器上都验证证书和服务器证书。

当 Stunnel 在 SSL 握手期间从远程获取证书时，它将尝试通过在该目录中查找本地证书副本来验证它。它将获取证书的哈希值，生成一个八位十六进制进制字符串，例如 `1ca0c052`。Stunnel 将在此目录下打开一个名为 `hash.0` 的文件，并将其内容与对端呈现的证书进行比较。如果它们匹配，则远程已通过验证。如果不匹配，连接将被关闭。
