
该关键字用于设置在用户登录系统或使用更改目录命令更改目录时要显示的文件名。例如，刚才显示的第一个默认设置会在用户成功登录时显示 `/welcome.msg` 文件的内容。第二个默认设置会在用户更改目录时显示 `.message` 文件的内容。当要显示的文件丢失时，不会显示任何内容。

要显示的文件可以包含表 10-2 所示的一个或多个魔术 cookie 字符串。

### 表 10-2 消息文件的魔术 Cookie 字符串

| Cookies | 替换文本 |
|---|---|
| `%C` | 当前工作目录 |
| `%E` | `ftpaccess` 中定义的维护人员的电子邮件地址 |
| `%F` | `CWD` 分区中的可用空间（K） |
| `%L` | 本地主机名 |
| `%M` | 此类允许的最大用户数 |
| `%N` | 此类中的当前用户数 |
| `%R` | 远程主机名 |
| `%T` | 本地时间（格式为“Thu Nov 15 17:12:42 1990”） |
| `%U` | 通过 `RFC 931` 身份验证确定的用户名 |
| `%U` | 登录时提供的用户名 |

### 清单 10-2 `/welcome.msg` 文件示例

```
Hello %U

Welcome to %L. You are user %N of possible %M users.
You are logging in from %R.

Local time is %T
```

## 列表 10-2 继续

```
Feel free to email (&E) if you have any questions or comments.
```

```
Your current directory is &C (Free &F KB)
```

消息文件每个目录仅显示一次。如果您计划为匿名访问显示消息文件，请使用相对于匿名 FTP 目录树基目录的相对路径。

### readme

```
Syntax: readme path {when {class . . .} }
Default:
readme README* login
readme README* cwd=*
```

此关键字与前面讨论过的 `message` 关键字类似。然而，它不会显示命名文件的内容，而是使 FTP 服务器通知用户该文件的存在，并告知用户该文件的修改日期和时间。

## 日志配置

日志配置可使用 `log commands` 和 `log transfers` 关键字指定。

### log commands

```
Syntax: log commands typelist
Default: none
```

此关键字允许您为一个或多个类型的用户记录 FTP 命令。例如，

```
log commands anonymous
```

logs all the FTP commands performed by all anonymous users.

### log transfers

```
Syntax: log transfers typelist directions
Default: log transfers anonymous,real inbound,outbound
```

此关键字允许您记录进出系统的文件传输。默认设置使服务器记录匿名用户和真实用户的入站和出站文件传输。

## 权限配置

以下关键字允许您控制用户的文件/目录权限设置。

### chmod

语法：`chmod yes|no typelist`

默认值：`chmod no guest,anonymous`

此关键字启用或禁用指定列表中的用户类型的 `chmod` 命令（`site chmod`）。例如，默认设置会为 `guest` 和 `anonymous` 用户禁用此命令。默认情况下，`chmod` 命令不可用。

### delete

语法：`delete yes|no typelist`

默认值：`delete no guest,anonymous`

此关键字启用或禁用 `type` 列表中指定的用户的 `delete`（`del`）命令。例如，默认设置会为 `guest` 和 `anonymous` 用户禁用 `delete` 命令。

### overwrite

语法：`overwrite yes|no typelist`

默认值：`overwrite no guest,anonymous`

此关键字启用或禁用 `typelist` 中指定的用户覆盖文件的操作。例如，默认设置会为 `guest` 和 `anonymous` 用户禁用文件覆盖。

### umask

此关键字启用或禁用指定 `typelist` 中用户的 `umask` 命令（`site umask`）。默认情况下，`umask` 命令不可用。

### passwd-check

```
Syntax: passwd-check none|trivial|rfc822 (enforce|warn)
```

```
Default: passwd-check rfc822 warn
```

此关键字定义匿名用户所需的密码类型。默认设置要求密码为电子邮件地址；然而，如果用户未能输入有效的电子邮件地址，则不会强制执行此规则——服务器仅警告用户密码无效。当不需要密码检查时，请按如下方式设置 `passwd-check` 关键字：

```
passwd-check none
```

如果将检查设置为 `trivial`，服务器仅检查密码中是否存在 `@` 字符。

### path-filter

```
Syntax: path-filter typelist mesg allowed_charset {disallowed regexp . . .}
```

```
Default: none
```

此关键字允许您限制 `typelist` 中指定的用户在文件上传时使用的某些文件名。

### upload

```
Syntax: upload root-dir dirglob yes|no owner group
```

```
Default: none
```

此关键字允许您启用或禁用上传目录。例如，

```
upload /home/ftp /dropbox yes root ftp 0600
```

在 `/dropbox` 目录下新建子目录，然后将前面的 `upload` 行更改为以下内容：

```
upload /home/ftp /dropbox yes root ftp 0600 nodirs
```

另一方面，如果您希望允许上传者创建子目录，则将 `nodirs` 替换为 `dirs`。

## 杂项配置

以下关键字允许您控制各种设置。

### alias

语法：`alias string dir`

默认值：`none`

此关键字允许您为目录创建别名。例如，

```
alias redhat /pub/linux/distributions/redhat
```

允许用户键入 `cd redhat` 命令以更改到 `/pub/linux/distributions/redhat` 目录。

### cdpath

语法：`cdpath dir`

默认值：`none`

此关键字将指定目录添加到更改目录（`cd`）命令的搜索路径中。例如：

```
cdpath /pub/linux/redhat
```

如果用户输入命令 `cd RPMS`，则服务器首先在用户当前目录中查找名为 `RPMS` 的目录。如果找不到，则查找名为 `RPMS` 的别名。如果仍然找不到，则尝试将目录更改为 `/pub/linux/redhat/RPMS`。

### compress

语法：`compress yes|no class [class ...]`

默认值：`compress yes all`

此关键字为指定类启用或禁用压缩功能。默认设置为名为 `all` 的类启用压缩功能，该类默认涵盖所有真实、匿名和访客用户。

当默认设置保持不变且 `ftpconversions` 文件未被修改时，使用 FTP 服务的所有用户都能够即时压缩文件。例如，想要以压缩文件形式获取整个目录内容的用户可以输入命令 `get directoryname.tar.gz`，并将下载压缩的 tar 文件。

### tar

语法：`tar yes|no class [class ...]`

默认值：`tar yes all`

此关键字为指定类启用或禁用 `tar`（磁带归档文件）功能。默认设置允许名为 `all` 的类的 `tar` 功能，该类默认涵盖所有真实、匿名和访客用户。当默认设置保持不变且 `ftpconversions` 文件未被修改时，使用 FTP 服务的所有用户都能够即时打包文件。例如，想要以压缩文件形式获取整个目录内容的用户可以输入命令 `get directoryname.tar`，并将下载 tar 文件。

### shutdown

语法：`shutdown path`

默认值：`shutdown /etc/shutmsg`

此关键字指定 FTP 服务器不时监控以检测关闭事件的文件。此文件可使用 `ftpshut` 命令创建。例如，要立即关闭服务器，请运行以下命令：

```
ftpshut now
```
