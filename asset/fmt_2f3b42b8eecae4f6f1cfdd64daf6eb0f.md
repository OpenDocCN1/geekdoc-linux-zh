
### 选项 `-e`（到期日期）

选项 `-e` 允许你以 `YYYY-MM-DD` 的形式为用户账户设置到期日期，如下所示：

```
useradd -m -e 2008-03-21 geeko
```

创建用户账户时，必要的标准配置信息（有效组、主目录位置、默认 Shell 等）是从 `/etc/default/useradd` 和 `/etc/login.defs` 文件派生的。以下是 `/etc/default/useradd` 文件的示例：

```
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
GROUPS=video,dialout
CREATE_MAIL_SPOOL=no
```

变量在以下列表中进行了解释：

- `GROUP` — 用户所属的主组
- `HOME` — 存储主目录的路径
- `INACTIVE` — 密码过期后在账户被锁定之前的不活动天数（`-1` 禁用此功能）
- `EXPIRE` — 账户将过期的日期（自 1970 年 1 月 1 日起的天数）
- `SHELL` — 登录 Shell 的路径
- `SKEL` — 主目录骨架的路径
- `GROUPS` — 用户所属的附加组
- `CREATE_MAIL_SPOOL` — 指定是否自动创建邮件 spool 目录

你也可以使用 `useradd` 命令来查看或更改默认值。选项 `--show-defaults` 显示的信息与 `cat /etc/default/useradd` 命令相同。选项 `--save-defaults` 后跟带值的选项会更改默认值：

```
da10: # useradd --save-defaults -d /export/home
da10: # useradd --show-defaults
GROUP=100
HOME=/export/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
GROUPS=video,dialout
CREATE_MAIL_SPOOL=no
```

你可以通过输入 `man 8 useradd` 来显示附加选项的描述。添加新用户后，需要为其分配密码。

### `passwd`

你可以使用 `passwd` 命令更改用户的密码。如果用户在不带用户名参数的情况下输入 `passwd`，用户可以更改自己的密码：

```
da10: # useradd -m -c "Geeko Chameleon" geeko
da10: # passwd geeko
New password:
Re-enter new password:
Password changed
```

除了用于更改用户密码外，`passwd` 命令还可以用于执行以下操作：

#### 锁定用户账户

使用选项 `-l` *lock* 锁定用户账户；使用选项 `-u` *unlock*，重新激活账户：

```
da10: # grep geeko /etc/shadow
geeko:$2a$05$QurFt5yTH2bhVxMxZ31c9YejHGt7XefIFMQ58QHspu8WDB
FWx7BhPK:13284:0:99999:7:::
da10: # passwd -l geeko
Password changed.
da10: # grep geeko /etc/shadow
geeko:!$2a$05$QurFt5yTH2bhVxMxZ31c9YejHGt7XefIFMQ58QHspu8WDB
BFWx7BhPK:13284:0:99999:7:::
da10: #
```

当密码以感叹号 `!` 开头时，账户即被锁定。

#### 用户账户状态

使用选项 `-S` 列出用户账户的状态：

```
da10:~ # passwd -S geeko
geeko LK 02/02/06 0 99999 7 -1
da10:~ #
```

状态直接跟在用户名之后。在前面的示例中，`LK` *locked* 表示用户无法登录。其他选项为 `NP` *no password* 或 `PS` *valid password*。

其后是最后一次密码更改的日期、有效性的最短长度、最长长度，以及指定密码过期的警告期和非活动期。

#### 更改密码时间

你可以使用表 9-1 中显示的选项更改各种密码时间。

| 选项 | 描述 |
|---|---|
| `-i number` | 在密码过期 *number* 天后禁用账户。 |
| `-n number` | 设置在密码可以更改之前的最少天数。 |
| `-w number` | 警告用户在 *number* 天内他的密码将过期。 |
| `-x number` | 设置密码保持有效的最大天数。*number* 天后，密码必须更改。 |

#### 表 9-1

以下是一个示例：

`passwd -x 30 -w 5 geeko`

在此示例中，用户 `geeko` 的密码有效期为 30 天。之后，密码必须由 `geeko` 更改。`Geeko` 在密码过期前 5 天会收到警告。

当使用 `passwd` 命令建立或更改用户账户的密码时，会检查 `/etc/default/passwd` 文件以确定要使用的加密方法：

```
# This file contains some information for
# the passwd (1) command and other tools
# creating or modifying passwords.

  Define default crypt hash
# CRYPT={des,md5,blowfish}
CRYPT=blowfish
...
# We can override the default for a special service
# by appending the service name (FILES, YP, NISPLUS, LDAP)
# for local files, use a more secure hash. We
# don't need to be portable here:
CRYPT_FILES=blowfish
```

加密方法在变量 `CRYPT` 中设置。默认情况下，它设置为 `DES`。对于本地文件（如 `/etc/shadow`），方法在 `/etc/default/passwd` 文件中稍后使用变量 `CRYPT_FILES` 改为 `Blowfish`。另一种可能的加密方法是 `MD5`。`YaST` 也使用 `/etc/default/passwd` 文件。

### `userdel`

此命令可让你删除现有用户账户。如果包含选项 `-r`，用户的 home 目录也会被删除。在使用 `userdel -r` 之前，你应确定用户的 UID `id user`。UID 使你能够定位分配给用户且位于其 home 目录之外的文件（如 `/var/mail/$USER`）。要删除这些文件，请输入命令：

```
find / -uid user_ID -exec rm {} \;
```

### `usermod`

修改现有用户账户的设置（如 UID、标准 shell、home 目录和主组）。`usermod` 选项基本上与 `useradd` 命令的选项相同。以下为示例：

- 更改 home 目录：

  `usermod --d /data/geeko --m geeko`

- 更改 UID：

  `usermod --u 1001 geeko`

你可以在终端窗口中使用 `id` 命令显示有关用户 UID 的信息以及用户所属的组。例如，输入 `id geeko` 会提供有关用户 `geeko` 的信息：

```
geeko@da10:~> id
uid=1000(geeko) gid=100(users)
groups=16(dialout),33(video),100(users)
geeko@da10:~>
```

此信息包括以下内容：

- *用户 ID* — `uid=1000(geeko)`
- *当前默认（有效）组* — `gid=100(users)`
- *geeko 所属的所有组* — `groups=16(dialout), 33(video), 100(users)`

### 从命令行管理组

你可以使用以下命令执行 `YaST` 中可用的相同组管理任务（以及 `YaST` 中不可用的某些任务）：

![](img/9129877170834ca9d5fdac5319bf5f12_294_0.png)

你需要以 root 身份登录（或通过输入 `su -` 切换到 root）才能使用这些命令。

- *groupadd* — 通过输入 `groupadd group_name` 创建新组。在这种情况下，使用下一个空闲的 GID。

  使用选项 `-g`（例如 `groupadd -g 200 sports`）可指定 GID。

  使用选项 `-p` 可指定加密密码。你可以使用 `mkpasswd` 命令创建加密密码。

- *groupdel* — 通过输入 `groupdel group_name` 删除组。此命令没有选项。
