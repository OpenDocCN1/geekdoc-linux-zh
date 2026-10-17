
一个类型列表字符串（`typelist string`），该命令适用于所有用户。关于其目的和参数的详细描述可以查看 `man` 页（帮助文档）。

## 为用户分配文件删除权限

`delete` 行决定用户是否可以使用 `rm` 命令删除文件。命令行格式如下：

```
delete<yes|no> <typelist>
```

`yes|no` 参数用于开启或关闭此权限，而 `typelist` 与 `chmod` 命令中的相同。

## 为用户分配文件覆盖权限

`ftpaccess` 文件中的此行命令行允许或拒绝用户覆盖现有文件的能力。其命令行格式如下：

```
overwrite<yes|no> <typelist>
```

FTP 客户端决定用户是否可以覆盖其本地机器上的文件；而此行专门控制上传到服务器的文件的覆盖权限。`yes|no` 开关用于开启或关闭权限，`typelist` 与在 `chmod` 行中看到的相同。

## 允许用户重命名文件

你可以使用此命令行来启用或阻止用户重命名文件：

```
rename<yes|no> <typelist>
```

`yes|no` 参数切换权限的开启或关闭，`typelist` 与 `chmod` 中看到的相同分隔符字符串。

## 允许用户压缩文件

此行决定用户是否能够对文件使用 `compress` 命令：

```
compress<yes|no> [<classglob>
```

`yes|no` 参数切换权限的开启或关闭，`classglob` 是一个普通字符串，用于指定一或多类用户。使用此命令后产生的转换结果在 `ftconversions` 文件中指定，该文件包含了何时对具有特定扩展的文件使用压缩或解压命令的说明，例如，`compress` 命令使用 `.z`，`gunzip` 命令使用 `.gz` 等。请参阅本章节后续的“配置 FTP 服务器文件转换操作”部分。

## 分配或拒绝使用 `tar` 的权限

此行决定用户是否能够对文件使用 `tar`（归档）命令：

```
tar<yes|no> [<classglob> ...]
```

## 在 ftpaccess 文件中使用命令配置 wu-ftp

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

`year` 可以是1970年之后（称为 epoch），`month` 为 0–11，`day` 为 0–23，`minute` 为 0–59。`deny_offset` 是关机前服务器禁用新连接的分钟数，`disc_offset` 是断开已连接用户前的分钟数，`text` 是在登录时显示给用户的消息。除了消息部分中定义的有效 cookie 之外，表 18.2 中列出的 cookie 也是可用。
