
电子商务应用程序（如在线购物和银行）通常使用安全套接层（SSL）或传输层安全（TLS）规范进行加密。TLS 基于 SSL 规范的 3.0 版本，因此本质上非常相似。由于这种相似性——由于 SSL 较旧——SSL 缩写通常被指代其中之一。对于 Web 连接，首先建立 SSL 连接，然后通过它“隧道化”HTTP 通信。

> 由于 SSL 协商发生在任何 HTTP 通信之前，发生在 HTTP 层的名称虚拟主机无法与 SSL 一起工作，因此你配置的每个 SSL 主机都需要一个唯一的 IP 地址。

在 SSL 客户端和 SSL 服务器之间建立连接期间，使用非对称（公钥）加密来验证身份并建立会话参数。使用 DES 或 RC4 等对称加密算法配合协商的密钥来加密会话期间传输的数据。在握手期间使用非对称加密可以在不使用共享密钥的情况下安全通信，而对称加密在处理数据时速度更快、更实用。为了让客户端验证服务器身份，服务器必须有一个预先生成的私钥，以及一个包含公钥和服务器信息的证书。该证书必须可以使用公钥进行验证。

在某些情况下，服务器还需要客户端提供一个它可以验证的证书。然而，这在客户端数量较少的高安全环境 Web 服务器上并不常见，在这种环境下管理证书更为实用。你可以在 `http://developer.netscape.com/docs/manuals/security/html` 找到有关 SSL 协议的更多信息。

证书通常由第三方证书机构（CA）进行数字签名，该机构验证了请求者的身份和请求的有效性。在大多数情况下，CA 是一家与 Web 供应商有自己的安排，以便默认安装其证书。商业证书机构在功能和浏览器支持方面有所异，但请记住价格并不总是质量的体现。一些流行的 CA 包括 InstantSSL (`www.instantssl.com`)、Thawte (`www.thawte.com`) 和 VeriSign (`www.verisign.com`)。

# 第 V 部分 ♦ 运行服务器

你也可以选择自签名证书，尽管这些应该只用于测试，或者当只有少数人访问你的服务器且你不计划在多台机器上部署证书时使用。生成自签名证书的说明包含在以下节。最后一个选项是运行你自己的证书机构。如果你预期的用户较少，并且需要向他们分发你的 CA 证书（包括协助他们在浏览器中安装），这可能是行的。创建 CA 的过程是生成自签名证书的替代方案。你可以在这些网站找到运行自己的 CA 的指南：

- `http://www.openssl.org/ssl/ca.html`

以下步骤描述了如何在 LAMP 服务器（运行在 Debian/Linux 系统上）生成和使用 SSL 密钥。有关 SSL 密钥的通用讨论以及 Fedora 和其他 Red Hat 系统的特定程序，请参考第 6 章。

## 生成你的密钥

开始设置 SSL，使用 `openssl` 命令（它是 OpenSSL 软件包的一部分）来生成你的公钥和私钥：

1. 使用 APT 验证 OpenSSL 是否安装。如果没有安装，APT 会自动下载并安装它：

```
# apt-get install openssl
```

2. 生成一个 1024 位的 RSA 私钥并将其保存到文件中：

```
# mkdir /etc/apache/ssl.key/
# cd /etc/apache/ssl.key/
# openssl genrsa -out server.key 1024
# chmod 600 server.key
```

> 你可以使用 `server.key` 以外的文件名，如果你计划在机器上运行多个 SSL 主机（这需要多个 IP 地址），则应该这样做。只需在稍后的 Apache 配置中指定正确的文件名即可。

在高安全环境中，在 `openssl` 命令行的 `genrsa` 参数后添加 `-des3` 参数来加密密钥是一个好主意：

```
# openssl genrsa -des3 -out server.key 1024
```

3. 你会被要求输入密码（passphrase），在每次启动 Apache 时都需要它。

# 第 24 章 运行 Linux、Apache、MySQL 和 PHP (LAMP) 服务器 669

![](img/a2d958d7eab32ca5b89b2b8af808aa70_700_0.png)

不要丢失这个密码，因为无法找回。

4. 如果你计划让证书由 CA 签名（包括你自己运行的 CA），请生成公钥和证书签名请求（CSR）：

```
# mkdir ../ssl/csr/
# cd ../ssl/csr/
# openssl req -new -key ../ssl/key/server.key -out server.key
```

国家名称（2 位代码） []:`US`

州或省名称（全称）[Some-State]:`Washington`

地区名称（例如，城市）[:`Belling`

组织名称（例如，公司）[Internet Widgets Pty Ltd]:`Example Company, LTD.`

组织单位名称（例如，部门）[:`Network Operations`

通用名称（例如，你的名称）[:`secure.example.org`

邮箱地址 [:`dom@example.org`

请输入以下随证书请求一起发送的“额外”属性

挑战密码]:

可选的公司名称 []:

通用名称（Common Name）应与客户端访问你的服务器时所使用的名称匹配。如果你计划让第三方 CA 签名 CSR，请确保其他细节无误。

5. 使用第三方 CA 时，将 CSR 提交给它，然后将它提供的证书认证到 `/etc/apache/ssl.crt/server.crt`（或所需的其他文件）。

6. 如果你不想签名证书，或者你想测试你的配置，请生成一个自签名证书并将其保存为命名的 `server.crt`：

```
# mkdir ../ssl/csr/
# cd ../ssl/csr/
# openssl req -new -x509 -nodes -days 365 -key ..///ssl/key/server.key -out server.crt
```

国家名称（2 位代码）[AU]:

州或省名称（全称）[Some-State]:

地区名称（例如，城市）[:

组织名称（例如，公司）[Internet Widgets Pty Ltd]:`TEST ONLY`

组织单位名称（例如，部门）[:`TEST USE ONLY`

通用名称（例如，你的名称）[:`secure.example.org`

邮箱地址 [:`dom@example.org`

## 配置 Apache 以支持 SSL/TLS

一旦生成了密钥，您需要安装 `mod_ssl` Apache 模块（该模块为 Apache 添加 SSL/TLS 支持），然后使用适当的配置指令对其进行配置。方法如下：

1. 通过安装 `mod_ssl` 包可以为 Apache 添加 SSL 和 TLS 支持：

```bash
# apt-get install libapache2-mod-ssl
# apache2conf enable mod_ssl
```

将配置文件 `/etc/apache/modules.conf` 替换为新版本

2. 在您的 Apache 配置文件中添加启用了 SSL 的虚拟主机。以之前的虚拟主机为例，您的配置看起来像像所示：

```
Listen *:443
<VirtualHost *:443>
  ServerName secure.example.org
  DocumentRoot /home/username/public_html/
  User username
  Group groupname
  DirectoryIndex Index.php index.htm
  SSLEngine On
  SSLCertificateKey /etc/apache/ssl.key/server.key
  SSLCertificate /etc/apache/ssl.crt/server.crt
  SSLCACertificate /etc/apache/ssl.crt/ca.crt
</VirtualHost>
```

此示例在 `VirtualHost` 声明中使用了 IP 通配符，这可以避免您在 IP 地址更改时需要修改配置文件，但它也会防止您拥有多个虚拟主机。如果需要支持多个 SSL 虚拟主机，请将其替换为分配给该主机的特定 IP 地址。

> 请参本章节前面的“故障排除”部分以获取有关 `Listen` 指令的更多信息。

CA 通常会为您提供一个证书文件放在 `ca.crt` 中，并提供另一个单独的文件，您需要使用 `SSLCertificateChain` 指令来引用该文件。`mod_ssl` 包还包含一个 `/etc/apache/ssl.crt/ca-bundle.crt`，它包含了大多数知名证书颁发机构的证书，只要安装了适当的 CA 证书就可以引用它。当引用自己的 CA 时，请将此指令指向包含该 CA 公钥的文件。使用自签名证书时，请省略此行。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_701_0.png)
