
`yes|no` 参数切换权限的开启或关闭，`classglob` 是一个正则表达式，用于指定一或多个定义的用户类。使用此命令后产生的转换结果在 `ftpaccess` 文件中指定。

## 确定可应用于用户上传文件的权限

此行与权限控制部分中的其他命令略有不同。`umask` 命令决定用户可以使用什么权限创建新文件；它就在这里：

```
umask <yes|no> <typelist>
```

`yes|no` 参数的切换取决于用户是否允许在上传文件时使用默认权限创建文件。与你之前在本节之前读到的 `overwrite` 命令一样，此命令行专门用于上传的文件，因为客户端机器决定了如何从下载创建新文件。

## 配置指向 `cdpath` 的命令

此别名（`alias`）允许管理员为目录提供标准名称之外的名称：

```
alias <string> <dir>
```

`alias` 行仅适用于 `cd` 命令。如果目录位于匿名 FTP 用户目录树的深处，此行特别有用。以下是一个条目：

```
alias linux-386 /pub/slackware/11/i386/
```

这将允许用户输入 `cd linux-386` 并自动进入 `/pub/slackware/11/i386` 目录。

`cdpath` 行指定 `cd` 命令查找用户输入字符串的顺序。搜索是按照 `ftpaccess` 文件中 `cdpath` 行输入的顺序执行的。

例如，如果 `ftpaccess` 文件中存在以下 `cdpath` 条目：

```
cdpath /pub/slackware/
cdpath /pub/linux/
```

当用户在任何定义的别名中搜索条目时，会首先在 `/pub/slackware` 目录查找，然后在 `/pub/linux` 目录查找。如果了大量的别名，建议使用创建的目录符号链接代替别名。这样做可以减少 FTP 服务器的工作量并缩短用户的等待时间。

![](img/92338f4b411c2c2b03a4b8b5ff1a50b2_487_0.png)

## shutdown 文件的结构

`shutdown` 命令告诉服务器去哪里查找由 `ftpshutdown` 命令或用户生成的关机消息。`shutdown` 命令配合关机文件的文件路径使用，例如：

```
shutdown /etc/uftptshutdown
```

如果该文件存在，服务器将检查该文件以确定服务器何时关机。该文件的语法如下：

```
<year> <month> <day> <hour> <minute> <deny_offset> <disc_offset> <text>
```

`year` 可以是1970年之后（称为 epoch），`month` 为 0–11，`day` 为 0–23，`minute` 为 0–59。`deny_offset` 是关机前服务器禁用新连接的分钟数，`disc_offset` 是断开已连接用户前的分钟数，`text` 是在登录时显示给用户的消息。除了消息部分中定义的有效 cookie 之外，表 18.2 中列出的 cookie 也是可用。

## 表 18.2 关机文件的魔法 Cookie（Magic Cookies）

| Cookie | 描述 |
| --- | --- |
| `%s` | 关机时间 |
| `%r` | 拒绝连接的时间 |
| `%d` | 断开已连接用户的时间 |

## 配置 FTP 服务器文件转换操作

`shutdown` 命令告诉服务器去哪里查找由 `ftpshutdown` 命令或用户生成的关机消息。`shutdown` 命令配合关机文件的文件路径使用，例如：

```
shutdown /etc/uftptshutdown
```

如果该文件存在，服务器将检查该文件以确定服务器何时关机。该文件的语法如下：

```
<year> <month> <day> <hour> <minute> <deny_offset> <disc_offset> <text>
```

# 第 18 章 使用 FTP 进行远程文件服务

`.tar:/bin/tar -c -f %s:T_REG|T_DIR:O_TAR:TAR`

后续章节描述了转换条目的字段。

## 类型 (Types)

你必须使用 `ftpconversions` 文件中的类型来告诉服务器转换规则适用于什么类型的文件。文件条目以 `!` 字符开头，每个类型提供 `T_REG`、`T_ASCII` 和 `T_DIR` 的值。

`T_REG` 表示普通文件，`T_ASCII` 表示 ASCII 文件，`T_DIR` 表示目录。一个典型的示例是 `T_REG | T_ASCII`，它表示一个普通的 ASCII 文件。

## 选项 (Options)

选项告知服务器正在对文件执行什么操作。与类型文件类似，选项通过 `!` 字符分隔。以下是你可以分配给选项字段中项的有效值范围：

- `O_COMPRESS` 压缩文件
- `O_UNCOMPRESS` 解压缩文件
- `O_TAR` 对文件进行 tar 处理

该字段的一个示例是 `O_COMPRESS | O_TAR`，表示文件既被压缩又被 tar 处理。

## 描述 (Description)

描述字段允许管理员快速理解该规则的作用。此字段没有任何语法限制，尽管它通常是一个单条目——例如 `TAR`、`TAR+COMPRESS` 或 `UNCOMPRESS`——这足以传达概念了。

## 转换运行示例

编写转换条目最好交给 Linux/Unix 专家的任务，但 `wu-ftp` 自带的 `ftpconversions` 文件为普通管理员提供了足够的示例。构建你自己的转换条目并不困难，让我们检查并解析一个示例：

```
:.Z : /bin/compress -d -c %s:T_REG|T_ASCII:O_UNCOMPRESS
```

在此示例中，前缀（字段 1）为空，因为它尚未实现，因此此规则不适用于前缀。该规则的第二个字段包含 `.Z` 前缀；因此它处理使用压缩工具压缩的文件。该规则未处理附加后缀或后缀，因此字段 3 和 4 为空。字段 5 是外部命令字段，告诉服务器根据 `-d` 参数指定解压所有扩展名为 .Z 的文件。`-c` 选项将压缩工具的输出写入标准输出，在此例中就是该处。`%s` 是应用该规则的文件名。字段 6 指定了这是一个 ASCII 格式的普通文件。字段 7 是选项字段，告诉服务器最后一个字段是注释，为管理员快速解码该转换规则正在做什么——即解压缩文件。

## 示例 (Examples)

`wu-ftpd` 的默认 `ftpconversions` 文件中可以指定多个转换规则。额外的示例（例如 Sun 的 Solaris 操作系统）也可能在额外的 `wu-ftpd` 文档中找到。

## 使用 ftposts 文件允许或拒绝 FTP 服务器连接

`ftposts` 文件的目的是允许或拒绝特定用户或地址连接 FTP 服务器。该文件的格式为单词 `allow` 或 `deny`，可选后跟一个用户名，然后是 IP 或 DNS 地址。

```text
allow username address
deny username address
```

列表 18.3 显示了该文件的示例配置。

```
LISTING 18.3 用于允许或拒绝用户的 ftposts 配置文件

# 示例主机访问文件
# '#' 之后的所有内容都被视为注释，
# 空行被忽略
tdc 128.0.0.1
tallow tdc 192.168.101.*
tallow tdc insanepenguin.net
tallow tdc *.exodous.net
deny anonymous 201.*
deny anonymous *.pilot.net
```

`*` 是通配符，匹配该地址的任何组合。例如，`allow tdc *.exodous.net` 允许用户 `tdc` 从任何包含域名 `odous` 的地址登录 FTP 服务器。同样，如果匿名用户来自 201 公有类类 IP 地址，则不允许其访问 FTP。

对系统 FTP 服务器配置文件的更改只有在重启 `inetd` 后才会生效，因为配置文件仅在启动时解析。要以 root 身份重启 `inetd`，请执行命令 `/etc/init.d/inetutils-inetd restart`。这将调用在系统启动和关闭时针对任何运行级别启动或停止守护进程 `inetd` 的 shell 脚本。`inetd` 应报告其状态：

```bash
# /etc/init.d/inetutils-inetd restart
```

![](img/92338f4b411c2c2b03a4b8b5ff1a50b2_491_0.png)

停止互联网超级服务器 inetd:

启动互联网超级服务器 inetd:

一旦重启，FTP 服务器将对所有入站请求可访问。

## 使用命令进行服务器管理

`wu-ftp` 提供了一些命令来辅助服务器管理。这些命令是：

- `ftpwho`—显示有关当前 FTP 服务器用户的信息
- `ftpcount`—按类别显示当前服务器用户的信息
- `ftpshut`—提供自动服务器关机和用户通知
