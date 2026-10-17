
指令必须输入到`httpd.conf`文件中。`Port`指令放置在`httpd.conf`文件的主服务器部分，并指示 Web 服务器在端口 80 监听请求。`Name-VirtualHost`指令是配置基于名称的虚拟主机所必需的，建议使用 Web 服务器的 IP 地址。最后三个条目由`VirtualHost`块指令组成。请注意，默认服务器（`www.sniglets.com`）也被视为一个虚拟主机。

## .htaccess

`.htaccess`文件允许你在不重启 Apache 的情况下更改目录中的指令，且`.htaccess`是文件访问指令的默认文件名。此文件允许用户在无需网页管理员协助的情况下控制自己的网页。这些文件必须在每次请求时解析，并会带来轻微的性能损失。`AccessFileName`指令可以指定要检查的文件访问指令的文件名。`AccessFileName`是一个全局指令。`AllowOverride`指令告诉服务器`.htaccess`文件中哪些指令可以覆盖先前设置的指令。有关`AllowOverride`指令的最新选项，请查阅 Apache 文档。

## Common Gateway Interface (CGI)

CGI 是 Web 服务器与外部应用程序交互的标准。纯 HTML 文档是静态的；它们是不变的文档。CGI 程序允许实时执行程序，使用户能够查询数据库或在网页上的表单中输入信息。Apache 每次调用 CGI 程序时都会调用一个解释器。保持一个

用于 CGI 脚本的单独目录（`/usr/local/apache/cgi-bin`）。系统管理员或网站管理员可以对该目录进行更严格的控制，以确保脚本不会对 Web 目录的其余部分产生不利影响。

执行脚本可能会对 Web 服务器的安全性和稳定性造成严重破坏。维护一个非生产环境的 Web 服务器，作为新脚本和程序的测试平台，这一点非常重要。一旦脚本/程序在非生产服务器上测试通过，就可以将它们移至生产服务器。

## 日志记录

Apache Web 服务器可以通过其日志记录模块（`mod_log_config.c`）向网站管理员提供大量信息。表 16.5 包含了 Apache 中的主要日志记录指令。`LogFormat`指令使用标准的 CLF，大多数商业日志分析器都支持该格式。`LogLevel`指令至少应设置为`error`级别。

**表 16.5 — 日志记录指令**

| 指令 | 作用 |
| --- | --- |
| `LogLevel level` | 设置错误日志中记录的信息量，其中`level`可以是`emerg`、`alert`、`crit`、`error`、`warn`、`notice`、`info`或`debug`。 |
| `LogFormat format [nickname]` | 设置由`TransferLog`指令设定的默认日志文件的格式。 |
| `ErrorLog filename`<br>`syslog:facility` | 设置服务器记录所有错误的文件名。如果系统支持，`syslog`将通过 syslogd 启用日志记录。`Facility`可以是 syslog 中有文档记载的名称。 |
| `TransferLog` | 以`LogFormat`指令定义的格式添加一个日志文件。 |

## Apache 与 SSL

Apache-SSL 和 Apache 到 OpenSSL 的接口（`mod_ssl`）软件包为 Apache Web 服务器提供加密功能。Apache-SSL 将 SSL 实现为一组针对 Apache 源代码的补丁。Apache 到 OpenSSL 的接口是 Apache 源代码的扩展和一组补丁。Apache 到 OpenSSL 的接口实现了 SSL 和传输层安全协议。这些软件包是免费的，可以在美国和加拿大境外用于非商业和商业目的。

这两个软件包都可以通过从 RSA Security Inc.（www.rsa.com）获取许可证在美国和加拿大使用。另外，也有商业软件包可为 Apache 提供 SSL。Red Hat Linux Professional（www.redhat.com）随 Red Hat Linux 发行版一起提供安全的 Web 服务器。Covalent Raven SSL（www.covalent.net）和 Stronghold（www.c2.net）是为 Apache 提供 SSL 的模块。

## 安全

在设置 Apache Web 服务器时，安全不容忽视。配置和可执行目录的权限应仅允许 root 用户具有写权限。`httpd`二进制文件应由 root 拥有，并且所有用户都可执行。

在保护 Web 服务器安全时，应采取以下操作：

- 使用`ScriptAlias`指令将所有 CGI 强制放到一个单独的目录。这使系统管理员能够控制该目录中允许的内容。
- 运行非生产环境的 Apache Web 服务器。要求所有 CGI 程序在移至生产 Web 服务器之前，先在这台机器上经过充分测试。
- 不允许`.htaccess`文件覆盖用于保护 Web 服务器的安全设置。
- 锁定`ServerRoot`，仅允许基于目录或虚拟主机进行访问。
- 目录默认允许访问。使用`order`指令保护`ServerRoot`，并通过特定目录启用访问。
- 不要忽略块指令的合并顺序。`Files`和`Location`块指令可以覆盖`Directory`块中的指令。

## WIN32 二进制安装

Apache Web 服务器二进制文件可在 http://www.apache.org 获取。Apache Web 服务器最初是为 UNIX 设计的。截至 1.3.9 版本，它仍被视为适用于 Windows（NT 和 2000）的 beta 级代码。

在安装 Apache 服务器期间，系统会提醒您这是 beta 级代码，并且存在已知的错误和安全问题。考虑到这些警告，您或许应该对此加以利用。

Apache Web Server 在 Windows 2000 上的版本，作为公司防火墙后面的内部 Web 服务器。当然，一旦 Apache Web Server 不再被视为测试版，你就必须决定是否将其部署为主要 Web 服务器。

## Windows 2000 安装

Windows 2000 的 Apache 发行版二进制文件是一个可执行文件。执行该二进制文件需要你选择安装目录、开始菜单名称和安装类型。表 16.6 概述了可用的不同选择以及将安装的软件包。

安装程序会将 Apache 服务器配置在所选安装目录下的`conf`目录中。如果配置文件已存在，安装程序不会覆盖当前文件，而是放置一份带有`*.default`扩展名的配置文件副本。安装完成后，请检查`*.default`配置文件，了解你可能需要对原始配置文件做的更改。

Apache Web Server 从安装目录下的`htdocs`目录提供文件服务。它不会覆盖`htdocs`目录中现有的`index.html`文件。这样可以在不丢失现有网站的情况下升级服务器。

Apache Web Server 二进制文件位于安装目录的顶层。服务器二进制文件是`apache.exe`。

## Windows 2000 配置

Apache Web Server 的配置文件安装在`conf`目录中。主配置文件是`httpd.conf`。配置文件已在“Apache Web Server 配置”一节中描述。接下来的几段将重点介绍配置 Windows 2000 时的主要差异。

**表 16.6 Windows 2000 上的 Apache Web Server 安装选项**

| 选项 | 组件 |
|--------|----------|
| 最小 | 应用程序文件 |
| 典型 | 应用程序文件、手册 |
| 自定义 | 应用程序文件、手册、源代码 |

Apache 服务器在内部使用 UNIX 文件名。这要求使用正斜杠（/）而不是反斜杠（\）。配置文件（`httpd.conf`、`srm.conf`和`access.conf`）以及网页文件（`htdocs`目录）必须使用正斜杠。可以包含驱动器号，默认驱动器为包含 Apache 可执行文件的驱动器。但是，接受文件名作为参数的指令必须使用反斜杠或 Windows 风格的文件名。下面是使用 Windows 风格文件名的指令示例：

```
E:\program files\Apache Group\Apache>apache -f "c:\mywebsite\conf\web.conf"
```

DSO 模块已编译到 Apache Web Server 二进制文件中。这允许服务器在运行时加载模块。发行版中包含的但未编译到 Web 服务器二进制文件中的 DSO 模块位于`modules`目录下。在运行时激活 DSO 模块，需要在`httpd.conf`文件中添加`LoadModule`指令。下面一行是添加`rewrite`模块的正确条目（注意使用正斜杠）：

```
LoadModule rewrite_module modules/ApacheModuleRewrite.dll
```
