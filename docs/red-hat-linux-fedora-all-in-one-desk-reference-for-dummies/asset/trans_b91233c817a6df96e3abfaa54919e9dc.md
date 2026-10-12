
## 第5章：设置 DNS 和 NIS
### 本章内容
- ✔ 了解 DNS
- ✔ 了解 BIND
- ✔ 配置 DNS
- ✔ 设置缓存名称服务器
- ✔ 配置主名称服务器
- ✔ 了解 NIS
- ✔ 配置 NIS 服务器和客户端
- ✔ 尝试使用 NIS

域名系统（DNS）是一种 Internet 服务，它将完全限定域名（如 www.redhat.com）转换为对应的 IP 地址（如 216.148.218.195）。你可以将 DNS 视为 Internet 主机的目录——正是因为 DNS，你可以使用易于记忆的主机名，即使 TCP/IP 在数据传输中需要数字 IP 地址。DNS 基本上是一个分布式的 DNS 服务器层级结构。在本章中，我将概述 DNS，并向您展示如何在 Red Hat Linux 系统上设置缓存 DNS 服务器。

网络信息系统（NIS）是另一项客户端/服务器服务，旨在管理网络上多个主机计算机之间共享的信息。通常，NIS 在局域网（LAN）上的一组主机为 UNIX 或 Linux 系统维护一组公共的用户账户和其他系统文件。此服务等使用户能够使用相同的用户名和密码登录所有主机。本章简要介绍了 NIS 客户端和服务器软件，并向您展示如何在 Red Hat Linux 系统上使用它们。

### 了解域名系统（DNS）
在 TCP/IP 网络中，每个网络接口（例如以太网卡或拨号调制解调器连接）都由一个 IP 地址标识。由于 IP 地址难以记忆，因此会为 IP 地址分配一个易于记忆的名称——就像电话号码与姓名相对应一样。例如，您无需记住 Red Hat Web 服务器的 IP 地址为 216.148.218.195，只需通过其名称 www.redhat.com 来引用该主机即可。当您在 Web 浏览器中输入 www.redhat.com 作为 URL 时，该名称必须被翻译成对应的 IP 地址。这就是 DNS 概念发挥作用的地方。

### 什么是 DNS？
域名系统是一个分布式、分层的数据库，用于保存有关 Internet 上计算机的信息。这些信息包括主机名、IP地址和邮件路由规范。由于这些信息存储在 Internet 上的许多 DNS 主机中，因此 DNS 被称为分布式数据库。DNS 的主要任务是将主机名与 IP 地址关联起来，反之亦然。

在 ARPANET——当今 Internet 的前身——主机名及其对应 IP 地址的列表保存在名为 HOSTS.TXT 的文本文件中，该文件由中央管理并定期分发给网络上的每台主机。随着主机数量的增长，维护这张静态主机表很快变得不合理。Paul Mockapetris 提出了 DNS 以缓解静态主机表的问题。正如在请求评论（RFC）882 和 883 中正式记录的那样（1983 年 11 月发布，参见 www.faqs.org/rfcs/rfc882.html 和 www.faqs.org/rfcs/rfc883.html），原始 DNS 引入了两个关键概念：
- 使用分层域名，例如 www.ee.umd.edu 和 www.redhat.com
- 通过在整个 Internet 上使用 DNS 服务器来分担管理主机数据库的责任

我们今天所知的 DNS 是一项在 RFC 1034 和 1035 中记录的 Internet 标准。该标准已被其他多个 RFC 更新和扩展——1101、1183、1348、1876、1982、1996、2065、2181、2136、2137、2308、2535、2845 和 2931。较早的更新定义了数据编码，而较新的更新则侧重于改进 DNS 安全。要在线阅读这些和其他 RFC，请访问俄亥俄州立大学的 Internet RFC 页面，网址为：

```
www.cis.ohio-state.edu/hypertext/information/rfc.html
```

DNS 定义了以下内容：
- 用于主机的分层域名系统。
- 一个将每个域名与 IP 地址关联的分布式数据库。
- 库例程（解析器），网络应用程序可使用它来查询分布式 DNS 数据库。（该库称为 *resolver library*。）
- DNS 客户端和服务器之间交换名称和 IP 地址信息的协议。

如今，Internet 上的所有主机都依赖 DNS 来访问远程主机上的各种 Internet 服务。正如您从个人经验中可能知道的那样，当您从 Internet 服务提供商（ISP）获得 Internet 访问权限时，您的 ISP 会为您提供名称服务器的 IP 地址——每当主机名需要映射到 IP 地址时，您的系统就会访问这些 DNS 服务器。

如果您有一个小型局域网，您可以决定在一台主机上运行 DNS 服务器，或使用 ISP 提供的名称服务器。对于使用多个子网的中型网络，您可以在每个子网上运行 DNS 服务器以提供高效的 DNS 查找。在大型企业网络中，企业域（如 microsoft.com）会进一步细分为子域层级；每个子域中可能会使用多个 DNS 服务器。

在下面的章节中，我将概述分层域名命名约定，并介绍 BIND——在大多数 UNIX 系统（包括 Red Hat Linux）上使用的 DNS 软件。

### 学习分层域名
DNS 使用域的层次树来组织命名空间——整个名称集合。每个更高级别的域对其下级子域具有管理权限。每个域代表命名空间的一个独立块，并由单一的管理机构管理。图 5-1 说明了 DNS 命名空间的层次组织。

Figure 5-1:
The DNS namespace is organized in a hierarchy.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_698_0.png)

树的根称为根域，由一个点（.）表示。接下来是顶级或根级域。顶级域进一步细分为二级域，而二级域又可以细分为更低的子域。

顶级域相对固定，包括众所周知的域，如 COM、NET、ORG、EDU、GOV 和 MIL。这些是美国常用的顶级域。这些顶级域是在 20 世纪 90 年代初 Internet 普及时出现的。

还有一组用于国家的顶级域名。这些域名使用国际标准化组织（缩写为 ISO；参见 www.iso.ch）分配的两字母国家代码。例如，美国的顶级国家代码域是 US。在美国，许多地方政府和组织使用 US 域。例如，mcps.k12.md.us 是美国马里兰州蒙哥马利县公立学校的域名。

完全限定域名（FQDN）是通过将子域名从低级到高级串联起来，使用点（.）作为分隔符构造的。例如，REDHAT.COM 是一个完全限定域名；EE.UMD.EDU 也是如此。请注意，这些也可能指特定的主机计算机。图 5-2 说明了完全限定域名的组成部分。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_699_0.png)

域名不区分大小写。因此，就 DNS 而言，域 UMD.EDU 和 umd.edu 都代表马里兰大学的域。然而，通常的做法是以全小写输入域名。

### 探索伯克利 Internet 域名（BIND）
大多数 UNIX 系统，包括 Red Hat Linux，都附带 BIND 系统——一种众所周知的 DNS 实现。只要在选择安装包时选择 DNS 名称服务器包组，BIND 软件就会在 Red Hat Linux 安装期间安装。

要查看 Red Hat Linux 系统上安装的 BIND 版本，请键入以下命令：

```
rpm -q bind
```

如果安装了 BIND，此命令应显示类似以下的行，其中包含 RPM 文件的版本号：

```
bind-9.2.2-19
```

正如此输出所示，我的系统上安装了 BIND 版本 9.2.2。

BIND 包含三个主要组件：
- The named daemon — the name server — that responds to queries about host names and IP addresses
- A resolver library that applications can use to resolve host names into IP addresses (and vice versa)
- Command line DNS utility programs (DNS clients), such as dig (Domain Internet Groper) and host that users can use to query DNS

我将在接下来的几节中描述 BIND 的这些组件。在后面的章节中，我将解释如何配置解析器和名称服务器。

### named — BIND 名称服务器
named 守护进程是响应主机名和 IP 地址查询的名称服务器。根据配置文件和本地 DNS 数据库，named 要么提供查询的答案，要么向其他服务器查询并缓存其响应。named 服务器还执行称为区域传输的功能，该功能涉及在域中的名称服务器之间复制数据。

名称服务器以三种模式之一运行：
- Primary or Master — In this case, the name server keeps the master copy of the domain's data on disk. There is one primary server for each domain or subdomain.
- Secondary or Slave — A secondary name server copies its domain's data from the primary server using a zone transfer operation. You can have one or more secondary name servers for a domain.
- Caching — A caching name server loads the addresses of a few authoritative servers for the root domain and gets all domain data by caching responses to queries it has resolved by contacting other name servers. Primary and secondary servers also cache responses.
