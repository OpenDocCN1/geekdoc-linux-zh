
如果你在文件的前面的部分更改了 `DocumentRoot`，你需要将 `/var/www/html` 修改为该值。目录的 `Options` 是 `Indexes` 和 `FollowSymLinks`。这些和其他服务器功能见表 21-2。`AllowOverride` 指令指示服务器 `.htaccess` 文件（或 `AccessFileName` 值）不能覆盖任何特殊访问功能。你可以用表 21-3 中描述的任何特殊访问功能替换 `None`。

| 功能 | 说明 |
| :--- | :--- |
| ExecCGI | 允许执行 CGI 脚本。 |
| FollowSymLinks | 服务器将跟踪符号链接。 |
| Includes | 允许服务器包含。 |
| IncludesNOEXEC | 允许服务器包含，但排除 #exec 元素。 |
| Indexes | 如果指定的 DirectoryIndex 文件不存在，将由 mod_autoindex 生成目录索引。 |
| MultiViews | 服务器根据浏览器偏好（如首选语言、字符集和媒体类型）允许内容协商。 |
| SymLinksOwnerMatch | 只有当目标的所有者与链接的所有者相同时，服务器才会跟踪符号链接。 |
| None | 以上所有功能均启用。 |
| All | 以上所有功能均启用，但 MultiViews 除外。必须显式启用。 |

### 21-3: AllowOverride 指令的特殊访问功能

| 特性 | 描述 |
| --- | --- |
| AuthConfig | 启用身份验证相关的指令（AuthName, AuthType, UserFile, AuthGroup, Require 等）。 |
| FileInfo | 启用与 MIME 相关的指令（AddType, AddEncoding, AddLanguage, LanguagePriority 等）。 |
| Indexes | 启用与目录索引相关的指令（FancyIndexing, DirectoryIndex, IndexOptions, IndexIgnore, HeaderName, ReadmeName, AddIcon, Description 等）。 |
| Limit | 启用控制主机访问（Allow, Deny 和 Order）。 |
| Options | 启用 Options 指令（如表 21-2 所示）。 |

> 注意：请记住，除非你专门启用了表 21-2 和表 21-3 中描述描述的功能，否则该功能在你的服务器上是不启用的（Indexes 和 FollowSymLinks 除外）。

## 识别用户目录

如果你在服务器上拥有多个用户，并且希望他们每个人都能发布自己的 Web 内容，通常的做法是识别用户在自己的主目录中创建的用于存储这些内容的目录名称。当你识别出附加到用户主目录 (~user) 之后的名称时，该目录名称以前默认被设置为 `public_html`；但现在默认是关闭的。

要访问用户的个人 Web 页面，请在 `UserDir disable` 行上添加注释字符 (#)。删除 `UserDir public_html` 行中的 `#`，即可允许通过 Web 服务器访问用户的 `public_html` 目录。在删除多余的注释行后，以下文本显示了启用部分的样式：

```
# UserDir: 当接收到 ~request 请求时，附加到用户

# 主目录的目录名称。

<IfModule userdir.c>

  # UserDir disable

UserDir public_html

</IfModule>
```

除了取消上例所示 `UserDir public_html` 行的注释外，你必须让用户的主目录和 `public_html` 都具有可执行权限，`UserDir` 指令才能允许访问特定用户的 `public_html` 目录。例如，用户 `cjb` 可以输入以下命令来使目录可访问。

```
$ chmod 711 /home/cjb/public_html

$ mkdir /home/cjb/public_html

$ chmod 755 /home/cjb/public_html
```

为了让 `UserDir` 工作，还必须加载 `mod_userdir` 模块（默认已加载）。

`UserDir` 指令有两种方式处理包含用户名的传入请求（例如 `~cjb`）。其中一种格式可以识别单个用户可访问目录的物理路径。另一种格式可以将请求重定向到请求重定向到的 URL。表 21-4 给出了一些示例，使用 URL `http://www.box.com/~cjb/proj/c004.html` 作为示例请求。

## 表 21-4：UserDir 路径名和 URL 示例

| UserDir 指令 | 引用的路径或 URL |
| --- | --- |
| UserDir public_html | ~cjb/public_html/proj/c004.html |
| UserDir/*/WWW | /cjb/WWW/proj/c004.html |
| UserDir/*/local/web | /usr/local/web/proj/c004.html |
| UserDir http://www.box.com/users | http://www.box.com/users/~cjb/proj/c004.html |
| UserDir http://www.box.com/~* | http://www.box.com/~cjb/proj/c004.html |
| UserDir http://www.box.com*/html | http://www.box.com/cjb/html/c004.html |

`UserDir` 指令也可以用于显式允许或拒绝特定用户的 URL 到路径名的翻译。例如，包含以下行是一个好主意，可以避免发布不应公开的数据：

```
UserDir root
```

或者，使用以下行禁用所有少数用户的翻译：

```
UserDir disable

UserDir enable wilhelm cjb jsmith
```

> 注意：你应该始终对自己在互联网上发布的关于自己的内容小心（姓名、地址、个人信息等），并记住你可能对在 Web 服务器上发布的内容负责。当你允许其他人在你的 Web 服务器上发布内容时，你的责任可能会延伸到这些发布用户。请确保对在 Web 服务器上发布什么是可以接受的（且合法的）有一个明确的政策，并将该信息提供给允许使用服务器的人。

## 为目录设置默认索引文件

`DirectoryIndex` 指令建立了一个文件列表，当传入请求指定目录而不是文件时使用。例如，客户端请求 URL `http://www.mybox.com/~jsmith/`。因为它是一个目录，它会被翻译为 `http://www.mybox.com/~jsmith/`。现在该目录会搜索 `DirectoryIndex` 指令中列出的任何文件。使用第一个匹配项（来自默认列表 index.html 和 index.var）。如果文件都不存在且选择了 Indexes 选项（在 `httpd.conf` 文件中），服务器将自动生成目录中文件的索引。

```
# DirectoryIndex: 设置当请求目录时 Apache 

# 将提供的文件。

# index.html.var 文件（一种类型映射）用于交付经过

# 修改的文档。MultiViews 选项可以用于相同的

# 目的，但它的速度慢得多。

DirectoryIndex index.html index.var
```

有时，动态内容（如 `index.php` 或 `index.cgi`）会被添加到 `DirectoryIndex` 中，以确保当用户请求域名或目录时，在访问静态内容之前先访问该动态内容。

## 设置目录访问控制

你和用户可以为每个目录添加一个访问文件以访问该目录。默认情况下，`AccessFileName` 指令设置包含信息的 `.htaccess` 文件。以下行设置了此文件名，并防止网站访问者查看该文件的内容。如果你将文件更改为 `.htaccess` 以外的名称，请务必更改下面行（`"^\\.ht"`）以拒绝对该文件的访问。

```
# AccessFileName: 在每个目录中查找的用于

# 访问控制信息的文件名。

AccessFileName ~"\\.ht"
```

```
<Files ~"\\.ht">

Order allow, deny

Deny from all

</Files>
```

你可以像在 `httpd.conf` 文件中那样将相同的访问指令添加到 `.htaccess` 文件中。通常情况下，在 `httpd.conf` 文件中使用 `<Directory>` 指令比创建 `.htaccess` 文件更有效。通过 `<Directory>` 指令，你可以单独对该目录进行识别。由于放在 `.htaccess` 中的指令适用于当前目录下的所有目录，Apache 必须搜索所有目录。
