

ScriptAlias 指令还执行一个相关功能，但它所别名的目录包含可执行代码（很可能是 CGI 脚本）。其语法与 Alias 指令相同。

## 重定向旧内容请求

随着 Web 服务器上的内容变化，某些内容可能会过时，而其他内容可能会移动到文件系统中的不同位置或不同的服务器上。使用 Redirect 指令，你可以将针对旧内容的请求重定向到新位置。

默认情况下，你的 Apache 服务器没有设置任何 Redirect 指令。但是，这里是关于该指令的描述文本：

```
#
# Redirect allows you to tell clients about documents which used to
# exist in your server's namespace, but do not anymore. This allows you
# to tell the clients where to look for the relocated document.
# Format: Redirect old-URI new-URL
```

可以通过简单地指示旧位置和新位置，使用 Redirect 来指示客户端它们所寻求的文档已移至他处（同一服务器或外部位置）。如果存在以下 Redirect 选项：

```
Redirect /test http://www.mybox.com/prod
```

客户端尝试访问 http://www.mybox.com/test/dmgr.html 将导致重定向到 http://www.mybox.com/prod/dmgr.html。

## 定义索引

你可以让 Apache 服务器为不同类型的文件显示不同的图标。要使用此功能，IndexOptions 应设置为 FancyIndexing，并且应使用 AddIconByEncoding、AddIconByType 和 AddIcon 指令：

```
#
# FancyIndexing: whether you want fancy directory indexing or standard
# IndexOptions FancyIndexing NameWidth=* 
#
# AddIcon* directives tell the server which icon to show for different 
# files or filename extensions. These are only displayed for
# FancyIndexed directories.
#
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip

AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*

AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wr1.gz .vrml .vrm .iv
AddIcon /icons/compressed.gif .Z .z .tgz .gz .zip
AddIcon /icons/a.gif .ps .ai .eps
AddIcon /icons/layout.gif .html .shtml .htm .pdf
AddIcon /icons/text.gif .txt
AddIcon /icons/c.gif .c
AddIcon /icons/p.gif .pl .py
AddIcon /icons/f.gif .for
AddIcon /icons/dvi.gif .dvi
AddIcon /icons/uencoded.gif .uu
AddIcon /icons/script.gif .conf .sh .shar .csh .ksh .tcl
AddIcon /icons/tex.gif .tex
AddIcon /icons/bomb.gif core

AddIcon /icons/back.gif ..
AddIcon /icons/hand.right.gif README
AddIcon /icons/folder.gif ^\^DIRECTORY\^\^
AddIcon /icons/blank.gif ^\^BLANKICON\^\^

#

# DefaultIcon: which icon to show for files which do not have an icon
# explicitly set.
#

DefaultIcon /icons/unknown.gif

#
# AddDescription: allows you to place short description after a file in
# server-generated indexes. These are only displayed for FancyIndexed
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
# HeaderName: the name of a file which should be prepended to
# directory indexes.
#
# The server will first look for name.html and include it if found.
# If name.html doesn't exist, the server will then look for name.txt
# and include it as plaintext if found.

#
ReadmeName README
HeaderName HEADER

#
# IndexIgnore: a set of filenames which directory indexing should
# ignore and not include in the listing. Shell-style wildcarding is
# permitted.
#
IndexIgnore .??* *~ *# HEADER* README* RCS CVS *,v,t
```

上一块选项涉及如何处理服务器生成的目录索引。`IndexOptions FancyIndexing NameWidth=*` 指令使自动生成的目录索引能够包含关于每个文件或目录的若干信息，包括代表文件类型的图标、文件名、文件的最后修改时间、文件大小以及文件的描述。`NameWidth=*` 选项允许显示任意长度的文件名。你可以通过将 `*` 更改为表示 Name 列中可显示的最大字符数的数字来更改此设置。如果 `IndexOptions` 指令未设置为 `FancyIndexing`，则索引中仅列出文件名。

`AddIconByEncoding` 指令用于配置 `FancyIndexing` 指令的输出。它强制显示匹配特定 MIME 编码的文件的特定图标。在上一示例的 `AddIconByEncoding` 行中，`compressed.gif`（带有用于不加载图像的浏览器的替代图像标签“CMP”）将显示在 MIME 编码为 x-compress 和 x-gzip 的文件上。`AddIconByType` 指令具有相同的语法，但基于 MIME 类型匹配文件。

`AddIcon` 指令执行类似的功能，但图标是基于文件名中的模式显示的。例如，在上述行中，`bomb.gif` 将显示在以 `core` 结尾的文件上，而 `binary.gif` 将显示在以 `.bin` 和 `.exe` 结尾的文件上。`folder.gif` 图标代表子目录，`back.gif` 文件将显示以允许导航回父目录，名为 `README` 的文件将与 `hand.right.gif` 文件关联。`blank.gif` 文件插入到自动生成的列表中，以保持正确的格式。

如果 `AddIcon`、`AddIconByEncoding` 或 `AddIconByType` 指令之间存在冲突，则 `AddIcon` 指令具有优先权。`DefaultIcon` 指令指定如果没有先前指令将与特定文件关联的图标时，应显示的图像（根据上一行，为 unknown.gif）。

`HeaderName` 和 `ReadmeName` 指令都指定如果存在，将插入到自动生成的目录索引顶部和底部的文件。使用上述默认值，服务器将首先查找 `HEADER.html`，然后查找 `HEADER`，以将其包含在“豪华索引”的顶部。在索引末尾，插入 `README.html` 或 `README`（以先找到者为准）。

`IndexIgnore` 指令指定不应出现在自动生成的目录索引中的文件。上一行排除了：

- 任何以点开头并包含至少两个额外字符的文件名。
- 任何以波浪号 (~) 或通常称为井号 (#) 结尾的文件名（通常用作文本编辑器的临时文件或备份文件）。
- 以 HEADER 或 README 开头的文件名（根据 `HeaderName` 和 `ReadmeName` 指令，在目录列表的顶部和底部显示的文件）。
- RCS（修订控制系统）目录。

## 定义编码和语言

`AddEncoding` 指令允许你设置压缩定义，浏览器可以使用这些定义对到达的数据进行编码。`AddLanguage` 指令允许你根据文件后缀指示文档的语言。

```
#
# AddEncoding: allows you to have certain browsers (Mosaic/X 2.1+)
# uncompress information on fly. Note: Not all browsers support this.
# Despite name similarity, the following Add* directives have nothing
# to do with the FancyIndexing customization directives above.
#
AddEncoding x-compress Z
AddEncoding x-gzip gz tgz

#
# AddLanguage: allows you to specify language of a document. You can
# then use content negotation to give a browser a file in a language
# it can understand.
#
#
# Danish (da) - Dutch (nl) - English (en) - Estonian (ee)
# French (fr) - German (de) - Greek-Modern (el)
# Italian (it) - Korean (kr) - Norwegian (no)
# Portuguese (pt) - Luxembourgish (lb)
# Spanish (es) - Swedish (sv) - Catalan (ca) - Czech (cz)
# Polish (pl) - Brazilian Portuguese (pt-br) - Japanese (ja)
# Russian (ru)
#
AddLanguage da .dk
AddLanguage nl .nl
AddLanguage en .en
AddLanguage et .ee
AddLanguage fr .fr
```

