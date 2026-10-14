
Here you may limit the number of concurrent users from a given user class. To configure this option, you must provide a class for which the rule will apply, and the maximum number of users to allow to log in simultaneously. Next, you can choose times in UUCP `L.sys` format. This format is pretty simple, you choose the days by entering the first two letters with the first capitalized (i.e., `Su` for Sunday, or `Mo` for Monday), or `Any` for all days. Then the time is set in military format (1000 for 10AM, 2300 for 11PM, etc.). So to limit users during business hours, for example, we could enter `MoTuWeThFr0800-1800`. This option configures the `limit` directive.

## File and data transfer limits

This option provides access to the transfer limits features of WU-FTPD. It is possible to limit user's downloads based on files or data or both. You may also configure limits for outgoing and incoming transfers, and to which classes the limits should apply. This option configures the `file-limit` and `data-limit` directives.

## Deny access to files and Allow access to files even if denied

If there are files in your directory tree that you do not wish to be retrievable by one or more classes of users, you may enter it here. The path may be relative to the FTP `chroot`, or it may be an absolute path (select which using the Relative to `chroot` option). This option correlates to the `noretrieve` directive. The Allow access to files even if denied option allows you to unselect files that would ordinarily be made inaccessible by the previous option. This option correlates to the `allow-retrieve` directive.

## 匿名会话限制 访客会话限制

匿名用户和访客用户可以限制为指定的时间。此选项与 `limit-time` 指令相关。

## 最大登录失败次数

此选项允许您定义在向用户显示“登录失败次数过多”消息并关闭 FTP 连接之前允许的失败登录尝试次数。此选项配置 `loginfails` 指令，默认值为 5。

## 可以切换组？

如果启用此选项，用户在登录后可以切换到新组。用户随后将具有新组的权限。此选项配置 `private` 指令，默认关闭。

## 网络

在此处配置 WU-FTPD 的一些网络相关选项。

## TCP 窗口大小

此选项配置数据连接的 TCP 数据包窗口大小。如果客户端是 PPP 拨号用户，则可能有用，因为较小的 TCP 窗口可以提供更快的传输。通常无需修改此项。此选项与 `tcpwindow` 指令相关。

## PASV 连接的地址

允许控制对 `PASV` 命令响应的地址。此操作不会更改守护进程监听的地址，仅更改其在被动连接上向客户端报告的地址。此选项配置 `passive address` 指令。

## PASV 连接的端口

配置可用于被动数据连接的端口号。您可以为特定网络选择端口范围。当控制连接匹配指定的网络时，将从提供的范围内随机选择一个端口供守护进程监听。此功能允许使用限制开放端口的防火墙，同时仍提供 FTP 服务。此选项对应于 `passive ports` 指令。

## 日志

在此处配置 WU-FTPD 的日志行为（图 9-4）。该守护进程的日志记录相当简单，与 Apache 或 BIND 等服务器提供的选项相比几乎不算什么。尽管如此，仍可以从 FTP 守护进程收集大量有用的信息。

![](img/d84604054810a13cacfdac212ebee2f7_182_0.png)

图 9-4：日志

## 记录所有命令

在此处选择一种或多种用户类型，将提供该类型用户执行的每个命令的日志。此选项配置 `log commands` 指令。

## 记录传输

同上，您可以选择一种或多种用户类型进行日志记录。启用此选项后，将记录任何给定类型用户所做的每次文件传输。此选项配置 `log transfers` 指令。

## 记录传输到

此选项设置传输日志的存储位置。如果选择系统日志，传输将通过 `syslog` 守护进程记录到标准系统日志（由您的 `syslog` 配置决定）。如果选择 `XFER` 日志，传输将记录到单独的传输日志文件。此选项配置 `log syslog` 指令。

## 记录安全违规

可以配置服务器记录特定类型用户尝试执行被服务器拒绝的操作。此选项配置 `log security` 指令。

## 别名和路径

此页面允许您配置 FTP 守护进程在客户端发出 `cd` 命令时使用的别名。如果在 `cd` 目录别名部分定义了别名，则别名名称是客户端可以输入的目录名，而别名到目录字段定义客户端将切换到的目录。例如，如果别名名称为 `bin`，别名到目录为 `/home/ftp/pub/usr/local/bin`，则当客户端输入 `cd bin` 时，他将被定向到 `/home/ftp/pub/usr/local/bin`。

接下来是 `cd` 目录搜索路径。通过此选项，您可以配置任意数量可用于搜索路径的目录。例如，如果客户端输入 `cd bin`，而当前目录中没有 `bin` 目录，则服务器将检查搜索路径中的目录。如果请求目录存在于这些目录之一中，客户端将被定向到该目录。

## 匿名 FTP

WU-FTPD 为提供匿名（即未认证）用户服务提供了多种功能。匿名用户通常在服务器上只有非常有限的功能，通常无法上传文件或修改服务器上的任何内容。此页面提供与 FTP 服务器上的匿名用户相关的许多功能的访问。

## 匿名 FTP 根目录

此选项允许您为特定类别的匿名用户配置根目录。因此，将其设置为 `all` 类别的 `/home/ftp`，将导致服务器对任何匿名用户 `chroot` 到指定目录。初始目录（位于 `chroot` 目录之上）将是 `/etc/passwd` 中为用户 `ftp` 指示的主目录。使用此选项，可以使本地网络用户被 `chroot` 到与来自 Internet 的用户不同的目录。例如。此选项配置 `anonymous-root` 指令。

## 访客根目录

此选项与前一个选项类似，配置服务器的 `chroot` 行为。在这种情况下，它配置已使用有效用户名和密码登录的访客用户。因此，可以将 `chroot` 环境设置为 `/home`，从而使用户无法遍历该点以下的目录树。初始工作目录，除非另有指定，将是 `/etc/passwd` 中指定的用户主目录。此选项配置 `guest-root` 指令。

## 匿名用户的 Unix 组

在此处您可以配置默认的 UNIX 组，其权限将适用于特定类别的匿名用户。此选项配置 `autogroup` 指令。

## 匿名 FTP 密码检查

服务器始终在允许访问之前执行用户名和密码身份验证检查。惯例是接受空白用户名和用户的有效电子邮件地址。在此处您可以配置对给定电子邮件地址检查的严格程度，以及在电子邮件地址因某种原因无效时是否发出警告但仍允许登录，或拒绝访问。此选项配置 `passwd-check` 指令。

## 匿名 FTP 拒绝的密码

如果您希望更严格地禁止生成的密码，例如某些 Web 浏览器提供的密码，您可以在此处输入这些地址。这不会阻止浏览器客户端用户访问您的服务器，它只是强制他们配置浏览器以提供合法的电子邮件地址。此选项配置 `deny-email` 指令。

## 权限

此页面允许您配置每种类型用户对给定类别的权限。您可以创建任意数量的权限规则。

## 命令限制
