

ServerName reboot.nitec.com
DocumentRoot  "/www/reboot/public/htdocs"
ScriptAlias "/cgi-bin/" "/www/reboot/public/cgi-bin/"
</VirtualHost>

这里，虚拟主机 *reboot.nitec.com* 在虚拟主机容器标签内没有定义 *TransferLog* 或 *CustomLog* 指令。所有日志信息将存储在 *logs/access_log* 文件中。如果你在日志页面看到虚拟主机 *reboot.nitec.com* 的所有日志都记录在 *vhost_logs/reboot_access_log* 文件中，那么 *logs/access_log* 和 *logs/agents_log* 文件将不会用于名为 *reboot.nitec.com* 的虚拟主机。

TransferLog vhost_logs/reboot_access_log

## 记录 Cookie

到目前为止，讨论的日志选项无法唯一地识别访问者。唯一地识别访问者非常重要，因为如果你知道每个访问者发出的请求，你就能更好地了解你的内容是如何被使用的。例如，假设你的网站上有一个非常酷页面，并且你有办法在日志中识别访问者。如果你查看日志页面，发现许多访问者必须从一页跳到另一页才能找到最后那个酷页面，你可能会重新考虑站点设计，让那个酷页面在点击流中更早出现。Apache 有一个名为 *mod_usertrack* 的模块，它允许你通过记录 HTTP cookie 来跟踪你的网站访问者。

### HTTP Cookie……没有巧克力豆

HTTP cookie 不是由饼干面团制成的。它只是服务器提供给 Web 浏览器的一小段信息。这些信息通常存储在键=值对中，可以与整个网站或网站上的特定 URL 相关联。Cookie 由服务器发出并被 Web 浏览器接受后，该 cookie 将驻留在 Web 浏览器系统中。每次 Web 浏览器请求相同的 URL，或任何属于该 cookie URL 范围的 URL 时，cookie 信息都会返回给服务器。在设置 cookie 时，服务器可以告知 Web 浏览器在特定时间后使该 cookie 过期。时间可以指定为 cookie 在后续会话中永不被使用，或者可以使用很长一段时间。

关于 cookie 的使用存在很多争议。许多人认为 cookie 是对隐私的侵犯。使用 cookie 来跟踪用户行为非常流行。事实上，互联网上的几家广告公司大量使用 cookie 来跟踪用户。需要强调的是，cookie 本身不会造成任何伤害。

Cookie 数据通常以文本文件的形式写入你的浏览器软件的目录中。例如，使用标准日志模块中的 `CustomLog` 指令，你可以将 cookie 存储在一个单独的文件中：

CustomLog logs/clickstream "%{cookie}C %r %t"

现在，让我们来看看新的 `mod_usertrack` 模块。

请记住，`mod_usertrack` 并不保存 cookie 的日志；它只是为每个访问者生成唯一的 cookie。你可以使用 `CustomLog`（如前所述）将这些 cookie 存储在日志文件中以供分析。

`mod_usertrack` 指令并未编译到 Apache 的标准发行版中，因此你需要在使用该选项之前使用 `--enable-usertrack` 选项进行编译。该模块提供了以下各节中讨论的指令。

### **CookieExpires 指令**

该指令用于设置由模块生成的 cookie 的过期时间。过期时间可以定义为秒数，或者定义为如“1 month 2 days 3 hours”这样的格式。

**语法：** `CookieExpires expiry-period`

**上下文：** 服务器配置，虚拟主机

在以下示例中，第一个指令以秒为单位定义过期时间，第二个指令使用特殊格式定义过期时间。请注意，当过期时间未以数字形式定义时，将假设使用特殊格式。但是，特殊格式要求你用双引号将格式字符串括起来。如果未使用此指令，cookie 仅持续当前浏览器会话。

CookieExpires  3600
CookieExpires  "2 days 3 hours"

### **CookieTracking 指令**

该指令启用或禁用自动 cookie 的生成。当设置为 on 时，Apache 开始为所有新请求发送用户跟踪 cookie。该指令可用于按服务器或按目录基础开启或关闭此行为。默认情况下，编译 `mod_usertrack` 不会激活 cookie。

**语法：** `CookieTracking On | Off`

**上下文：** 服务器配置，虚拟主机，目录，按目录访问控制文件（`.htaccess`）

**重写：** `FileInfo`

## 使用错误日志

本章讨论了记录每个 Web 事务的请求和响应阶段各种有趣数据的几种方法。你收集关于访问者的数据越多，你的营销部门就会越高兴。然而，作为系统管理员，如果一切运行顺利你会很高兴。Apache 通过编写错误日志来让你知道哪里出了问题。如果不记录错误，你无法确定出了什么问题以及错误发生在哪里。毫不奇怪，错误日志记录是在核心 Apache 中支持的，而不是在像 `mod_log_config` 这样的模块中支持的。

`ErrorLog` 指令使你可以记录 Apache 遇到的所有错误。本节探讨如何将 Apache 错误日志整合到几乎所有 Unix 平台上广泛使用的 `syslog` 设施中。

`Syslog` 是记录由守护进程（服务器）进程发送的消息的传统方式。你可能会问：“Apache 是一个守护进程，为什么它不能写入 syslog？”实际上它可以。你所需要做的就是在配置文件中用以下内容替换现有的 `ErrorLog` 指令：

ErrorLog syslog

然后重启 Apache。使用 Web 浏览器访问你的 Web 服务器上的一个不存在的页面，并监视 `syslog` 日志文件，查看是否显示了 httpd 条目。你应该查看你的 `/etc/syslog.conf` 文件，以了解 httpd 消息将出现的位置。

例如，列表 8-1 显示了 Linux 系统的 `/etc/syslog.conf`。

### 列表 8-1: /etc/syslog.conf

# Log all kernel messages to the console.
# Logging much else clutters up the screen.
*kern.*				/dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none		/var/log/messages

# The authpriv file has restricted access.
authpriv.*			/var/log/secure

# Log all the mail messages in one place.
mail.*				/var/log/maillog

# Everybody gets emergency messages, plus log
# them on another machine.
*.emerg				*

# Save mail and news errors of level err and higher in a
# special file.
uucp,news.crit				/var/log/spooler

# Save boot messages also to boot.log
local7,local0,local1,local2,local3,local4,local5,local6,local7.*
				/var/log/boot.log

就 Apache 而言，此列表中有两行很重要，我在上面用**粗体**标出了它们。

第一行（以 `*,info;mail.none;` 开头）告诉 *syslog* 将所有信息类型的消息（除邮件和私有认证外）写入 `/var/log/messages` 文件，第二行（以 `*,emerg` 开头）规定所有紧急消息应写入所有日志文件。使用 `LogLevel` 指令，你可以指定 Apache 应发送给 *syslog* 的消息类型。例如：

ErrorLog syslog
LogLevel debug

这里，Apache 被指示将调试消息发送给 *syslog*。如果你希望通过 *syslog* 将调试消息存储在不同的文件中，则需要修改 `/etc/syslog.conf`。例如：

*.debug					/var/log/debug

在 `/etc/syslog.conf` 中添加这一行，并重启 *syslogd*（`kill -HUP syslogd_PID`）和 Apache，就可以将所有 Apache 调试消息存储到 `/var/log/debug` 文件中。有几种日志级别设置：

- **Alert：** 警报消息
- **Crit：** 严重消息
- **Debug：** 以调试级别记录的消息还包括生成该消息的源文件和行号，以帮助调试和代码开发
- **Emerg：** 紧急消息
- **Error：** 错误消息
- **Info：** 信息消息
- **Notice：** 通知消息
- **Warn：** 警告
