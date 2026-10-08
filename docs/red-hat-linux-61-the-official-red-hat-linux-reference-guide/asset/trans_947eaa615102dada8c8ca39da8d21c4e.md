
# 第 12 章 伯克利互联网域名系统 (BIND)

## 12.6. 需要避免的常见错误

初学者在编辑 BIND 配置文件时经常会出错。请务必避免以下问题：

- 注意要增加序列号（serial number）
- 如果没有增加序列号，主域名服务器可能拥有正确的新信息，但从域名服务器永远不会收到更改通知，或不会尝试刷新该区域的数据。
- 在 `/etc/named.conf` 文件中，注意正确使用省略号（...）和分号（;）。缺少分号或意外的省略号会导致 named拒绝启动。
- 记住在区域文件中，所有完全限定域名（FDNs）之后都要使用点 (.)，而在主机名上省略省略。
- 域名名末尾的点表示完全限定名称（FQDN）。如果省略了点，named 会添加区域名称或 `$ORIGIN` 值来补全它。
- 如果防火墙阻止了 named 程序编辑其配置文件。

默认情况下，BIND 第 9 版本使用 1024 以上的随机端口查询其他域名服务器。防火墙通常期望所有域名服务器都仅使用端口 53 进行通信。通过向 `/etc/named.conf` 中的 `options` 语句添加以下行，强制 named 使用端口 53：`query-source-address * port 53;`

## 12.7. 额外资源

以下信息源将提供有关 BIND 的额外资源。

### 12.7.1 安装文档

- BIND 提供了涵盖许多不同主题的完整安装文档，每个文档都放在其主题目录下：
- `/usr/share/doc/bind-<version-number>/` — 包含一个带有最新功能列表的 README 文件。
- `/usr/share/doc/bind-<version-number>/arm/` — 包含 BIND 9 管理员手册的 HTML 和 SGML 版本，详细说明了 BIND 资源需求、如何配置不同类型的域名服务器、执行负载均衡以及其他主题。对于大多数 BIND 用户来说，这是最好的起点。
- `/usr/share/doc/bind-<version-number>/draft/` — 包含各种文档，审查了与 DNS 服务相关的问题以及解决这些问题的建议方法。
- `/usr/share/doc/bind-<version-number>/misc/` — 包含旨在解决特定高级问题的文档。BIND 版本 8 用户应咨询迁移文档，以了解迁移到 BIND 9 时必须做出的选项。选项文件列出了 `/etc/named.conf` 中使用的 BIND 9 中实现的所有选项。
- `/usr/share/doc/bind-<version-number>/rfc/` — 每个与 BIND 相关的 RFC 文档都在此目录下。
- man named — 探索可用于控制 BIND 域名服务器守护进程的方面。
- man named.conf — named 配置文件可用选项的完整列表。
- man rndc — 解释了在使用 rndc 命令控制 BIND 域名服务器时可用的不同选项。
- man rndc.conf — rndc 配置文件中可用选项的完整列表。

### 12.7.2. 有用网站

- http://www.isc.org/products/BIND — BIND 项目的主页，包含当前发布版本的信息以及 BIND 9 管理员手册的 PDF 版本。
- http://www.redhat.com/mirrors/LDP/HOWTO/DNS-HOWTO.html — 涵盖了如何将 BIND 作为解析器、缓存域名服务器使用，或配置作为域名主域名服务器所需的各种区域文件。

### 12.7.3. 相关书籍

- 《DNS and BIND》，Paul Albitz 和 Cricket Liu 著；O’Reilly & Associates —— 流行的参考书，解释常用和冷门的 BIND 配置选项，并提供了保护 DNS 服务器的策略。
- 《The Concise Guide to DNS and BIND》，Nicolai Langfeldt, Que 著 — 研究了多个网络服务与 BIND 之间的连接，重点关注任务为导向的技术主题。

# 第 13 章

# 轻量目录访问协议 (LDAP)

轻量目录访问协议 (LDAP) 是一组用于通过网络访问集中存储信息的协议。它基于目录共享的 X.500 标准，但其复杂性和资源消耗更低。因此，LDAP 有时被称为“X.500 Lite”。

与 X.500 一样，LDAP 使用目录以分级方式组织信息。这些目录可以存储各种信息，并可以类似于网络信息服务 (NIS) 的方式，允许任何人从任何启用 LDAP 的网络访问其账户。

在许多情况下，LDAP 仅被用作虚拟电话簿，允许用户轻松获取其他用户的联系信息。但 LDAP 比传统的电话簿更灵活，因为它可以引用全球范围内的其他 LDAP 服务器，提供即时的查询复制操作。当 LDAP 客户端连接到 LDAP 服务器时，LDAP 更多地用于单个组织，如大学、政府部门和私营公司。

LDAP 是一个客户端-服务器系统。服务器可以使用各种数据库来存储目录，每个数据库都针对快速大量的读取操作进行了优化。当 LDAP 客户端连接到 LDAP 服务器时，它可以查询目录，也可以尝试修改它。在查询情况下，服务器要么回答查询，或者在无法回答时，它可以引用一个拥有答案的 LDAP 服务器。如果客户端应用程序尝试修改 LDAP 目录。

## 13.1. 为什么选择 LDAP？

使用 LDAP 的主要优势是信息是集中的。例如，与其为组织管理用户列表，可以使用 LDAP 作为中央仓库。由于 LDAP 支持传输层安全 (TLS)，敏感数据可以得到保护。

### 13.1.1 OpenLDAP 2.0 功能增强

- LDAP3 支持 — OpenLDAP 包含了许多重要的功能。
- IPv6 支持 — OpenLDAP 支持下一代互联网协议版本 6。
- LDAP Over IPC — LDAP 可以在进程间通信。

## 13.2. LDAP 术语

任何关于 LDAP 的讨论都需要对一组术语的基本理解：

- 条目 (entry) 是 LDAP 目录中的单个单元。每个条目由其唯一的区分名 (DN) 标识。
- 属性 (attributes) 是与条目直接关联。例如，组织可以作为一个 LDAP 条目。与组织相关的属性可能是传真号码、地址等。人也可以表示为 LDAP 目录中的实体。人的属性包括电话号码和电子邮件。

某些属性是强制的，而另一些是可选的。对象类 (Objectclass) 定义了每个条目所需的属性。对象类定义位于各种架构文件中，位于 `/etc/openldap/schema/` 目录。有关 LDAP 架构的更多信息，请参见章节 13.5 /etc/openldap/schema/ 目录。

- LDIF 数据交换 数据交换格式是 LDAP 条目的 ASCII 文本表示。用于导入 LDAP 服务器的文件必须是 LDIF 格式。LDAP 条目看起来如下：

```
<id>
dn:<distinguished name>
<attrype>:<attrvalue>
<attrype>:<attrvalue>
<attrype>:<attrvalue>
```

每个条目可以根据需要包含任意数量 <attrype>:<attrvalue> 对。空行表示条目的结束。

> 注意 所有的 <attrype> 和 <attrvalue> 对都必须在相应的架构文件中定义，才能使用这些信息。

任何包含在 "" 和 "" 之间的值都是变量，可以在创建新的 LDAP 条目时设置。然而，此规则不适用于 <id>。<id> 是由你使用的应用程序确定的数字。
