
在列表 13.6 中，第 1 行定义了用于获取域名邮件的 ISP 邮件服务器。第 1 行还指示使用 `POP3` 协议进行连接。第 2 行到第 4 行定义了用于连接的选项。第 2 行指示 `fetchmail` 在邮件头中查找本地域名地址的标识符。因此，它将 `address@smallorg.org` 识别为本地邮件服务器用户。第 3 行指示不使用 `X-Envelope-To` 头部字段来解析收件人地址。邮件从一个站点传输到另一个站点时，`MTA`（邮件传输代理）通常会忽略这些头部字段，可能会让 `fetchmail` 产生困惑。第 4 行指示不使用 `DNS` 来确认发送主机的身份。第 5 行标识了 `fetchmail` 连接到 ISP 邮件服务器时使用的 ISP 信箱用户名和密码。这些由您的 ISP 提供。

第 6 行到第 13 行列出了 Linux 邮件服务器上所有可以接收邮件的本地用户。`fetchmail` 解析 `RFC822` 邮件头部字段并对这些用户名进行循环。如果找到了某个用户名，`fetchmail` 将将邮件递送到该本地用户。如果目标与列出的任何本地用户都不匹配，`fetchmail` 将将邮件递送到运行 `mailmail` 的用户（在此场景下为 `root` 用户）。邮件管理员的工作是向列表添加新的本地用户。第 14 行指示本地用户名位于运行 `fetchmail` 的本地主机上。

在创建 `.fetchmail` 文件并将其存储在运行 `fetchmail` 的用户（例如 `root` 用户）的 `$HOME` 目录中后，就可以运行该程序了。通过在命令行中输入 `fetchmail`，拨号程序应该自动启动 `PPP` 链路，`fetchmail` 应该自动连接到 ISP 邮件服务器并下载常用 ISP 信箱中等待的任何邮件消息。如果执行成功，下一步是使邮件取回过程自动化。

## 自动化邮件取回

在配置好 Linux 邮件服务器的所有各个部分后，下一步是自动化邮件检查和取回过程。必须定期执行的唯一功能是 `fetchmail` 操作。`sendmail` 程序应该已经作为后台进程在运行。

通过使用 Linux 的 `cron` 工具可以实现定期运行 `fetchmail` 操作。`cron` 工具读取一个包含在特定时间执行的脚本列表的表格。Linux 系统上的每个用户都有独立的 `cron` 表。例如，`root` 用户将运行 `fetchmail` 程序，因此必须修改 `root` 用户的 `cron` 表。修改表格的方法是登录为 `root` 用户并输入 `crontab -l`，你可以查看 `root` 用户现有的 `cron` 表。要更改表格，必须输入 `crontab -e`。这会使用 `vi` 编辑器编辑 `cron` 表。

要让 `fetchmail` 程序每 15 分钟执行一次，您需要在 `root` 用户的 `cron` 表中添加列表 13.7 所示的行。

### 列表 13.7 Fetchmail 示例 cron 条目

```
0,15,30,45 * * * /usr/bin/fetchmail
```

这表示每小时、每天、每周和每年的，在整点后的第 0、15、30 和 45 分钟将执行一次 `fetchmail` 程序。您可以根据需要修改此内容。注意不要频繁检查 ISP 信箱，否则拨号 `PPP` 链路可能没有机会在连接之间正确地断开。

## 带有 ISP 域名邮件池的按需拨号 PPP 连接

第三种场景也使用按需拨号 `PPP` 连接将邮件传输到 ISP 服务器。此场景的区别在于，您域名的域名邮件被缓存到 ISP 邮件服务器上的邮件队列中，而不是被递送到单个信箱。同样，这是 ISP 必须在它的邮件服务器上配置的功能。

在 Linux 邮件服务器建立 `PPP` 连接后，它可以与 ISP 邮件服务器建立 `SMTP` 连接，并请求邮件队列中的任何邮件发回。再次，这是 ISP 必须在它的邮件服务器上配置的功能。

在 Linux 邮件服务器建立 `PPP` 连接后，它可以与 ISP 邮件服务器建立 `SMTP` 连接，并请求邮件队列中的任何邮件发回。根据第 5 章的描述，ISP 配置。

在 Linux 邮件服务器建立 `PPP` 连接后，它可以与 ISP 邮件服务器建立 `SMTP` 连接，并请求邮件队列中的任何邮件发回。

`PPP` 配置 配置

此场景的 `PPP` 链路与之前场景。

，

与 Linux 邮件服务器建立 `SMTP` 连接。

```
3
```

取决于您的 ISP 环境，可能需要扩展超时值，以确保 ISP 邮件服务器有足够的时间建立连接。

`img/4afea5346095bafc057b1f7b908_380_0.png`

图 13.4
使用按需拨号 `PPP` 连接的 Linux 邮件服务器。

### sendmail 配置

使用按需拨号 `PPP` 连接的 Linux 邮件服务器。

### fetchmail 配置

使用按需拨号 `PPP` 连接的 Linux 邮件服务器。

### 连接邮件服务器到 ISP

第 13 章

### 列表 13.8 SMTP 示例 fetchmailrc

```
poll mail.net with proto ETRN

localdomains smallorg.org

no dns

no envelope
```

在列表 13.8 中，第 1 行指示要连接的远程主机，`fetchmail` 应该使用 `ETRN` 命令传输。第 2 行指示替代域名，因为 Linux 邮件服务器将接收邮件。您应该将该替代域名替换为您的域名。第 3 行和第 4 行指示 `fetchmail` 将不使用 `DNS` 验证邮件头中的域名，并且不会查看收件人的 `X-Receive-To:` `RFC2822` 字段。

与之前的场景相同，此场景能够自动运行 `fetchmail` 程序以检查 ISP 的新邮件。最简单的方法是使用 Linux `cron` 工具。再次，可以创建一个类似于列表 13.7 所示的脚本文件，并将其添加到 `root` 用户的 `cron` 表中。在此之前，可以设置 `cron` 调度频率。每当 `cron` 守护进程运行 `fetchmail` 程序时，拨号程序应与 ISP 邮件服务器建立 `PPP` 连接。

### 带有 ISP 邮件池的拨号 UUOC 连接

最后一个场景讨论了使用 `UUOC` 协议与邮件 服务器建立连接。任何发送邮件在 Linux 邮件服务器的 `UUOC` 区域缓存，并在 `UUOC` 连接建立时传输。同样，目标为 Linux 邮件服务器的入站邮件由 ISP 邮件服务器缓存，并在 `UUOC` 连接建立时传输。这在图 13.5 中所示。

### UUOC 配置

为了让 Linux 邮件服务器与 ISP 建立 `UUOC` 连接，必须安装 `UUOC` 软件。Linux 平台上常用的 `UUOC` 包是 Taylor `UUOC`。许多 Linux 发行版带有 Taylor `UUOC` 的二进制发行包。在 Mandrake Linux 6.0 中，软件包是 `uuecp-1.0mdk.i586.rpm`。可以使用标准的 `rpm` 包安装器安装 Taylor `UUOC`。

![](img/4af9afea53463095bafc6057b1f7b908_382_0.png)

图 13.5
使用拨号上网 `UUCP` 连接和 ISP 缓存域邮件的 Linux 邮件服务器。

如果你的 Linux 发行版没有包含 `UUCP` 的二进制发行包，你可以从 `sunite.unc.edu` 的 `/pub/Linux/systems/network/uucp` 目录下下载源代码。该位置提供的最新版本是 `uucp-1.05.tar.gz`。第 9 章“`UUCP` 协议”详细介绍了如何编译和安装该源码包。

在安装 Taylor `UUCP` 软件包后，必须对其进行配置以支持与 ISP `UUCP` 服务器的 `UUCP` 通信。Taylor `UUCP` 需要四个配置文件。通常位于 `/etc/uucp` 目录。第一个配置文件定义了 Linux 邮件服务器的 `UUCP` 节点名（`nodename`）。列表 13.9 显示了该文件的示例。

# 列表 13.9 Taylor UUCP 配置文件示例

`nodename smallorg`

下一个需要的文件是 `sys` 文件。`sys` 文件定义了 Linux 邮件服务器将通信的所有远程 `UUCP` 站点。在本例中，必须输入的站点只有 ISP `UUCP` 服务器。列表 13.10 显示了 `sys` 文件的示例。

# 列表 13.10 Taylor UUCP sys 文件示例

```
1 system ispmail

2 time Any

3 phone 555-1234

4 port modem

5 speed 38400

6 chat login: rich word: guitar
```
