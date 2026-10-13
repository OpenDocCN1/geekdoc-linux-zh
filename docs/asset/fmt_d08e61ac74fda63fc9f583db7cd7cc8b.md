
# 12de1f8616d71a_275_0 之后后的逻辑翻译

### `pam_rootok.so`
此模块用于以 root 身份登录时授予权限。

### `pam_securetty.so`
此模块读取 `/etc/securetty` 文件并确保 root 用户从指定的 tty 登录。
此模块读取该文件并确保 root 用户从指定的 tty 登录。

### `pam_shells.so`
此模块根据 shell 是否在 `/etc/shells` 中进行认证。

### `pam_stack.so`
此模块可以通过 `/etc/pam.d` 配置文件进行跳转。例如，`etc/pam.d/system-auth` 包含以下行：
```
account required /lib/security/pam_stack.so
```
如果被认证的用户列在 `/etc/myusers` 文件中，则认证将成功。

![](img/177ab5b774eeb101e12de61f8616d71a_273_0.png)

此模块的功能类似于 `pam_listfile.so` 模块。

### `pam_mail.so`
此模块检查用户是否有新的或未读的电子邮件，并播放消息。

### `pam_mkhomedir.so`
此模块在用户首次成功登录时创建用户的家目录。如果你使用中心用户信息存储库（使用 LDAP 或 NIS）来管理大量用户，此模块非常有用。例如，在 LDAP 服务器上创建用户账户后，不需要在所有具有权限的机器上预先创建家目录，如果这些机器在访问控制程序的配置中使用以下行作为 ssh 登录配置：
```
session required /lib/security/pam_mkhomedir.so \
skel=/etc/skel/ umask=0022
```
此行假设你想从 `/etc/skel` 目录获取资源文件（如 shell 的点文件），并为新的家目录和点文件设置 0022 的 umask。

### `pam_motd.so`
当用户成功登录时显示 `/etc/motd`（每日消息）文件。你也可以使用 `mod=/path/to/filename` 选项显示不同的文件。
不建议使用此模块，因为在用户通过验证之前显示不必要的信息可能会为潜在的入侵者提供线索。

![](img/177ab5b774eeb101e12de61f8616d71a_274_0.png)

### `pam_nologin.so`
此模块可以限制 root 以外的所有用户登录系统。
请参阅“限制 root 以外所有人的访问”章节。

### `pam_permit.so`
此模块作为 *auth、account、password 或 session* 模块工作，并始终返回成功。这应该仅用于极低风险的认证或授权任务。例如，允许任何用户使用 `kbrate` 命令来重置重复速率和延迟时间是没有风险的。因此，`/etc/pam/kbrate` 配置如下所示是可以的：
```
auth        sufficient    /lib/security/pam_rootok.so
auth        required        /lib/security/pam_console.so
account     required      /lib/security/pam_permit.so
```

### `pam_pwdb.so`
这是旧的密码数据库模块。

![](img/177ab5b774eeb101e12de61f8616d71a_274_1.png)

请使用 `pam_unix`。

### `pam_radius.so`
此模块为通过 RADIUS 服务器认证的用户提供会话服务。

### `pam_rhosts_auth.so`
这是 *rhosts* 模块。
> 远离启用了 *rhosts* 的服务，如 *login* 和 *rsh*。多年来，这些被认为是主要的安全漏洞。

![](img/177ab5b774eeb101e12de61f8616d71a_274_2.png)

### `pam_rootok.so`
这是 root 访问模块。当你以 root 身份登录并运行 shutdown、reboot、halt 或任何其他程序时，该模块生效。

![](img/177ab5b774eeb101e12de61f8616d71a_275_0)

### `pam_securetty.so`
此模块读取 `/etc/securetty` 文件并确保 root 用户从指定的 tty 登录。

### `pam_shells.so`
此模块根据 shell 是否在 `/etc/shells` 中进行认证。

### `pam_stack.so`
此模块可以通过 `/etc/pam.d` 配置文件进行跳转。例如，`etc/pam.d/system-auth` 包含以下行：
```
account required /lib/security/pam_stack.so
```

# 按时间控制

为了按时间限制访问，你需要一个名为 `pam_time` (`/lib/security/pam_time.so`) 的认证模块。该模块可以根据以下标准配置以拒绝访问：
- 他们的姓名
- 时间
- 星期
- 他们申请的服务
- 他们提交请求的终端
其操作由 `/etc/security/time.conf` 配置文件决定。遵循以下步骤：
1. 对于所有用户的访问控制，通过修改 `/etc/pam.d/system-auth` PAM 配置文件来添加以下行：
`account required /lib/security/pam_time.so`
2. 为登录服务制定一个访问策略。此示例假设用户应该在早上 6 点之后且晚上 8 点之前登录。
3. 配置 `/etc/security/time.conf` 文件。该文件的配置行格式如下：
`services;ttys;users;times`

## 表 10-3：/ETC/SECURITY/TIME.CONF 配置字段中的特殊字符
表 10-4 描述了此类配置行的字段。

## 表 10-4：/ETC/SECURITY/TIME.CONF 文件的字段

| 字段 | 说明 |
| --- | --- |
| services | 受时间限制影响的服务列表。例如，为了用规则控制 login 和 su，可以在配置行中指定服务为 `login&su`。 |
| ttys | 受时间限制影响的终端列表。例如，为了控制所有伪终端而不是控制台终端，请指定 `typ*/tty`，其中 `typ*` 列出通过 Telnet 等服务远程登录的所有伪终端，而 `tty*` 列出所有控制台终端。 |
| users | 受时间限制影响的用户列表。例如，要指定所有用户，在配置行中使用通配符 `*`。 |
| time | 限制生效的时间列表。你可以使用 24 小时制格式指定时间。例如，指定范围 `2000-0600`（即 HH 格式，其中 MM 为 00-59）。你还可以使用双字符代码指定日期，如 Mo（周一）、Tu（周二）、We（周三）、Th（周四）、Fr（周五）、Sa（周六）和 Su（周日）。也可以使用特殊代码，如 Wk 代表所有工作日，Wd 代表周末，Al 代表全天。例如，要限制每天晚上 8 点到第二天早晨 6 点对服务的访问，请指定时间范围为 `!A1200-0600`。 |

## 第 10 章：PAM

对于后续示例，你可以通过向 `/etc/security/time.conf` 文件添加以下行，来创建一个基于时间的规则，禁止所有通过远程手段（如 Telnet）访问系统的用户在晚上 8 点到第二天早晨 6 点登录：
```
login;ttyp=*:AI1200-0600
```
此行可以解释为：
- 如果（请求的服务是 login）且（通过伪终端设备进行访问）且（当前时间在晚上 8 点到第二天早晨 6 点之间），则不允许访问请求的服务。
- 否则，允许访问请求的服务。
结束

若要允许用户 kabir 随时访问系统，但让其他用户遵循先述规则，请按如下方式修改规则：
```
login;ttyp=*:kabir*:AI12000-0600
```

# 限制 root 以外的所有用户访问

`pam_nlogin` 模块可以限制 root 外的所有用户访问系统。该模块的使用方法如下：
```
auth required /lib/security/pam_nlogin.so
```
该模块会检查 `/etc/nologin` 文件是否存在。如果检查失败，模块将返回失败，但在屏幕上显示该文件的内容，用户就能看到限制的原因。
通常，`/etc/nologin` 文件在系统管理员（root）需要执行以下维护任务时创建：
- 重启服务器
- 安装特殊软件
- 配置磁盘驱动器
要禁用登录，运行 `touch /etc/nologin` 命令创建该文件。如果你想给用户写备注，可以修改此文件并告诉用户为什么他们现在无法访问你的系统。完成后，删除 `/etc/nologin` 文件，用户即可再次登录。

# 第三部分：系统安全
