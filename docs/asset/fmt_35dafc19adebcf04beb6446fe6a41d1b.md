
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

## 配置说明

前一组选项涉及如何处理服务器生成的目录索引。`IndexOptions` `FancyIndexing` `VersionSort` `NameWidth=*` 指令使自动生成的目录索引包含关于每个文件或目录的几个信息片段，包括代表文件类型的图标、文件名、文件的最后修改时间、文件大小以及文件的描述。图 21-2 展示了一个使用默认 `FancyIndexing` 设置的目录示例。

`VersionSort` 选项允许包含版本号的文件以最自然的方式排序（例如，在此选项开启时，`version-2` 会排在 `version-10` 之前）。`NameWidth=*` 选项允许显示任意长度的文件名。你可以将星号更改为一个数字，代表“名称”列中可以显示的最大字符数。如果 `IndexOptions` 未设置为 `FancyIndexing`，索引仅显示文件的名称。

![](img/fb202c163797a743c3c6cf236316bc96_898_0.png)

图 21-2：使用 `IndexOptions` 更改 Apache 中目录的显示方式。

`AddIconByEncoding` 指令用于配置 `FancyIndexing` 的输出。它使得对于匹配特定 MIME 编码的文件显示特定的图标。在前一个示例的 `AddIconByEncoding` 行中，对于 MIME 编码为 `x-compress` 和 `x-gzip` 的文件，将显示 `/icons/compressed.gif`（对于不加载图片的浏览器，提供带有 `CMP` 替代图像标签的备选方案）。`AddIconByType` 指令具有相同的语法，但基于文件的 MIME 类型进行匹配。

`AddIcon` 指令执行类似的功能，但图标是根据文件名中的模式显示的。例如，在上述行中，对于以 `core` 结尾的文件，将显示 `/icons/bomb.gif`；对于以 `.bin` 和 `.exe` 结尾的文件，将显示 `/icons/binary.gif`。`/icons/folder.gif` 图标代表子目录。

如果 `AddIcon`、`AddIconByEncoding` 或 `AddIconByType` 指令之间存在冲突，`AddIcon` 指令具有优先权。`DefaultIcon` 指令指定如果之前没有指令将图标与特定文件关联时要显示的图像（根据上面的一行，是 `/icons/unknown.gif`）。

`HeaderName` 和 `ReadmeName` 指令指定如果存在，将插入到自动生成的目录索引顶部和底部的文件。使用默认值，服务器首先查找 `HEADER.html`，然后查找 `HEADER`，将其包含在“花式索引”的顶部。在索引的末尾，插入 `README.html` 或 `README`（whichever 先找到）。

`IndexIgnore` 指令指定不应出现在自动生成的目录索引中的文件。上面的一行排除了：

- 任何以点开头且至少包含另外两个字符的文件名
- 任何以波浪号 `~` 或通常称为井号 `#` 结尾的文件名（通常用作文本编辑器的临时文件或备份文件）
- 以 `HEADER` 或 `README` 开头的文件名（根据 `HeaderName` 和 `ReadmeName` 指令，这些是显示在目录列表顶部和底部的文件）
- `RCS`（版本控制系统）或 `CVS`（并发版本系统）目录

## 定义编码和语言

`AddEncoding` 指令允许你设置压缩定义，浏览器可以使用这些定义在数据到达时对数据进行编码。`AddLanguage` 指令允许你根据文件后缀指示文档的语言。
