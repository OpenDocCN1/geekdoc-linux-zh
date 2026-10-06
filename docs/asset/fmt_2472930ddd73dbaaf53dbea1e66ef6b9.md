
### 通过此文档，你定义了用户看到的服务器命名空间。
# 更多信息请参阅 http://ncsa.uiuc.edu/docs/tutorials/
# NCSA httpd (httpd@ncsa.uiuc.edu)
### DocumentRoot: 你从中提供文档的目录。
# 默认情况下，所有请求都来自该目录，并可以使用
#符号链接和别名指向其他位置。
# UserDir: 当接收到“用户”请求时，附加到用户主目录的目录名称。
# DirectoryPublic_html/
# DirectoryIndex 用作预写 HTML 目录索引的文件名
`DirectoryIndex` `index.html`
# FancyIndexing 告诉你是想要花哨的目录索引还是标准的索引
`FancyIndexing`
# AddIcon 告诉服务器为不同的文件或文件名扩展名显示什么图标
`AddByType` (`TXT`, `/icons/text.xbm`) `text/*`
`AddByType` (`IMG`, `/icons/image.xbm`) `image*/`
`AddByType` (`STD`, `/icons/sound.xbm`) `audio*/`
`AddIcon` `/icons/movie.xbm` `.png` `.qt`
`AddIcon` `/icons/binary.xbm` `bin`
`AddIcon` `/icons/back.xbm` `...`
`AddIcon` `/icons/menu.xbm` `^"DIRECTORY>>^`
`AddIcon` `/icons/blank.xbm` `^"BLANKION"`
# DefaultIcon 是没有显式设置图标的文件所显示的图标
`DefaultIcon` `/icons/unknown.xbm`
# AddDescription 允许你在...后面放置一个简短描述

# 服务器生成索引中的文件。

# 格式：AddDescription "description" 文件名

# ReadName 是服务器默认查找的 README 文件名。

# 格式：ReadName 名称

## 服务器将首先查找 name.html，如果找到则包含它，

# 然后它会查找 name，如果找到则以纯文本形式包含它。

# HeaderName 是应该置于目录索引之前的文件名。

`ReadName` `README`

# HeaderName

# IndexIgnore 是目录索引应该忽略的文件名集。

# 格式：IndexIgnore name! name2.

`IndexIgnore=".*"` `*` `# /* HEADER */` `/README*`

# AccessFileName：在每个目录中查找用于访问控制信息的文件名。

# AccessFileName .htaccess

# DefaultType 是当服务器无法从 mime 扩展名找到类型时，文档的默认 MIME 类型。

`DefaultType` `text/plain`

# AddType 允许你在不实际编辑 mime.types 的情况下进行调整，

# 或为某些文件指定类型。

# 格式：AddType subtype ext1

# AddEncoding 允许某些浏览器（Mosaic/X 2.1+）

# 即时处理罕见的编码。注意：并非所有浏览器都支持。

# AddEncoding x-compress Z

# AddEncoding x-gzip zip

# Redirect 允许你告知客户端以前存在于服务器命名空间中

# 但已不再的文档。这允许你告诉客户端查找重定向后的文档。

# 格式：Redirect fakename url

# Alias：在此处添加你需要的别名，最多： 20 个。

# 格式：aliases realname

`Alias` `/icons/` `/usr/local/etc/httpd/icons/`

# ScriptAlias 控制哪些目录包含服务器脚本。

# 格式：ScriptAlias fakename realname

`ScriptAlias` `/cgi-bin` `/usr/local/etc/httpd/cgi-bin/`

# 如果你想使用服务器索引，请取消以下行的注释。

# ScriptAliasesDecomment 取消以下行的注释。

# AddType text/x-server-parsed-html .shtml

# AddType application/x-http .cgi

# 如果发生错误，请取消以下行并在发生错误时设置

# 版本，或者取消内置的如你所做的那样。注意：如果脚本被正确调用（例如在 ScriptAlias 中），

# 必须是绝对路径才能生效。

## 302 REDIRECT

## 400 BAD_REQUEST

## 401 AUTH_REQUIRED

## 403 FORBIDDEN

## 404 NOT_FOUND

## 500 SERVER_ERROR

## 501 NOT_IMPLEMENTED

#ErrorDocument 302 /cgi-bin/redirect.cgi

#ErrorDocument 500 /errors/server.html

#ErrorDocument 403 /errors/forbidden.html

构建你的个性化配置文件 `conf/srm.conf`，并按照与示例相同的顺序进行填充。以下是我为服务器资源配置文件所做选择的逐步说明：

- 1. # DocumentRoot：你用于提供文档的目录。

通过此变量，你指定服务器将显示文件的主目录。像往常一样，我将遵循标准（尽管如果你希望将所有日志文件放在一个中央位置，你完全可以它以适应你的需求），此配置文件将从如下开头：

```
DocumentRoot /usr/local/etc/httpd/htdocs
```

- 2. # UserDir：当接收到 ~user 请求时，附加到用户主目录的目录名称。

此指令用于分配一个用户目录中存在的目录，用户可以在那里存放自己的 HTML 文件供 Web 访问。标准是 `public_html` 目录：每当有人点击链接到例如 http://www.server.com/~user 时，他们实际上会去 http://www.server.com/~user/public_html。这在很大程度上是一种保持环境整洁并保持适当安全的方法，外部人员无法进入你的目录。

我配置文件中的下一行（因为我使用的是默认值）将如下所示：

```
UserDir public_html
```

- 3. # DirectoryIndex：用作预写 HTML 目录索引的文件名。

通过此指令，当外部用户通过链接进入某人的主目录时，你可以设置一个假定的文件名。在上面的示例 URL 中，注意没有列出文件名。那是因为设置了默认文件名，所以服务器首先查看该文件（通常是 `index.html`）。我将再次使用默认值，因此我的下一行是：

```
DirectoryIndex index.html
```

- 4. # FancyIndexing 决定你想使用花式目录索引还是标准索引。

## 配置你的 Web 服务器

`FancyIndexing` 指的是带有图标和文件大小显示目录和文件。如果你想以这种方式显示你的文件和目录，请开启此选项。如果不想，将其设置为关闭。我的下一行将其开启，如下：

```
FancyIndexing on
```

- 5. # AddIcon 告诉服务器为不同的文件或文件名扩展名显示哪个图标。

你可以使用此指令来定义你的 Web 服务器使用哪些图标来显示目录中的文件类型。这是让你的目录稍微增色的一种简单方法。没有默认值，所以如果你不定义它们，服务器将不知道显示什么。

我配置文件中的下一行（因为我使用的是默认值）将如下所示：

```
AddIcon /usr/local/etc/httpd/icons/
```

## 第 7 章—安装 Web 服务器软件

`AccessFileName .htaccess`

- **12. DefaultType** 是服务器无法从文件扩展名中找到类型的文档的默认 MIME 类型。

你可以使用此指令在服务器无法确定实际文件类型时分配一个默认文件类型。目前我将保持此项的默认设置，看看我是否会持续遇到需要使用的其他文件类型。我的下一行将是：

```
DefaultType text/plain
```

在这种情况下，`text` 指文件类型（标准文件类型），`plain` 指子类型（MIME 对文件类型的称呼）。

- **13. AddType** 允许你在不实际编辑 `mime.types` 文件的情况下进行调整，或为某些文件指定类型。

如果你想为具有特定扩展的文件分配特定类型，将使用此指令。你分配的类型将覆盖 `TypesConfig` 文件中已列出的类型。该文件已经包含了文件类型和相应的 MIME 类型的列表。

虽然你可能想查看它（可以在 `conf/mime.types` 中找到它），但你不需要编辑此文件。相反，通过在此使用 `AddType` 指令进行你的更改。

例如，假设我经常使用 `.help` 扩展，并且所有的 `.help` 文件都是文本文件。那么我会在资源配置文件中添加以下内容：

```
AddType text/plain help
```

- **14. AddEncoding** 允许某些浏览器（Mosaic/X 2.1+）动态解压缩信息。

如果你想让服务器在发送文件时进行解压缩（这样可以使用较磁盘空间），可以使用此指令。例如，我想让服务器能够解压缩 UNIX 压缩 (.z) 文件和 gzip 压缩 (.gz) 文件（如资源配置文件列表中的示例所示）。我会在配置文件输入：

```
AddEncoding x-compress Z
AddEncoding x-gzip gz
```

- **15. Aliases**: 根据需要添加多个别名，最多 20 个。

如果你想添加一个以后在 HTML 文件路径使用的别名，请使用此指令。要将路径 `/ftp/pub/docs` 别名为 `/docs`，你会在资源配置文件中添加以下行：

```
Alias /docs /ftp/pub/docs
```

### 设置访问配置文件

你要设置的第三个配置文件是告诉 Web 服务器哪些客户端可以访问哪些目录以及其他目录中有哪些服务。使用 `access.conf-dist`（见下方文件列表）作为你处理服务器配置文件那样的模板，但不要直接使用它：

```apache
# access.conf: 全局访问配置
# 在线文档 http://hohoo.ncsa.uiuc.edu/
# 我建议你咨询它们；这些很重要且复杂的
# /usr/local/etc/httpd/ 应该更改为你设置的
# ServerRoot 的值
<Directory>/usr/local/etc/httpd/cgi-bin
Options Indexes FollowSymlinks
</Directory>
# 这应该更改为你设置的 DocumentRoot 的值。
<Directory>/usr/local/etc/httpd/htdocs>
# 此处也可以是 "None", "All", 或 "Indexes"
# "Includes", 或 "FollowSymlinks" 的任何组合
# 这控制目录中的 .htaccess 文件可以覆盖哪些选项。
# 也可以是 "None", 或 "Options":"FileInfo", "AuthConfig", 和 "Limit" 的组合
AllowOverride All
# 控制谁可以从此服务器获取内容。
<Limit GET>
order allow,deny
allow from all
</Limit>
</Directory>
```

构建你的个性化配置文件 `conf/access.conf` 并按照与示例相同的顺序填充。在某种意义上，这是你最重要的配置文件，因为它控制了对系统的访问，所以请妥善对待。以下是我为服务器配置文件所做选择说明：

- **1. /usr/local/etc/httpd/** 应该更改为你设置 `ServerRoot` 的值。

```apache
<Directory /usr/local/etc/httpd/cgi-bin>
Options Indexes FollowSymlinks
</Directory>
```

`Directory` 指令不仅仅是一个行项目，它是一个语句。它从设置目录开始。只需查看你的服务器配置文件看看你将 `ServerRoot` 设置为了什么，以防你已经从 `/usr/local/etc/httpd/` 修改了它。然后在之后添加 `cgi-bin`。在我的情况下，我保留了默认值，所以我只需输入：

`Directory /usr/local/etc/httpd/cgi-bin`

现在，告诉服务器该目录中可用的功能（Options）。你的选项如下：

- **None**：禁用该目录中的所有功能。这是最高的安全，因为使用你 Web 服务器的人完全无法在该目录中执行任何操作。

- **All**：启用该目录中的所有功能。除非你真的想让用户访问所有内容（包括用户主目录），否则不要使用。事实上，如果从用户主目录创建了一个你不希望外部人员进入的目录，此选项将允许外部 Web 用户使用该链接。

- **FollowSymLinks**：允许服务器跟随符号链接。

- **OwnerMatch**：允许服务器在所有者匹配模式时跟随符号链接。

- **Indexes**：允许服务器在没有索引文件的情况下生成目录列表。

- **Includes**：允许服务器处理服务器端包含。

- **Symlinks**：允许服务器跟随符号链接。

*(注：后续由于原文中存在大量重复描述，已根据文档工程要求去重)*

## 选择服务器脚本

Web 服务器软件附带许多脚本，允许你对设置进行一些个性化处理。即使你不想使用其中任何脚本，它们也可以作为示例。你服务器文件中的 `cgi-bin` 目录包含许多示例脚本，它们可以提供关于如何编写自己的脚本的有用教程。

## Date 脚本

`date` 脚本是一个简单但脚本，用于观察 httpd 脚本如何工作。

```sh
#!/bin/sh
DATE=/bin/date
echo Content-type: text/plain
echo

if [ -x $DATE ]; then
$DATE
else
  echo Cannot find date command on this system.
fi
```

该脚本分解如下：

- 1. #!/bin/sh

  运行 sh 壳来解释此脚本中后续的所有内容。

- 2. DATE=/bin/date

  将变量 DATE 设置为确定日期的程序的完整路径。

- 3. echo Content-type: text/plain

  此代码在屏幕上显示 Content-type: text/plain。

- 4. echo

  在你的屏幕上显示一个空行。

- 5. if [ -x $DATE ]; then

  $DATE

  如果在 DATE 分配的位置有一个程序，则运行该程序并显示输出。

- 6. else

  echo Cannot find date command on this system.

  fi

如果 DATE 分配的位置没有程序，则显示“Cannot find date command on this system.”，然后程序结束。

如果你想创建一个脚本来运行其他类似 date 的小型程序（这些不需要输入且有纯文本输出），你只需要替换相应的术语即可获得一个新脚本！

## Finger 脚本

`finger` 脚本有助于观察如何处理表单。

```sh
#!/bin/sh
FINGER=/usr/ucb/finger
echo Content-type: text/html
echo
if [ -x $FINGER ]; then
if [ $# -ne 0 ]; then
cat << EOM
<HTML><HEAD><TITLE>Finger Gateway</TITLE></HEAD>BODY
<H1>Finger Gateway</H1>
<ISINDEX>
This is a gateway to "finger". 在你浏览器的搜索框中输入 user@host 组合。<P>
EOM
else
echo \<PRE>\n$FINGER "$@"
echo \<PRE>
else
echo Cannot find finger on this system.
fi
cat << EOM
</BODY></HTML>
EOM
```

再次，让我们分解这个脚本。注意它与 date 脚本的相似之处：

- 1. #!/bin/sh

  此命令运行 sh 壳，它将解释脚本的剩余部分。

- 2. FINGER=/usr/ucb/finger

  将变量 FINGER 设置为找到 finger 程序的路径。

- 3. echo Content-type: text/html

  ```
  echo
  ```

  这在屏幕上显示 Content-type: text/html 和一个空行。

- 4. if [ -x $FINGER ]; then

  此代码检查 FINGER 值所声称的位置是否真的有一个程序。如果在此位置没有找到任何内容，脚本将进行到第 15 项。

- 5. if [ $# -eq 0 ]; then

  如果没有输入参数（# = 0），则开始执行一个语句，为 finger 程序打印一个页头。如果输入了参数，脚本将跳转到第 11 项。

- 6. cat << EOM

  脚本显示它看到的内容，直到遇到 EOM 字母，然后正常继续。

- 7. <HTML><TITLE>Finger Gateway</TITLE></HEAD><BODY>

  <h1>Finger Gateway</h1>

  这为结果页分配了一个 HTML 头 (H1) 标题行。

- 8. <ISINDEX>

  这是 HTML <FORM> 命令的前身，它将提供一个输入表单块，用户可以在其中输入要 finger 的账户。

- 9. This is a gateway to "finger." 在你的浏览器搜索框中输入 user@host 组合。<P>
