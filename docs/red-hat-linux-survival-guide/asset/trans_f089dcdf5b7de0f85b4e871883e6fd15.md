
将使用 your_username 和 your_password 作为密码登录。macdef init 行定义了一个初始化宏，它只是一系列你希望客户端程序自动执行的命令列表。这里第一个命令是 bin，用于设置二进制传输模式；下一个命令切换提示模式；cd /some/path 命令更改 FTP 服务器上的路径，然后使用 get filename 命令下载文件，最后使用 quit 命令终止连接。

![](img/9eb7e89292d2f85707b4d49102c865b7_459_0.png)

> 请注意，最后一个命令（quit）之后有两个空行；这表示该宏在此结束。

你可以添加多个机器记录，以便对常用的 FTP 服务器自动化 FTP 上传或下载。

![](img/9eb7e89292d2f85707b4d49102c865b7_459_1.png)

> 你必须将 .netrc 文件权限设置为 600，以便只有文件所有者可以读取或写入该文件。你可以运行 chmod 600 ~/.netrc 命令来设置此权限。

尽管上述权限设置确保除所有者之外无人可以读取 .netrc 文件，但如果你不希望将密码保存在仅通过权限设置保护的文本文件中，你可能希望删除密码行。这样你仍然可以使用 .netrc 提供的自动化功能，只是例外情况是你将被提示一次输入密码。

当 FTP 客户端找不到要连接的 FTP 服务器的匹配机器记录时，它会查找要使用的默认设置。例如，你可以将以下行作为 .netrc 文件中的最后一行添加：

```
default login anonymous password your@email_address
```

现在，每当你尝试连接 .netrc 中没有机器记录的 FTP 站点时，它将使用默认登录（anonymous）。

![](img/9eb7e89292d2f85707b4d49102c865b7_459_2.png)

> 如果你连接了许多非匿名 FTP 站点并且不希望在 .netrc 文件中添加它们，这可能并不理想。

## 第 15 章
### 配置 DNS
### 本章内容
- 理解 DNS 配置
- 将 Red Hat Linux 系统设置为 DNS 客户端
- 设置 BIND DNS 服务器
- 使用 bindconf 配置 DNS 服务器
- 管理 DNS 服务器
- 为虚拟域设置 DNS
- 使用 Dlint 验证 DNS 配置
- 保护 DNS

域名系统（DNS）使互联网更易于使用。DNS 背后的基本思想是允许主机名转换为 IP 地址。在本章中，我将向你展示如何将 Red Hat Linux 系统配置为 DNS 客户端，以及如何使用最广泛使用的 DNS 服务器软件 BIND 在你的系统上设置 DNS 服务器。我还将向你展示如何验证你的 DNS 配置并增强其安全性。

## 配置 DNS 客户端

如果你计划从 Red Hat Linux 系统访问其他互联网主机计算机，你需要将其配置为 DNS 客户端系统。DNS 的客户端部分称为解析器。解析器是 C 库中的一组例程，允许任何程序执行 DNS 查询。解析器随 Red Hat Linux 标准提供。在本节中，你将学习如何配置解析器。

通常，Red Hat 安装程序会询问你的 DNS 服务器并自动配置必要的解析器配置文件。然而，经常需要更改解析器配置以反映你使用的 DNS 服务器的任何更改。例如，如果你在 Red Hat 安装期间配置了解析器，后来更改了你的 ISP，你需要手动重新配置它。本节将向你展示如何操作。

如果你计划使用 ISP 的 DNS 服务器来解析名称和 IP 地址，请向你的 ISP 询问其 DNS 服务器的主机名和 IP 地址。获得所需信息后，你可以配置解析器。

首先你需要修改名为 /etc/resolv.conf 的解析器配置文件。列表 15-1 显示了名为 evoknow.com 的域的典型 /etc/resolv.conf 文件。

### 列表 15-1 一个示例 /etc/resolv.conf 文件

```
# Default Domain
domain evoknow.com

# Default search list
search evoknow.com

# First name server
nameserver 206.171.50.50

# Second name server
nameserver 206.171.50.55
```

像许多其他常见的 Linux 配置文件一样，此文件具有非常简单的格式。任何空行或以 # 开头的行都被忽略。唯一有意义的行是带有 domain、search 或 name server 指令的行。

domain 指令使你能够指定系统的默认域名。如果你没有将此行设置为系统的域名，默认域名将自动从系统的主机名中提取。

search 指令用于影响解析器如何搜索未完全限定的主机名。例如，如果我想在具有前面解析器配置文件的系统上的 shell 中输入 ping www 命令，ping 程序会要求解析器解析 www。因为 www 是一个部分主机名，解析器使用搜索列表创建一个完整主机名（例如 www.evoknow.com）并尝试为该主机解析 IP。例如，如果我将前面的列表中的 search 指令设置为 integrationlogic.com 并发出相同的 ping 请求，解析器将返回 www.integrationlogic.com 的 IP 地址。如果你没有提供 search 指令，当需要解析部分主机名时，默认域名将自动应用。

name server 指令指定解析器应用于查询的域名服务器。你可以在配置文件中（并且应该）指定多个 name server 指令。每个域名服务器按配置文件中出现的顺序进行查询。例如，如果程序要求解析器解析名为 www.ad-engine.com 的主机名，解析器首先尝试使用 206.171.50.50 域名服务器将名称解析为 IP。如果 206.171.50.50 域名服务器未能返回响应（即查询超时），则会联系第二个域名服务器 206.171.50.55。目前，你只允许在配置文件中列出三个 name server 指令。一般来说，最好至少设置两个 name server 指令指向两个不同的名称服务器。

![](img/9eb7e89292d2f85707b4d49102c865b7_462_0.png)

你可以将 name server 指令设置为互联网上任何域名服务器的 IP 地址。然而，你应该只使用最近的域名服务器 IP 地址以减少域名解析的延迟。此外，切勿在未经许可的情况下在解析器配置文件中使用他人的域名服务器 IP 地址。这被认为是不礼貌的，如果你的解析器给某人的名称服务器带来沉重负载，可能会产生法律后果。

到目前为止，你已经学习了如何配置系统上的 DNS 解析器以使用远程 DNS 服务器。也可以在 /etc/hosts 文件中将一个或多个 IP 地址硬编码到其各自的主机名中。此文件具有非常简单的格式如下：

```
IP address hostname short_cut hostname
```

以下是 /etc/hosts 文件的示例：

```
206.171.50.50 picaso.evoknow.com picaso
127.0.0.1 localhost localhost
```

当远程 DNS 服务器不可用时，解析器可以使用此文件解析地址。此外，如果你有一个小型网络并且不想运行本地 DNS 服务器，你可以使用此文件解析本地主机名。然而，当远程 DNS 服务器和 /etc/hosts 文件都可用时，解析器需要知道以何种顺序处理 DNS 查询。你可以使用 /etc/host.conf 文件中的 order 指令设置顺序。例如：

```
order hosts,bind
```

如果你的 /etc/host.conf 文件具有此 order 指令，则解析器首先尝试使用 /etc/hosts 文件为查询提供服务。如果文件中不包含可用的条目，则使用 /etc/resolv.conf 文件中指定的 DNS 服务器。

![](img/9eb7e89292d2f85707b4d49102c865b7_463_0.png)

如果你有大量用户，可以通过使用本地 DNS 服务器而不是 /etc/hosts 文件来提高与 DNS 相关的性能，因为每次新的 DNS 请求时读取文件可能非常慢。

设置完上面描述的文件后，你的 DNS 解析器配置就完成了。测试 DNS 配置最简单的方法是尝试 ping 互联网上的计算机。如果 ping 程序因未知主机名而失败，请仔细检查你的 DNS 解析器配置是否有拼写错误。

运行自己的 DNS 服务器有相当多的管理优势。例如，如果你拥有一个或多个互联网域名，你可以根据需要添加、删除或修改 DNS 记录。在下一节中，你将学习如何在 Red Hat Linux 系统上设置 DNS 服务器。

## 安装 BIND DNS 服务器

Red Hat Linux 附带 Berkeley Internet Name Domain（BIND）服务器软件。如果你没有在操作系统
