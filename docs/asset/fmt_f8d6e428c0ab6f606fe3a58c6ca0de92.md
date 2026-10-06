
如果你在 `ErrorLog` 中没有获得足够的信息，可以使用 `Level` 指令配置它以记录更多信息。这些可用选项按详细程度递增排序依次为：`emerg`、`alert`、`error`、`warn`、`notice`、`info` 和 `debug`。仅选择其中一个。任何至少与所选 `Level` 等等重要的消息都将存储在 `ErrorLog` 中。在典型的服务器上，此值被设置为 `warn`。你不应该将其设置为任何低于 `crit` 的值，并应避免将其设为 `debug`，因为这会减慢服务器和客户端。

作为最后的手段，你还可以手动运行 `apache2` 来检查崩溃或其他错误消息：

```bash
#usr/sbin/apache2 -d /etc/apache2 -F ; echo $?
```

`-d` 标志告诉 `apache` 寻找其配置文件，`-F` 标志告诉它在前台运行。分号将此命令与 `echo` 命令隔开，`echo` 显示 Apache 退出后的返回代码 (`$?`)。如果 `apache` 在此步骤发生崩溃，你可以使用 `gdb` 和 `strace` 等工具来追踪问题。

## 访问禁止和服务器内部错误

在查看服务器上的特定页面时，可能会遇到两种常见的错误：权限错误和服务器内部错误。这两种错误通常都可以通过错误日志中的信息进行隔离。

## 第 15 章：运行 Linux Web 服务器

在对下列表描述的任何更改以尝试解决这些问题后，再次尝试请求，然后检查错误日志查看消息是否发生了变化（例如，显示操作成功完成）。

### 注意

“文件未找到”（File not found）错误可以按照“访问禁止”和“服务器内部错误”的方法进行检查。你有时可能会发现 Apache 并没有在你认为的地方查找某个特定文件。通常，整个路径都会出现在错误日志中。确保你访问的是正确的虚拟主机，并检查任何可能将你的位置重定向到意外之外地点的 `Alias` 设置。

- **文件权限** — 文件权限引起的访问错误表明 `apache` 进程正在以一个无法打开请求文件的用户身份运行。确保你的账户对该目录及其上级目录具有执行权限，并对文件本身具有权限。如果你想让 Apache 生成文件索引，则目录也需要读取权限。参见 `chmod` 的手册页以获取有关查看和更改权限的信息。

### 注意

对于编译后的二进制文件，不需要读取权限，但用 C 或 C++ 编写的文件可以安全地隐藏，除非有需要保持程序内容秘密。

- **拒绝访问** — “客户端被服务器配置拒绝”（client denied by server configuration）错误表明 Apache 被配置为拒绝访问该对象。检查影响你尝试访问的文件的 `<Location>` 和 `<Directory>` 设置。记住，应用于路径的设置也会应用于其下方的任何路径。你可以通过仅更改你想要允许访问的特定路径的权限来覆盖此设置。

- **未找到索引** — “根据规则禁止目录索引”（Directory index forbidden by rule）错误表明 Apache 无法找到 `Directory` 指令中指定的名称索引文件，并且被配置为不在目录中创建文件索引列表。确保你的索引页（如果有的话）具有相关 `Directory Index` 指令中指定的名称之一，或者为该对象的相应 `<Directory>` 或 `<Location>` 部分添加 `Indexes` 行。

- **脚本崩溃** — 脚本头部的过早退出可能表示脚本在完成之前就崩溃了。偶尔，导致此错误的错误也会出现在错误日志中。在使用 `suePHP` 时，此错误也可能由文件所有或权限错误引起。这些错误记录在 `/var/log/apache2/suex.log` 或 `/var/log/apache2/suphp.log` 中。

## 使用 SSL/TLS 保护你的网络流量

你想为你的服务器添加安全性，包括你自己的证书。你的数据很重要，你的能力也是如此。本节研究了你可以帮助保护通信的方法。

## 第四部分：设置 Linux 服务器

电子商务应用程序（如在线购物和银行）通常使用安全套字层（SSL）或传输层安全（TLS）进行加密。TLS 基于 SSL 3.0 版本，它们的性质非常相似。

在 SSL 客户端和 SSL 服务器之间建立连接期间，使用非对称（公钥）加密来验证身份并建立会话参数和会话密钥。然后使用对称加密算法（如 DES 或 RC4）加密数据。为了让客户端验证服务器身份，服务器必须有一个预先生成的私钥，以及包含公钥和服务器信息的证书。该证书必须可以使用已知的公钥进行验证。

证书由第三方证书机构（CA）数字签名，该机构验证了请求者的身份以及签署证书请求的有效性。在大多数情况下，CA 是一家与网络浏览器供应商达成安排的公司，使其证书在默认安装时被信任。CA 然后会对其服务收费。

商业证书机构在价格、功能和浏览器支持方面有所不同，但记住价格并不是质量的指标。流行的 CA 包括 InstantSSL (`www.instantssl.com`)、`Thawte` (`www.thawte.com`) 和 `Verisign` (`www.verisign.com`)。

你也可以选择自签名证书，尽管这些应该仅用于测试，或者只有少数人访问你的服务器且你不计划在多台机器部署证书。生成自签名证书的说明包含在以下节中。

最后一个选项是运行自己的证书机构。如果你有少数位专家用户，并将你的 CA 证书分发给他们的方法（包括让他们在浏览器中安装），这可能是可行的。创建 CA 的过程太复杂，书中无法涵盖，但它是生成自签名证书的值得的替代方案。你可以在 `http://openssl.org/howto/openssl/ca/` 找到运行自己的 CA 的指南。

以下步骤描述了如何在本章配置的 Web 服务器（运行在 Ubuntu 系统上）上生成和使用 SSL 密钥。

# 第 15 章：运行 Linux Web 服务器

## 生成你的 SSL 密钥

要开始设置 SSL，请使用 OpenSSL 软件包中的 `openssl` 命令来生成你的公钥和私钥：

1. 使用 APT 验证是否安装了 OpenSSL。如果不存在，APT 会自动下载并安装：

```bash
sudo apt-get install openssl
```

2. 生成一个 1024 位的 RSA 私钥并将其保存到文件中：

```bash
sudo su -
# mkdir /etc/apache2/ssl.key
# cd /etc/apache2/ssl.key
# openssl genrsa -out server.key 1024
# chmod 600 server.key
```

### 笔记

你可以使用 `server.key` 以外的文件名，如果你计划在机器上运行多个 SSL 主机（这需要多个 IP 地址），那么就应该这样做。只需确保稍后在 Apache 配置中指定正确的文件名即可。

在高安全环境中，在 `openssl` 命令的 `genrsa` 参数后添加 `-des3` 参数来对密钥进行加密是一个好主意：

```bash
openssl genrsa des3 -out server.key 1024
```

3. 系统会要求输入一个密码（passphrase），每次启动 Apache 时都需要它。

### 注意

不要丢失此密码，因为无法轻松恢复。

4. 如果你计划让证书由 CA（包括你自己运行的 CA）签名，请生成公钥和证书签名请求 (CSR)：

国家名称（两个字母） [:]:US

州或省名称（全称） [Some-State]:Washington

城市名称（例如，城市） [:]:Bellingham

组织名称（例如，公司） [Internet Widgets Pty Ltd]:Example Company, LTD.

组织部门名称（例如，部门） []:Network Operations

通用名称（例如，你的名称） [:]:secure.example.org

电子邮件地址 [:]:dom@example.org

请输入以下随证书请求一起发送的“额外”属性

挑战密码 []:

可选的公司名称 []:

通用名称（Common Name）应该与客户端访问你的服务器时使用的名称相匹配。如果你计划让第三方 CA 签名 CSR，请务必获取其他详细信息。

5. 使用第三方 CA 时，将 CSR 提交给它，然后将证书放入 `/etc/apache2/ssl/server.crt`（或所需的其他文件）。

6. 如果你不计划让证书被签名，或者想测试配置，请生成一个自签名证书并将其保存到名为 `server.crt` 的文件中。

```bash
# mkdir ../ssl.crt/
# cd ../ssl.crt/
# openssl req new -x509 -sha256 -days 365 -key server.key -out server.crt
国家名称（两个字母代码） [AU]: 
州或省名称（全称） [Some State]:
城市名称（例如，城市） []:
组织名称（例如，公司） [Internet Widgets Pty Ltd]:TEST USE ONLY
组织部门名称（例如，部门） [:TEST USE ONLY
通用名称（例如，你的名称） []:secure.example.org
电子邮件地址 []:domain@example.org
```

# 配置 Apache 支持 SSL/TLS

生成密钥后，你需要启用 Apache `mod_ssl` 模块（该模块为 Apache 添加 SSL/TLS 支持），然后使用相应的配置指令对其进行配置。`mod_ssl` 模块包含在基本的 `apache2.2-common` 软件包中。以下是为你的虚拟主机启用它的：

1. 运行 `a2enmod` 来启用 SSL：

```bash
$ sudo a2enmod ssl
Module installed; run /etc/init.d/apache2 force reload to enable.
```

2. 向你的 Apache 配置文件中添加一个启用 SSL 的虚拟主机。以之前的虚拟主机为例，你的配置看起来像这样：

```apache
Listen *:443
<VirtualHost *:443>
ServerName secure.example.org
ServerAlias web.example.org
DocumentRoot /home/username/public_html/
DirectoryIndex index.php index.htm

SSLEngine On
SSLCertificateKey /etc/apache2/ssl/server.key
SSLCertificateFile /etc/apache2/ssl.crt/server.crt
SSLCACertificateFile /etc/apache2/ssl.crt/ca.crt
</VirtualHost>
```

此示例在 `VirtualHost` 声明中使用通配符来表示 IP 地址，这可以避免你在 IP 地址更改时需要修改配置文件，并防止你拥有多个 SSL 虚拟主机。如果你确实需要支持多个 SSL 虚拟主机，请将 `*` 替换为分配给该主机的特定 IP 地址。

### 笔记

请本章节前面的“排排除你的 Web 服务器”部分获取有关 `Listen` 指令的更多信息。

- CA 通常会为你提供一个证书文件并放在 `ca.crt` 中，有时还会提供一个单独的文件，你需要使用 `SSLCertificateChainFile` 指令来引用该文件。

3. 测试 Apache 配置，然后执行完全重启：

```bash
$ sudo apache2ctl configtest
Syntax OK
$ sudo apache2ctl stop
$ sudo apache2ctl start
```

4. 如果你计划让证书由 CA（包括你自己运行的 CA）签名，请生成公钥和证书签名请求 (CSR)：

## 第 16 章：运行邮件服务器

### 关于系统和所使用的软件

本章描述的邮件服务器配置基于 Exim 邮件传输代理。除了 Exim 之外，还添加了其他几个组件用于管理服务器以及检查垃圾邮件和病毒：

- [Exim](www.exim.org/) — 一个由剑桥大学的 Philip Hazel 编写并设计的 MTA（邮件传输代理），并收到了全球许多人士的贡献。本章中涉及的版本包含了来自 Tom Kister 的 [Exim-ACL 补丁](http://duncthrax.net/exican-acl/)。该补丁允许在 Exim 内部进行扫描。由于该补丁已集成到 Exim 中，因此在本章的范围内，其功能被视为 Exim 的一部分。

- [Maildrop](www.courier-mta.org/maildrop/) — 一个社区支持的本地 MDA（邮件投递代理），是 Courier MTA 软件包的一部分，也可以作为独立程序使用。在此配置中，它被允许使用高级功能，例如信箱配额和服务器端消息排序。另一个 MDA 是 `procmail`（在 Ubuntu 中受官方支持）。

- [Courier IMAP 和 POP](www.courier-mta.org/imap/) — 与 Maildrop 类似，它们是 Courier MTA 的部分，也可以单独提供。它们因其安装简单、性能良好以及对 Maildir 格式目录的兼容性而被选中。该软件包也受社区支持，你可以考虑将其替换为 `dovecot` 软件包。

- [ClamAV](www.clamav.net/) — 一个开源病毒扫描器，可以检测超过 20,000 种病毒、蠕虫和木马。它使用病毒特征数据库来识别病毒，并包含一个全新的扫描程序。与 SpamAssassin 类似，ClamAV 包含一个守护进程（`clamd`）、一个客户端（`clamscan`）和一个不使用守护进程的命令行工具（`clamscan`）。

- [SpamAssassin](http://spamassassin.apache.org/) — 一个用 Perl 编写的垃圾邮件过滤程序。它使用大量的规则来判断邮件看起来有多像“垃圾”，并根据规则值的总和分配评分。出于性能考虑，SpamAssassin 使用一个名为 `spamd` 的后台守护进程来执行消息分析。通过邮件客户端访问该守护进程。它已安装，但本章中的两种配置均未使用它。

### 准备你的系统

对于本章涵盖的邮件服务器配置，你需要一些常用项目，首先是合适的硬件。个人邮件服务器可以轻松地运行在奔腾电脑上，尽管你可能会注意到在扫描传入邮件时偶尔会出现变慢的情况。磁盘空间需求取决于你想为邮件留出多少空间，因此请为操作系统留出几个 GB（这将为你留出足够的额外空间以备万一），加上你想存储的邮件数量。

## 第四部分：设置 Linux 服务器

如果你没有空闲的系统作为专用邮件服务器，可以将邮件服务器添加到你的工作站中。虽然这种方法显然仅建议用于个人使用，但本章的过程是从安装 Ubuntu 工作站开始的。

在开始安装邮件软件之前，你还应该正确配置你的网络设置。具体要求取决于邮件传递到你服务器的方法：

- 直接投递（Direct delivery）是大多数传统邮件服务器使用的方法。DNS 服务器上的邮件记录（MX）会告诉远程服务器，任何发送到你域名的邮件都应该通过 SMTP 发送到你的服务器。

- 使用 MRA（邮件获取代理）如 `Fetchmail` 从邮件主机获取邮件也是可能的。如果你在共享域有一个信箱，但想在自己的服务器上访问邮件，可以使用此选项。如果你既有自己的域名又有共享域下的信箱，也可以与直接投递结合使用。

**注意**

`Fetchmail` 的配置将在本章的“配置邮件客户端”部分进行说明。

### 配置 DNS 以实现直接投递

为了使直接投递生效，SMTP 服务（TCP 端口 25）必须通过 DNS 中的一个固定名称被外部世界访问。该名称将采用 A（地址）记录的形式。A 记录允许 DNS 解析器进程根据特定名称确定 IP 地址，并被 Internet 上大多数常用协议使用。一个典型的 A 记录如下：

```
bigserver.example.org IN A 10.0.12.16
```

第一个参数 `bigserver.example.org.` 是标签（label），第二个参数是类（IN 代表 Internet，即大多数 DNS 记录所在之处）。A 表示类型，最后一个参数是与标签关联的 IP 地址。

在你拥有一个 A 记录后，可以使用 MX（邮件邮件交换者）记录将邮件指向你的服务器。A 记录和 MX 记录不需要属于同一个域名，这提供了更大的灵活性。以下是一个 MX 记录示例：

```
widgets.test. IN MX 0 bigserver.example.org.
```

此 MX 记录表示，任何 `any@widgets.test` 都应该通过服务器 `bigserver.example.org` 发送。0 表示此 MX 记录的数字优先级。当一个标签存在多个 MX 记录时，会先尝试优先级最低的。如果遇到临时错误，将尝试下一个优先级的邮件服务器，依此类推，直到列表耗尽。此时，发送服务器将定期重试，直到消息超时（通常为五天）。如果存在多个优先级相同的 MX 记录，将按随机顺序尝试。

**注意**

在没有 MX 记录的情况下，大多数邮件服务器也将回退到标签的 A 记录中列出的 IP 地址。然而，依赖此功能被认为是不良做法。

在某些情况下，由于你的 IP 地址经常变化，建立 A 记录可能会变得复杂。某些服务可以接收邮件，这显然是可能的。以下是一些受欢迎的服务之一：

- [ZoneEdit](www.zoneedit.com/) — 支持 ez-update 

- [No-IP](www.no-ip.com/) — 支持 no-update 

**注意**

邮件服务器通常也会回退到 A 记录中列出的 IP 地址。然而，依赖此功能被认为是不良做法。

在某些情况下，由于你的 IP 地址经常变化，建立 A 记录可能会变得复杂。某些服务可以接收邮件，这显然是可能的。以下是一些受欢迎的服务之一：

- [ZoneEdit](www.zoneedit.com/) — 支持 ez-update 

- [No-IP](www.no-ip.com/) — 支持 no-update 

**注意**

邮件服务器通常也会回退到 A 记录中列出的 IP 地址。然而，依赖此功能被认为是不良做法。
