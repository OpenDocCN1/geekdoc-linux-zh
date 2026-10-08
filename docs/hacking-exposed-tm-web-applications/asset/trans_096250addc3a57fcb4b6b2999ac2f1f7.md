

# 第3 章：破解 Web 服务器

身份认证。对 `/admin/Docs/` 目录的请求不需要。可以从 `/admin/Docs/` 目录获取 `default.cfg` 文件：

```
[rohan]$ echo -e "GET /admin/Docs/default.cfg HTTP/1.0\n\n" \
| nc www.victim.com 27556
```

```xml
<?XML Version="1.0"?>
<!-- 在向此文件添加任何条目之前， -->
<!-- 请先阅读说明书中的配置部分 --> -->
<!-- SYSTEM -->
<!-- PATHS -->
<!-- PORTS -->
<!-- PASSWORDS -->
<Var MonitorPassword="Re14nt13"/>
```
```

为了强调密码的存在，已删除了部分内容。该文件还将提供有关其他端口、URL、完整路径名和数据库的有用信息。

> > > 请务必牢记这个漏洞。不当的目录访问限制允许任何用户访问配置文件。我们在第 4 章中讨论对应用程序进行调查时，这是你在目标应用程序中寻找的漏洞之一。

# RealServer 应对措施

对 `/admin/Docs` 目录应用适当的 ACL。

# Lotus Domino

Lotus Domino 是 IBM 的协作平台，已像其他平台一样转向了以 Web 为中心。审查 Lotus Domino 服务器的第一步是列出它的数据库（.nsf 文件）并检查它们的访问权限。可能存在几个常见文件（这听起来像是自动化扫描器的工作！）。以下是几个高关注文件：

- *Admin.nsf*
- *Admin4.nsf*
- *Catalog.nsf*
- *Events4.nsf*
- *Names.nsf*
- *Setup.nsf*

更完整的列表（包括一个用于 Stealth 漏洞扫描器的文件）可以在 http://domilockbeta.2y.net/web/domilock/domilock.nsf/pages/rulesstealth 找到。

# Web 应用破解 (Hacking Exposed Web Applications)

（我们将在接下来的章节“自动化漏洞扫描软件”中讨论 Stealth）。

这些文件提供了关于用户、文件系统、日志信息、对等体信息以及服务器其他数据的丰富信息。

# Servlet 引擎

Java 和 servlet 破解本身就是一个领域。某些引擎有特殊的癖，某些漏洞在各个引擎之间共享。最有用的利用程序之一是信息泄露攻击。旧版本的 BEA WebLogic 和 Apache Tomcat 会受到 %70 攻击。通常情况下，对如 http://www.victim.com/login.jsp 等 URL 的请求会显示页面。然而，对 http://www.victim.com/login.js%70 的请求将导致显示 login.jsp 的源代码。这之所以有效，是因为 %70 代表字母 p，它创建了 .js 扩展名，但当解析引擎将 .js%70 解释为 .jp 时，它认为这是一个静态的、不可执行的脚本。

一个类似的漏洞会泄露目录列表。在这种情况下，提交的 URL 包含 %3f.jsp。例如，http://www.victim.com/private/%3f.jsp 返回 `/private/` 目录的目录列表。%3f 值对应于正斜杠 (\/)。

# 杂项 Web 服务器破解技术

如第 1 章所述，Web 应用通常位于外围技术之上，例如负载均衡器和代理服务器。本节简要回顾了如何绕过或颠覆此类技术，以直接访问 Web 服务器。

# 使用反向代理映射到网络

正常的代理配置允许内部网络上的主机为互联网上的 Web 站点发送 HTTP 请求。配置不当的代理允许互联网主机为主代理内部网络上的站点发送 HTTP 请求，甚至对于不可路由的 IP 地址（如 10.0.3.4）。

第一步是识别代理。这种攻击针对代理的功能，该漏洞基于配置不当而非错误的配置。

