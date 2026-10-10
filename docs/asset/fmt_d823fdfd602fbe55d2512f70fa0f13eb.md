
## CGI 文件

通用网关接口（CGI）文件是可以由访问您站点的 Web 浏览器执行的程序。CGI 文件通常由执行该程序作为其显示内容一部分的网页发起。传统上，CGI 程序被放置在一个名为 `cgi-bin` 的目录中，并且只有当它们驻留在这样一个特殊目录中时才能被执行。

### CGI-Bin 配置

通常，每个网站只有一个 `cgi-bin` 目录。发行版通常会在默认的 Web 服务器目录中设置一个 `cgi-bin` 目录（在 Fedora 上为 `/var/www/cgi-bin`）。在此处，你可以放置任何可以在你的网站上执行的 CGI 程序。`ScriptAlias` 指令为 `cgi-bin` 目录指定一个别名。任何 Web 页面或浏览器都可以使用该别名来引用此目录。

```
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
```

### 自动目录索引

当给定目录的 URL 而非 HTML 文件，且该目录中没有默认 Web 页面时，Apache 会即时创建一个页面并显示它。这通常只是该目录中不同文件的列表。实际上，Apache 为你索引了目录中的项目。你可以为生成和显示此类索引设置多个选项。如果 `FancyIndexing` 被开启，Web 页面项目将以图标和列标题显示，这些列标题可用于对列表进行排序。

```
FancyIndexing on
```

### 身份验证

你的 Web 服务器还可以基于每用户或每组的基础来控制对网站上特定目录的访问。你可以要求不同级别的认证。访问可以限制为特定用户并要求密码，或者扩展为允许组成员访问。你可以完全取消密码要求，或者设置一种类似于 FTP 使用的匿名访问类型。

要将身份验证指令应用于特定目录，你可以将这些指令放在 `Directory` 块或目录的 `.htaccess` 文件中。你使用 `require` 指令来确定哪些用户可以访问该目录。你可以列出特定的用户或组。`AuthName` 指令向用户提供认证域，该名称用于标识此认证过程访问的特定资源集。`AuthType` 指令指定认证类型，例如 basic 或 digest。`require` 指令还要求 `AuthType`、`AuthName` 以及指定组和用户认证文件位置的指令。在以下示例中，仅允许用户 `george`、`robert` 和 `mark` 访问 `newpics` 目录：

```
<Directory /var/www/html/newpics>

    AuthType Basic

    AuthName Newpics

    AuthUserFile /web/users

    AuthGroupFile /web/groups

    <Limit GET POST>

        require users george robert mark

    </Limit>

</Directory>
```

下一个示例允许管理员组访问 CGI 目录：

```
<Directory /var/www/html/cgi-bin>

    AuthType Basic

    AuthName CGI

    AuthGroupFile /web/groups

    <Limit GET POST>

        require groups admin

    </Limit>

</Directory>
```

要为目录设置匿名访问，请将 `Anonymous` 指令及其参数用户 anonymous 放在该目录的 Directory 块或 .htaccess 文件中。你还可以使用 `Anonymous` 指令允许特定用户访问而不需要他们提供密码。

Apache 维护自己的用户和组认证文件，指定哪些用户和组被允许访问哪些目录。这些文件通常是简单的平面文件，类似于系统密码和组文件。然而，它们可能会变得很大，从而可能减慢认证查找速度。作为一种替代方案，许多站点使用数据库管理文件来代替这些平面文件。然后使用数据库方法来访问文件，提供更快的响应时间。Apache 有用于指定认证文件的指令，具体取决于你使用的文件类型。`AuthUserFile` 和 `AuthGroupFile` 指令用于指定具有标准平面文件格式的认证文件的`位置`。`AuthDBUserFile` 和 `AuthDBGroupFile` 指令用于 DB 数据库文件，而 `AuthDBMGroupFile` 和 `AuthDBMGroupFile` 用于 DBM 数据库文件。

`htdigest`、`htpasswd` 和 `dbmmanage` 程序是 Apache 软件包提供的工具，用于创建和维护*用户认证文件*，即列出有权访问你网站上特定目录或资源的用户的用户密码文件。`htdigest` 和 `htpasswd` 程序管理简单的平面用户认证记录文件，而 `dbmmanage` 使用更复杂的数据库管理格式。如果你的用户列表非常广泛，你可能希望使用数据库文件以便快速查找。`htdigest` 的参数为认证文件、域和用户名，用于创建或更新用户条目。`htpasswd` 还可以对密码进行加密。`dbmmanage` 拥有一系列广泛的选项来添加、删除和更新用户条目。有多种不同的数据库格式用于设置此类文件。三种常见的格式是 Berkeley DB2、NDBM 和 GNU GDBM。`dbmmanage` 按此顺序查找这些格式的系统库。请注意使用相同的格式来设置你的认证文件。

# 日志文件

Apache 维护所有用户对网站请求的日志。默认情况下，这些日志包含使用通用日志格式（CLF）的记录。每个请求的记录占一行，由多个字段组成：主机、身份检查、认证用户（用于登录）、日期、客户端提交的请求行、发送给客户端的状态以及以字节为单位发送的对象大小。

## Webalizer

可以使用 Webalizer 工具生成 Web 日志报告。Webalizer 将显示你网站使用情况的信息。当你运行 `webalizer` 命令时，使用报告将被放置在 `/var/www/html/usage` 目录中。访问索引页面以显示包含月度报告链接的页面，`file:/var/www/html/usage/index.html`。报告配置在 `/etc/webalizer.conf` 文件中指定。之前的摘要保存在 `/etc/webalizer.history` 文件中。

## 自定义日志

使用 `LogFormat` 和 `CustomLog` 指令，你可以自定义日志记录，以添加不同详细程度的更多细节。这些指令使用由字段限定符组成的格式字符串来确定日志记录中记录的字段。你可以添加任何想要的字段，并且顺序任意。字段限定符由百分号（`%`）符号后跟一个标识字符组成。例如，`%h` 是远程主机的字段限定符，`%b` 是以字节为单位的大小，`%s` 是状态。有关完整列表，请参阅 mod_log_config 模块的文档。你应该引用可能包含不止一个单词的内容的字段。引号本身必须用反斜杠转义才能包含在格式字符串中。以下示例是将通用日志格式实现为 `LogFormat` 指令：

```
LogFormat "%h %l %u %t \"%r\" %s %b"
```

日志格式中的某些字段限定符可以限定以记录特定信息。`%I` 限定符记录服务器接收的请求中的头部行。要记录的特定头部行的引用放在 `%` 和字段限定符之间的大括号内。例如，`User-agent` 是指示请求中使用的浏览器软件的头部行。要记录 User-agent 头部信息，使用转换限定符 `%{User-agent}.I`。

为了与 NCSA 服务器保持兼容，Apache 最初实现了 `AgentLog` 和 `RefererLog` 指令来记录 User-agent 和 Referer 头部。这些后来被用于 `LogFormat` 和 `CustomLog` 指令的限定 `%I` 字段限定符所取代。Referer 头部记录来自客户端的链接信息，检测谁可能链接到你的网站。以下是一种符合 NCSA 标准的日志格式：

```
"%h %l %u %t \"%r\" %s %b" "%{Referer}i\n \"%{User-agent}i\n"
```

## 生成和管理日志文件

你可以使用 `CustomLog` 或 `TransferLog` 指令创建多个日志文件，而不是维护一个大型日志文件。这对虚拟主机很有帮助，你可能希望为每个主机维护一个单独的日志文件。你使用 `LogFormat` 指令定义日志记录的默认格式。`TransferLog` 然后在创建新日志文件时使用此默认值作为其格式。`CustomLog` 将这两个操作结合在一起，允许你创建新文件并为其定义格式。

```
LogFormat "%h %l %u %t \"%r\" %s %b"

# 使用 LogFormat 格式创建名为 myprojlog 的新日志文件

TransferLog myprojlog

# 使用其自己的格式创建名为 mypicslog 的新日志文件
```
