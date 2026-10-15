
![](img/9139201cfcaf4292284a0eed074928e5_760_0.png)

## 14

# Apache Web 服务器

## 认证目标

|  |  |
|---|---|
|14.01 Apache Web 服务器|14.05 部署一个基本的 CGI 应用程序|
|14.02 标准 Apache 安全配置|✓ 两分钟速览|
|14.03 专用 Apache 目录|问答|
|14.04 普通和安全的虚拟主机|自测|

Unix 由 AT&T 在 1960 年代末和 1970 年代初开发，在这些年里它在众多主要大学之间自由分发。当 AT&T 开始对 Unix 收费时，一些大学开发者尝试创建该操作系统的克隆版本。其中一个克隆版本 Linux 于 1990 年代初开发并发布。

其中许多大学也在开发演变为互联网的网络。经过当前的改进，这使得 Linux 可能是可用的最适合互联网的网络操作系统。Linux 可用的广泛网络服务不仅在各自领域处于顶尖水平，而且它们创造了迄今为止在任何价格下都可用的最强大、最实用的互联网就绪平台之一。目前，Apache 是互联网上最流行的 Web 服务器。根据 Netcraft (`www.netcraft.com`) 调查，该调查追踪互联网上几乎每个站点相关的 Web 服务器，Apache 目前被比所有其他 Web 服务器合计更多的互联网网站使用。Apache 包含在 RHEL 6 中。本章涉及在基本配置级别使用 Apache Web 服务器的基本概念。

## 考试内容

本章直接涉及四个 RHCE 目标。虽然目标指定了 HTTP（超文本传输协议）和 HTTPS（HTTP 安全）协议，但这是对 Apache Web 服务器的隐含引用。它是目前 RHEL 6 上唯一受支持的 Web 服务器。通常，普通网站和安全网站配置在不同的文件中。目标是

- 配置虚拟主机
虚拟主机是 Apache 的核心，它支持在同一服务器上配置多个网站。
- 配置私有目录
Apache Web 服务器上的私有目录在某种程度上介于普通网站和安全网站之间。它是一个只能由一个用户访问的目录。
- 配置组管理内容
用户组需共同维护站点内容。如私有目录可为个人用户在主目录配置，目录也可为用户组在共享目录配置。
- 部署基本 CGI 应用程序

不必了解 Common Gateway Interface (`CGI`)，但动态网页依赖 CGI 等脚本。无需编写 CGI 脚本，但需配置 Apache 支持其部署。

此外还有第 10、11 章讨论的标准网络服务要求。回顾要点：安装服务、使其与 SELinux 协同工作、开机启动、基本操作配置、设置用户和主机安全。

## 认证目标 14.01

### Apache Web 服务器

Apache 是目前最流行的 Web 服务器。基于 HTTP daemon (`httpd`)，Apache 可通过常规 HTTP 及其安全版本 HTTPS 简单安全地提供各类内容。

Apache 源自 National Center for Supercomputing Applications (`NCSA`) 的服务器代码，因补丁众多而得名“patchy”。Apache Web 服务器持续推动 Web 艺术发展，提供最稳定、安全、健壮可靠的服务器之一，由 Apache Software Foundation (`www.apache.org`) 持续开发。

为获得完整文档，安装时请包含 `httpd-manual` RPM，它会在 `/var/www/manual` 提供完整的 Apache 手册 HTML 副本。

### Apache 2.2

鉴于其可靠性和稳定性，RHEL 6 包含更新的 Apache 2.2。RHEL 5 也包含稍旧的 Apache 2.2。RHEL 6 提供的 Apache 2.2 已包含支持最新网页所需更新，并提供最佳互联网风险安全防护。

### LAMP 堆栈

Apache 的强大之处在于可与其他软件集成。最常见的是 LAMP 堆栈，指 Linux、Apache、MySQL 和三种脚本语言之一（Perl、Python 或 PHP）。

RHCE 目标不要求安装结构化查询语言数据库如 MySQL (`My Structured Query Language`) 或脚本语言。但它们解释了 Apache 配置文件中的许多模块。Apache 也可与其它 SQL 数据库和脚本语言协同工作。

### 安装

Apache 所需 RPM 包包含在 Web Server 包组中。安装后最简单的方式是：

```
