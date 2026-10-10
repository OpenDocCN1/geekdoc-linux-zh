

CustomLog 指令将已定义的 LogFormat 格式之一分配给一个文件名（同样，指定为绝对路径名或相对于 ServerRoot 的路径名）。唯一的未注释定义将组合（combined）格式分配给 /etc/httpd/logs/access_log 文件。若要单独保留代理或引用源信息，请取消相应定义的注释。此外，您也可以选择注释掉 CustomLog logs/access_log combined 行，并改用 common 格式的定义。

## 添加签名

由 Apache 服务器生成的任何页面都可以在页面底部添加一行签名。服务器生成页面的示例包括目录列表、错误页面、状态页面或信息页面。ServerSignature 指令可以设置为 On、Off 或 EMail。以下是 ServerSignature 的默认显示方式：

```
# Optionally add a line containing the server version and virtual # host name to server-generated pages (error documents, FTP directory # listings, mod_status and mod_info output etc., but not CGI generated # documents). # Set to "EMail" to also include a mailto: link to the ServerAdmin. # Set to one of: On | Off | EMail # ServerSignature On
```

当 ServerSignature 设为 On 时，服务器生成的页面底部会出现类似下面的一行：

```
Apache/2.0.48 (Fedora) Server at toys.linuxtoxys.net Port 80
```

当 ServerSignature 设置为 EMail 时，会在签名行中添加指向 Web 页面管理电子邮件账户的链接（服务器名称变为链接）。如果该指令设置为 Off，则该行根本不会显示。在启用 SSL 或 webdav 的情况下，此信息也会出现在服务器签名中。

## 别名重定向内容

定义别名内容的方式有很多种。这包括 Alias 和 ScriptAlias 指令。以下是 httpd.conf 中的别名相关设置（已移除注释）：

```
# # Aliases: Add here as many aliases as you need (with no limit). The format is # Alias fakename realname # Alias /icons/ "/var/www/icons/" <Directory "/var/www/icons"> Options Indexes MultiViews FollowSymLinks AllowOverride None Order allow,deny
 Allow from all
</Directory>

# ScriptAlias: This controls which directories contain server scripts.
ScriptAlias "/cgi-bin/" "/var/www/cgi-bin/"
# "/var/www/cgi-bin/" should be changed to whatever your ScriptAliased
# CGI directory exists, if you have that configured.
<Directory "/var/www/cgi-bin">
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
</Directory>
```

`Alias` 指令指向一个文件系统位置（不一定在 `DocumentRoot` 内）。例如，如果在配置中包含以下行，对 `/bigjob` 中文档（http://www.mybox.com/bigjob/index.html）的请求将导致检索 `/home/newguy/proj/index.html`。

```
Alias /bigjob /home/newguy/proj
```

`icons` 别名允许访问 Apache 用于您的网站 Web 服务器的 `icons`。`icons` 目录可从 `/var/www` 目录访问。

`ScriptAlias` 指令执行相关功能，但它所别名的目录包含可执行代码（通常是 CGI 脚本）。其语法与 `Alias` 指令相同。每次使用 `ScriptAlias` 时都要特别注意。因为 `ScriptAlias` 定义了服务器上可从 Web 内容运行的脚本所在位置，所以应确保仅分配那些包含经过安全验证且不会在系统中打开安全漏洞的脚本的目录。

### 重定向旧内容请求

随着 Web 服务器上的内容变化，一些内容将变得过时，而其他内容可能会移动到文件系统中的不同位置或不同的服务器。使用 `Redirect` 指令，您可以将旧内容的请求重定向到新位置。

默认情况下，您的 Apache 服务器没有设置任何 `Redirect` 指令。然而，您可以取消以下示例的注释并根据您的需要进行定制：

```
# Redirect permanent /foo http://www.example.com/bar
```

`Redirect` 可用于指示客户端其寻找的文档已移至其他位置（同一服务器或外部位置），只需指出旧位置和新位置即可。如果之前的 `Redirect` 选项已生效，客户端尝试访问 `http://www.mybox.com/foo` 将被重定向到 `http://www.example.com/bar`。

除了使用 permanent 作为 Redirect 的服务（这将产生重定向状态 301）外，还可以使用 temp（重定向状态 302）、seeother（替代状态 303）或 gone（永久移除状态 401）。您还可以提供 300 到 399 之间的任何状态代码作为服务，这些代码代表不同的错误响应。（这些数字是 HTTP 状态代码。）

> **交叉参考：** HTTP 状态代码在 RFC 2616 中作为 HTTP 协议的一部分进行定义。请参考该文档，网址为 www.w3.org/Protocols/rfc2616/rfc2616.txt。

### 定义索引

让您的 Apache 服务器为不同类型的文件显示不同的图标是可行的。要使用此功能，`IndexOptions` 应设置为 `FancyIndexing`，并且应使用 `AddIconByEncoding`、`AddIconByType` 和 `AddIcon` 指令：

```
# Directives controlling display of server-generated directory listings.

# FancyIndexing is if you want fancy directory indexing or standard.
# VersionSort is whether files containing version numbers should be
# compared in the natural way, so that 'apache-1.3.9.tar' is placed
# before 'apache-1.3.12.tar'.
#
IndexOptions FancyIndexing VersionSort NameWidth=* HTMOTable
#
# AddIcon* directives tell the server which icon to show for different
# files or filename extensions. These are only displayed for
# FancyIndexed directories.
#
AddIconByEncoding (CMP, /icons/compressed.gif) x-compress x-gzip

AddIconByType (TXT, /icons/text.gif) text/*
AddIconByType (IMG, /icons/image2.gif) image/*
AddIconByType (SND, /icons/sound2.gif) audio/*
AddIconByType (VID, /icons/movie.gif) video/*

AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wrl.gz .vrml .vrm .iv
AddIcon /icons/compressed.gif .Z .z .tgz .gz .zip
AddIcon /icons/a.gif .ai .eps
AddIcon /icons/layout.gif .html .shtml .htm .pdf
AddIcon /icons/txt.gif .txt
AddIcon /icons/c.gif .c
AddIcon /icons/p.gif .pl .py
AddIcon /icons/f.gif .for
AddIcon /icons/dvi.gif .dvi
AddIcon /icons/unencoded.gif .uu

AddIcon /icons/script.gif .conf .sh .shar .cs .ksh .tcl
AddIcon /icons/tex.gif .tex
AddIcon /icons/bomb.gif core

AddIcon /icons/back.gif ..
AddIcon /icons/hand.right.gif README
AddIcon /icons/folder.gif ^\*DIRECTORY^\*
AddIcon /icons/blank.gif ^\*BLANKICON^\*

#
# DefaultIcon: which icon to show for files which do not have an icon
# explicitly set.
#
DefaultIcon /icons/unknown.gif

#
# AddDescription: allows you to place short description after a file in
# server-generated indexes.  These are only displayed for FancyIndexed
# directories.
# Format: AddDescription "description" filename
#
#AddDescription "GZIP compressed document" .gz
#AddDescription "tar archive" .tar
#AddDescription "GZIP compressed tar archive" .tgz

#
# ReadmeName: the name of the README file the server will look for by
# default, and append to directory listings.
#
# HeaderName is the name of a file which should be prepended to
# directory indexes.
#
ReadmeName README.html
HeaderName HEADER.html

#
# IndexIgnore is a set of filenames which directory indexing should
# ignore and not include in the listing.  Shell-style wildcards are
# permitted.
#
IndexIgnore .??* ~ *# \*HEADER\* README\* RCS CVS *,v *,t
```

前一组选项涉及如何处理服务器生成的目录索引。IndexOptions FancyIndexing VersionSort NameWidth=* 指令使自动生成的目录索引包含关于每个文件或目录的几个信息片段，包括代表文件类型的图标、文件名、文件的最后修改时间、文件大小以及文件的描述。图 21-2 展示了一个使用默认 FancyIndexing 设置的目录示例。

