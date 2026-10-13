
# 54 第1章

> 注意：MultiViews 不包含在 All 配置中。

使用 `+` 和 `–` 符号可以修改之前在父目录中设置的选项。这里讨论了其中几项：

- 如果用户使用 `All`，除了 `MultiViews` 以外的所有项都会被设置。
- `ExecCGI` `ExecCGI` 允许执行 CGI 脚本。
- `FollowSymlinks` 允许服务器跟踪符号链接。开启此项时要要小心。例如，如果用户有一个指向 `/ /etc` 的符号链接且设置了 `FollowSymlinks`，Apache 将向客户端提供这些目录的访问。

一旦安装了 Apache，就必须对其进行妥善的操作和维护。运行 Apache 服务器的职责将在下一章中讨论。

## 第2章

## 系统管理

### 目标

- 阐述 Web管理员（Webmaster）的共同职责。
- 列出 Web 服务器安全的基本步骤。
- 描述 MySQL 的功能。
- 阐述保留日志的优势。
- 比较 `Addhandler` 和 `ScriptAlias` 的用法。
- 比较静态模块和动态模块。
- 描述 `ab`'s 基准测试方法。
- 列出使用重定向脚本的原因。
- 描述从单台机器运行多个站点的方法。
- 列出 `httpd` 在接受连接时采取的步骤。
- 列出别名（aliases）有用的原因。

### 工作原理

既然 Apache 已经安装，就必须继续管理 Apache 服务器和模块，以及运行 Apache 服务器的硬件和操作系统。本节将讨论系统管理员或 Web 管理在配置和运行 Apache 服务器时将承担的各种角色和职责。

### 成为 Web 管理

Web 管理这一称号包含了许多不同的职责，在一些较小的 Web 安装中，所有职责都可能由一个人承担。在较大的安装中，任务的不同部分可能会分配给几个不同的人。职责主要分为几大类：

- 系统管理员。对系统拥有完全控制权。
- 配置管理。配置 Web 服务器。
- 内容管理。控制 Web 页面的设计和部署。

系统管理员负责系统本身的完整性。他们对系统的更改保持警惕，并时刻警惕来自外部或普通用户越界行为的入侵。系统管理员负责基础操作系统，通常也负责硬件。

在 Web 服务器的空间内，有针对每个 Web 服务器的特定设置，Web 管理对保护系统的兴趣大于对系统本身的保护，然而对服务器配置文件的更改可能会给系统管理员带来问题。这种经理必须对 Web 运行特定的层面的后果有认识，这超出了通用 Unix 系统管理员的知识范围。虽然 Web 守护进程必须由具有 root 权限的人启动，但此人没有其他 root 权限的需求。Web 服务器配置文件的完整性是此任务的首要任务。

还有另一种 Web 管理——他们比起配置，更多地交易内容和流程。这个人与创建 Web 页面的艺术家合作，并指导网站的结构。此人依赖配置的正确性，并根据网站的需求提出请求。网站的树结构由此人构建。直接参与构建 Web 服务器和设置配置并不是这项工作的核心，尽管当出现新功能或新版本时，此人需要请求更改。

在个人站点或中等规模的企业站点中，这三个相互冲突的性格可以体现在同一个人身上，或者所有职责可以由几个人共同。在较大的站点中，它们由两个、三个人或更多人处理，且 root 用户与 Web 管理不是同一个人。区分职责的界限在不同的安装之间可能会不同。在互联网服务提供商（ISP）处，提供商可以执行第一项或第二项工作（第三项工作将主要归终端所有）。通过虚拟系统方法，ISP 可以获得对客户整个“虚拟系统”的控制，或者仅仅是对配置文件或内容文件的控制。如果你负责一个系统。

# 允许 (Allow) 与 拒绝 (Deny)

取决于使用方式，`Allow` 和 `Deny` 指令可能会降低运行速度。如果目标位置是 IP 地址，则没有问题。如果目标是域名，则需要一些时间将域名解析为 IP 地址。Apache 使用这些指令结合了伪装保护；同时还会发生反向查找。在使用这些指令时使用 IP 地址以避免锁定惩罚。从系统根目录开始拒绝访问，并在需要的地方选择性地允许。这样，就不必在每次请求时都检查访问权限。

## 最大客户端数 (MaxClients)

此指令控制 Apache 同时处理的访问者数量。如果请求数超过此值，客户端将被锁定在外。这是一项安全功能，防止 Apache 在吸收所有可用系统资源时将整个机器拖垮。当达到 `MaxClients` 时，检查是否正在发生交换（swapping），并相应地调整该值。如果此时没有交换，则可以增加该值。减小该值可以减少交换。增加 RAM 也可以减少交换并允许增加 `MaxClients`，从而实现更多的并发连接。

`256` 的上限是在编译时硬编码的。超过当前限制的增加需要重新编译，这需要在 `httd.h` 中定义的 `HARD_SERVER_LIMIT` 变量中放入所需的值。

## TCP/IP 版本

确保拥有最新版本的系统内核。HTTP 服务使得 1994 年或 1995 年以来 Unix 内核内置的许多假设失效。

# 主机名查找 (Host Name Look-Ups)

在 Apache 1.3 之前，主机查找默认设置为 On。这要求 Apache 在完成请求之前必须完成 DNS 查找。在 Apache 1.3 中，该功能默认设置为 Off。现在，当使用从域名允许或从域名拒绝的功能时，将执行双 DNS 查找（先反向查找，后正向查找，以确保反向查找未被伪装）。如果使用 IP 地址而不是域名，则不会发生这种惩罚。

# 60 第 2 章

> 注意：这些指令可以进行范围限制，以便仅对匹配特定标准的请求执行查找。以下示例代码禁用了 `.html` 和 `.cgi` 文件以外的查找：

```
HostnameLookups off

<Files ~ ".(html|cgi)$">

HostnameLookups on

</Files>
```

在 CGI 内部还有另一种替代方案。考虑在需要 DNS 查找的特定 CGI 中使用 `gethostname` 调用。

# FollowSymLinks (跟随链接) 与 SymLinksIfOwnerMatch

在 Web 目录树中，任何没有 `Options FollowSymLinks` 或具有 `SymLinksIfOwnerMatch` 的地方，Apache 都必须发出额外的系统调用（每个文件名组件额外增加一次）。例如：

```
DocumentRoot /etc/apache/htdocs

<Directory />

Options SymLinksIfOwnerMatch

</Directory>
```

如果对 `/index.html`、`/etc`、`/etc/apache`、`/etc/apache/htdocs` 和 `/etc/apache/htdocs/index.html` 发起请求，这些请求将永远不会被缓存，它们每次请求都会发生。如果不使用符号链接安全检查，以下配置将提供更高的性能：

```
DocumentRoot /etc/apache/htdocs

<Directory />

Options FollowSymLinks

</Directory>

<Directory /etc/apache/htdocs>

Options -FollowSymLinks +SymLinksIfOwnerMatch

</Directory>
```

Web 目录树之外的任何 `Alias` 或 `RewriteRule` 部分都需要类似的处理。为了获得最佳性能，请在各处设置 `FollowSymLinks`，并且不要使用 `SymLinksIfOwnerMatch`。

## AllowOverride (允许覆盖)

在任何允许覆盖的地方，Apache 都会尝试打开 `htaccess` 文件。例如：

```
DocumentRoot /etc/apache/htdocs

<Directory />

  AllowOverride All

</Directory>
```

每次尝试打开 `/index.html` 时，Apache 都会尝试查找并打开 `/.htaccess`、`/etc/.htaccess`、`/etc/apache/.htaccess` 和 `/etc/apache/htdocs/.htaccess`，无论它们是否存在。

> 注意：这些指令可以进行范围限制，以便仅对匹配特定标准的请求执行查找。以下示例代码禁用了 `.html` 和 `.cgi` 文件以外的查找：

```
HostnameLookups off

<Files "\.\(html|cgi)$">

  HostnameLookups on

</Files>
```

在 CGI 内部还有另一种替代方案。在下面的示例中，考虑在需要 DNS 查找的特定 CGI 中使用 `hostname`：

```
FollowSymLinks and SymLinksIfOwnerMatch
```

## 内容协商 (Content Negotiation)

可以衡量速度提升的一个机会是 `DirectoryIndex` 指令。与其使用方便的通配符，不如提供一个完整的选项列表，并将最常用的选择放在第一个（或如果有多个，则将首选的放在第一个）。与其使用：
