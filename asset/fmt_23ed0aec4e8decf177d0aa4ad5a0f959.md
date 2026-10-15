
摘要与原始消息之间的匹配确认了服务器的身份。为什么呢？服务器最初发送了由 CA 签名的证书，因此客户端完全确定这个公钥属于谁。然而，客户端证明了发送证书的服务器确实是其所声称的身份，因此服务器发送了一个简单的身份识别消息以及一个用公钥加密的消息摘要。如果发送服务器没有相应的私钥，它将无法产生客户端从身份识别消息计算出的相同摘要。

如果这看起来很复杂，那是刻意如此——而且还没此此。客户端现在可以向服务器发送一个对称加密密钥，使用服务器的公钥加密这条新消息。服务器可以使用这个新密钥来
加密数据并将其传输到客户端。为什么要重来一遍？很大程度上是因为对称加密比非对称加密快得多。

非对称加密（使用私钥和公钥）将随机生成的对称密钥从客户端安全地传输到服务器；该密钥用于建立一个快速、安全的通信通道。

![](img/177ab5b774eeb101e12de61f8616d71a_288_0.png)

如果一个冒充者存在于客户端和服务器系统之间，并且能够拦截传输的数据，它能造成多大的破坏？它不知道客户端和服务器使用的密钥，因此无法确定数据的内容；最坏的情况下，它可以通过向数据包中注入自己的数据来在数据中引入垃圾信息。

针对这一点，SSL 协议允许使用消息认证码（MAC）。MAC 仅仅是通过对称密钥和传输的数据计算出的一段数据。冒充者不知道对称密钥，因此无法计算 MAC 的值。例如，一种名为 MD5 的著名加密算法（由 RSA Data Security, Inc. 开发）可以为每个传输的数据包生成 128 位的 MAC 值。通过这种方式成功猜出正确 MAC 所需的计算能力和时间几乎是不可能的。SSL 让互联网上的安全交易成为可能。

# 获取 SSL

多年来，SSL 主要在商业 Linux 软件可用，例如 Stronghold，这是一种基于 Apache 的商业 Web 服务器。由于专利和美国出口限制，很一段时间内没有适用于 Linux 的 开源 SSL 版本。最近，OpenSSL 项目改变了这一切。

# 了解 OpenSSL

OpenSSL 项目是一个开源社区协作项目，旨在开发商业级 SSL、传输层安全协议（TLS）以及全强度、通用的加密库包。SSL 的当前实现（也称为 OpenSSL）基于 SSLeay 库，该库由 Eric A. Young 和 Tim J. Hudson 开发。OpenSSL 软件包的许可允许出于商业和非商业目的均使用该软件。

# OpenSSL 的用途

SSL 可用于许多应用程序，以增强并确保交易数据的安全：OpenSSL 只是让这种能力变得更加普及。本节将探讨如何使用 OpenSSL 执行以下安全任务：

# 第 11 章：OpenSSL 267

- 使用 Apache-SSL 保护 Web 上的交易（详情请参见第 15 章）
- 保护远程访问您的 Linux 计算机的用户访问
- 通过基于 OpenSSL 的隧道软件通过 PPP 保护私有网络（VPN）连接（详情请参见第 20 章）
- 通过使用 OpenSSL 的隧道软件保护电子邮件（IMAP, POP3）（详情请参见第 20 章）。

# 获取 OpenSSL

OpenSSL 二进制文件目前以 RPM 包的形式随 Red Hat Linux 发行版一起提供。你可以直接使用 Red Hat 提供的 RPM 版本，也可以直接从 OpenSSL 官方网站 www.openssl.org/source 下载源代码。

尽管如上述，我更倾向于从真实的 Web 或 FTP 站点下载源码发行版来安装安全软件。在接下来的章节中，我将讨论从 OpenSSL 网站下载的官方源码进行编译和安装 OpenSSL 的细节。

![](img/177ab5b774eeb101e12de61f8616d71a_289_0.png)

> 如果你必须从 RPM 安装 OpenSSL，请使用可信的二进制发行版，例如官方 Red Hat 光刻盘上的版本。要从 RPM 包安装 OpenSSL 二进制文件，只需运行 `rpm -ivh openssl-packagename.rpm` 命令。

# 安装并配置 OpenSSL

OpenSSL 网站提供 gzip 压缩 tar 包格式的 OpenSSL 源码。本文版本是 `openssl-0.9.6.tar.gz`。在开始编译过程之前，你必须确保系统符合先决条件。

## OpenSSL 先决条件

OpenSSL 源码发行版要求你安装了 Perl 5 和 ANSI C 编译器。我假设在设置 Linux 系统时已经安装了 Perl 5 和 `gcc`（C 编译器）。

## 编译并安装 OpenSSL

编译 OpenSSL 是一个简单的任务。请按照下面的步骤操作。

1. 从控制以 root 身份登录 Linux 系统。
2. 将 OpenSSL 源码 tar 包拷贝到 `/usr/src/redhat/SOURCES` 目录。
3. 运行 `tar xvzf openssl-version.tar.gz` 命令解压源码包。

例如，为了提取 `openssl-0.9.6.tar.gz` 文件，我可以运行 `tar xvzf openssl-0.9.6.tar.gz` 命令。`tar` 命令会创建一个名为 `openssl-version` 的目录，在我的示例中是：

> 提示：如果磁盘空间对你来说是个问题，此时可以删除 tar 包。但是，请确保你已成功编译并安装了 OpenSSL。

4. 将新创建的目录设置为当前目录。

此时，可以自由阅读发行包中包含的 README 或 INSTALL 文件。下一步是配置安装选项；在编译软件之前需要某些设置。

要将 OpenSSL 安装在默认的 `/usr/local/ssl` 目录，运行以下命令：

```
/config
```

然而，如果你必须安装在不同的目录，请在前面的命令后附加 --prefix 和 openssldir 标志。例如，要将 OpenSSL 安装在 `/opt/security`，前面的命令看起来如下：

```
/config
```

### 表 11-1：编译时的配置选项

| 配置选项 | 目的 |
| :--- | :--- |
| --prefix=DIR | 将 OpenSSL 安装在 DIR。 |
| --openssldir=DIR | 指定目录。 |
| no-threads | 禁用多线程应用程序。 |
| no-shared | 共享库。 |
| no-asm | 禁用汇编代码。 |
| 386 | 仅用于 386 机器。 |
| no-cipher | OpenSSL 使用许多加密算法，如 bf, des, dh, hmac, mdc2, rc2, rc4, rc5, sha。 |
| -Dxxx,-Lxxx,-fxxx,-Kxxx | 这些选项允许你指定系统相关选项。 |
| -fPic,-fPIC,-KPIC | 启用位置无关代码 (PIC)。 |

# 第三部分：系统安全

在 `make` 工具执行成功后，运行 `make test` 测试二进制文件。最后，运行 `make install` 将 OpenSSL 安装到你的系统中。

![](img/177ab5b774eeb101e12de61f8616d71a_292_0.png)

如果你在编译 OpenSSL 时遇到问题，原因可能是库文件不匹配——在旧系统上安装最新版本的软件时并不罕见。或者可能是命令行指定的某个选项缺少组件。例如，如果你系统中没有安装 RSA 库（Red Hat Linux 不包含），而你尝试使用它，编译就会失败。这里传统的编程智慧派上了用场：在使用特定选项时，确保你完全清楚自己在做什么。如果这些方法都不能解决问题，请尝试搜索 OpenSSL FAQ 页面 www.openssl.org/support/faq.html。或者直接安装 OpenSSL 的 RPM 包。

# 理解服务器证书

在使用许多支持 SSL 的应用程序（如 OpenSSH 和 Apache-SSL）之前，你需要创建适当服务器证书。

## 什么是证书？

在 SSL 交易中，证书是放置在消息中的数据，用于证明发送者的真实性。它由加密信息组成，将公钥与个人、服务器或其他实体的真实身份相关。它还包含了颁发者的标识和电子签名。颁发者被称为证书机构（CA）。

证书可能包含其他帮助 CA 管理证书的信息（如序列号和有效期）。使用支持 SSL 的 Web 浏览器（如 Netscape Navigator 或 Microsoft Internet Explorer），你可以查看服务器证书。

证书中的标识实体通过区分名字段（由 X509 标准定义）表示。表 11-2 列出了常见的区分名字段。

### 表 11-2：区分名称字段 (DN Fields)

| DN 字段: | 缩写 | 含义 |
| --- | --- | --- |
| 通用名称 (Common Name) | CN | 认证实体以此名称已知。 |
| 组织或公司 (Organization or Company) | O | 实体与此组织相关。 |
| 组织单位 (Organizational Unit) | OU | 实体与此组织相关。 |
| 城市/地区 (City/Locality) | L | 实体所在的城市。 |
