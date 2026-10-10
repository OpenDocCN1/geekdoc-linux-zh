
- 生成通用网关接口（CGI）脚本或自定义应用程序接口（API）程序，以评估提交表单的内容、呈现动态创建的文档或访问数据库。
- 记录任何成功的访问和错误。

### Apache Web 服务器

Apache Web 服务器最初基于 HTTPd，这是一个来自国家超级计算应用中心（NCSA）的免费服务器。曾经有一段时间，HTTPd 是互联网上第一个也是唯一的 Web 服务器。不幸的是，该服务器的发展没有跟上网站管理员的需求，并且发现了许多安全问题。许多网站管理员一直独立地对 NCSA 源代码应用他们自己的功能和修复。

1995 年初，这些开发人员中的一群人齐心协力，基于这个代码库创建了一个名为 Apache 的新项目。从那以后，现在的 Apache 软件基金会（`http://www.apache.org`）重新编写了大部分代码，并创建了一个稳定的、多平台的 Web 服务器守护进程。Apache 软件基金会赞助了二十多个相关项目。这些项目包括 `mod_perl`（使用 Perl 语言创建动态网站）、Jakarta（提供服务器端 Java 内容）、DB（创建和维护商业质量的数据库解决方案）以及 SpamAssassin（识别和处理垃圾邮件）。

Apache Web 服务器的主要功能包括：
- 由大型协作志愿者程序员群体带来的稳定性和快速开发周期
- 完整的源代码，可免费下载（没有最终用户许可协议 [EULAs] 的限制，也没有对可运行的服务器数量设限）
- 使用纯文本文件进行配置的便捷性
- 基于客户端主机名/IP 地址或用户名/密码组合的访问控制
- 支持服务器端脚本以及 CGI 脚本；这包括允许不同用户控制脚本执行的能力（如果单个脚本被攻破，可限制整个 Web 服务器的脆弱性）
- 一个自定义 API，允许外部模块（例如用于扩展日志记录能力、改进身份验证、缓存、连接跟踪等）被服务器守护进程使用

Apache 并不是 Fedora 系统唯一的 Web 服务器，但它是与 Linux 最常用的服务器之一，且根据 Netcraft（`http://news.netcraft.com/archives/web_server_survey.html`）的数据，它仍是互联网上最受欢迎的服务器。

### Fedora 可用的其他 Web 服务器

其他可以在 Fedora 和其他 Linux 发行版上运行的 Web 服务器在下述列表中进行了描述，并附有提供详细信息的 URL。
- `lighttpd` — lighttpd Web 服务器（`http://www.lighttpd.net`）为安全、速度、合规性和灵活性而构建，因此绰号为“Lighty”。由于它具有低内存占用并平衡 CPU 负载，因此特别适合高性能环境。YouTube、Wikipedia 和 meebo 等网站已使用 lighttpd 用于某些专门的 Web 应用。
- `telnetd` — TelHttpd Web 服务器（`telhttpd` 软件包）是使用工具命令语言（TCL）创建的。除了作为 Web 服务器外，TelHttpd 还可用作 TCL 应用程序服务器。
- `thttpd` — thttpd HTTP 服务器（`http://acme.com/software/thttpd`）旨在简单、小巧、可移植、快速且安全。其创建者称其为微型、涡轮、节流型 HTTP 服务器。它仅实现了满足 HTTP/1.1 合规所需的最小功能，因此在极端负载下可以比许多大型 Web 服务器运行得更快。

### 快速启动 Apache Web 服务器

如果在安装 Fedora 时未安装 Apache，你可以稍后安装它。你需要 `httpd` 软件包，可选地需要 `httpd-manual` 软件包（在早期版本中分别名为 `apache` 和 `apache-manual`）。

以下是一种让 Apache Web 服务器快速运行的简便方法。从这里开始，你需要根据你的需求和环境对其进行自定义（如下文所述）。

1. 通过从终端窗口输入以下内容来确保 Apache 已安装：

```bash
$ rpm -qa | grep httpd
system-config-httpd-1.4.6.1-1.fc12.noarch
httpd-tools-2.2.13-4.fc12.i686
httpd-devel-2.2.13-4.fc12.i686
httpd-2.2.13-4.fc12.i686
httpd-manual-2.2.13-4.fc12.i686
```

你看到的版本号可能不同。你只需要 `httpd` 软件包即可开始。我推荐 `httpd-manual`，因为它提供了关于整个 Apache 设置的 excellent 信息。`httpd-devel` 软件包包含用于构建和安装扩展模块的 `apxs` 工具。`httpd-tools` 软件包包含用于运行基准测试和管理 Apache 密码的工具。

`system-config-httpd` 软件包包含一个基于图形界面的 Apache 配置工具。根据你提供的内容类型，你可能还需要添加包含模块的软件包以在 Apache 服务器内运行该代码（例如 `mod_perl`、`mod_python` 和 `mod_mono`）。

2. 如果你计划建立一个公共 Apache 服务器（例如，www.handsonhistory.com），建议设置有效的主机名。如果你没有真实的完全限定域名，你可以编辑 `/etc/httpd/conf/httpd.conf` 文件并将 `ServerName` 定义为你计算机的 IP 地址。以 root 用户身份在任何文本编辑器中打开 `httpd.conf` 文件，搜索包含 `ServerName www.example.com:80` 的行，并取消注释。它应该如下所示：

```
ServerName www.example.com:80
```

如果你没有为 `ServerName` 提供名称，服务器将对你的 IP 地址进行反向查找以尝试找到名称。如果失败，它将使用你的回环地址（127.0.0.1）。（对于公共 Web 服务器，获取一个真实的 DNS 主机名。（有关 DNS 信息和使服务器公开的信息，请参阅第 24 章。））要将 Apache 可用于本地主机，无需对此文件进行任何更改。

3. 添加一个管理电子邮件地址，以便在遇到服务器错误时可以联系你。在 `/etc/httpd/conf/httpd.conf` 文件中，默认管理地址如下所示：

```
ServerAdmin root@localhost
```

将 `root@localhost` 更改为你的 Apache 管理员的电子邮件地址。

4. 启动 `httpd` 服务器。以 root 用户身份输入以下内容：

```
# service httpd start
```

如果一切顺利，应该会显示以下消息：Starting httpd: [OK]。现在你可以开始了。

### 配置 Apache 服务器

现在你的 Web 服务器已经可以工作了（或者，至少我希望是这样），请按照下一节进行操作。这有助于你了解如何设置更复杂的 Web 服务器架构，并保护你的服务器免受滥用。按照该部分操作还将帮助你排查 Web 服务器的问题，以防它无法正常工作。

> **提示：** 如果你的 Web 服务器可以从本地主机访问，但在你的局域网或互联网上对其他用户不可用，你可能需要修改防火墙规则以允许更广泛的访问。附录 B 解释了如何让你的 Web 服务器或其他服务器服务可被访问。特别是，你需要开放 tcp 端口 80，以及可能的 tcp 端口 443（如果你提供 https 内容）。此外，如果启用了 SELinux，它可能会阻止你访问原本应该可以工作的 Web 服务器。要禁用 SELinux，请以 root 身份输入 `setenforce 0`。或者输入 `man httpd_selinux` 以了解如何在使用 `httpd` 时配置 SELinux。特别是，确保所有布尔值都已正确设置以允许你需要的服务，并且所有文件上下文标签对于你的内容和配置文件都是正确的。

配置 Apache Web 服务器的主要文件是 `httpd.conf`（位于 `/etc/httpd/conf` 目录中）。几年前，Apache 项目开始建议不要使用额外的配置文件，例如 `srm.conf` 和 `access.conf`，而是将所有内容都放在 `httpd.conf` 中。然而，在最近的版本中，趋势是让与 Apache 一起使用的模块和其他组件拥有自己的配置文件（通常位于 `/etc/httpd/conf.d/` 目录中）。

所有 Apache 配置文件都是纯文本文件，可以使用你喜欢的文本编辑器进行编辑。`/etc/httpd/conf/httpd.conf` 文件将在下一节中完整复现，并在相关的选项块后插入解释（旨在补充每个文件提供的注释）。
