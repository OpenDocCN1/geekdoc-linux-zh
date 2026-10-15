
# VirtualHost: 允许守护进程响应多个服务器地址的请求，如果你的服务器配置配置为接收多个地址的 IP 数据包。这可以通过 `ifconfig` `alias` 标志，或通过像 VIF 这样的内核补丁来实现。

任何 `httpd.conf` 或 `srm.conf` 指令都可以放入 `VirtualHost` 命令。另参见 `BindAddress` 条目。

```
<VirtualHost host.some_domain.com>
#ServerAdmin webmaster@host.some_domain.com
#DocumentRoot /www/docs/host.some_domain.com
#ServerName host.some_domain.com
#ErrorLog logs/host.some_domain.com-error_log
#TransferLog logs/host.some_domain.com-access_log
</VirtualHost>
```

Apache 支持虚拟主机概念，这意味着你的服务器可以同时作为 `al.mybox.com`（具有 `mybox.com` 的 DNS 别名）、`www.verysmallcompany.com` 和 `www.wehavenmoney.org` 存在。虚拟主机的实现只需配置你的机器以接收指向额外 IP 地址的数据包，并为 Apache 提供更多的配置指令。上述讨论的相同指令（在 `srm.conf` 和 `access.conf` 文件中）可以用于 `<VirtualHost>... </VirtualHost>` 标签之间。

## 配置内容可用性

服务器资源映射（Server Resource Map）文件包含了用于控制客户端请求的选项。该规范规定了作为客户端请求响应发送的内容。默认文件名 (`/etc/httpd/conf/srm.conf`) 可以被 `ResourceConfig` 指令覆盖。以下章节显示了 `srm_conf` 的内容并描述了如何使用它。

## 识别 HTTP 内容目录

在 `srm_conf` 文件中，你可以定义包含 Web 内容目录。指令包括 `DocumentRoot`、`UserDir` 和 `DirectoryIndex`：

```
##
## srm_conf - Apache HTTP 服务器配置文件
```

```
# 通过此文档，你定义了用户所看到的你的 http
# 服务器的命名空间。此文件还定义了影响请求处理方式
# 以及结果应如何格式化的服务器设置。
```

```
# 更多信息请参阅 http://www.apache.org/ 的教程。
```

```
# 最初由 Rob McCool 编写；为 Apache 适配
```

```
# DocumentRoot: 你提供文档的目录。
# 默认情况下，所有请求都来自此目录，但可以使用
# 符号链接和别名指向其他位置。
```

```
DocumentRoot /home/httpd/
```

```
# UserDir: 当接收到 -user 请求时，附加到用户主目录
# 之后的目录名称。
```

```
UserDir public_html
```

```
# DirectoryIndex: 用作预写的 HTML 目录
# 索引的文件或多个文件。多个条目之间用空格分隔。
```

```
DirectoryIndex index.html index.shtml cgi
```

`DocumentRoot` 指令指定了用于 HTTP 请求的目录树。例如，URL `http://localhost/manual/mod/core.html`（该 URL 提供了关于 `http_core` 模块的信息）引用了物理文件 `/home/httpd/manual/mod/core.html`（使用上方的默认值）。

`UserDir` 有两种方式可以处理包含用户名（即 `-cj`）的传入请求。一种可能的格式是识别用户公开访问目录的物理路径。另一种可以是指定一个请求将被重定向的 URL。表 21-3 展示了几个示例，使用 URL `http://www.mybox.com/~cjb/proj/c004.html` 作为示例请求。

### 表 21-3

UserDir 路径名和 URL 示例

| UserDir 指令 | 所引用的路径或 URL |
| --- | --- |
| UserDir public_html | ~cjb/public_html/proj/c004.html |
| UserDir /public/*/WWW | /public/cjb/WWW/proj/c004.html |
| UserDir /usr/local/web | /usr/local/web/cjb/c004.html |
| UserDir http://www.mybox.com/users | http://www.mybox.com/users/cjb/c004.html |
| UserDir http://www.mybox.com/~* | http://www.mybox.com/~cjb/proj/c004.html |
| UserDir http://www.mybox.com/*/html | http://www.mybox.com/cjb/html/c004.html |

`UserDir` 指令也可用于显式允许或拒绝特定用户的 URL 到路径名的转换。例如，包含以下行代码以避免发布不应公开的数据是件好主意：

```
UserDir disable root
```

或者，使用以下行禁用除少数用户以外的所有用户的转换：

```
UserDir disable
UserDir enable wilhelm cjb jsmith
```

`DirectoryIndex` 建立了一个文件列表，当传入的请求指定目录而不是文件时使用该列表。例如，客户端请求 URL `http://www.mybox.com/~jsmith`。因为是一个目录，它会自动翻译为 `http://www.mybox.com/~jsmith/`。现在会搜索该目录并寻找 `DirectoryIndex` 指令中列出的任何文件。第一个匹配项（来自 `index.html`、`index.shtml` 和 `index.cgi` 的默认列表）被用作目录的默认文档。如果不存在这些文件（如 `access.conf` 文件中所示），服务器将自动生成目录中文件的索引。

## 定义索引

对于你的 Apache 服务器，为不同类型的文件显示不同的图标是可能的。应该开启 `FancyIndexing` 并使用 `AddIconEncoding`、`AddIconByType` 和 `AddIcon` 指令：

```
# FancyIndexing 决定你想要 fancy 目录索引还是标准的
FancyIndexing on
```

```
# AddIcon 通知服务器为不同的文件或文件名扩展名
# 显示哪个图标
```

```
AddIconByEncoding(CMP,/icons/compressed.gif) x-compress x-gzip

AddIconByType(TXT,/icons/text.gif) text/*
AddIconByType(IMG,/icons/image2.gif) image/*
AddIconByType(SND,/icons/sound2.gif) audio/*
AddIconByType(VID,/icons/movie.gif) video/*

AddIcon/icons/binary.gif .bin .exe
AddIcon/icons/bin.gif .hqx
AddIcon/icons/tar.gif .tar
AddIcon/icons/world.gif .wrl .grz .vrm .iv
AddIcon/icons/compressed.gif .Z .tgz .zip
AddIcon/icons/a.gif .ps .eps
AddIcon/icons/layout.gif .html .shtml .htm .pdf
AddIcon/icons/text.gif .txt
AddIcon/icons/c.gif .c
AddIcon/icons/p.gif .pl .py
AddIcon/icons/f.gif .for
AddIcon/icons/d.gif .dvi
AddIcon/icons/uencoded.gif .uu
AddIcon/icons/script.gif .conf .sh .ksh .tcl
AddIcon/icons/tex.gif .tex
AddIcon/icons/bomb.gif core

AddIcon/icons/back.gif .DIRECTORY
AddIcon/icons/hand.right.gif README
AddIcon/icons/folder.gif DIRECTORY
AddIcon/icons/blank.gif BLANK
```

```
# DefaultIcon 是对于没有显式设置图标的文件，
# 显示哪个图标。
```

```
DefaultIcon /icons/unknown.gif

# AddDescription 允许你在服务器生成的索引中，
# 在文件之后放置一个短的描述。
# 格式：AddDescription "description" filename
```

```
# ReadName 是服务器默认查找的 README 文件名。
# 格式：ReadName
# 服务器将首先查找 name，如果找到则包含它，
# 然后它会再次查找 name，如果找到，则将其作为纯文本包含。
# HeaderName 是应该在目录索引前部追加的文件名。
```

```
ReadName README
HeaderName HEADER
```

```
# Indexignore 是一组目录索引应该忽略的文件名
# 格式：Indexignore name
```

```
Indexignore . RCS
```

上一个选项块处理了如何处理服务器生成的索引。`FancyIndexing` 指令允许自动生成的目录索引包含关于每个文件或目录的几项信息，包括代表文件类型的图标、文件名、文件的最后修改时间、文件的大小，以及对该的描述。如果 `FancyIndexing` 指令设置为关闭（off），则索引中仅列出文件名。

`AddIconByEncoding` 指令用于配置 `FancyIndexing` 指令的输出。它强制为匹配特定 MIME 编码的文件显示特定的图标。在上面的行中，对于 MIME 编码为 `x-compress` 和 `x-zip` 的文件，将显示 `compressed.gif`（对于不加载图像的浏览器，带有备用标签 "CMP"）。`AddIconByType` 指令具有相同的语法，但它是根据文件的 MIME 类型进行匹配。

`AddIcon` 指令执行类似的功能，图标根据文件名中的模式显示。例如，在上面的行中，对于以 ".core" 结尾的文件将显示 `bomb.gif`，对于以 ".bin" 和 ".exe" 结尾的文件将显示 `binary.gif`。文件夹图标代表子目录，`back.gif` 文件将显示以允许导航回父目录，而名为 `README` 的文件将与 `hand.right.gif` 文件关联。`blank.gif` 文件被插入到自动生成的列表中，以保持适当的格式。

如果 `AddIcon`、`AddIconByEncoding` 或 `AddIconByType` 指令之间存在冲突，则 `Default` 指令具有优先级。它指定了如果没有之前的指令将图标与特定文件关联，则要显示的图像（根据上面的行，为 `unknown.gif`）。

`HeaderName` 和 `ReadName` 指令指定了如果这些文件存在，将哪些文件插入到自动生成的目录索引的顶部和底部。使用上面的默认值，服务器将首先查找 `HEADER.html`，然后查找 `HEADER`，以包含在“fancy索引”的顶部。在索引末尾，插入 `README.html` 或 `README`（以先找到的为准）。

`Indexignore` 指令指定了不应出现在自动目录索引中的文件。上面的行排除了：
- 任何以点开头且包含至少两个字符的文件名
- 任何以 - 或 # 结尾的文件名（通常由文本编辑器用临时文件或备份文件）
- 以 `HEADER` 或 `README` 开头的文件（根据 `HeaderName` 和 `ReadName` 指令，显示在目录列表顶部和底部的文件）
- `RCS`（版本控制系统）目录

## 设置访问控制、MIME 类型、编码和语言

访问控制信息和 MIME 类型的位置由 `AccessFileName` 和 `TypesConfig` 指令定义。`DefaultType` 和 `AddEncoding` 允许数据在某些浏览器请求时进行即时解压缩：

```
# AccessFileName：在每个目录中查找用于
# 控制信息的文件。
AccessFileName .htaccess

# TypesConfig 描述 mime.types 文件（或等效文件）
# 所在。
TypesConfig /etc/mime.types

# DefaultType 是服务器无法从文件名
# 找到类型的默认 MIME 类型。
DefaultType /plain

# AddEncoding 允许某些浏览器（Mosaic/X 2.1+）
# 即时解压缩信息。注意：并非所有浏览器都支持此功能。
AddEncoding x-compress Z

AddEncoding x-gzip gz

# AddLanguage 允许为文档指定语言。
# 随后你可以使用内容协商为浏览器提供语言。
# 注意，后缀不需要与语言代码相同。
```

```
AddLanguage .en
AddLanguage .fr
AddLanguage .de
AddLanguage .da
AddLanguage .el
AddLanguage .it

# LanguagePriority 允许在冲突时给某些语言
# 优先级。只需按降序列出语言。
LanguagePriority en de
```

## 别名内容

有多种方法可以定义别名内容。这些包括 `Alias` 指令和 `ScriptAlias` 指令：

```
# Redirect 允许你所有客户端以前存在于
# 服务器命名空间但已不存在的文档。这允许你告诉
# 客户端去哪里查找移动文档。
# 格式：Redirect filename url

# Aliases：在此处添加你需要的多个别名（无限制）。格式为
# Alias filename realname

# 注意，如果在文件名包含包含斜杠 /，则服务器
# 要求在 URL 中包含它。因此在此示例中没有为 "icons" 设置别名。
Alias /icons/ /home/httpd/icons/

# ScriptAlias：这控制哪些目录运行服务器脚本。
# 格式：ScriptAlias filename realname
ScriptAlias /cgi-bin/ /home/httpd/cgi-bin/

# 如果你想使用服务器端包含，或者在 ScriptAlias
# 目录之外使用 CGI，请取消以下行的注释。
```

`Redirect` 可用于指示客户端其寻求的文档已移动到其他处（到同一台服务器或外部位置）。如果设置了以下重定向选项：

```
Redirect /test http://www.mybox.com/prod
```

客户端尝试访问 `http://www.mybox.com/test/dmgr.html` 将导致重定向到 `http://www.mybox.com/prod/dmgr.html`。

`Alias` 指令实现了类似的功能，但它指向的是文件系统位置（也不一定在 `DocumentRoot` 内部）。例如，如果设置了以下行：

```
Alias /bigjob /home/newguy/proj
```

任何对 `/bigjob` 中文档的客户端请求（例如 `http://www.mybox.com/bigjob/index.html`）都将导致获取 `/home/newguy/proj/index.html`。

`ScriptAlias` 也执行相关功能，但它别名映射的是可执行代码（可能是 CGI 脚本）的目录。其语法与 `Alias` 指令相同。

## 添加 MIME 类型和处理器

通过 `AddType` 指令，你可以增强为 Apache Web 服务器分配的 MIME 类型，而无需编辑 `mime.types` 文件。通过 `AddHandler` 指令，你可以将选的文件扩展名映射到处理器（这将导致执行某些操作）：

```
# AddType 允许你在不实际编辑它的情况下调整 mime.types，
# 或将某些文件指定为特定类型。
# 格式：AddType type/subtype ext1

# 例如，PHP3 模块（不属于 Apache 分发版）
# 通常会使用：
#AddType application/x-httpd-php3 .php3
#AddType application/x-httpd-php3 source .php
# 以下用于 PHP/FGI (PHP2)：
#AddType application/x-httpd-php .phtml
```

```
# AddHandler 允许你将某些文件扩展名映射到“处理器”，
# 与文件类型无关的操作。这些处理器可以是服务器内置的
# 也可以通过 Action 命令添加（见下文）
# 格式：AddHandler action-name ext1
```

```
# 要使用 CGI 脚本：
#AddHandler cgi-script .cgi
```

```
# 使用服务器解析的 HTML 文件
AddType text/html .shtml
AddHandler server-parsed .shtml
```
