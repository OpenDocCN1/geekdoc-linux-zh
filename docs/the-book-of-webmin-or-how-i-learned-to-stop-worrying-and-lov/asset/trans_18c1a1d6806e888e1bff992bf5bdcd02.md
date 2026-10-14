

## 代理 IP 地址

客户端连接所在的本地 IP 地址。这允许在代理上存在多个接口时构建仅匹配一个物理网络的 ACL，等等。此选项配置 myip 指令。

## RFC931 用户

由客户端机器上运行的 ident 守护进程提供的用户名。这要求 ident 必须在要以这种方式进行身份验证的任何客户端机器上运行。Ident 在安全性方面不应被视为安全，除非在私有网络上，在那里安全性不是很重要。你可以找到以下操作系统的免费 ident 服务器：Win NT [http://info.ost.eltele.no/freeware/identd/]、Win 95/Win 98 [http://identd.sourceforge.net/]，以及 UNIX [http://www2.lysator.liu.se/~pen/pidentd/]。大多数 UNIX 系统，包括 Linux 和 BSD 发行版，都包含一个 ident 服务器。

## 请求方法

此 ACL 类型匹配请求头中的 HTTP 方法。这包括方法 GET、PUT 等等。这对应于 method ACL 类型指令。

## URL 路径正则

此 ACL 匹配 URL 路径，去除了任何协议、端口和主机名信息。它不包括例如请求中的 "http://www.swelletech.com" 部分，只留下对象实际的路径。此选项与 urlpath_regex 指令相关。

## URL 端口

此 ACL 匹配请求的端口号，并配置 port ACL 指令。

## URL 协议

此 ACL 匹配请求的协议，例如 FTP、HTTP、ICP 等等。

## URL 正则

使用正则表达式匹配完整的 URL。此 ACL 可用于根据 URL 的部分提供访问控制，或对 URL 进行不区分大小写的匹配，以及更多。Squid 中使用的正则表达式由 GNU Regex 库提供，其文档见第 7 节和第 3 节 regex 手册页。正则表达式也在 Guido Socher 在 LinuxFocus 上的一篇不错的文章中简要讨论 [http://www.linuxfocus.org/English/July1998/article53.html]。此选项等同于 url_regex ACL 类型指令。

## Web 服务器地址

此 ACL 根据目标 Web 服务器的 IP 地址进行匹配。Squid 支持单个 IP、带网络掩码的网络 IP，以及 "192.168.1.1-192.168.1.25" 形式的地址范围。此选项与 dst ACL 类型指令相对应。

## Web 服务器主机名

此 ACL 匹配目标 Web 服务器的主机名。

## Web 服务器正则

使用正则表达式匹配目标 Web 服务器的主机名。

有关 Squid 中访问控制列表的更多信息，可在 Squid FAQ 的 [第 10 节 http://www.squid-cache.org/Doc/FAQ/FAQ-10.html] 中找到。身份验证信息可在 Squid FAQ 的 [第 23 节 http://www.squid-cache.org/Doc/FAQ/FAQ-23.html] 中找到。

## 管理选项

管理选项提供了对 Squid 背后多个选项的访问。此页面允许你配置多样化的选项，包括 Squid 进程的用户 ID 和组 ID、缓存层级公告设置以及身份验证领域 [图 12-17]。

![](img/d84604054810a13cacfdac212ebee2f7_264_0.png)

图 12-17：管理选项

## 以 Unix 用户和组运行

Squid 将作为其运行的用户名和组名。Squid 设计为以 root 启动，但在不久后会切换到此处指定的用户/组。这允许你出于安全原因限制 Squid 运行时的权限。虽然 Squid 在数千个站点数年的使用中已证明自己相当安全，但采取额外的预防措施以避免问题永远不是坏事。默认情况下，Squid 将作为 nobody 用户和 nogroup 组运行，或在某些从 RPM 安装的 Squid 中作为 squid 用户和组运行。这些选项与 cache_effective_user 和 cache_effective_group 指令相对应。

## 代理身份验证领域

在执行身份验证时将向客户端报告的领域。此选项通常默认为 Squid proxy-caching web server，并与 proxy_auth_realm 指令相对应。此名称很可能会出现在浏览器弹出窗口中，当客户端被要求提供身份验证信息时。

## 缓存管理器电子邮件地址

此缓存管理员的电子邮件地址。此选项对应于 cache_mgr 指令，并在基于 RPM 的系统上默认为 webmaster 或 root。此地址将被添加到显示给客户端的任何错误页面中。

## 可见主机名

Squid 将在其上自我宣传的主机名。这会影响 Squid 在提供错误消息时使用的主机名。如果你在缓存集群中收到 IP 转发错误，则可能需要配置此选项。此选项配置 visible_hostname。

## 唯一主机名

配置 unique_hostname 指令，并为 Squid 在缓存集群中报告设置一个唯一主机名，以便检测转发循环。如果你的集群中有多台机器具有相同的可见主机名，请使用此选项。

## 缓存公告主机、端口和文件

Squid 将用于宣布其参与缓存层级的可用性的主机地址和端口。缓存公告文件只是一个包含要随公告发送的消息的文件。这些选项对应于 announce_host、announce_port 和 announce_file 指令。

## 公告周期

配置 announce_period 指令，并指 Squid 将向公告主机发送公告消息的频率。

## 杂项选项

杂项选项正是其名称所暗示的：一些似乎无处可归的杂项选项。在这里你会找到几个与内存相关的选项、关于头信息和用户代理设置的选项，以及强大的 HTTP 加速器选项 [图 12-18]。

## 启动 DNS 测试地址

这应指向 Squid 可用于测试你的网络上 DNS 服务是否正常工作的多个主机。如果 DNS 不能正常工作，Squid 将无法提供服务，因此它将拒绝启动，并在 cache.log 中简要说明原因。建议你选择两个或更多互联网上的主机名，以及你内部网上的一个或两个主机名，假设你有内部网并且 Squid 预期为其提供服务。默认情况下，dns_testnames 指令检查一些知名且流行的站点：netscape.com、internic.net、nlanz.net 和 microsoft.com。

![](img/d84604054810a13cacfdac212ebee2f7_266_0.png)

图 12-18：杂项选项

## SIGUSR1 日志文件轮转

Squid 将保留的旧轮转日志文件的数量。在 Red Hat 系统上，此选项默认为零，因为日志是通过系统标准的 logrotate 程序轮转的。在其他系统上，这默认为 10，这意味着 Squid 将在覆盖最旧文件之前保留 10 个旧日志文件。此选项对应于 logfile_rotate 指令。

## 默认域

Squid 将附加到不是完全限定域名（更准确地说，是其中不包含点的）的请求的域。此选项与 append_domain 指令相关。

## 错误消息文本

提供一种自动向 Squid 的错误页面添加一些额外信息的方法。你可以在此处添加 HTML 或纯文本注释或链接，这些内容将被添加到显示给客户端的错误消息中。此选项与 err_html_text 指令相关。

## 每客户端统计？

允许你选择 Squid 是否会保留有关每个单独客户端的统计信息。此选项配置 client_db 指令，默认为开启。

## X-Forwarded-For 头？

此选项允许你选择 Squid 是否会向源服务器报告最初发出请求的系统的主机名。例如，如果此选项被禁用，则通过你的缓存的所有请求都将被报告为源自缓存。通常，这应保持启用。此选项与 forwarded_for 指令相关，默认为开启。

## 记录 ICP 查询？

决定 Squid 是否会记录 ICP 请求。如果 ICP 负载非常高，禁用此项可能是一个好主意。此选项与 log_icp_queries 指令相关，默认为开启。

## 最小直接跳数

在使用 Squid 的 ICMP ping 功能确定到对等方和源服务器的距离时，这会配置 Squid 何时应更倾向于直接连接而不是通过对等方。此选项要求你的 Squid 使用 --enable-icmp 编译，并且你必须与其他 Squid 缓存处于对等关系中，这些缓存也使用适当的构建选项编译。此选项与 minimum_direct_hops 指令相关。

## 保留内存以备将来使用？

此选项打开 memory_pools 并允许 Squid 保留已分配但不再需要的内存，以便将来无需重新分配内存。这可以小幅提高性能，但在系统内存紧张时可能需要关闭。此选项默认为开启，通常应保持开启，除非你知道自己在做什么。

## 保留内存量

Squid 将保留已分配的内存量，假设已打开“保留内存以备将来使用”选项。此选项配置 memory_pools_limit 指令，默认为无限制。任何非零值都会指示 Squid 不保留超过该量的分配内存，如果 Squid 需要更多内存来满足请求，它将使用你系统的 malloc 库。Squid 不预先分配内存，因此将其设置得合理地高是安全的。如果你的 Squid 运行在专用主机上，最明智的做法是将其保持为默认的无限制。如果它必须与其它服务器进程（如 Apache 或 Sendmail）共享系统，则可能适当限制一些。

## 要透传的头信息

配置 Squid 的匿名化功能。此选项允许你规定允许通过 Squid 的请求头类型。例如，为防止源服务器能够检测客户端使用的浏览器类型，你将选择允许除 User-Agent 之外的所有头。此选项用途大多晦涩，通常无需从其默认允许所有头透传的设置中更改。有一个相关的 Squid FAQ 部分 [http://www.

