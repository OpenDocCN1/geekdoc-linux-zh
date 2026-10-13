
### times
指定限制何时生效。时间可以以 24 小时制格式指定。例如，`0700–1700` 是涵盖上午 7 点至下午 5 点的范围。时间格式也可以包括天数，如表 10-1 所示。

**表 10-1 limit 的时间格式**

| 关键字 | 含义 |
| :--- | :--- |
| Any | 任何时间 |
| Wk | 任何工作日 |
| Sa | 星期六 |
| Su | 星期日 |
| Mo | 星期一 |
| Tu | 星期二 |
| We | 星期三 |
| Th | 星期四 |
| Fr | 星期五 |

你还可以组合天数。例如：`SaSu07–17` 涵盖从上午 7 点到下午 5 点的周末。以下是一个设置访问限制的配置示例：

```
class  local   real     *.nitec.com
class  remote  anonymous  *

limit local  200  Any /etc/msgs/msg.toomany
limit remote 100  Any /etc/msgs/msg.toomany
```

上述配置允许来自 `nitec.com` 域的多达 200 名用户在任何时间登录，并且仅允许 100 名匿名用户在任何时间访问系统。

#### noretrieve

**语法：** `noretrieve filename filename . . .`

**默认：** 无

此关键字禁止 FTP 用户检索指定名称的文件。例如，

```
noretrieve /etc/passwd
```

禁止任何人检索 `/etc/passwd` 文件。会显示诸如“`/etc/passwd` 被标记为不可检索”之类的消息。请注意，如果文件名不包含完全限定路径名，则所有具有此类名称的文件都被标记为不可检索。例如，

```
noretrieve passwd core
```

防止任何人从任何目录检索任何名为 `passwd` 或 `core` 的文件。文件名中不能使用通配符。

#### loginfails

**语法：** `loginfails number`

**默认：** `loginfails 5`

此关键字定义用户在断开连接前可以尝试登录的次数。当用户在指定次数内未能输入有效的用户名/密码对进行登录时，会记录错误消息并断开该用户的连接。

#### private

**语法：** `private yes or no`

**默认：** 无

`wu-ftpd` 服务器提供了一组非标准的扩展 FTP 命令。其中一个命令称为 `SITE`，被视为安全风险。因此，不建议使用 `private` 关键字。事实上，随 Red Hat 发行的 `wu-ftpd` 默认版本中已禁用了 `SITE` 命令。你需要自行编译 `wu-ftpd` 才能启用 `SITE` 命令，但不推荐这样做。

#### autogroup

**语法：** `autogroup groupname class [class . . . ]`

**默认：** 无

此关键字允许你更改匿名用户的有效组 ID，前提是该用户属于一个或多个指定的类。

### 信息配置

可以使用 `banner`、`email`、`message` 和 `readme` 关键字指定信息配置。

#### banner

**语法：** `banner filename`

**默认：** 无

此关键字可用于显示指定文件的内容。通常，许多系统使用横幅（banner）来标识系统并提供用户策略和联系信息。

如果你使用 `banner` 关键字在登录前显示文件，某些非标准 FTP 客户端可能无法登录，因为它们无法处理来自服务器的多行响应。

#### email

**语法：** `email user@host`

**默认：** `email root@localhost`

此关键字设置 FTP 站点管理员的电子邮件地址。

#### message

**语法：** `message path {when [class . . . ]}`

**默认：** `/welcome.msg login`, `.message cwd=*`

此关键字用于设置在用户登录系统或使用更改目录命令切换目录时显示的文件名称。例如，上面显示的第一个默认设置会在用户成功登录时显示 `/welcome.msg` 文件的内容。第二个默认设置会在用户更改目录时显示 `.message` 文件的内容。如果要显示的文件缺失，则不会显示任何内容。

### 魔术 Cookie 字符串

要显示的文件可以包含表 10-2 中所示的一个或多个魔术 Cookie 字符串。

#### 表 10-2 消息文件的魔术 Cookie 字符串

| Cookie | 替换文本 |
|---|---|
| `$C` | 当前工作目录 |
| `$E` | 在 `ftpaccess` 中定义的文件维护者电子邮件地址 |
| `$F` | CWD 分区的可用空间 (K) |
| `$L` | 本地主机名 |
| `$M` | 此类中允许的最大用户数 |
| `$N` | 此类中当前的用户数 |
| `$R` | 远程主机名 |
| `$T` | 本地时间（格式为“Fri 30 15 17:12:42 2001”） |
| `$U` | 通过 RFC 931 认证确定的用户名 |
| `$U` | 登录时给出的用户名 |

#### 清单 10-2 /welcome.msg 文件的示例

清单 10-2 显示了我用于 Red Hat 系统的 *welcome.msg* 文件。

```
Hello $U
Welcome to $L. You are user $N of possible $M users. You are logging in from $R.
Local time is $T
Feel free to email ($E) if you have any questions or comments.
Your current directory is $C (Free $F KB).
```

消息文件在每个目录下仅显示一次。如果您计划显示匿名访问的消息文件，请使用相对于匿名 FTP 目录树根目录的相对路径。

#### readme

**语法：** `readme path {when {class . . .}}`

**默认值：** `readme README* login`

`readme README* cwd=*`

此关键字类似于之前讨论的 `message` 关键字。然而，它不会显示指定文件的内容，而是让 FTP 服务器通知用户该文件的存在，并告知用户该文件的修改日期和时间。

### 日志配置

可以使用 `log commands` 和 `log transfers` 关键字指定日志配置。

#### log commands

**语法：** `log commands typelist`

**默认值：** `none`

此关键字允许您记录一个或多个类型用户的 FTP 命令。例如，

```
log commands anonymous
```

记录所有匿名用户执行的所有 FTP 命令。

#### log transfers

**语法：** `log transfers typelist directions`

**默认值：** `log transfers anonymous,real inbound,outbound`

此关键字允许您记录进出货系统的文件传输。默认设置使服务器记录匿名用户和真实用户的入站和出站文件传输。

### 权限配置

以下关键字允许您控制用户的文件/目录权限设置。

#### chmod

**语法：** `chmod yes|no typelist`

**默认值：** `chmod no guest,anonymous`

此关键字为列表中指定的用户类型启用或禁用 `chmod` 命令 (`site chmod`)。例如，默认设置为游客和匿名用户禁用此命令。默认情况下，`chmod` 命令不可用。

#### delete

**语法：** `delete yes|no typelist`

**默认值：** `delete no guest,anonymous`

此关键字为 `typelist` 中指定的用户启用或禁用 `delete` (`del`) 命令。例如，默认设置为游客和匿名用户禁用 `delete` 命令。

#### overwrite

**语法：** `overwrite yes|no typelist`

**默认值：** `overwrite no guest,anonymous`

此关键字为 `typelist` 中指定的用户启用或禁用文件覆盖。例如，默认设置为游客和匿名用户禁用文件覆盖。

#### rename

**语法：** `rename yes|no typelist`

**默认值：** `rename no guest,anonymous`

此关键字为 `typelist` 中指定的用户启用或禁用 `rename` 命令。例如，默认设置为游客和匿名用户禁用 `rename` 命令。

#### umask

**语法：** `umask yes|no typelist`

**默认值：** `none`

此关键字为 `typelist` 中指定的用户启用或禁用 `umask` 命令 (`site umask`)。默认情况下，`umask` 命令不可用。

#### passwd-check
