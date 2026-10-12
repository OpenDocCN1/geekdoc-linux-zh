
## 邮件用户代理与邮件传输代理

要在你的 Red Hat Linux 电脑上配置用户电子邮件，你需要两种类型的邮件软件：

- **邮件用户代理**软件（有时用缩写 MUA 表示）允许你读取用户邮件消息、撰写回复以及创建新消息。通常，邮件用户代理使用 POP3 或 IMAP4 协议从邮件服务器检索消息。POP3 是邮政协议第 3 版，而 IMAP4 是互联网消息访问协议第 4 版。Red Hat Linux 光盘包含了几个流行的邮件用户代理，例如 *pine* 和 *elm*。
- **邮件传输代理**（MTA）软件实际负责发送和接收邮件消息文本。用于邮件传输的具体方法取决于底层网络。在 TCP/IP 网络中，邮件传输代理使用简单邮件传输协议 (SMTP) 来投递邮件。本书的 Red Hat Linux 光盘包含了 *sendmail*，这是 TCP/IP 网络中功能强大且流行的邮件传输代理。

大多数邮件传输代理以 *守护进程*（后台进程）的形式运行，只要你的系统处于开启状态，它们就会一直运行。因为系统中你或其他用户可以随时发送邮件，所以传输代理必须随时待命，以便将邮件投递到其目的地。邮件用户代理仅在用户希望读取来信、撰写和发送去信或检查新邮件时运行。

![](img/5fe8f856723cde0b366f73584b9e64b8_163_0.png)

通常，邮件传输代理在系统启动后开始运行。Red Hat Linux 的系统启动文件设置为当 Linux 系统处于 *多用户模式* 时启动 *sendmail* 邮件传输代理。Shell 脚本文件 */etc/rc.d/init.d/sendmail* 负责启动 *sendmail*。

## sendmail

由于系统已设置为在启动时自动运行 *sendmail*，你只需使用适当的 *sendmail* 配置文件即可在 Linux 系统上启用电子邮件。在正确配置 *sendmail* 邮件传输代理之前，你无法发送或接收电子邮件。*sendmail* 传输代理以其复杂但完整的邮件投递系统而闻名。如果你快速查看 *sendmail* 的配置文件 */etc/sendmail.cf*，你会发现 *sendmail* 确实很复杂。幸运的是，你不需要成为 *sendmail* 配置文件的专家。你只需要使用本书配套光盘中的预定义配置文件即可。

如果在安装 Red Hat Linux 期间安装了邮件/新闻工具组件，你的系统应该具有可用的 *sendmail* 配置文件 */etc/sendmail.cf*。默认文件假设存在互联网连接和名称服务器。只要你拥有互联网连接，一旦将 Linux 电脑连接到互联网，你应该就能发送和接收电子邮件。然后，你可以使用 *elm* 等邮件用户代理来撰写和发送邮件消息。

## 设置 Apache Web 服务器

你可能已经知道使用 Web 是什么感觉。然而，你可能不知道如何设置 Web 服务器，以便通过网页向全世界提供信息。要成为 Web 上的信息提供者，你必须在互联网上的 Red Hat Linux 电脑上运行 Web 服务器。

Web 服务器使用超文本传输协议 (HTTP) 提供信息。由于它们是持续运行的服务器，Web 服务器也被称为 HTTP 守护进程。本章节介绍的 Web 服务器通常名为 *httpd*。

在可自由获得的 Web 服务器中，Apache Web 服务器最受欢迎。Apache 可以通过互联网免费获取，并随本书的配套光盘一起提供给 Red Hat Linux。

当你从本书的配套光盘安装 Red Hat Linux 时，你也可以选择安装 Apache Web 服务器。如果在 Red Hat Linux 安装过程中安装了 Mail/WWW/News Tools 软件包，Red Hat Linux 将在系统启动时自动启动 Apache Web 服务器。

执行以下步骤以验证 Apache Web 服务器软件是否已安装并在你的系统上运行：

1. 输入以下命令以检查是否安装了 Apache Web 服务器：
   ```bash
   rpm -q apache
   apache-1.3.19-5
   ```
   如果输出显示 *apache* 包名称，则表示你的系统上已安装 Apache 软件。

2. 输入以下命令以检查 *httpd* 进程是否在运行：Apache Web 服务器程序的名称是 *httpd*：
   ```bash
   ps ax | grep httpd
   ```
   输出应该显示多个 *httpd* 进程。通常运行一个父进程和几个子 Web 服务器进程是很常见的，以便通过为每个 HTTP 请求分配一个 *httpd* 进程来高效地处理请求。

3. 在你的 Linux 系统上使用 *telnet* 程序，执行 HTTP HEAD 命令以查询 Web 服务器，如下所示：
   ```bash
   telnet localhost 80
   Trying 127.0.0.1...
   Connected to localhost.
   Escape character is '^]'.
   HEAD / HTTP/1.0
   ... Press Enter once more to type a blank line
   HTTP/1.1 200 OK
   Date: Sat, 19 Aug 2000 23:57:14 GMT
   Server: Apache/1.3.12 (Unix) (Red Hat/Linux)
   Last-Modified: Mon, 07 Aug 2000 10:21:07 GMT
   ETag: "328fe-b4a-398e8d93"
   Accept-Ranges: bytes
   Content-Length: 2890
   Connection: close
   Content-Type: text/html

   Connection closed by foreign host.
   ```
   如果你得到如上所示的响应，则说明你的系统已经正确安装并设置了 Apache Web 服务器。你只需要理解配置，以便将 HTML 文档放在正确的目录中即可。

4. 使用 Web 浏览器加载你系统的主页。通过点击 GNOME 面板上的大 "N" 图标启动 Netscape Navigator；查看 URL `http://localhost/`，然后看看会发生什么。你应该会看到标题为 "Red Hat Linux 上 Apache Web 服务器的测试页面" 的网页。

Apache Web 服务器被设置为从 */var/www/html* 目录提供 HTML 文档。因此，你应该将网页放在该目录中。特别是，你应该编辑或替换 */var/www/html/index.html* 文件，使其成为你自己的主页。

除了 HTML 文件，Apache Web 服务器还支持通用网关接口 (CGI) 程序，Web 服务器可以调用这些程序来访问其他文件和数据库。你应该将任何 CGI 程序放在 */var/www/cgi-bin* 目录中。请注意以下关于 Apache Web 服务器的有用信息：

- Apache Web 服务器配置文件位于 */etc/httpd/conf* 目录中。配置文件 *httpd.conf* 控制服务器的运行方式、提供哪些文档以及谁可以访问这些文档。
- */var/log/httpd* 目录是 Apache Web 服务器的访问日志和错误日志文件所在的位置。
- */etc/rc.d/init.d/httpd* 脚本在你的 Red Hat Linux 系统启动时启动 *httpd* 进程。

## 设置 FTP 服务器

除了电子邮件和 Web 服务外，匿名 FTP 是互联网主机上的常见服务。你可能熟悉 FTP，你可以使用它在互联网上将文件从一个系统传输到另一个系统。当你使用 FTP 传输文件到远程系统或从远程系统传输文件时，你必须先登录到远程系统才能使用 FTP。

如果你从本书的配套光盘安装 Red Hat Linux，你的系统应该已经设置了匿名 FTP，并且 FTP 服务器已配置为在需要时运行。默认设置还采用了必要的安全预防措施。

![](img/5fe8f856723cde0b366f73584b9e64b8_165_0.png)

输入以下命令以检查是否安装了 FTP 服务器：

```bash
rpm -q wu-ftpd
wu-ftpd-2.6.1-16
```

如果输出显示 *wu-ftpd* 包名称，则表示你的系统上已安装 FTP 服务器软件。

匿名 FTP 指的是用户名为 *anonymous*，任何人都可以使用该名称通过 FTP 从系统传输文件。匿名 FTP 是在互联网上共享文件的常见方式。许多企业使用匿名 FTP 来支持其客户。

输入以下命令以检查你的系统是否安装了匿名 FTP 支持：

```bash
rpm -q anonftp
anonftp-4.0-7
```

如果输出显示 *anonftp* 包名称，则表示你的系统支持入站匿名 FTP。

如果你曾使用匿名 FTP 从各种互联网站点下载文件，你已经知道该服务的便利性。匿名 FTP 使你能够将信息提供给互联网上的任何人。即使你没有明确使用匿名 FTP，你的 Web 浏览器也经常使用匿名 FTP 来下载文件。（你只需点击一个链接；Web 浏览器完成其余部分。）

要查看匿名 FTP 的运行情况，你可以尝试使用 FTP 客户端访问你的系统。例如，以下是某个用户从局域网上的另一台电脑访问其系统时的示例会话（他的输入以粗体显示）：

```text
ftp Inbp200
Connected to Inbp200
220 Inbp200.InbpSoft.com FTP server (Version wu 2.6.1.0(1)) Fri Feb 4 23:37:48 EST 2000) ready.
220 Inbp200 FTP server (Version wu 2.6.1(l)) Wed Aug 9 0:54:50 EDT 2000) ready.
Name (Inbp200:): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> bye
221 You have transferred 0 bytes in 0 files.
221 Total traffic for this session was 299 bytes in 0 transfers.
221 Thank you for using the FTP service on Inbp200.
221 Goodbye.
```

当你成功通过匿名 FTP 登录时，你将访问名为 *ftp* 的用户的家庭目录（默认目录为 */var/ftp*）。你应该将可公开访问的文件放在 */var/ftp/pub* 目录中。

