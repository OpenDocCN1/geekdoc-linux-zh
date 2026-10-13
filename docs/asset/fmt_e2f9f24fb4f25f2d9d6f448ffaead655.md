
`typelist` 与 `log` 命令和 `log security` 行中的相同。`directions` 是关键词 `inbound`（上传的文件）和 `outbound`（下载的文件）的逗号分隔列表。如果没有提供 `directions`，则将记录上传和下载的文件。默认开启入站和出站日志记录。

## 配置 Wu-FTPd 服务器

`alias linux-386 /pub/redhat/7.3/en/i386/`

此行允许用户输入 `cd linux-386` 并自动跳转到 `/pub/redhat/7.3/en/i386` 目录。

`cdpath <dir>` 行指定了 `cd` 命令查找用户输入的字符串的顺序。搜索路径按照 `ftpaccess` 文件中 `cdpath` 行的输入顺序进行。

例如，如果 `ftpaccess` 文件中有以下 `cdpath` 条目：

```
cdpath /pub/redhat/
cdpath /pub/linux/
```

当用户输入 `cd i386` 时，服务器将在 `/pub/redhat` 目录中搜索条目，然后在 `/pub/linux` 目录中搜索。如果定义了大量的别名，建议创建目录的符号链接而不是别名。这可以减少 FTP 服务器的工作量并缩短用户的等待时间。

## shutdown 文件的结构

`shutdown` 命令告诉服务器去哪里查找由 `ftpshutdown` 命令或用户生成的关闭消息。`shutdown` 命令配合关闭文件的路径使用，例如：

```
shutdown /etc/rh8ftpshutdown
```

如果此文件存在，服务器将检查该文件以确定服务器应该关闭的时间。该文件的语法如下：

`<year> <month> <day> <hour> <minute> <deny_offset> <disc_offset> <text>`

`<year>` 可以是 1970 年后的任何年份（称为 Epoch），`<month>` 为 0–11，`<hour>` 为 0–23，`<minute>` 为 0–59，`<deny_offset>` 是关闭前的分钟数，服务器在此期间将禁用新连接，`<disc_offset>` 是断开已连接用户的分钟数，`<text>` 是登录时显示给用户的消息。除了消息部分定义的有效魔术 Cookie（magic cookies）外，表 18.2 中列出的 Cookie 也可用。

### 表 18.2 shutdown 文件的 Magic Cookies

| Cookie | 说明 |
| :--- | :--- |
| `%s` | 系统将关闭的时间 |
| `%r` | 拒绝新连接的时间 |
| `%d` | 断开当前连接的时间 |

## 配置 FTP 服务器文件转换操作

FTP 服务器可以在传输过程中转换文件，以自动压缩和解压缩文件。假设用户正在向其 Microsoft Windows 机器传输一个在 Linux 机器上经过 TAR 和 GZIP 处理的文件。如果用户没有安装解压缩文件的存档工具，他们无法访问或使用这些文件。

作为 FTP 服务器管理员，你可以配置 FTP 服务器在下载前自动归档这些文件，以支持可能没有归档能力的用户。此外，你可以为用户配置一个上传区域，然后配置 FTP 服务器自动压缩任何传输到服务器的文件。

> 注意
> 允许用户向 FTP 服务器上传文件是极度危险的，除非限制在授权的本地用户。匿名上传区域通常是病毒、无许可软件以及系统破解者用于恶意用途的破解软件的滋生之地。如果允许匿名上传区域，请务必定期检查。

`ftpconversions` 文件的格式结构为：

`1:2:3:4:5:6:7:8`

其中 1 是删除前缀（strip prefix），2 是删除后缀（strip postfix），3 是添加前缀（add-on prefix），4 是添加后缀（add-on postfix），5 是外部命令（external command），6 是类型（types），7 是选项（options），8 是描述（description）。

### 删除前缀 (Strip Prefix)

删除前缀是文件名开头的一个或多个字符，当请求文件时，服务器会自动将其删除。通过在转换规则中指定一个要删除的前缀（例如 `devel_`），用户可以通过 `get proman.tar.gz` 命令请求 `devel_.gz` 文件，FTP 服务器将执行适用于该文件的其他规则并从服务器上检索它。尽管该功能已有文档说明，但截至 2.6.1 版本，尚未实现。

### 删除后缀 (Strip Postfix)

删除后缀的工作原理与删除前缀相同，不同之处是从文件名末尾提取一个或多个字符。通常，此功能用于在服务器向客户端发送文件之前执行自动解压缩操作时，从经过 TAR 和 GZIP 处理的文件删除 `.gz` 扩展名。

### 添加前缀 (Add-On Prefix)

添加前缀转换指示服务器在名称传输到服务器或客户端之前，在其前面插入一个或多个字符。例如，用户请求 `procman.tar.gz` 文件。服务器有一条转换规则为所有 `.tar.gz` 文件添加 `gnome_` 前缀；因此服务器会在将文件发送给客户端之前附加此规则。用户将收到一个名为 `gnome_procman.tar.gz` 的文件。在此功能可以使用大写和小写等关键词，用于为大小写敏感的操作系统更改文件名的大小。与删除前缀转换类似，此功能在 2.6.2 版本中尚未实现。

### 添加后缀 (Add-On Postfix)

添加后缀指示服务器在传输或接收文件期间，在文件名末尾附加一个或多个字符。服务器可以包含未解压缩的应用程序 TAR 包。如果服务器上配置了添加后缀，服务器可以压缩文件，并在文件压缩后添加 `.gz` 扩展名。

### 外部命令 (External Command)

外部命令告诉服务器如何处理该文件。以下是一个示例：

```
tar -czf %
```

### 类型 (Types)

类型字段告诉服务器适用于哪些类型的文件。

### 选项 (Options)

选项字段告诉服务器应该采取什么操作。

### 描述 (Description)

描述字段允许管理员快速解码转换规则的作用。

## 转换实例示例

编写复杂的转换条目可能是交给 Linux/UNIX 专家的任务，但 wu-ftpd 附带的示例 `ftpconversions` 文件为 Red Hat 管理员提供了足够的示例。构建自己的简单转换条目并不困难，让我们来看一个示例：

```
.:Z::/bin/compress -c %:T_REG;T_ASCII:0:UNCOMPRESS
```

在此示例中，删除前缀（字段 1）为空，因为它尚未实现，因此该规则不适用于缀。规则的第二个字段是后缀 `.Z`；因此它处理使用 `compress` 工具压缩的文件。规则未涉及添加前缀或后缀，因此字段 3 和 4 为空。字段 5 外部命令字段告诉服务器运行 `compress` 工具解压缩所有带有 `-d` 参数的文件。`-c` 选项告诉 `compress` 将输出写入到标准输出（在本例中为服务器）。`%` 是应用该规则的文件名。字段 6 指定该文件为 ASCII 格式的正文件。字段 7 选项字段告诉服务器该命令解压缩文件。最后，最后一个字段是注释

## 示例

wu-ftpd 的默认 `ftpconversions` 文件可能指定了多个转换规则。额外的示例（例如针对 Sun Solaris 操作系统）也可能出现在额外的 wu-ftpd 文档中。

# 在 fthosts 文件中使用命令允许或拒绝 FTP 服务器连接

`fthosts` 文件的作用是允许或拒绝特定用户或地址连接到 FTP 服务器。该文件的格式为 `allow` 或 `deny` 单词，后面可选跟随一个用户名，然后是 IP 地址或 DNS 地址。

```
allow username address

deny username address
```

列表 18.4 显示了该文件的示例配置。

# 列表 18.4 允许或拒绝用户访问的 fthosts 配置文件

```bash
# 示例主机访问文件

# '#' 之后的所有内容都被视为注释，
# 空行会被忽略
allow tdc 128.0.0.1
allow tdc 192.168.101.*
allow tdc insanepenguin.net
allow tdc *.exodous.net
deny anonymous 201.*
deny anonymous *.pilot.net
```

`*` 是一个通配符，可以匹配任何地址的组合。例如，`allow tdc *.exodous.net` 将允许用户 `tdc` 从任何包含域名 `exodous.net` 的地址登录到 FTP 服务器。同样，如果匿名用户来自 `201.*` 公共类 IP 地址，将不被允许访问 FTP。
