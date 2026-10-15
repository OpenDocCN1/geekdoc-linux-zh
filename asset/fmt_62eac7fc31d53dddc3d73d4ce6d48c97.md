
`/etc/passwd` 文件是用户信息的主要来源。`/etc/shadow` 文件包含安全密码信息。`/etc/group` 文件包含组信息。`/home` 目录通常包含用户的主目录。

`login` 程序设置你的用户 ID 和组 ID（见下文），派生（创建自身的副本），该副本将变为你在 `/etc/passwd` 中指定为你偏好的任何 shell。该 shell 告诉你的当前工作目录是（你能猜到吗？）`/etc/passwd` 文件中指定为你的主目录的文件。

Linux 系统中的用户概念定义得相当严格，并且比你想象的要更具数值化。在登录提示符处，你输入一段字符字符串（例如 `hawkins`, `root`），称为你的用户名。系统获取此字符串，将其与 `/etc/passwd` 文件中的条目进行比较，并找到与该用户相关的加密密码。然后提示你输入密码。你输入的任何字符串都会被加密，加密结果与 `/etc/passwd` 中存储的密码字符串进行比较。如果它们匹配，系统将确认你的存在权限并开始登录过程。

`login` 程序设置你的用户 ID 和组 ID（见下文），派生（创建自身的副本），该副本将变为你在 `/etc/passwd` 中指定为你偏好的任何 shell。该 shell 告诉你的当前工作目录是（你能猜到吗？）`/etc/passwd` 文件中指定为你的主目录的文件。

## 命令

- `-s` 显示登录名、真实姓名、终端名称、写入状态、空闲时间、登录时间、办公室位置和办公电话。
- `-l` 显示多行输出，包括 `-s` 选项包含的所有信息，以及用户的家目录；家庭电话、登录 shell、邮件状态，以及（最后）其 `.plan`、 `.project` 和 `.forward` 文件的内容。
- `-p` 抑制打印 `.plan` 和 `.project` 文件。
- `-m` 抑制将用户参数与用户的真实姓名进行比对。

### `groupmod [-g gid [-o]] [-n group_name ] group`

修改与组信息相关的系统账户文件。

示例：将组 `"chem"` 的名称更改为 `"chemistry"` `(-n` 选项)，同时将其新组 ID 设置为 `127` `(-g` 选项)：

```
chgrp -g 127 -n chemistry
```

- `-g gid` 指定一个新的数字组 ID。在默认情况下，此值必须是唯一的。小于 `100` 的值预留给系统组（根据惯例）。值不能为负数。
- `-o` 允许使用非唯一的组 ID。
- `-n group_name` 为组指定新名称。

### `group [USERNAME]...`

显示指定用户的组信息。

示例：显示用户 `shae` 所属的所有组的信息：`groups shae`

- `-help` 显示帮助信息并退出。
- `--version` 显示版本信息并退出。

### `grpck [-r] [group shadow]`

检查 `/etc/group` 和 `/etc/gshadow` 中的条目是否有效（确保数据有效）。

示例：在不修改任何内容的情况下测试你的组文件的有效性：`grpck`

- `-r` 只读模式。

### `id [OPTION]... [USERNAME]`

显示指定用户的和组 ID 信息；如果未指定用户，则显示运行进程的信息。

示例：显示用户 `Michael` 的用户和组信息：

```
id michael
```

| 选项 | 描述 |
| :--- | :--- |
| `-g`, `--group` | 限制输出仅显示组 ID。 |
| `-G`, `--groups` | 仅显示附加组。 |
| `-n`, `--name` | 显示用户或组名而非 ID 数字。必须与 `-u`, `-g` 或 `-G` 之一配合使用。 |
| `-r`, `--real` | 显示真实的用户或组 ID，而非有效的。 |
| `-u`, `--user` | 仅显示用户 ID。 |

### `passwd [-u] [username]`

更改指定用户的密码。你必须是 `root` 才能对自己以外的任何用户运行此命令。

示例：如果你是 `root`，可以通过输入来重置 `Timmy` 的密码：

```
passwd timmy
```

并按照提示输入两次密码。

- `-u` 仅更新过期的密码。

### `pwck [-r] [passwd shadow]`

检查 `/etc/passwd` 和 `/etc/shadow` 中的条目是否有效。

示例：对你的密码文件进行一致性检查：

```
pwck
```

- `-r` 只读模式。

### `su [OPTION]... [USER [ARG]...]`

将身份切换为指定用户，或者在不带选项的情况下变为超级用户。

示例：要成为超级用户，输入：

```
su
```

并在提示处输入正确的密码。

示例：在不改变当前环境变量的情况下假冒 `shawkins` 的用户 ID，输入：

```
su shawkins
```

并在提示处输入正确的密码

示例：假冒 `shawkins` 的用户 ID，并用 `shawkins` 的环境变量替换你当前的所有环境变量：

```
su - shawkins
```

- `-c COMMAND`, `--command=COMMAND` 以指定用户的身份运行指定的命令，而不启动交互式 shell。
- `-l`, `-login` 使 shell 成为登录 shell。也就是说，新 shell 的行为将像你刚刚从空终端登录指定用户一样。
- `-m`, `-p`, `--preserve-environment` 不更改 `HOME`, `USER`, `LOGNAME` 环境变量。
- `-s SHELL`, `--shell=SHELL` 运行指定的 shell 而非用户密码条目中的 shell。

```
useradd [-c comment] [-d home_dir] [-f expire_date] [-f inactive_time] [-g initial_group] [-G group,...]] [-m [-k skeleton_dir] | [-M] [-s shell] [-u uid [-o]] [-n] [-r] login
```

```
useradd -D [-g default_group] [-b default_home] [-f default_inactive] [-e default_expire_date] [-s default_shell]
```

此命令用于在系统上创建新用户账户。用户必须提供登录名，但所有其他值都是可选的。

示例：创建用户 `"mary"`，其家目录 `(-d` 选项) 为 `/home/mary`，shell `(-s` 选项) 为 `/bin/bash`，组 `(-g` 选项) 为 `"chemistry"`:

```
useradd -g chemistry -s /bin/bash -d /home/mary mary
```

你还没有完成。使用密码命令为她设置新密码。如果你是繁忙的多用户系统上的系统管理员，编写一个可以以最少工作量添加新用户的脚本（对用户名、电话、家目录等使用默认值进行提示），将极大地延长你的工作寿命。如果你不是多用户系统上的系统管理员，你应该这样做。

- `-c comment` 按照指定更改注释字段。
- `-d home_dir` 将登录目录更改为指定值。
- `-e expire_date` 指定账户过期日期。
- `-f inactive_days` 指定在密码过期后永久禁用账户之前的等待天数。
- `-g initial_group` 指定一个新的初始组。
- `-G group,[...]` 指定用户所属的附加组列表。
- `-l login_name` 指定一个新的登录名。
- `-s shell` 指定一个新的登录 shell。
- `-u uid` 指定一个新的数字用户 ID。

### 修改默认值

`useradd` 有某些默认值，可以通过带有 `-D` 选项调用命令来显示或修改。（未提供选项时仅显示；否则将设置选项。）

- `-b default_home` 为新家目录指定初始路径。
- `-e default_expire_date` 指定账户过期日期。
- `-f default_inactive` 指定在密码过期后等待天数。
- `-g default_group` 为新用户指定默认组。
