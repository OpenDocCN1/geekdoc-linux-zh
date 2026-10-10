

*完全限定域名*（FQDN）是通过使用点（.）作为分隔符，将子域名从低级别到高级别依次串联起来构建的。*例如*，`REDHAT.COM` 是一个完全限定域名；`EE.UMD.EDU` 也是如此。请注意，其中每一个也可以指代一台特定的主机计算机。图 5-2 展示了完全限定域名的组成部分。

![](img/792720823146d68f19fd50c99ebfce4b_667_0.png)

域名不区分大小写。因此，就 DNS 而言，`UMD.EDU` 和 `umd.edu` 这两个域名都代表马里兰大学（University of Maryland）的域名。不过，惯例是全小写输入域名。

## 探索 Berkeley Internet Name Domain (BIND)

大多数 UNIX 系统（包括 Linux）都附带 BIND 系统——一种广为人知的 DNS 实现。在安装 Linux 时，只要你在选择安装软件包时选中了名称服务器，BIND 软件就会随之安装。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，输入 `dpkg -i bind*` 以查看是否已安装 BIND。在 Fedora Core 和 SUSE 中，输入 `rpm -q bind` 并查看是否已安装 `bind` 软件包。

在 Debian、MEPIS 和 Ubuntu 中，输入 `apt-get install bind9` 以安装 BIND。在 Fedora Core 中，以 `root` 身份登录，挂载 DVD，并输入 `cd /media/cdrom/Fedora/RPMS`，接着输入 `rpm -ivh bind*`。在 SUSE 中，在 YaST 控制中心的软件类别中点击*软件管理*。然后使用 YaST 的搜索功能查找 `bind`，选择相关的软件包并安装。在 Xandros 中，首先运行 Xandros Networks，选择 Edit→Set Application Sources，并点击 Debian Unsupported Site 链接作为来源。然后输入 `apt-get install bind9` 以安装 BIND 服务器。

BIND 包括三个主要组件：

-   named 守护进程——即名称服务器——它负责响应关于主机名和 IP 地址的查询
-   解析器库，应用程序可使用它将主机名解析为 IP 地址（反之亦然）
-   命令行 DNS 实用程序（DNS 客户端），例如 dig（Domain Internet Groper）和 host，用户可以使用它们来查询 DNS

我将在接下来的几个部分中描述 BIND 的这些组件。在后几节中，我将解释如何配置解析器和名称服务器。

### named— BIND 名称服务器

named 守护进程是响应主机名和 IP 地址查询的名称服务器。基于配置文件和本地 DNS 数据库，named 要么提供查询的答案，要么向其他服务器请求查询并缓存其响应。named 服务器还执行一项称为区域传输（zone transfer）的功能，这涉及在域内的名称服务器之间复制数据。

名称服务器以三种模式之一运行：

-   **主服务器或主节点：** 在这种情况下，名称服务器在磁盘上保留域名数据的主副本。每个域或子域都有一个主服务器。
-   **从服务器或从节点：** 从名称服务器使用区域传输操作从主服务器复制其域名数据。一个域可以有一个或多个从名称服务器。
-   **缓存：** 缓存名称服务器加载根域少数几个权威服务器的地址，并通过联系其他名称服务器已解析的查询响应来缓存获取所有域名数据。主服务器和从服务器也缓存响应。

根据*名称服务器*提供的信息，它可以是权威的或非权威的。顾名思义，权威名称服务器的响应应该是准确的。主服务器和从名称服务器对于其自身的域是权威的，但对于从缓存信息提供的响应则不是权威的。

![](img/792720823146d68f19fd50c99ebfce4b_668_0.png)

缓存名称服务器永远不是权威的，因为它们的所有响应都来自缓存信息。

要在你的 Linux 系统上运行名称服务器，你必须使用适当的配置文件运行 *named*。在本章的后面部分，你将了解控制名称服务器如何操作的配置文件和数据文件。

### 解析器库

查找主机名的 IP 地址被称为*解析主机名*。具备网络感知功能的应用程序（如 Web 浏览器或 FTP 客户端）使用*解析器库*来执行从名称到 IP 地址的转换。根据 `/etc/host.conf` 文件中的设置，解析器库会查阅 `/etc/hosts` 文件或发起 DNS 查询，以将主机名解析为其 IP 地址。解析器库查询 `/etc/resolv.conf` 文件中列出的名称服务器。

除非你正在编写具备网络感知功能的应用程序，否则你不需要了解太多的解析器库知识。要正确运行 Internet 服务，你只需要知道如何配置解析器即可。在本章的后面，我将向你展示如何配置服务器以及 DNS 的其他方面。

### DNS 实用程序

你可以使用 DNS 实用程序——`dig` 和 `host`——从 shell 提示符交互式地试用 DNS。这些实用程序是 DNS 客户端。你可以使用它们查询 DNS 数据库并调试你在系统上设置的任何名称服务器。默认情况下，这些程序查询系统 `/etc/resolv.conf` 文件中列出的名称服务器。

你可以使用 `dig`（Domain Internet Groper 程序）查找域名或 IP 地址。例如，要查找 `ftp.redhat.com` 的 IP 地址，请输入

```text
dig ftp.redhat.com
```

`dig` 会详细打印 DNS 查询的结果。在输出中标记为 `ANSWER SECTION` 的部分查找结果。例如，对于此示例查询，该部分看起来像这样：

```text
;; ANSWER SECTION:
ftp.redhat.com.        300 IN A 66.187.224.30
```

此输出意味着名称 `ftp.redhat.com` 指的是 IP 地址 66.187.224.30。

使用 `dig` 进行*反向查找*（查找 IP 地址的主机名）也很简单。例如，要查找与 IP 地址 209.132.176.30 对应的主机名，请输入以下内容：

```text
dig -x 66.187.224.30
```

同样，答案出现在输出的 ANSWER SECTION 中，对于这个例子，看起来像这样：

```text
;; ANSWER SECTION:
30.224.187.66.in-addr.arpa. 600 IN PTR ftp.redhat.com.
```

在这种情况下，与 IP 地址 66.187.224.30 对应的主机名恰好是 `ftp.redhat.com`。

你还可以通过使用 `host` 程序来查询 DNS。`host` 程序产生紧凑格式的输出。例如，这是使用 `host` 查找主机名的 IP 地址的典型用法：

```text
host www.gao.gov
```

此命令生成以下输出：

```text
www.gao.gov has address 161.203.16.2
www.gao.gov mail is handled by 5 listserv.gao.gov.
```

默认情况下，`host` 打印 IP 地址和任何 *MX 记录*（这些记录列出了主机邮件处理器的名称）。

要进行反向查找，请使用 `-t ptr` 选项，并将 IP 地址作为参数，如下所示：

```text
host -t ptr 161.203.16.2
```

以下是 `host` 的结果：

```text
2.16.203.161.in-addr.arpa domain name pointer www.gao.gov.
```

在这种情况下，`host` 打印 *PTR 记录*（来自 DNS 数据库），该记录显示了与 IP 地址对应的主机名。(*PTR 指*指针*，且* PTR *记录指定与地址对应的名称。)*

你也可以尝试其他类型的记录，例如 *CNAME*（规范名称），如下所示：

```text
host -t cname www.ee.umd.edu
```

`host` 的响应如下：

```text
www.ee.umd.edu is an alias for edison.eng.umd.edu.
```

此输出表明 `www.ee.umd.edu` 的*规范名称*（或别名）是 `edison.eng.umd.edu`。

## 配置 DNS

你通过使用多个配置文件来配置 DNS。具体的文件集取决于你是否正在运行名称服务器，如果是，则是名称服务器的类型——缓存型或主型。无论你运行名称服务器与否，都需要一些配置文件。

### 配置解析器

要使用 DNS 客户端（dig 和 host），你的系统上不需要运行名称服务器。你可以使用它们查询你所在域的名称服务器。通常，你的 ISP 会提供此信息。你必须在 `/etc/resolv.conf` 文件中列出这些名称服务器的 IP 地址——解析器库读取此文件以确定如何解析主机名。此文件的格式如下

```text
domain your-domain.com
search your-domain.com
nameserver A.B.C.D
nameserver X.Y.Z.W
```

其中 A.B.C.D 和 X.Y.Z.W 是主要和次要名称服务器的 IP 地址（点分十进制地址，例如 192.168.0.1），由你的 ISP 提供。

domain 行列出本地域名。search 行指定首先搜索的主机名所属的域（通常，你将自己的域放在 search 行中）。search 行列出的域会在解析器库尝试解析之前附加到任何主机名后面。例如，如果你查找名为 mailhost 的主机，解析器库会先尝试 mailhost.your-domain.com；如果失败，它会尝试 mailhost。search 行适用于你尝试访问的任何主机名。例如，如果你试图访问 www.redhat.com，解析器会先尝试 www.redhat.com.your-domain.com，然后尝试 www.redhat.com。

另一个重要的配置文件是 `/etc/host.conf` —— 此文件告诉解析器在尝试解析主机名时该怎么做。典型的 `/etc/host.conf` 文件包含以下行：

```text
order hosts,bind
```

此命令告诉解析器首先查阅 `/etc/hosts` 文件，如果失败，则查询 `/etc/resolv.conf` 文件中列出的名称服务器。`/etc/hosts` 文件通常列出任何本地主机名及其 IP 地址。以下是 `/etc/hosts` 文件中的一行典型示例：

```text
127.0.0.1    hnpb200    localhost.localdomain    localhost
```

