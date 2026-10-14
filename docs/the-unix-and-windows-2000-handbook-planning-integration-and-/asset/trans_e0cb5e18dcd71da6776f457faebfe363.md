

用于 CGI 脚本的单独目录（`/usr/local/apache/cgi-bin`）。系统管理员或网站管理员可以对该目录进行更严格的控制，以确保脚本不会对 Web 目录的其余部分产生不利影响。

执行脚本可能会对 Web 服务器的安全性和稳定性造成严重破坏。维护一个非生产环境的 Web 服务器，作为新脚本和程序的测试平台，这一点非常重要。一旦脚本/程序在非生产服务器上测试通过，就可以将它们移至生产服务器。

## 日志记录

Apache Web 服务器可以通过其日志记录模块（`mod_log_config.c`）向网站管理员提供大量信息。表 16.5 包含了 Apache 中的主要日志记录指令。`LogFormat` 指令使用标准的 CLF，大多数商业日志分析器都支持该格式。`LogLevel` 指令至少应设置为 `error` 级别。

**表 16.5 — 日志记录指令**

| 指令 | 作用 |
| --- | --- |
| `LogLevel level` | 设置错误日志中记录的信息量，其中 `level` 可以是 `emerg`、`alert`、`crit`、`error`、`warn`、`notice`、`info` 或 `debug`。 |
| `LogFormat format [nickname]` | 设置由 `TransferLog` 指令设定的默认日志文件的格式。 |
| `ErrorLog filename`<br>`syslog:facility` | 设置服务器记录所有错误的文件名。如果系统支持，`syslog` 将通过 syslogd 启用日志记录。`Facility` 可以是 syslog 中有文档记载的名称。 |
| `TransferLog` | 以 `LogFormat` 指令定义的格式添加一个日志文件。 |

## Apache 与 SSL

Apache-SSL 和 Apache 到 OpenSSL 的接口（`mod_ssl`）软件包为 Apache Web 服务器提供加密功能。Apache-SSL 将 SSL 实现为一组针对 Apache 源代码的补丁。Apache 到 OpenSSL 的接口是 Apache 源代码的扩展和一组补丁。Apache 到 OpenSSL 的接口实现了 SSL 和传输层安全协议。这些软件包是免费的，可以在美国和加拿大境外用于非商业和商业目的。

这两个软件包都可以通过从 RSA Security Inc.（www.rsa.com）获取许可证在美国和加拿大使用。另外，也有商业软件包可为 Apache 提供 SSL。Red Hat Linux Professional（www.redhat.com）随 Red Hat Linux 发行版一起提供安全的 Web 服务器。Covalent Raven SSL（www.covalent.net）和 Stronghold（www.c2.net）是为 Apache 提供 SSL 的模块。

## 安全

在设置 Apache Web 服务器时，安全不容忽视。配置和可执行目录的权限应仅允许 root 用户具有写权限。httpd 二进制文件应由 root 拥有，并且所有用户都可执行。

在保护 Web 服务器安全时，应采取以下操作：

- 使用 ScriptAlias 指令将所有 CGI 强制放到一个单独的目录。这使系统管理员能够控制该目录中允许的内容。
- 运行非生产环境的 Apache Web 服务器。要求所有 CGI 程序在移至生产 Web 服务器之前，先在这台机器上经过充分测试。
- 不允许 .htaccess 文件覆盖用于保护 Web 服务器的安全设置。
- 锁定 ServerRoot，仅允许基于目录或虚拟主机进行访问。
- 目录默认允许访问。使用 order 指令保护 ServerRoot，并通过特定目录启用访问。
- 不要忽略块指令的合并顺序。Files 和 Location 块指令可以覆盖 Directory 块中的指令。

## WIN32 二进制安装

Apache Web 服务器二进制文件可在 http://www.apache.org 获取。Apache Web 服务器最初是为 UNIX 设计的。截至 1.3.9 版本，它仍被视为适用于 Windows（NT 和 2000）的 beta 级代码。

在安装 Apache 服务器期间，系统会提醒您这是 beta 级代码，并且存在已知的错误和安全问题。考虑到这些警告，您或许应该对此加以利用。

