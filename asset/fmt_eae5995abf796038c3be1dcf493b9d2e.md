
在这里你可以看到有两个用户登录（允许无限数量的用户连接）。第一个是自称为 `sshah@domain.com` 的匿名用户。第二个名为 `heidi` 的用户正在执行某些功能。第二个用户正在检索文件 `mklinux-ALL.sit.bin`。

# 总结

你可能认为万维网的普及会让 FTP 服务器灭亡；然而，过去几年的情况表明，事实恰恰相反。人们仍然全力部署 FTP 站点，因为它们的建立和维护非常简单。不需要编写精美的 HTML，不需要额外的工作——只需将文件放在正确的位置进行下载，让人们获取即可。

本章涵盖了配置 `wu-ftpd` 服务器的许多细节。在使用 FTP 服务器时需要记住的关键点如下：

- 密切关注与 FTP 服务器相关的安全公告，特别是 `wu-ftpd` 服务器。
- 监控日志以发现可疑活动。
- 仔细测试你的配置。由于可用选项非常多，你需要确保它的行为符合你的预期。
- 在设置文件所有者和权限时，务确保权限是正确的。
- 使用大量的消息帮助你的服务器对外部用户进行自文档。

![](img/7675e31a0e104594fbf0bbbebdf7e922_248_0.png)

## Apache 服务器

作者：Jack Tackett, Jr.

## 本章内容

- 服务器安装 218
- 运行时服务器配置设置 219
- 配置 `inetd` 服务器 224
- 首次运行 Web 服务器 227
- 启动和停止服务器 229
- 使用 Squid 加速 232
- 托管虚拟主机 234
- 配置文件列表 236

## 配置服务

第二部分

本章将引导你如何使用 Red Hat 的 RPM 系统安装和配置 Apache Web 服务器。Red Hat 在其整体 Linux 产品中包含了当前版本的 Apache。然而，如果最新版本的 Red Hat Linux 已经几个月了，你可以在 Red Hat FTP 服务器的 `/pub/contrib` 区域找到更新版本的 Apache。有关 Apache 最新版本的信息（例如添加了哪些 bug 修复和新功能），请访问 Apache 组网站 http://www.apache.org 或 Apache Week 网站 http://www.apacheweek.org。

当前的 Red Hat Linux 版本 5.1 包含了 Apache 1.2.6 版本。在本书出版时，可用的 Apache 最新稳定版本为 1.3.2，可以通过 http://www.apache.org 获取。1.2.6 版本以 RPM 格式提供在 Red Hat FTP 服务器上。

Apache 新和测试版本与其对应的 RPM 包之间存在延迟。在 Red Hat Linux 上从源码安装 Apache 是可能的，但超出了本章的范围，因为安装程序必须要么修改工作站的目录结构，要么模拟之前的 Apache RPM 的目录结构。

### 服务器安装

你可以在 Red Hat Linux 安装媒体或 Red Hat FTP 服务器上找到 Apache RPM。你可以像安装其他 RPM 一样，使用命令行 `rpm` 工具或 `glint`（X Window 软件包管理实用程序）安装它。使用 `rpm` 安装包请执行：

```
rpm -i latest_apache.rpm
```

其中 `latest_apache.rpm` 是最新 RPM 的名称。

如果你的系统中已经安装了 Apache，你可能想升级到新版本。使用 `rpm` 升级包请执行：

```
rpm -U latest_apache.rpm
```

Apache RPM 将文件安装在以下目录：

- `/etc/httpd/conf`——此目录包含所有的 Apache 配置文件，包括 `access.conf`、`httpd.conf` 和 `smd.conf`。
- `/etc/rc.d/**`——该目录下的树包含系统启动脚本。Apache RPM 为 Web 服务器安装了一套完整的脚本。你可以这些脚本从命令行启动和停止服务器，它们在工作站停止、启动或重启时也会自动启动和停止服务器。
- `/home/httpd`——RPM 将默认服务器图标和 CGI 脚本安装在此位置。
- `/usr/doc` 和 `/usr/man`——RPM 包含手册页和 readme 文件，它们存放在这些目录中。与大多数 RPM 包一样，`readme` 和其他相关文档存放在 `/usr/doc` 下以服务器版本命名的目录下。
- `/usr/sbin`——可执行程序放置在此目录中。

> 注意
> 如果你正在升级到更高版本的 Apache，RPM 将不会覆盖你当前的配置文件。RPM 会移动你当前的文件并追加扩展名 `.rpmnew`；例如，`srm.conf` 变为 `srm.conf.rpmnew`。

## 运行时服务器配置设置

Apache 从三个文件读取其配置设置：`access.conf`、`httpd.conf` 和 `srm.conf`。这种组织形式最初开发是为了与 NCSA 服务器保持向后兼容，但其背后的逻辑非常有道理。配置文件位于服务器分发包的 `conf` 子目录下。配置文件的备份副本——`access.conf-dist`、`httpd.conf-dist` 和 `srm.conf-dist`——包含在软件分发包中。

> 注意
> 最新版本的 Apache 使用不同的配置文件，但保持了与 NCSA 文件的后兼容。

你通过配置指令对服务器进行运行时配置，指令是设置某些选项的命令。你使用它们告诉服务器你想启用的各种选项，例如对服务器配置和运行重要的文件位置。配置指令遵循以下语法：

```
directive option option...
```

## 配置服务

第二部分

每行指定一个指令。某些指令仅设置值（如文件名）；其他允许你指定各种选项。某些特殊指令被称为“段”（sections），看起来像 HTML 标签。段指令由角括号包围，例如 `<directive>`：

```
<Directory dir/path>

directive option

directive option

</Directory>
```

所有段都用 `</directive>` 关闭。注意段标签与其他任何指令一样，每行指定。

> 提示 为了帮助维护你的服务器，你应该将全局范围配置放在 `httpd.conf` 中。你应该将目录特定的配置放在 `access.conf` 中，将资源配置放在 `srm.conf` 中。

## 编辑 httpd.conf

`httpd.conf` 包含了控制服务器如何运行的配置指令，日志文件在哪里、它运行的用户 ID `UID`、监听的端口等。你需要将某些默认配置值修改为适用于你网站的设置。我保留了大部分默认值，除了以下：

- `ServerAdmin` `ServerAdmin` 指令应设置为管理服务器的地址。它应该有效的电子邮件地址或别名，例如 `webmaster@your.domain`。设置此值很重要，因为当发生问题时会向访问者返回此地址（见图 9.1）。
- `User` and `Group` `User` and `Group` 指令设置处理请求时使用的 UID 和组 ID `GID`。我将它们保持为默认值：`nobody` 和 `group`。在 `/etc/passwd` 和 `/etc/group` 中验证这些名称是否存在。（由 Red Hat Linux 提供，因此应该已经定义。）如果你想使用不同的 UID GID，尽管这样做；但请注意服务器将以你定义的权限运行。指定 UID 和 GID 的权限应该是有限的，因为由于服务器（或更有可能是你自己的 CGI 程序）的安全漏洞，这些程序将以分配的 UID 运行。与其使用名称指定 `User` 和 `Group` 指令，你可以使用 UID 和 GID 数字。如果你使用数字，请确保指定的数字与你想要的用户和组对应，并且它们由井号 `#` 符号预测。

图 9.1
发生错误时返回的服务器消息之一。注意 Server 被设置为 `alberto@accessalink.com`。

![](img/7675e31a0e104594fbf0bbbebdf7e922_254_0.png)

如果按名称指定，这些指令如下：
`User nobody`
`Group nogroup`

按 UID 和 GID 指定的相同方式：
`User #-1`
`Group #-1`

`ServerName` `ServerName` 指令设置服务器返回的主机名。将其设置为完全限定域名名 `fqdn`。如果此

## 配置服务

第二部分

如果未设置值，服务器将自行确定名称并将其设置为其规范名称。然而，你可能希望服务器返回一个更易友的地址，例如 `www.your.domain`。无论你如何做，`ServerName` 应该是你网络的的真实域名系统（DNS）名称。如果你在管理自己的 DNS，请记住为你的主机添加一个 CNAME 别名。如果是其他人为你管理 DNS，请要求该人员为你设置此名称。

你的 `ServerName` 条目应该如下：
`ServerName servername.your.domain`

> 提示
> 如果你想在独立机器上为了测试目的安装 Web 服务器，可以通过指定 `ServerName` 为 `localhost` 来实现。然后你可以从独立机器通过 http://www.localhost 访问服务器。这种方法对于尝试新配置或互联网 Web 服务器非常有用。

### ServerRoot

此指令设置服务器目录的绝对路径。该指令告诉服务器去哪里寻找所有的资源和配置文件。许多这些资源在配置文件中是相对于 `ServerRoot` 目录指定的。你的 `ServerRoot` 指令应为：
`ServerRoot /etc/httpd`

## 编辑 httpd.conf

`httpd.conf` 文件是资源配置文件。它控制与你的 Web 文档树位置、CGI 程序目录以及其他影响你网站的资源配置问题相关的设置。我在我的 `httpd.conf` 文件中保留了大部分默认设置。此配置文件上最重要的指令如下：

- `DocumentRoot`
将此指令设置为你文档树的绝对路径。你的文档树是 Apache 提供服务的顶层目录。默认情况下，它被设置为 `/home/httpd/html`。

- `UserDir`
此指令定义了相对于本地用户主目录的目录，该用户将在该目录下放置公共 HTML 文档。它是相对的，因为每个用户将有其自己的 HTML 目录。此指令的默认设置为 `public_html`，因此每个用户都可以在其或或主主目录下创建一个名为 `public_html` 的目录，放置在该目录中的 HTML 文档将可以通过 http://servername/~username 访问，其中 `username` 是该特定用户的名称。

允许单个用户在你的服务器上放置 Web 内容涉及几个重要的安全考量。如果你在互联网上而非私有网络上运行 Web 服务器，你应该阅读 Lincoln Stein 编写的《WWW 安全 FAQ》。你可以在 http://www.genome.wi.mit.edu/WWW/www-security-faq.html 找到副本。

本章末的列表 9.3 包含一个 `conf/httpd.conf` 文件的副本。

## 编辑 access.conf

`access.conf` 是全局访问控制文件；它配置用户对你的网站及你提供的文档的访问类型，以及定义用户可以在多大程度上更改你可能设置的安全设置的问题。默认配置对 `DocumentRoot` 中的文档提供不受限制的访问。我在我的 `access.conf` 文件中保留了所有默认设置。

如果你想提供一组更严格的设置，你可能需要验证所有的 `<Directory>` 部分都与你在配置中列出的目录匹配。目录按目录指定了一组选项，通常涉及安全问题。特别是，你可能想在如下所示的部分删除位于 `Options` 指令之后的 `Indexes` 选项：

```
<Directory /home/httpd/html>

Options FollowSymLinks

</Directory>
```

（注：原文后半部分存在大量重复，已根据逻辑进行去重处理。）

## 配置服务

| 服务名称 | Socket 类型 | 协议 | 等待/不等待 | 服务器程序运行的用户 | 服务器程序 | 服务器程序参数 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| httpd | stream | | nowait | nobody | /sbin/ | |
| httpd | http | | | | httpd -f /etc/httpd/conf/httpd.conf | |

## 注意

上述示例以 `nobody` 身份启动服务器。通常情况下，你可能希望由 `root` 用户启动独立服务器，以便服务器能够绑定到 80 端口（标准 HTTP 端口），并能够更改其子进程的 UID 和 GID。当独立服务器启动时，它会派生（fork）出子进程。除非你通过 `User` 和 `Group` 指令指定了不同的设置，否则这些子进程将以 `nobody` 的 UID 和 `nogroup` 的 GID 运行。子进程处理 HTTP 请求。由 `root` 拥有的主进程负责创建和销毁其子进程。这使得标准的独立服务器变得安全。

如果你在示例中指定 `root` UID 的目的是在 80 端口运行 `inetd` 服务器，那么处理请求的进程将归 `root` 所有。这种设置可能会产生安全问题；与独立服务器不同，`inetd` 服务器不会派生任何子进程，因此它使用进程所有者的 UID 和 GID 来请求。

在 `/etc/inetd.conf` 中添加 `httpd` 条目后，你需要重启 `inetd`。你可以通过使用 `ps` 找到 `inetd` 进程号并向其发送 `HUP` 信号来实现：

```
# kill -HUP InetdProcessID
```

将 `InetdProcessID` 替换为 `ps` 命令列出的数字。如果显示的 PID 是 86，你就输入 `kill -HUP 86`。

`inetd` 随后会重启并重新读取配置文件，根据指令监听 8080 端口的请求。

## 首次运行 Web 服务器

在第一次运行服务器之前，你需要创建一个 HTML 文档。标准的 Apache 分发版包含此类文件，但我创建了另一个更有用的文件，我相信你将反复使用它。使用你喜欢的文本编辑器，在 `hdocs` 目录下创建一个名为 `index.html` 的文件，内容如下：

```html
<HTML>
<HEAD>
<TITLE>Red Hat Linux Unleashed</TITLE>
</HEAD>
<BODY BACKGROUND="#ffffff" LINK="#000080" VLINK="#000080">
<H1><CENTER>Red Hat Linux Unleashed</CENTER></H1>
<H2><CENTER>恭喜！您的 Apache 服务器已成功安装。</CENTER></H2>
<H3>这里有一些关于 Apache 服务器信息的有趣网站：</H3>
<UL>
<LI><A HREF="http://www.apache.org">Apache Group</A> 的官方首页
<LI><A HREF="http://www.apache-ssl.com">Community Connexion</A> 的官方首页
- Stronghold: Apache-SSL-US 的开发人员
- (一个基于 Apache 的兼容 Netscape 的 SSL 服务器)
<LI><A HREF="http://www.algroup.co.uk/Apache-SSL">Apache-SSL</A> 的官方首页
  (一个基于 Apache 的兼容 Netscape 的 SSL 服务器 - 仅供美国境外用户使用)。
<LI><A HREF="http://www.zyzyyva.com/server/module_registry/">Apache Module Registry</A>，你可以在这里找到关于第三方 Apache 模块和其他开发相关内容的信息。
<LI><A HREF="http://www.apacheweek.com">The Apache Week Home</A>，在这里你将找到一份关于 Apache 服务器信息的精要每周指南。
<LI><A HREF="http://www.ukweb.com">UK Web's Apache Support Center</A>
<LI><A HREF="http://www.fastcgi.com">The FastCGI Website</A>
</UL>
```

<P>

将此文件放在你的 `hdocs` 目录中。此时，你已经准备好测试服务器了。

## 启动独立服务器

如果你正在运行独立服务器，你需要手动启动 `httpd`。你可以通过输入以下行来实现：

```
# /sbin/httpd -f /etc/httpd/conf/httpd.conf
```

注意，我是从 `root` 账户启动独立服务器的，行开头的井号（#）表示了。你需要以 `root` 身份启动独立服务器，以便发生两个重要事件：

- 如果你的独立服务器使用默认 HTTP 端口（端口 80），只有超级用户才能绑定低于 1025 的互联网端口。
- 只有归 `root` 所有的进程才能根据 `User` 和 `Group` 指令更改它们的 UID 和 GID。如果你启动服务器...

## 配置服务

第二部分

```html
<STRONG>Deja News 一个非常实用的 USENET 搜索引擎</STRONG>
<FORM ACTION="http://search.dejanews.com/dquery.xp" METHOD=POST>
<P>
<CENTER>
<STRONG>快速搜索：</STRONG> <INPUT NAME="query" VALUE="Apache SIZE="7">
<INPUT TYPE="submit" VALUE="Search!"><INPUT NAME="defaultOp VALUE="AND" TYPE="hidden">
