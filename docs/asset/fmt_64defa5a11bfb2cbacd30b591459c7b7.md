
```bash
[stacia]$ gpg --verify message.txt.asc
gpg: Signature made Wed Nov 29 21:12:23 2000 EST using DSA key
ID 3C9EA164
gpg: Good signature from 'Ramon J. Hontanon (Linux Student)
<rstanton@sybex.com>'
```

考虑这样一种情况：你希望同时确保消息的隐私性和完整性。以下命令对文件 `message.txt` 中包含的消息进行签名和加密：

```
[ramon]$ gpg --encrypt --sign --armor message.txt

You need a passphrase to unlock the secret key for
user: 'Ramon J. Hontanon (Linux Student)
<rstanton@sybex.com>'

1024-bit DSA key, ID 3C9EA164, created 2000-11-29

You did not specify a user ID. (you may use "-r")

Enter the user ID: stacia@example.com
```

当 `Stacia` 收到消息时，她随后使用她的 `gpg` 工具解密并验证生成的 `message.txt.asc` 文档的签名：

```
[stacia]$ gpg --decrypt message.txt.asc

You need a passphrase to unlock the secret key for
user: 'Stacia S. Hontanon (Linux Master)
<stacia@example.com>

1024-bit ELG-E key, ID A0626845, created 2000-11-29 (main key
ID 3C9EA034)

This is just a test message. We would like to ensure the integrity
of this message by attaching a digital signature to it.

Regards,

-- ramon
gpg: Signature made Wed Nov 29 21:21:54 2000 EST using DSA key
ID 3C9EA164
gpg: Good signature from 'Ramon J. Hontanon (Linux Student)
<rjhontanon@sybex.com>'
```

在这个例子中，解密/验证的输出直接显示在屏幕上。如果你希望输出定向到文件 `message.txt`，只需使用以下命令（注意 `--output` 指令）：

```
[stacia]$ gpg --output message.txt --decrypt message.txt.asc
```

正如你所见，`GnuPG` 是一个综合软件包，包含用于加密、解密、签名和验证任何类型文档（包括电子邮件消息）的工具，以及管理提供此服务所需的私钥和公钥的工具。

像 `GnuPG` 这样的工具不仅对保护电子邮件交换有用，也是保护你需要存储在 Linux 服务器上的关键文件的一项额外隐私措施。我建议你使用 `GnuPG` 加密敏感的网络拓扑图、包含认证密码的笔记以及揭示任何漏洞的网络审计报告，至少在你有机会解决这些漏洞之前。

### 总结

应用程序安全的多层方法要求采用机制来确保应用传输（例如，`SSL`）的隐私性和认证，并通过在流量到达网络之前对数据应用加密和数字签名来确保数据包内容的完整性和真实性（例如，`GnuPG`）。

对于电子邮件应用来说，这一点尤为相关，因为它们的流量巨大，且公司越来越依赖电子邮件处理敏感内容。无论你选择哪种 `MTA`，都需要确保你的邮件用户代理（客户端）支持与你的邮件传输代理相同类型的隐私和认证机制。同样重要的是，确保你的用户接受必要的培训，以便按照你的安全策略使用应用程序。

电子邮件和网页浏览构成了当今穿越互联网流量的大部分。第 7 章“HTTP 服务”将继续讨论应用层安全，通过考察适用于 Linux 服务器的三种开源 HTTP 服务器围绕的安全问题。

![](img/3258bbaf790525f8c4eb25fabff7844a_199_0.png)

# 7 HTTP 服务

本章继续第三部分“应用安全”的讨论，深入探讨 `Apache HTTP` 服务器，它是过去五年 Web 服务器爆发式增长背后的主导力量。本章描述了基础 `Apache` 软件包的整体安全功能，以及标准的认证和访问控制配置。

虽然系统和网络层安全有助于封堵大多数针对你的 Linux 服务器的低级威胁，但残酷的现实是，像 `HTTP` 这样的服务要求你向广大互联网用户开放若干端口（`TCP 80` 以及有时是 `TCP 443`）。这迫使你在应用层实施完整的安全措施，包括认证、访问控制以及保护 `HTTP` 应用服务器本身。

此外，如果你的公司使用 `HTTP` 服务器进行电子商务，你需要确保交易的隐私性，并向你的潜在客户和合作伙伴提供强大的认证。这可以通过使用基础 `Apache HTTP` 发行版的 `SSL`（安全套接字层）扩展来实现。本章描述了两个你可以部署以确保 `HTTP` 交易隐私性和认证性的不同软件包：

- `mod_ssl`（`OpenSSL` 计划的一部分）

- `Apache-SSL`，`mod_ssl` 最初基于此构建

让我们从描述安装、配置和维护 `Apache HTTP` 服务器时涉及的安全特定问题开始讨论。

#### Apache HTTP 服务器

由 `Apache` 软件基金会开发，`Apache HTTP Web` 服务器可以说是自 Linux 操作系统诞生以来最成功的公共可用软件。`Apache` 团队是由地理上分散的开发者组成的群体，他们自愿投入时间来增强和维护 `HTTP` 服务器及其他项目，例如 `XML-Apache`（以及一个 `XML` 开发环境）和 `TomCat`（一个 `Java` 服务器参考实现）。目前，大约十分之六的 Web 服务器正在运行 `Apache` 的 `HTTP` 软件。这个数字是微软互联网信息服务（`IIS`，即 `Apache` 最接近的竞争者）的三倍。

`Apache` 最初源于美国国家超级计算应用中心（`NCSA`）开发的 `HTTP` 实现。`Apache` 得名于它最初是原始 `NCSA HTTP` 服务器的一个“打补丁”（`patchy`）版本这一事实。当 `NCSA` 暂时停止其 `HTTP` 项目的开发时，一群程序员建立了一个论坛，最终导致了第一个版本的 `Apache HTTP` 服务器（版本 `0.6.2`）于 1995 年 4 月发布。八个月后，该小组发布了 `Apache 1.0`，这是他们的第一个生产级服务器，支持多平台。

得益于全球六百万用户的持续关注，以及不断壮大的开发团队的努力，当前的 `Apache` 发行版是一个健壮、强大、可扩展且模块化的服务器。它在性能方面与商用 Web 服务器产品不相上下，并且在安全性方面往往超越它们。要了解 `Apache` 项目的更多信息，请访问 `Apache HTTP` 服务器项目主页 `www.apache.org/httpd`（图 7.1）。

接下来的部分将描述如何在考虑安全性的前提下配置现有的 `Apache` 安装。有关在 Linux 服务器上安装、配置和管理 `Apache` 的基本参考信息，请参阅 `Charles Aulds` 撰写的 *Linux Apache Web Server*（`Sybex`, 2001），该书是 `Craig Hunt Linux` 库系列的一部分。

### 图 7.1 Apache HTTP 服务器项目主页

![](img/3258bbaf790525f8c4eb25fabff7844a_202_0.png)

## 配置 Apache 安全性

传统上，`Apache` 服务器有三个独立的配置文件：

- `httpd.conf`：`httpd.conf` 是主配置文件。它包含控制服务器整体操作的指令，例如日志记录和管理服务器池。

- `srm.conf`：`srm.conf` 文件包含控制文件系统中命名空间和资源管理的指令，包括文件类型、目录索引和别名。

- `access.conf`：`access.conf` 文件包含针对各个目录的访问控制指令。

这三个文件位于同一个目录（通常是 `/etc/httpd/conf`）中，并在守护进程启动时按照上述顺序进行处理。然而，将所有指令放在单个文件中更容易；我建议为此目的使用 `httpd.conf`。

接下来的几节将讨论用于控制 `Apache` 服务器安全性的特定指令。所有这些指令都应包含在 `httpd.conf` 文件中。

### 身份验证

用户身份验证通常是在其他公开服务中的一项必要功能。`Apache HTTP` 服务器具有在授予用户其 `HTTP` 请求之前执行某些规则的能力。基于以下两个标准之一，用户可以被授予其 `HTTP` 请求：

- `HTTP` 请求方提供的用户名/密码

- 生成请求的主机 `IP` 地址
