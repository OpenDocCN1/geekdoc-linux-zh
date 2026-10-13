
**表 23.2（续）**

| 指令名称 | 描述 |
|---|---|
| `DefaultIcon` | 指定当启用 FancyIndexing 时，在目录列表中为没有指定其他图标的文件显示的默认图标。图标文件名应为网站根目录下的路径。也就是说，如果你以 `http://my.host/icons/file.gif` 访问该文件，则指定 `/icons/file.gif` 作为文件名。 |
| `DefaultType` | 指定对于没有关联其他 MIME 类型的文件所使用的默认 MIME 类型。默认值 `text/plain` 与 `text/html` 都是不错的选择。 |
| `DirectoryIndex` | 指定当浏览器请求一个目录但未指定文件名时，默认从该目录提供服务的文件名。例如，如果浏览器向你的系统请求 `http://my.domain/`，Apache 必须知道根文档目录中的哪个文件应发送给浏览器。此指令以一个由空格分隔的文件名列表作为其值。Apache 会搜索该列表，直到在请求的目录中找到匹配文件，然后将该文件发送给客户端。在列表中指定多个文件名很有用，因为你可能在某些目录中提供 HTML 文件，而在另一些目录中提供特殊应用程序文件（如 PHP 应用程序或 ColdFusion 应用程序）。但你应当注意将目录索引文件列表保持在最小限度，原因有二。服务器每次被请求一个目录时都必须搜索该列表，列表越长效率越低。如果目录中有两个文件与列表中的文件匹配，你希望发送给浏览器的文件可能不是 Apache 会选择的那一个。 |
| `DocumentRoot` | 指定用作 Web 服务器根文档目录的物理目录。例如，如果你希望站点的根 URL（如 `http://my.domain/`）指向物理目录 `/usr/local/apache/htdocs/`，请使用以下指令：`DocumentRoot /usr/local/apache/htdocs`。 |
| `FancyIndexing` | 指定在网站上显示目录中的文件列表时是否使用花式索引。启用花式索引后，你在 `srm.conf` 文件中指定的图标将用于目录列表中的文件显示。要启用花式索引，请将该指令设置为 on；要禁用该功能，请将该指令设置为 off。 |
| `HeaderName` | 指定将在目录列表之前显示的文件的名称。此指令的值指定一个必须存在于被列出目录中的文件名。这允许你指定一个文件名，并在不同目录中使用该文件的不同版本。 |
| `IndexIgnore` | 指定将被忽略且不在显示给用户的目录列表中出现的文件名。此指令的值为一个或多个文件名或 POSIX.2 正则表达式，以空格分隔。 |
| `LanguagePriority` | 设置向浏览器提供内容的语言优先顺序，浏览器会指明可接受的语言列表。此指令的值是一个以空格分隔的 MIME 语言编码列表，例如 en de。默认 `srm.conf` 文件中指定的值对于仅使用英语的站点非常理想。 |
| `ReadmeName` | 指定将在目录列表末尾显示的文件的名称。此指令的值指定一个必须存在于被列出目录中的文件名。这允许你指定一个文件名，并在不同目录中使用该文件的不同版本。 |
| `TypesConfig` | 指定服务器 MIME 类型配置文件的名称和位置。除非你在其他位置创建自定义文件，否则请保持此指令的默认值。 |
| `UserDir` | 指定用户主目录中的一个子目录名称，该子目录可用作用户个人 Web 文件的文档根目录。这允许用户将文件放置在此目录中，并通过 Web 以 `http://my.domain/~<username>/` 访问这些文件。 |

## 根文档目录的权限与安全

使用由 DocumentRoot 指令指定的根文档目录的目的是防止 Web 浏览器通过 Web 服务器访问你的整个系统。这有效地将访问限制在 DocumentRoot 指令指定的文档树内，除非你使用诸如 Alias 这样的指令来允许访问其他目录。在选择根文档目录以及任何其他目录（如别名目录）时应格外小心，以确保 Apache 只提供你希望在 Web 上可用的文件。

然而，仅仅注意选择合适的文档根目录和别名还不足以保护你的文件系统。例如，如果在根文档目录树中的某处有指向此层级之外目录或文件的符号链接，你就相当于允许访问位于文档树之外的数据，从而使你通过将 Apache 限制在特定根文档目录树上所获得的安全性失效。

> **注意**
>
> 正如我们稍后将在“access.conf 文件”一节中了解到的，如果对某个目录禁用了 FollowSymLinks，这就不是问题，因为禁用此功能可防止此安全漏洞。

## 一个典型的 srm.conf 文件

Apache Web 服务器的一个典型 `srm.conf` 文件可能如下所示：

```
DocumentRoot /home/httpd/html
UserDir public_html
DirectoryIndex index.html index.shtml index.cgi
FancyIndexing on
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wrl.gz .vrml .vrm .iv
AddIcon /icons/compressed.gif .Z .z .tgz .gz .zip
AddIcon /icons/a.gif .ps .ai .eps
AddIcon /icons/layout.gif .html .shtml .htm .pdf
AddIcon /icons/text.gif .txt
AddIcon /icons/c.gif .c
AddIcon /icons/p.gif .pl .py
AddIcon /icons/f.gif .for
AddIcon /icons/dvi.gif .dvi
AddIcon /icons/uuencoded.gif .uu
AddIcon /icons/script.gif .conf .sh .shar .csh .ksh .tcl
AddIcon /icons/tex.gif .tex
AddIcon /icons/bomb.gif core
AddIcon /icons/back.gif ..
AddIcon /icons/hand.right.gif README
AddIcon /icons/folder.gif ^^DIRECTORY^^
AddIcon /icons/blank.gif ^^BLANKICON^^
DefaultIcon /icons/unknown.gif
ReadmeName README
HeaderName HEADER
IndexIgnore .??* *~ *# HEADER* README* RCS
AccessFileName .htaccess
TypesConfig /etc/mime.types
DefaultType text/plain
AddEncoding x-compress Z
AddEncoding x-gzip gz
AddLanguage en .en
AddLanguage fr .fr
AddLanguage de .de
AddLanguage da .da
AddLanguage el .el
AddLanguage it .it
LanguagePriority en fr de
Alias /icons/ /home/httpd/icons/
ScriptAlias /cgi-bin/ /home/httpd/cgi-bin/
AddType text/html .shtml
AddHandler server-parsed .shtml
AddHandler imap-file map
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\.0b2;" nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\.0" force-response-1.0
BrowserMatch "Java/1\.0" force-response-1.0
BrowserMatch "JDK/1\.0" force-response-1.0
```

![](img/6c13bcf02a08ad7923caab46f051d96a_513_0.png)

> **注意**
>
> `srm.conf` 文件通常包含大量描述条目及其用途的注释。为简明和本书展示清晰起见，这些注释已被删除。注释以井号（#）开头，一直延续到行尾，这与大多数 Linux 配置文件的做法一致。

## access.conf 文件

`access.conf` 文件通常用于指定 Apache Web 服务器所服务资源的访问控制信息。`access.conf` 文件通常位于默认的 Apache 配置目录中（如果 Apache 是从源代码分发包安装并使用默认设置，则为 `/usr/local/apache/conf/access.conf`）。

> **注意：** 如前所述，这里列出的配置指令也可以放在 `httpd.conf` 文件中。Apache 建议将指令放在 `httpd.conf` 中，但两种方式都可以使用。

此文件的格式不同于 `httpd.conf` 和 `srm.conf` 文件，因为前者由跨多行的指令块组成，从类似于 `<Directory ...>` 的开头标记或标签开始，一直到类似于 `</Directory>` 的结束标签。

在这些指令块内部，使用一个或多个指令来指定对特定目录的访问控制。开头的 `<Directory ...>` 标签采用以下形式：

`<Directory <Directory name>>`

这指示块中的指令应用于哪个目录。在 `<Directory ...>` 块内，你会看到如下一般形式的指令：

`<Directive Name> <Directive Value>`

一个典型的 `access.conf` 文件很可能会在其 `<Directory ...>` 块中包含表 23.3 中列出的指令。

**表 23.3 典型的 access.conf 指令**

| 指令名称 | 描述 |
|---|---|
| `allow from` | 指定允许访问此目录及其子目录的主机名或 IP 地址。以空格分隔主机，规则如下：特殊关键字 `all` 允许所有客户端访问；主机名的尾部可用于匹配以该尾部结尾的所有主机（如 `cnn.com`）；IP 地址的前部可用于匹配以该前部开头的所有 IP 地址（如 `192.168.147`），或者使用 `<网络地址>/<网络掩码>` 对。 |
| `AllowOverride` | 指定哪些功能可以被存储在特定目录中的本地访问文件（通常是 `.htaccess`）覆盖。可能的值包括 `AuthConfig`（允许覆盖与身份验证和授权相关的指令）；`FileInfo`（允许覆盖与文档类型和语言相关的指令）；`Indexes`（允许覆盖与目录索引相关的指令）；`Limit`（允许覆盖与主机访问控制相关的指令）；以及 `Options`（允许覆盖 `Options` 和 `XBitHack` 指令）。多个值可以以空格分隔列出。 |
