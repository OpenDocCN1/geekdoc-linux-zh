
`ServerAdmin` 设置当 Apache 报告错误时页面上显示的电子邮件地址。接收错误的人应该使用此电子邮件地址通知你错误。如果你不经常转发或检查你的 root 邮箱地址，你应该将此地址设置为一个你经常检查的地址。

```
ServerAdmin root@localhost
```

`ServerName` 定义了你所托管的特定 Web 网站的完整域名。该指令始终是完整域名，例如 `www.example.com`、`web.example.org` 或另一个 `example.net`。请记住，除非你设置了适当的 DNS，否则你不能随意发明主机。

```
ServerName www.example.com
```

`DocumentRoot` 指令是 Apache 服务器上用于该条目 Web 页面和数据的文件位置。管理员通常使用一个单一目录存放所有 Web 页面，例如 `/home/html/`，并在 `/home/html/` 目录下为每个域名创建一个目录。在这种情况下，`DocumentRoot` 将被设置为 `/home/html/domain`。其他时候，管理员会将 `DocumentRoot` 链接到用户的家目录，并在家目录下创建一个目录来包含文档。在这种情况下，`DocumentRoot` 将被设置为 `/home/user/domain` 或类似内容。

```
DocumentRoot "/home/httpd/html"
```

当有人尝试访问如 `http://www.example.com/-kara` 这样的 URL 时，Apache 查找的目录可以通过 `UserDir` 指令设置。通常，Linux 系统使用 `public_html` 作为此默认目录。

```
UserDir public_html
```

## 第 10 章

`DirectoryIndex` 指令是 Web 目录内假定首先加载的默认文件。这意味着如果你访问 `http://www.example.com`，`httpd` 将在 `DocumentRoot` 指令中查找，并根据 `DirectoryIndex` 列表的指定，自动加载名为 `index.html`、`index.shtml` 或 `index.cgi`（以存在的那个为准）。`index.html` 文件和相关文件是默认选项。如果你想更改此项，添加如 `home.html` 等文件，则需要修改以下内容：

```
DirectoryIndex index.html index.shtml index.cgi
```

`ErrorLog` 指令指定错误日志文件的位置。如果你在 `VirtualHost` 容器内没有指定 `ErrorLog` 指令，错误消息将默认记录在此处。许多管理员将所有日志放在一个主日志目录下。因此，在自定义场景下，`ErrorLog` 的适当设置为 `ErrorLog logs/www.example.com/error_log`。

```
ErrorLog /var/log/httpd/error_log
```

注意：在配置 Apache 或进行诸如添加虚拟主机等更改后，你必须重启 `httpd` 才能使更改生效。要重启 `httpd`，请通过运行 `/etc/rc.init.d/httpd restart` 或 `service httpd restart` 使用 restart 选项。

## 虚拟主机 (Virtual Hosts)

如上一节所述，虚拟主机是在 `httpd.conf` 文件中配置的。虚拟主机是允许不同的主机托管在同一台机器上的所有条目。最初，Web 服务器通常只能在单台机器上托管一个域名。虽然其他 Web 服务器开发了在单台机器上托管多个主机的方法，但 Apache 是第一个开发出在单一机器上托管多个域名的简单接口的。在机器上托管多个主机的概念被称为虚拟托管。

在虚拟托管开发的早期，Apache 要求为每个主机分配多个 IP 地址。现在 Apache 允许你配置多个主机共享同一个 IP 地址。这意味着两个域名可以分配相同的 IP 地址但拥有独立的 Web 站点。

## 配置虚拟主机

在你正确配置 Apache 后，有几个步骤通过编辑 `httpd.conf` 文件来配置你的虚拟主机：

- **设置 NameVirtualHost。** 只有在设置相同 IP 地址的主机时才需要 `NameVirtualHost`。如果你为每个主机都有独立的 IP 地址，请跳过此步骤。`NameVirtualHost` 设置可以是基于名称（`www.example.com`），也可以是基于 IP（`192.168.0.1`）。使用此设置告诉 `httpd` 特定名称（`www.domain.com`）或 IP 地址（`192.168.0.1`）下的多个主机。`NameVirtualHost` 指令下的 `VirtualHost` 条目由 `ServerName` 设置进行索引。`NameVirtualHost` 指令下的 IP 地址或域名请求将与 `ServerName` 和相应的 `DocumentRoot` 设置匹配。例如，`NameVirtualHost 192.168.0.1`。

- **设置 VirtualHost。** `VirtualHost` 的设置可以是基于名称（`www.example.com`），也可以是基于 IP（`192.168.0.1`）。管理员通常倾向于使用基于名称的设置。这种方法允许管理员在 DNS 中更改主机的 IP 地址而无需更改 `httpd.conf` 文件。确保你已经注册了域名并设置了 DNS 以确保其正常工作。例如，`<VirtualHost www.example.com>`。

- **设置 DocumentRoot。** `DocumentRoot` 设置指向存放主机 Web 文档的目录。此设置可能指向较大专用目录下的主机子目录（例如 `/home/httpd/domain`），或者指向用户家目录下的专用子目录（例如 `/home/user/domain`），或任何你喜欢的地方。在这个专用目录中，你应该放置 Web 站点所需的任何 HTML 或其他 Web 文件。确保 `DocumentRoot` 目录、子目录和文件都是可读且可执行的（目录权限至少设置为 755，文件权限设置为 644）。例如，`DocumentRoot /home/exampleadmin/example/`。

- 6. 设置 TransferLog。`TransferLog` 的设置指定了 `httpd` 记录主机所有访问信息的目录和文件。`TransferLog` 的默认设置为 `logs/access_log`。例如，`TransferLog logs/access_log`。

- 7. 关闭 VirtualHost 条目。要指定特定虚拟主机条目的结束，你必须通过提供 `</VirtualHost>` 选项作为虚拟主机条目的的最后一行来关闭它。例如，`</VirtualHost>`。

- 8. 保存并重启。保存 `httpd.conf` 文件中的更改，并重启 `httpd`（而不是重启系统）。要重启 `httpd`，请输入 `/etc/rc.d/init.d/httpd` 或执行 `service httpd restart`。

还有其他几个选项用于自定义你的单个虚拟主机条目。三个特定的选项包括 `Alias`、`Redirect` 和 `ServerAlias` 的设置：

- `Alias /sublocation /alternate_document_root` — 使用 `Alias` 设置允许你为主机下方的路径设置备备的位置文件。例如，如果你想为 `www.example.com/example/` 设置一个 `DocumentRoot`，但为 `www.example.com/` 使用完全不同的路径，你可以在 `www.example.com` 的虚拟主机条目中提供 `Alias` 以指向其 Web 文件的另一个目录。例如，`Alias /example /home/example`。

- `Redirect /sublocation/other.new.location` — 使用 `Redirect` 设置允许你在特定虚拟主机条目下为子目录指定备的位置。例如，如果你想让 `www.example.com/somewhere` 重定向到 `www.somewhere.org`，你可以为 `www.example.com` 的虚拟主机条目添加 `Redirect` 选项。例如，`Redirect /somewhere http://www.somewhere.org`。

- `ServerAlias *.example.com` — 使用 `ServerAlias` 允许你指定用于访问相同 Web 额外 `ServerName`。例如，你可以在 `www.example.com` 的虚拟主机条目中设置 `ServerAlias` 设置，允许用户不仅可以访问 `http://www.example.com/`，还可以访问 `http://example.com/` 和 `http://web.example.com/`。例如，`ServerAlias example.com *example.com`。

## 虚拟主机场景

为了更好地理解 `httpd.conf` 文件中虚拟主机条目的布局，请考虑以下场景，并查看以下场景的 `httpd.conf` 文件的片段。

## 场景

你的 Web 服务器被分配了三个 IP 地址：`123.12.12.1`、`123.12.12.2` 和 `123.12.12.3`。你想托管五个域名：`www.choc.com`、`www.bar.net`、`www.baz.org`、`www.example.com` 和 `www.iluvinus.com`。你决定为 `www.choc.com` 分配独立的 IP 地址 `123.12.12.1`。你决定将 `123.12.12.2` 共享给 `www.bar.net` 和 `www.baz.org`。你还决定将 `123.12.12.3` 共享给 `www.example.com` 和 `iluvinus.com`。你希望每个主机都在一个名为 `web` 的目录中拥有其文件，该目录是为具有相同主机名（即 `choc`、`bar`、`baz`、`example` 和 `iluvinus`）的用户专门设立。你决定将日志放在 `/etc/httpd/conf/` 下的某个位置。请注意，在共享指定 IP 的条目上方，你只需要使用一次 `NameVirtualHost` 设置（此 IP 设置可以被替换为地址解析到共享 IP 地址的域名）。列表 10.1 列出了此场景中的示例虚拟主机条目。

### 列表 10.1 httpd.conf 中的虚拟主机条目。

```
<VirtualHost 10.12.12.2
DocumentRoot /home/choc/web
ServerName www.choc.com
ErrorLog logs/www.choc.com/error_log
TransferLog logs/www.choc.com/access_log
</VirtualHost>
```

```
<VirtualHost www.bar.net>
DocumentRoot /home/bar/web
ServerName www.bar.net
ErrorLog logs/www.bar.net/error_log
TransferLog logs/www.bar.net/access_log
</VirtualHost>
```

```
<VirtualHost www.baz.org
DocumentRoot /home/baz/web
ServerName www.baz.org
ErrorLog logs/www.baz.org/error_log
TransferLog logs/www.baz.org/access_log
</VirtualHost>
```

```
<VirtualHost www.example.com>
DocumentRoot /home/example/web
ServerName www.example.com
ErrorLog logs/www.example.com/error_log
TransferLog logs/www.example.com/access_log
</VirtualHost>
```

```
<VirtualHost www.iluvlinus.com
DocumentRoot /home/iluvlinus/web
ServerName www.iluvlinus.com
ErrorLog logs/www.iluvlinus.com/error_log
TransferLog logs/www.iluvlinus.com/access_log
</VirtualHost>
```

## 邮件服务

邮件服务由三个部分组成：邮件传输代理 (MTA)、邮件传递代理 (MDA) 和邮件用户代理 (MUA)。

## procmail

Red Hat Linux 6.2 和 sendmail 默认使用的邮件传递代理是 procmail。procmail MDA 用于处理 MTA (sendmail) 和 MUA (邮件阅读器) 之间的邮件。通常，procmail 在安装 Red Hat Linux 6.2 时已安装。然而，如果有必要，你可以通过 RPM 安装 procmail。Red Hat Linux 6.2 附带的 procmail RPM 文件是 `procmail-3.14-i386.rpm`，位于 Red Hat Linux 6.2 光盘的 `/RedHat/RPMS/` 目录下。

## 配置 procmail

对于 procmail 的 MDA 服务，没有任何需要配置。这意味着安装后，procmail 可以开箱即用。你可以自定义 procmail 如何处理每个用户的邮件；你通过编辑每个用户主目录下的 `.procrc` 文件来实现。通过编辑用户主目录下的 `.procmailrc`，你可以启用邮件过滤、拦截等功能。有关通过 procmail 提供的过滤选项的详细说明，请运行 `man procmail`。

## 邮件客户端

邮件客户端是用户用于读取邮件的邮件用户代理（MUA）。有多种 MUA 可用。只要 MUA 支持 POP 或 IMAP 协议（在第 4 章中讨论）以远程接收邮件，就可以使用任何 MUA。Linux 上常用的邮件客户端包括 elm、pine 和 Netscape 邮件阅读器。

## Elm

MUA Elm 是一种用于 Unix 系统的基于文本的邮件阅读器。该界面是基于文本的，通过邮件阅读器提示的简单按键命令提供指令。邮件正文通过使用你的默认编辑器（emacs、elm 等）编辑文本文件来获取，该编辑器在运行 Elm 时会自动启动。要安装 Elm，请从 Red Linux 6.2 CD-ROM 的 `/RedHat/RPMS` 目录安装 `elm-2.5.3-6.i386.rpm`。图 10.1 显示了使用 Elm MUA 的界面。

## Pine

另一个流行的文本文本 MUA 是 Pine。Pine 阅读器比 Elm 基于按键组合菜单的选项更用户友好；Pine 使用了更简单的文本编辑器。要从 Red Hat Linux 6.2 CD 安装 Pine，请安装 `pine-4.21-8.i386.rpm` 文件。图 10.2 显示了 Pine 的文本界面。

## Netscape

除了大多数 Unix 系统上找到多个基于文本的 MUA 之外，还存在图形 MUA。记住，任何支持 POP 和 IMAP（在第 4 章中讨论）的 MUA 都应该可以在你的 Red Linux 系统上运行。我们的图形 GUI 是包含在 Netscape Communicator 中的 Netscape 邮件阅读器。Netscape MUA 具有图形用户界面，左侧是邮件箱的目录样式选项，右侧是邮件列表索引和邮件内容文本。Netscape 邮件阅读器顶部的按钮允许你操作 MUA 程序。要安装 Red Hat Linux 6.2 CD 上的 Netscape 邮件阅读器，你必须安装位于 CD 上 `/RedHat/RPMS/` 目录下的 `Netscape Communicator-4.72-i386.rpm`。图 10.3 显示了 Netscape 邮件阅读器的图形界面。

```
root@server: ~~
Mailbox: "/var/spool/mail/root" with 52 messages [ELM 2,5 PL]
DON'T DELETE THIS MESSAGE - FOLD
1 Aug 08 * Mail System Item (2)
2 Aug 08 * Mail Delivery Subs (6) Returned mail: Data format error
3 May 07 * Cron Daemon (22) Cron: rootbody:/run-parts/etc
4 May 07 * root               (20) errors rotating logs
5 May 07 * root               (20) errors rotating logs
6 May 06 * root               (20) errors rotating logs
7 May 06 * Cron Daemon (22) Cron: rootbody:/run-parts/etc
8 May 0*
9 Apr 09 * root               (20) errors rotating logs
10 10 Apr * root               (20) errors rotating logs

You can use any of the following commands by pressing the first character:
delete or undelete mail, a mail message, reply or forward mail, quit
To read a message, press 'return', j = move down, k = move up, ? = help
Command: _
```

图 10.1 Elm。

图 10.2 Pine。

## 域名服务 (DNS)

DNS 是负责管理主机名和域名到映射 IP 地址转换的服务。因此，DNS 负责将 IP 地址转换为其域名，并将域名转换为其分配的 IP 地址。运行在 Linux DNS 服务器上的程序名为 `named`。`named` 服务器是 BIND（Berkeley 互联网名称域）包的一部分，该包被全球超过 85% 的 DNS 服务器使用。
