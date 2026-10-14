
在这里，程序由用户 ID 0 所有，组仍然是 kabir (500)，因此 `suEXEC` 拒绝运行它。如你所见，`suEXEC` 正在执行它应该做的事。为了确保 `suEXEC` 在其他目录中运行 `test.pl` 程序，请在 `~kabir/public_html` 中创建一个 `cgi-bin` 目录并将 `test.cgi` 放入其中。在确定新目录和文件的用户组所有权设置为用户 ID 和组 ID 后，使用以下地址访问脚本：

```
http://veracruz.paunchy.net/~kabir/cgi-bin/test.pl
```

如果你有虚拟主机并想运行 CGI 程序，必须在 `<VirtualHost>` 容器内部使用 `suEXEC`。

# CGIWRAP

`CGIWrap` 对 CGI 执行多项检查，如果任何检查失败，将不会执行。`CGIWrap` 由 Nathan Neulinger 编写；最新版本可以在站点 `http://ftp.cmr.edu/pub/cgi/cgiwrap/` 获取。它通过 HTML 文档使用。

# 降低服务器端包含风险

如果你使用 SSI 命令运行外部应用程序，其安全风险与 CGI 应用程序相同。然而，你可以通过 `Options` 指令在 Apache 中轻松禁用此命令：

```
<Directory />
Options IncludesExec
</Directory>
```

这禁用了所有的包含；但你可以通过定义范围更窄的目录容器在需要时启用它们。这是一个示例：

```
<Directory />
Options IncludesExec
</Directory>

<Directory /ssi>
Options +Include
</Directory>
```

# 使用 SSL 进行安全交易

电子商务以惊人的速度增长。许多公司正在建立电子商务网站以便在互联网上开展业务。电子商务网站的一个前提是具备安全交易能力，这由安全套接层（SSL）提供。遗憾的是，由于美国对加密出口的法律限制，Apache 并不自带 SSL 支持。然而，目前有多种第三方 SSL 软件适用于 Apache。表 11-2 将帮助你根据需求选择合适的软件。

| 软件 | 分发 | 限制 | 备注 |
| :--- | :--- | :--- | :--- |
| `Apache-SSL` | 免费 | 在美国的使用可能受到版权和专利法的限制。 | 不推荐，因为它不是最整洁的解决方案。`Apache-SSL` 基本上是 Apache 的一组补丁，且文档不够完善。 |
| `mod_ssl` | 免费 | 在美国的使用可能受到版权和专利法的限制。 | 作者推荐。 |
| SuSE Secure Server | 商业 | 对于美国和加拿大以外的国家，受美国加密相关的出口限制。 | 最便宜的商业解决方案。基于 `mod_ssl`。 |

### 表 11-2 APACHE SSL 解决方案（续）

| 软件 | 发行版 | 限制 | 注释 |
| :--- | :--- | :--- | :--- |
| Raven SSL 模块 | 商业版 | 无 | 价格适中的解决方案。 |
| Stronghold Web Server | 商业版 | 无 | 作者针对严肃电子商务网站的最喜爱的 SSL 解决方案。然而，它是所有商业选项中最昂贵的。 |

`mod_ssl` 模块比 `Apache-SSL` 方法纯洁得多，而且它是免费的。虽然它部分基于 `Apache-SSL`，但它是由 Ralf S. Engelschall 编写的另一个文档齐全的模块。如果你使用的是最新版本的 Apache，我建议使用它。

## 获取 MOD_SSL

`mod_ssl` 模块没有包含在标准的 Apache 源码发行版中。你必须从以下网站下载它：`http://www.modssl1.org/`。由于该模块依赖于 `SSLeay` 包（与 `Apache-SSL` 一样），你还需要从同一个网站获取 `SSLeay` 包。

你还需要一个可以运行的 Perl 5 解释器，它是作为最小化 SuSE Linux 安装的一部分的。你还必须确保已从 Apache 网站或其镜像站获取了最新的 Apache 源码。

## 获取 CA 签名证书

你只需要从其中一个知名的证书颁发机构 (CA) 获取一个浏览器可识别的证书即可。以下是可能为你提供 `Apache-SSL` 证书的几个 CA：

- Verisign，地址：`http://www.verisign.com/`
- Thwaite Consulting，地址：`http://www.thawte.com/certs/server/request.html`
- Certisign Certificao Digital Ltd.，地址：`http://www.certisign.com.br/`
- IKS GmbH，地址：`http://www.iks-jena.de/produkte/ca/`

认证过程需要产生证明你业务真实性的文件。此类文件还必须来自你组织权威机构的信函。可以为你的个人 Web 服务器获取证书；你不需要拥有合法的公司。对于个人服务器证书，大多数 CA 只需要现有的账户证明。

## 总结

在本章中，你学习了如何使用最流行的 Web 服务器——Apache 创建强大的 Web 服务。你学习了如何通过源码编译创建一个自定义的 Apache 服务器。源码编译比下载并安装他人制作的二进制更具灵活性。你学习了通过修改配置文件快速让 Apache 服务器运行起来。你学习了为虚拟 Web站点和个人用户提供 CGI 支持，启用服务器端包含，支持基于 IP 和基于名的虚拟 Web站点，并使用 Apache 作为缓存和反代理服务器。此外，你还学习了如何使用 HTTP 认证在你的 Web站点中创建受限访问区域，监控 Apache 服务器，使用 `suEXEC` 和 `CGIWrap` 等封装增强你的 Web站点安全性，以及通过 `mod_ssl` 模块使用 SSL。

# 第 12 章 配置 FTP 服务器

## 本章

- 配置 `wu-ftpd` 用于标准 FTP 服务
- 配置 `wu-ftpd` 用于匿名 FTP 服务
- 配置 `wu-ftpd` 用于访 FTP 服务
- 配置 `wu-ftpd` 用于虚拟 FTP 服务
- 了解其他 FTP 服务器

从一台计算机传输文件到另一台计算机是常见的活动。尽管在互联网等 TCP/IP 网络上存在多种传输方法，但最常用的方法是文件传输协议 (FTP)。在本章中我们将检查如何将你的 SuSE Linux 服务器变成 FTP 服务器。

## 使用 FTP

SuSE Linux 发行版带有一个名为 `wu-ftpd` 的 FTP 版本。它是互联网上最流行的 FTP 服务器。因此，它被全球数千个 FTP 站点使用。`wu-ftpd` 系统默认未安装。要安装它，请进入 root 并挂载 CD-ROM。运行以下命令：

```
rpm -ivh /cdrom/suse/nl/ftp.rpm
rpm -ivh /cdrom/suse/nl/wuftpd.rpm
```

接下来，你需要修改 `/etc/inetd.conf` 以启动 `wu-ftpd`。找到引用 `ftp` 的行。取消 `wu.ftpd` 行的注释（`#`），并在 `in.ftpd` 行添加注释。`inetd.conf` 应该如下：

```
#
# 这些是标准服务。
#
ftp stream nowait root /usr/sbin/tcpd wu.ftpd -
```

## 第三部分：设置局域网/互联网服务

```
# ftp stream nowait root /usr/sbin/tcpd proftpd
# ftp stream nowait root /usr/sbin/tcpd inpd
```

按照以下方式重启 `inetd` 守护进程：`/etc/rc.d/init.d/inetd restart`

尝试 FTP 连接到你的服务器：

```
ftp localhost
```

你应该看到以下欢迎信息：

```
Connected to veracruz.paunchy.net.

220 veracruz.paunchy.net FTP server (Version wu-2.4.2-academ[BETA-18]) Sat Mar 11 17:51:53 GMT 2000) ready.

Name (veracruz:paul):
```

你可以使用常规用户名和密码登录。

## 配置 FTP 服务

你的 FTP 服务器配置由 `/etc` 目录下的文件组成：

- `services`
- `inetd.conf`
- `ftpaccess`
- `ftpversions`
- `ftpmsg`
- `ftpusers`

`wu-ftpd` 服务器像许多其他基于 TCP/IP 的服务器一样，通过名为 `inetd` 的互联网超级服务器运行，它监听端口 21 的 FTP 连接。当检测到此类连接请求时，`inetd` 会启动 `wu-ftpd` 服务器。在启动时，`inetd` 查看两个文件 `/etc/services` 和 `/etc/inetd.conf`，以确定哪个服务或端口关联服务器。

## `/etc/services`

你可能已经知道，`/etc/services` 文件描述了你的 Linux 服务器上提供的 TCP/IP 服务。
