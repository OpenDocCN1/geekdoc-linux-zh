

# 第四部分：Fedora RHEL 网络与服务器设置

# 重定位重定向内容

定义别名内容有多种方法。包括 Alias 和 ScriptAlias 指令。以下是 httpd.conf 中与别相关的设置（已移除注释）：

```
# Aliases: 在此处添加你需要的任意别名（无数量限制）。
# Alias 别名 实际名称
#
Alias /icons/ "/var/www/icons/"
```

```
<Directory "/var/www/icons">
Options Indexes MultiViews FollowSymLinks
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

```
# ScriptAlias: 这控制哪些目录包含脚本。
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
```

```
# "/var/www/cgi-bin" 应该更改为你的 ScriptAliased
# CGI 目录路径，如果你已经配置了的话。
```

```
<Directory "/var/www/cgi-bin">
AllowOverride None
Options None
Order allow,deny
Allow from all
</Directory>
```

Alias 指令指向系统位置（不一定在 DocumentRoot 内）。例如，如果设置了以下行，对 /bigjob 文的请求（http://www.myapp.com/bigjob/index.html）将导致检索 /home/newguy/proj/index.html。

Alias /bigjob /home/newguy/proj

icons 允许 Web 服务器为你的网站访问 Apache 图标。icons 目录可以通过 /var/www/directory 访问。

ScriptAlias 指令执行相关的功能，但它用于为可执行文件（最可能是 CGI 脚本）设置别名。其语法与 Alias 指令相同。每当你使用 ScriptAlias 时，请务必注意。因为 ScriptAlias 定义了脚本从服务器上 Web 内容中运行的位置，你应该确保只分配那些包含受保护且不会为你的系统留下安全漏洞的脚本的目录。

# 第 21 章：设置 Web 服务器 

# 对旧内容的请求重定向

随着你的 Web 服务器上内容的变化，某些内容将变得过，而另一些内容可能会移动到文件系统的不同位置或不同的服务器。使用 Redirect 指令，你可以将对旧内容的请求重定向到新位置。

默认情况下，你的 Apache 服务器没有 Redirect 指令。但是，你可以取消以下示例的注释并根据需要进行定制：

```
# Redirect permanent /foo http://www.example.com/bar
```

Redirect 可用于指示客户端它们正在寻找的文档已移动到其他地方（同一服务器或外部位置），只需指示旧位置和新位置即可。如果之前的 Redirect 选项生效，客户端访问 http://www.mybox.com/ 的尝试将重定向到 http://www.example.com/bar。

除了使用 permanent 作为 Redirect 的服务（导致 301 重定向状态）外，你还可以使用 temp（重定向状态 302）、seeother（替换状态 303）或 gone（永久删除状态 401/410）。你也可以使用 300 到 399 之间的任何状态代码作为服务，它们代表不同的错误响应。（这些是 HTTP 状态码）。

> 交叉引用：HTTP 状态码在 RFC 2616 中作为 HTTP 协议的一部分定义。请参阅该文档 www.w3.org/Protocols/rfc2616/rfc2616.txt。

# 定义索引

你可以让 Apache 服务器为不同类型的文件显示不同的图标。要使用此功能，应将 IndexOptions 设置为 FancyIndexing，并且 AddIconEncoding、AddIconByType 和 AddIcon 指令应为：

```
# 控制服务器生成的目录列表显示的目录。
# FancyIndexing 决定包含版本号的文件是否应该
# 以自然方式进行排序，使得 'apache-1.3.9.tar' 位于
# 'apache-1.3.12.tar' 之前。
IndexOptions FancyIndexing VersionSort NameWidth*=HTMLTable
# AddIcon* 指令告诉服务器为不同的
# 文件或文件名扩展名显示什么图标。这些仅在
# FancyIndexed 目录显示。
```

```
AddIconEncoding(CMP,/icons/compressed.gif) x-compress x-gzip
AddIconByType(TXT,/icons/text.gif) text/*
AddIconByType(IMG,/icons/image2.gif) image/*
```

```
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar-gif .tar
AddIcon /icons/world2.gif .wrl .wrl.gif .vrm .ivm
AddIcon /icons/compressed.gif .Z .tgz .zip
AddIcon /icons/a.gif .ps .ai
AddIcon /icons/layout.gif .html .shtml .htm
AddIcon /icons/text.gif .txt
AddIcon /icons/c.gif .c
AddIcon /icons/p.gif .pl .py
AddIcon /icons/f.gif .for
AddIcon /icons/bwi.gif .dvi
AddIcon /icons/uencoded.gif .uu
AddIcon /icons/script.gif .conf .sh .shsh .ksh .tcl
AddIcon /icons/tex.gif .tex
AddIcon /icons/bomb.gif core

AddIcon /icons/back.gif
AddIcon /icons/hand.right.gif ^^DIRECTORY
AddIcon /icons/unknown.gif ^^DIRECTORY^
AddIcon /icons/blank.gif ^^DIRECTORY^

# DefaultIcon: 允许服务器为没有匹配的文件显示默认图标。
# 你也可以使用波号 (~) 来忽略某些文件。
```

