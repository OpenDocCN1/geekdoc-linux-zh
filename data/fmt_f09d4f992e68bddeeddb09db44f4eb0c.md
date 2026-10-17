
```
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*

AddIcon /icons/binary.gif .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wrl.gz .vrm .iv
AddIcon /icons/compressed.gif .Z .tgz .zip
AddIcon /icons/a.gif .ps .ai .eps
AddIcon /icons/layout.gif .html .htm .pdf
AddIcon /icons/text.gif .txt
AddIcon /icons/c.gif .c
AddIcon /icons/p.gif .py
AddIcon /icons/f.gif .for
AddIcon /icons/dvi.gif .dvi
AddIcon /icons/uencoded.gif .uu
AddIcon /icons/script.gif .conf .sh .csh .ksh .tcl
AddIcon /icons/tex.gif .tex
AddIcon /icons/bomb.gif core

AddIcon /icons/back.gif ..
AddIcon /icons/hand.right.gif README
AddIcon /icons/folder.gif ^DIRECTORY^^
AddIcon /icons/blank.gif ^BLANKICON^^
```

# DefaultIcon 是对于没有显式设置图标的文件显示哪个图标。

```
DefaultIcon /icons/unknown.gif
```

# AddDescription 允许在服务器生成的索引中在文件后放置一个简短描述。格式：`AddDescription 'description'`

# ReadName 是服务器默认查找的文件名。格式：`ReadName`

# 服务器将首先查找 `name.html`，如果找到则包含它，然后查找 `name`，如果找到则以纯文本格式包含它。

# HeaderName 是应该在目录索引之前的文件名。

```
ReadName README
HeaderName HEADER
```

# IndexIgnore 是索引应该忽略的文件名。格式：`IndexIgnore name...`

```
IndexIgnore /* ~*
```

# AccessFileName 是在每个目录中查找访问控制信息的文件名。

```
AccessFileName .htaccess
```

# DefaultType 是服务器无法从扩展名找到文档的默认 MIME 类型。

```
DefaultType text/plain
```

# AddEncoding 允许某些浏览器解压文件。注意：并非所有浏览器都支持此项。

```
AddEncoding x-compress
AddEncoding gz
```

# AddLanguage 允许指定文档语言，然后使用内容协商为浏览器提供它可以理解的语言。注意，后缀不必与语言代码相同，以避免与 perl 脚本常用的后缀产生冲突。

```
AddLanguage .en
AddLanguage .fr
AddLanguage .de
AddLanguage .da
AddLanguage .el
AddLanguage .it
```

# LanguagePriority 允许在内容协商出现平局时赋予某些语言优先级。按偏好程度降序列出语言即可。

```
LanguagePriority en fr
```

# Redirect 允许告知客户端曾存在于你的服务器命名空间但现在不再存在的文档。这允许客户端查找重定向后的文档。格式：`Redirect fakename url`

# Aliases：允许根据需要设置任意别名（受限制）。格式为 `Alias fakename`

```
Alias /icons/ /home/httpd/icons/
```

# ScriptAlias：这控制包含服务器脚本的目录。格式：`ScriptAlias fakename realname`

```
ScriptAlias /cgi-bin/ /home/httpd/cgi-bin/
```

# 如果你想使用服务器包含（server includes），请取消以下行的注释。`AddType` 允许在不实际编辑 `mime.types` 的情况下对其进行调整，或将某些文件指定为特定类型。格式：`AddType type/subtype ext`

# `AddHandler` 允许将某些文件扩展名映射到“处理器”。这些可以是服务器内置的，也可以通过 `Action` 命令添加（见下文）。格式：`AddHandler action-name ext`

# 要使用 CGI 脚本：

```
AddHandler cgi-script .cgi
```

# 使用服务器解析的 HTML 文件

```
AddType text/html .shtml
AddHandler server-parsed .shtml
```

# 解消以下行以启用 Apache 的 send-as HTTP 功能

# AddHandler send-as-is

# 如果你想使用服务器解析的 imagemap 文件，使用：

```
AddHandler imap-file-map
```

# 要启用类型映射，你可能需要使用

# AddHandler type-map

# Action 允许在匹配的文件被调用时执行脚本。这消除了重复常用 CGI 文件处理器的 URL 路径的需求。格式：`Action media/type /cgi-script/location`

# 例如，要为具有 `.foot` 扩展名的文件添加页脚（文档根目录下的 `footer.html`），可以使用：

# AddHandler foot-action-foot

#Action foot-action /cgi-bin/footer

# 或者对所有 HTML 文件这样做，例如使用：

#Action text/html /cgi-bin/footer

# MetaDir：指定 Apache 可以找到元信息文件的目录名称。这些文件包含发送文档时包含的额外 HTTP 头

```
.MetaDir .web
```

# MetaSuffix：指定包含元信息的文件名后缀。

```
#MetaSuffix .meta
```

# 自定义错误响应（Apache 样式）

# 这些有三种类型

#

1) 纯文本

#ErrorDocument 500 'The server made a boo boo.'

# n.b. (*) 标记其为文本，不会被输出

#

2) 本地重定向

#ErrorDocument 404 /missing.html

# 重定向到本地 URL /missing.html

#ErrorDocument 404 /cgi-bin/missing_handler.pl

# n.b. 可以重定向到脚本或使用服务器包含的文档。

#3) 外部重定向

#ErrorDocument 404 http://other.server/info.html

```

例如，在我们上面的示例文件中，我们使用了指令：

```
ScriptAlias /cgi-bin/ /home/httpd/cgi-bin
```

此行表示 URL `http://linux.juxta.com/cgi-bin/` 指向 `home/httpd/cgi-bin/`。在该目录下，文件被视为 CGI 脚本，服务器将尝试执行这些文件，而不是将它们直接返回给请求客户端。

## AddHandler 和 AddType

`AddHandler` 和 `AddType` 指令确实需要结合考虑。

`AddHandler` 允许具有特定扩展名的文件映射到特定的操作，该操作可以是服务器的内置操作（例如运行 CGI 程序），也可以是外部操作（后者通常会调用服务器外的特殊程序，并通过该程序处理所涉及的文件）。

`AddType` 为特殊的扩展名创建一个新的 MIME 类型。MIME 类型对于告知客户端如何处理一个文件非常重要。例如，如果一个文件以 MIME 类型 `text/plain` 传递给浏览器，浏览器将不会解释该文件中所包含的任何 HTML 内容；而 `text/html` 的 MIME 类型则会导致浏览器将收到的文件作为 HTML 文件处理。

这两个指令两个主要用途是：允许在指定的 CGI 脚本目录之外执行 CGI 脚本，以及启用服务器解析的 HTML（这允许在将页面返回给客户端之前，由服务器处理 HTML 文件中嵌入的特殊标签）。

### 启用 CGI 脚本

你可以使用 `AddHandler` 指令在指定的 CGI 目录之外启用 CGI 处理。在我们的示例 `srm.conf` 文件中，我们使用：

```
AddHandler cgi-script .cgi
```

来表示任何具有 `.cgi` 扩展名且在指定 CGI 目录之外的文件都应被视为 CGI 程序并以这种方式处理。如果没有此指令，在 CGI 目录之外的 CGI 脚本将不会作为 CGI 程序处理；相反，文件的内容将直接返回给客户端。通常，这意味着用户将看到脚本的实际程序代码，而不是运行脚本的结果。

## 启用服务器解析的 HTML

`AddHandler` 和 `AddType` 指令都用于启用服务器解析的 HTML。Apache 的正常用法是：

```
AddType text/html .shtml

AddHandler server-parsed .shtml
```

在这里，`AddType` 确保服务器解析的 HTML 文件（扩展名为 `.shtml` 的文件）的结果将由客户端浏览器视为 HTML 并进行显示。

`AddHandler` 行表示扩展名为 `.shtml` 的文件应由服务器的 `server-parsed` 操作处理。这实际上为 `.shtml` 文件启用了服务器解析的 HTML。

## Access.conf

`access.conf` 的作用与 `httpd.conf` 和 `srm.conf` 有些许不同。此文件定义了允许在何时以及允许哪些类型的操作。它可以用于许多目的，包括指定访问限制以及限制脚本的执行位置（覆盖 `srm.conf` 中的设置）。

- # access.conf: 全局访问配置
- 在线文档：http://www.apache.org/
- # 此文件定义了服务器设置，这些设置影响允许哪些类型的服务以及在什么情况下允许。
- Apache 可访问的每个目录都可以针对该目录（及其子目录）允许和/或禁用的服务和功能进行配置。
- 原由 Rob McCool 创建
- 由 Arman Dansh 为 linux.juxta.com 适配
- # 这应该更改为你设置的 DocumentRoot 的任意值。

```
<Directory /home/httpd/None>
```

- # 也可以是 "None"、All" 或 "Indexes","Includes","FollowSymLinks","ExecCGI" 或 "MultiViews" 的任何组合。
- # 注意 "MultiViews" 必须“显式”命名 —— "Options All" 不会提供它（或者至少，目前还没有）。
- # Options Indexes FollowSymLinks

Options Includes

```
# 这控制了目录中的 .htaccess 文件可以

# 覆盖哪些选项。也可以是 'All' 或 'Options'、

# 'FileInfo' 'AuthConfig' 和 'Limit' 的组合
```

AllowOverride All

```
# 控制谁可以从此服务器获取内容。
```

```
# order allow,deny

# allow from all
```

```
order allow,deny

allow from all
```

```
<Directory>
# /usr/local/etc/httpd/cgi-bin 应该更改为任何存在的

# ScriptAliased 的 CGI 目录，如果你配置了该目录的话。
```

```
<Directory /home/httpd/cgi-bin>

AllowOverride None

Options None

</Directory>
```

```
# 允许服务器状态报告，URL 为 http://servername/status

# 将 ".nowhere.com" 更改为匹配你的域名以启用。
```

```
#<Location>/status>

#SetHandler server-status

#order deny,allow

#deny from all

#allow from .nowhere.com

#</Location>
```

```
# 你可以在此目录之后放置你想要

# 访问信息的任何其他目录或位置。
```

至少，`access.conf` 需要设置必要的权限以启用根目录 HTML 目录和 CGI 目录。你通常会发现，通过位于相关目录中的 `.htaccess` 文件为特定目录实现访问控制更简单。正如我们在上面讨论 `srm.conf` 文件的节中看到的，你必须启用这种目录级别的访问控制，它才能生效。

在下一节中，我们将讨论如何设置 `access.conf` 以启用 HTML 和 CGI 目录。

## 启用 HTML 目录

下面的代码是我们的示例 `access.conf` 中处理 HTML 文档根目录的章节：

```
<Directory /home/httpd/html>

Options Includes

AllowOverride All

order allow,deny

allow from all

</Directory>
```

此结构指定了 `/home/httpd/html` 目录。在 `Directory>` 和 `</Directory>` 标签之间包含了必要的指令。`Options` 指令用于指示在该目录（及其子目录）可以采取哪些特殊操作。可能值包括 `None`、`All`、`Indexes`、`Includes`、`FollowSymLinks`、`ExecCGI` 和 `MultiViews`。

下一个指令是 `AllowOverride`，它指示了本地 `.htaccess` 文件拥有覆盖条目的权限。可能值包括 `None`、`All`、`Options`、`FileInfo`、`AuthConfig` 和 `Limit`。例如，`Options` 值限制了 `.htaccess` 文件的覆盖。

在管理员对所有内容有良好控制的服务器上，允许完全覆盖是最简单的。当你运行具有多个用户控制自己目录的服务器时，限制这些用户覆盖全局配置可能是明智的。

最后，`order` 和 `allow` 指令共同控制谁可以访问该目录的页面。在这里，`order allow deny` 表示首先使用 `allow` 指令，如果该指令未允许用户获取所请求的文件，则应用任何 `deny` 指令。

通常，当你不应用访问控制时，你想使用 `order allow,deny`。当你尝试实施访问控制时，`order deny,allow` 是最佳选择（正如稍后我们构建带有访问控制的小示例站点时所示）。

紧随 `order` 指令的是 `allow` 指令，指示允许所有用户访问。如果你想完全理解如何拒绝用户，应该阅读 http://www.apache.org/ Apache 文档。

## 启用 CGI 目录

我们的 CGI 目录条目看起来略有不同：

```
<Directory /home/httpd/cgi-bin>

AllowOverride None

Options None

</Directory>
```

你可能对 `Options` 指令缺少 `ExecCGI` 选项感到惊讶。因为通过 `srm.conf` 中的 `ScriptAlias` 将 `/home/httpd/cgi-bin` 指定为 CGI 目录，所以没有在这里启用 CGI 执行。然而，如果你想在该目录之外允许脚本执行，将需要使用 `ExecCGI` 选项来允许它。

同样注意，所有的覆盖都被禁用。这通常是一个明智的主意，因为即使在配置良好的系统中，CGI 也是一个安全漏洞，防止 CGI 目录出现任何可能的安全错误是谨慎的。

## 管理您的 Web 服务器

除了能够启动和停止 Web 服务器之外，一旦您的 Web 服务器启动并运行，您将需要偶尔执行一些任务，以确保您的服务器继续无故障地运行。这些步骤包括创建和删除用户及用户组、使用访问控制保护目录，以及维护服务器日志以确保它们持续发挥作用。

## 启动和停止 Apache

如果你是通过 Red Hat 安装的 Apache，你的启动文件已经设置好在系统自启动时启动 Apache。这发生在 `/etc/rc.d/init.d/httpd.init` 文件中。该文件是一个可执行脚本，接受两个可能的参数：`start`（启动）和 `stop`（停止）。如果你计划使用 Red Hat 安装自带的 Apache 版本，并且不打算移动配置文件的位置，可以使用以下命令手动启动和停止 Web 服务器：

```
$ /etc/rc.d/init.d/httpd.init start
```

启动服务器

```
$ /etc/rc.d/init.d/httpd.init stop
```
