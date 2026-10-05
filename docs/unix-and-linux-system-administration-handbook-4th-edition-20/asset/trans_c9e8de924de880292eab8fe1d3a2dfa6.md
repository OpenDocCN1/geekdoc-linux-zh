

# 超越你的限制

以下是一段反向代理配置片段，用于在提供基于网络的电子邮件服务的 Microsoft Outlook (OWA) 服务器前插入一个 UNIX DMZ 系统。

```
<rpc>
ProxyPass https://wm.monkeypaw.com/rpc
ProxyPassReverse https://wm.monkeypaw.com/rpc
SSLRequireSSL
</rpc>
<exchange>
ProxyPass https://wm.monkeypaw.com/exchange
ProxyPassReverse https://wm.monkeypaw.com/exchange
SSLRequireSSL
</exchange>
<exweb>
ProxyPass https://wm.monkeypaw.com/exweb
ProxyPassReverse https://wm.monkeypaw.com/exweb
SSLRequireSSL
</exweb>
<public>
ProxyPass https://wm.monkeypaw.com/public
ProxyPassReverse https://wm.monkeypaw.com/public
SSLRequireSSL
</public>
<oma>
ProxyPass https://wm.monkeypaw.com/oma
ProxyPassReverse https://wm.monkeypaw.com/oma
SSLRequireSSL
</oma>
<Microsoft-Server-ActiveSync>
ProxyPass https://wm.monkeypaw.com/Microsoft-Server-ActiveSync
ProxyPassReverse https://wm.monkeypaw.com/Microsoft-Server-ActiveSync
SSLRequireSSL
</Microsoft-Server-ActiveSync>
```

在此示例中，代理服务仅为几个顶级 URL 提供了服务：/rpc、/exchange、/exweb、/public、/oma 和 /Microsoft-Server-ActiveSync。出于安全考虑，限制允许通过代理的请求是一个明智的主意。

# 23.6 越你的限制进行扩展

在网络上，“一夜之间的成功”可能是系统管理员的噩梦。在热门博客上被提及，或者在 dig.com 上显示出“真实”的人气增长，可能会迅速超出你本地服务器的容量或网络连接的带宽。但不要担心；这些是令人欢迎的问题，而且有很多可能的解决方案。

# 第 23 章 Web 托管

# 云计算

有关云计算的更多信息，请参阅第 24 章“虚拟化”。

云托管让你能够访问你所选择的操作系统的虚拟化实例，而无需在你的现场安置硬件。事实上，硬件及其维护被完全抽象了——你只拥有关于虚拟化实例实际运行位置的最通用理想。

市场上存在许多云提供商，但亚马逊凭借其 Amazon Web Services (AWS) (aws.amazon.com) 仍然是先驱和市场领导。在不到 5 分钟内，你可以启动一个新的 Linux 或 Unix 实例。你通过 ssh 登录并管理它，就像管理你自己数据中心中的系统一样。最重要的是，该服务极其廉价（目前美国地区最低服务层级每小时约为 10 美分）。

在云之上可以层叠多种服务，以根据负载或其他条件自动将服务器上线或离线。亚马逊的原生设施称为 Auto Scaling（自动扩展）。ScaleRight (rightscale.com) 是一个销售集成良好的扩展服务的第三方提供商。

# 共同托管 (Co-hosting)

托管托管是在远程数据中心中托管你的系统的另一种方式，但在托管托管场景下，你通常拥有或租用服务器硬件。在标准或监管要求禁止使用云数据中心（例如某些涉及 PCI DSS 的情况）或需要自定义硬件的情况下，这种安排可能比基于云的解决方案更好。某些 I/O 密集型应用程序在专用硬件上的运行得也更好，尽管虚拟化世界正在迅速追赶。

有关数据中心分级的更多信息，请参阅第 27 章。

有数百个托管提供商。根据 Uptime Institute (uptimeinstitute.org) 定义的你的需求选择一个合适的层级。商业应用程序通常托管在 Tier 3 或 Tier 4 数据中心中。

# 内容分发网络

互联网上的大部分内容都是静态的：图像、文档、软件安装包。通过将这些静态组件放置在用户附近（在网络术语中），你可以减少或消除从原始源提供这些数据并跨越网络骨干传输数据的需求。

提供此类服务的计算机系统被称为内容分发网络，或 CDN。跨洲网络链路通常很拥挤，因此当需要访问其他大陆的热内容时，CDN 特别重要。

大多数 CDN 作为营利性事业运营，由内容提供者资，以确保他们在扩展自身基础设施时网站的可用响应速度。Akamai Technologies (akamai.com) 运营着最成功且最著名的 CDN 平台。Limelight (limelynetworks.com) 和迪士尼拥有的 EdgeCast (edgecast.com) 是最大的后起者。

# 练习

当实施正确时，使用 CDN 对终端用户是完全透明的。某些对象可能来自较本地的服务器或缓存，而其他对象可能直接源自源。然而，这种透明性是有高昂代价。你需要一个大钱包才能将 CDN 包含在你的托管计划中。

# 23.7 练习

E23.1 在你的工作站上配置一个虚拟接口。在配置前后运行 `ifconfig` 查看发生了什么变化。你能从同一子网的另一台机器 ping 通该虚拟接口吗？从不同的网络可以吗？为什么可以或为什么不行？（需要 root 权限。）

E23.2 在你的浏览器中，访问一个内容丰富的热门网站（如 abcnews.com）并查看页面源代码（Firefox 中是“查看->页面源代码”，IE 中是“文件->查看”）。使用 dig 查询单个对象 URL 对应主机的 DNS 条目。你能确定哪些对象是由 Web 服务器托管的吗？

- E23.3 使用数据包嗅器 (tcpdump) 捕获上传信息的双向 HTTP 会话（例如填写表单或搜索字段）。注释句子以显示你的浏览器如何向 Web 服务器传递信息。（需要 root 权限。）

- E23.4 使用数据包嗅器在你打开繁忙的网页（如 amazon.com 或 cnn.com 的首页）时捕获流量。打开了多少个独立的 TCP 连接？是谁发起的？系统可以变得更高效吗？（需要 root 权限。）

- E23.5 定位来自互联网可访问的 Web 服务器的日志文件，也许是你网站的主服务器。检查日志文件。关于几周内的访问模式你可以说明些什么？在此期间出现了哪些错误？日志文件的内容说明了哪些隐私问题？（可能需要 root 权限）

- E23.6 在你的系统上安装 Apache 并创建几个内容页面。从其他机器验证你的 Web 服务器正在运行。找到 Apache 日志文件，让你看到哪些浏览器正在访问你的服务器。配置 Apache 将其某些内容页面提供给 E23.1 中的虚拟接口。（需要 root 权限。）

# 第三部分
各种东西

![](img/579efec8c67772f31ecf3484bbb71a2_1029_0.png)

# 24 虚拟化

企业数据中心不断堆叠服务器以满足现代业务对信息贪渴的需求，系统管理员面临着一个技术困境：如何更有效地管理现有系统以节省电力、空间和冷却成本，同时继续满足用户需求？

软件供应商历史上一直反对管理员与其他软件一起运行他们的程序，理由是潜在的不兼容性，在某些情况下甚至威胁说要在不合规的情况下停止支持。结果是单用途服务器的泛滥。

解决这一困境的答案是虚拟化：允许在同一物理硬件上同时运行多个独立的操作系统。管理员可以将每个虚拟机视为一个独特的服务器，从而在满足挑剔供应商（在大多数情况下）的同时，减少数据中心成本。各种硬件平台都支持虚拟化，而虚拟化特定 CPU 指令的发展以及多核处理器的日益普及极大地提高了性能。虚拟服务器易于安装，且比物理机器所需的维护工作更少。

