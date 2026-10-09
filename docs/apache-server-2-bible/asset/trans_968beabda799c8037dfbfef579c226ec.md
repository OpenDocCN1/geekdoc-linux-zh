

请注意，Apache 查找文件的顺序与上述配置中显示的顺序（从左到右）相同。换句话说，如果 Apache 找到了 `index.html`，它将不再查找 `index.htm`、`welcome.html` 或 `welcome.htm`。你还可以将 CGI 脚本名称指定为默认索引。例如，以下指令使 Apache 在处理目录请求时始终运行 `/cgi-bin/show_index.cgi` 脚本：

```
DirectoryIndex /cgi-bin/show_index.cgi
```

## mod_autoindex

mod_autoindex 模块在 Apache 中默认被编译。当 Apache 接收目录请求时，它会查找由 DirectoryIndex 指令指定的一个或多个目录索引文件。通常，此文件是 `index.html` 或 `index.htm`。然而，如果没有这样的索引文件，Apache 可以生成动态目录列表。该模块允许你控制 Apache 如何创建动态目录列表。

Apache 生成两种类型的动态目录索引：简单和详细。详细索引以及许多其他索引选项可从该模块获得。mod_autoindex 的指令如下。

### AddAlt

当启用 FancyIndexing 时，此指令将为参数中指定的一个或多个文件或文件扩展名设置的图标设置替代文本。这是针对非图形浏览器（如 Lynx）完成的。

- **语法：** AddAlt "text" filename [filename ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令使 Apache 能够针对此处指定的每种图形文件类型显示替代文本“Pictures”以取代图标。对于图形浏览器，如 Netscape Navigator 或 Internet Explorer，替代文本在流行的 Windows 平台上显示为帮助文本。在这样的系统中，当用户将鼠标光标移动到代表某类文件的图标上方时，可以获得关于该文件的提示或帮助：

```
AddAlt "Pictures" gif jpeg jpg bmp
```

### AddAltByEncoding

如果你不想通过 AddAlt 指令为文件名或文件扩展名分配替代文本，你可以使用 AddAltByEncoding 指令为一个或多个 MIME 编码分配此类文本。与 AddAlt 一样，此指令也仅在启用 FancyIndexing 时可用。

- **语法：** AddAltByEncoding "text" MIME_encoding [MIME_encoding ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令使 Apache 对所有 MIME 类型为 x-compress 的文件显示“Compressed File”替代文本。

```
AddAltByEncoding "Compressed File" x-compress
```

### AddAltByType

与 AddAltByEncoding 指令类似，AddAltByType 指令为文件设置替代文本，而不是为 FancyIndexing 设置图标。但是，它使用 MIME 类型而不是 MIME 编码。

- **语法：** AddAltByType "text" MIME_type [MIME_type ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令针对非图形浏览器显示“HTML FILE”文本以取代图标。对于图形浏览器，此文本可能作为提示或帮助出现：

```
AddAltByType "HTML FILE" text/html
```

### AddDescription

当启用 FancyIndexing 时，AddDescription 指令为文件名、部分文件名或通配符文件名设置描述文本。

- **语法：** AddDescription "text" file [ file ... ]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令在生成的目录列表中显示所有 GIF、JPEG、JPG 和 BMP 文件的描述：

```
AddDescription "Graphics File" *.gif *.jpeg *.jpg *.bmp
```

### AddIcon

AddIcon 指令允许你为显示在 FancyIndexing 中的文件和目录名称分配图标。

- **语法：** AddIcon icon name file [filename ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令告诉 Apache 在具有 .gif、.jpg 和 .bmp 等扩展名的文件旁边显示 /icons/picture.gif：

```
AddIcon /icons/picture.gif .gif .jpg .bmp
```

如果你还想为列出的文件扩展名提供替代文本，可以使用如下格式，其中 IMG 是为非图形浏览器显示的替代文本：

```
AddIcon (IMG. /icons/picture.gif) .gif .jpg .bmp
```

如果你想为目录显示图标，可以如下使用该指令：

```
AddIcon /path/to/your/directory/icon ^^DIRECTORY^^
```

同样地，如果你想为详细索引方案显示的每个空白行显示一个图标，可以使用：

```
AddIcon /path/to/your/blank/line/icon ^^BLANKICON^^
```

### AddIconByEncoding

AddIconByEncoding 指令允许你为 MIME 编码分配图标。换句话说，你可以将图标图像分配给 MIME 类型。

- **语法：** AddIconByEncoding icon_file MIME_encoding [MIME_encoding ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下 AddIconByEncoding 指令告诉 Apache 对所有 x-gzip（即 .gz 扩展名）MIME 类型文件显示 /icons/zip.gif 图标。

```
AddIconByEncoding /icons/zip.gif x-gzip
```

### AddIconByType

AddIconByType 指令也允许你为一个或多个 MIME 类型分配图标。

- **语法：** AddIconByType icon_file MIME_type [MIME_type...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下 AddIconByType 指令告诉 Apache 为所有 text/html 文件显示 /icons/html.gif 图标。

```
AddIconByType (HTML,/icons/html.gif) text/html
```

### DefaultIcon

当没有为文件匹配任何 AddIcon、AddIconByEncoding 或 AddIconByType 时，可以显示默认图标。DefaultIcon 指令允许你设置该图标。

- **语法：** DefaultIcon URL
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令每当文件的图标关联未知时显示 idontknow.gif：

```
DefaultIcon /icon/idontknow.gif
```

### FancyIndexing

FancyIndexing 指令允许你启用或禁用目录的详细索引。你可以通过 IndexOptions 指令实现相同的效果。

- **语法：** FancyIndexing On | Off
- **上下文：** 服务器配置、虚拟主机、目录、每目录配置（.htaccess）
- **覆盖：** Indexes

### HeaderName

如果你使用 FancyIndexing，可以在索引列表的顶部插入文件内容。HeaderName 指令允许你指定用于此类插入的文件名。

- **语法：** HeaderName filename
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令告诉 Apache 在列表目录中查找名为 welcome 或 welcome.html 的文件；如果找到此类文件，内容将插入在实际列表之前：

```
HeaderName welcome
```

### IndexIgnore

如果你需要某些文件或文件扩展名在目录列表中不可见，可以使用 IndexIgnore 指令来实现这一点。

- **语法：** IndexIgnore file [file...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令确保 Apache 不在目录列表中列出 welcome、welcome.html 或每目录配置文件（.htaccess）：

```
IndexIgnore welcome welcome.html .htaccess
```

点号（.）字符自动包含在 IndexIgnore 列表中；因此，以该字符开头的文件不会被列出。然而，你可能仍倾向于将每目录配置文件（.htaccess）添加到列表中，只是为了让你感到更安全。

### IndexOptions

IndexOptions 指令指定自动生成的目录索引的行为。

- **语法：** IndexOptions option [option] [...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

