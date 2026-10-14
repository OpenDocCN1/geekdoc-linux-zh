

+   ► 一个网络/子网掩码对，例如 212.85.67.0/255.255.255.0。

+   ► 以无类别域间路由（CIDR）格式指定的网络地址；例如，212.85.67.0/24。这是前一个示例中使用的相同网络和子网掩码的 CIDR 表示法。

如果可以选用的话，最好基于 IP 地址而不是主机名来设置访问控制。这样做可以获得更快的性能，因为不需要名称查找——客户端的 IP 地址包含在每个请求中。

你也可以使用 allow 和 deny 来根据特定环境变量是否存在与否来提供或拒绝对网站内容的访问。例如，下面的语句拒绝包含名为 NOACCESS 的环境变量的上下文的请求访问：

```
deny from env=NOACCESS
```

Apache 的默认行为是先应用所有 deny 指令，然后再检查 allow 指令。如果你想更改此顺序，可以使用 order 语句。Apache 可能以三种不同的方式解释此语句：

+   ► Order deny,allow—deny 指令在 allow 指令之前被评估。如果主机未被明确拒绝访问，则允许其访问资源。这是如果未指定其他内容时的默认排序。

+   ► Order allow,deny—所有 allow 指令在 deny 指令之前被评估。如果主机未被明确允许访问，则拒绝其访问资源。

+   ► Order mutual-failure—只有同时在 allow 指令中指定并且在同一时间未出现在 deny 指令中的主机才被允许访问。如果主机未出现在任一指令中，则不授予访问权限。

考虑这个例子。假设你只想允许来自你自己域内的人员访问你的网站上的 server-status 资源。如果你的域名为 gnulix.org，你可以在配置文件中添加以下几行：

```
<Location /server-status>
SetHandler server-status
Order deny,allow
Deny from all
Allow from gnulix.org
</Location>
```

## Authentication

身份验证是确保访客确实是他们声称的人的过程。你可以配置 Apache 仅允许能够验证其身份的客户端访问特定 Web 内容区域。Apache 中有几种身份验证方法；基本身份验证是最常见的（也是本章讨论的方法）。

在基本身份验证下，Apache 要求用户提供用户名和密码以访问受保护的资源。然后 Apache 验证用户是否被允许访问相关资源。如果用户名可接受，Apache 会验证密码。如果密码也通过检查，用户将被授权，Apache 将提供请求。

HTTP 是一种无状态协议；发送到服务器的每个请求和每个响应都是单独处理的，而不是以智能方式处理。因此，身份验证信息必须包含在每个请求中。这意味着对受密码保护区域的每个请求都更大，因此会稍慢一些。为了避免不必要的系统使用和延迟，只保护绝对需要保护的网站区域。

要使用基本身份验证，你需要一个列出哪些用户被允许访问资源的文件。该文件由包含名称和密码对的纯文本列表组成。它看起来非常像你的 Linux 系统的 /etc/passwd 用户文件。

### CAUTION

不要使用 /etc/passwd 作为身份验证的用户列表。当你使用基本身份验证时，密码和用户名以 base64 编码文本的形式从客户端发送到服务器——这与纯文本一样可读。用户名和密码包含在发送到服务器的每个请求中。因此，任何可能在网络流量中窃听的人都能够获取这些信息！

要为 Apache 创建用户文件，请使用 htpasswd 命令。它包含在 Apache 软件包中。如果你使用软件包安装，它位于 /usr/bin。运行不带任何选项的 htpasswd 会产生以下输出：

```
Usage:  htpasswd [-c[m dps]] passwordfile username
htpasswd -b[c[m dps]] passwordfile username password

    htpasswd -n[m dps] username
    htpasswd -nb[m dps] username password

-c Create a new file.
-n Don't update file; display results on stdout.
-m Force MD5 encryption of the password.
-d Force CRYPT encryption of the password (default).
-p Do not encrypt the password (plaintext).
-s Force SHA encryption of the password.
-b Use the password from the command line rather than prompting for it.
-D Delete the specified user.
On Windows, TPF and NetWare systems the '-m' flag is used by default.
On all other systems, the '-p' flag will probably not work.
```
