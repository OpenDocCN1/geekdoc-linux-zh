
第一种形式创建一个名为 `username` 的新用户账户。未使用选项指定的可选值将从 `/etc/login.defs` 和 `/etc/default/useradd` 分配默认值。表 18-1 列出了 `useradd` 接受的选项。

# 表 18-1 useradd 选项和参数

| 选项 | 描述 |
| --- | --- |
| -c comment | 使用注释作为名称字段 |
| -d home_dir | 将新用户的家目录命名为 home_dir |
| -e expire_date | 将账户过期日期设置为 expire_date |
| -f inactive_time | 在密码过期后 inactive_time 天禁用禁用账户 |
| -g initial_group | 将用户的主组身份（或登录组）设置为 initial_group |
| -G [group[...]] | 使用户成为每个附加组的成员 |
| -m | 如果家目录不存在则创建该家目录，并复制 /etc/skel 中的文件和目录结构到新目录 |
| -k skeleton_dir | 将 skeleton_dir 而非 /etc/skel 中的文件和目录结构到新的家目录；必须配合 -m 使用 |
| -M | 禁止创建家目录；不能指定 -m 和 M |
| -p passwd | 将账户密码设置为加密后的密码 passwd |
| -s shell | 将用户的默认 shell 设置为 shell |
| -u uid | 将用户的 UID（用户 ID）设置为 uid，uid 必须是唯一的数字 |
| 0 | 允许通过 -u uid 指定 UID 不唯一；必须配合 -u 使用 |

# 第 18 章：在命令行上配置系统

| 选项 | 描述 |
| --- | --- |
| -n | 禁用 Red Hat Linux 用户组的使用 |
| -r | 创建系统账户（UID 小于 100 的账户），但不创建家目录 |
| username | 将登录名设置为 *username* |

`adduser` 程序是 `useradd` 的符号链接。

调用 `useradd` 的第二种方法是使用 `-D` 选项。仅用 `-D` 调用时，`useradd` 会显示其当前的默认设置。在使用表 18-2 列出的任何选项配合 `-D` 时会修改相应字段的默认值。以下是第二种方法的语法：

```
useradd [-g default_group] [-b default_home_dir]
  [-f default_inactive_time] [-e default_expire_date]
  -s default_shell
```

`useradd` 的默认值存储在 `/etc/default/useradd` 中。

# 表 18-2 修改 useradd 默认值的选项

| 选项 | 描述 |
| --- | --- |
| -g default_group | 将默认组设置为 *default_group* |
| -b default_home_dir | 将默认家目录设置为 *default_home_dir* |
| -f default_inactive_time | 将默认账户禁用时间设置为 *default_inactive_time* 天 |
| -e default_expire_date | 将默认账户过期日期设置为 *default_expire_date* |
| -s default_shell | 将默认登录 shell 设置为 *default_shell* |

# 第部分：Red Hat Linux 系统维护

`userdel` 命令删除用户账户，并可选地删除相关文件。语法为：

```
userdel [-r] username
```

`username` 指定要删除的用户账户。使用 `-r` 会删除相应的家目录和邮件池。如果不使用 `-r`，`userdel` 仅移除用户和组数据库文件中的账户引用。你不能删除已登录用户的账户；如果 `username` 正在登录，`userdel` 将失败。

`usermod` 修改现有的用户账户。其语法为：

```
usermod [-c comment] [-d home_dir [-m]] [-e expire_date]
 [- inactive] [q initial_group]
 [-G group...] [-n new_username] [-p passwd]
 [-s shell] [-u uid [-o]] [-L--U] username
```

`usermod` 接受表 18-1 列出的 `useradd` 选项和参数，并增加了三个：`-n new_username` 和 `-U`。`-l new_username` 将账户名从 `username` 更改为 `new_username`。`-l` 通过在 `/etc/shadow` 中用户的加密密码前放置 `!` 来禁用（锁定）用户账户。`-u` 通过移除 `!` 来启用（解锁）账户。必须指定至少一个选项；`-p`、`-U` 和 `-L` 可以任意组合使用。如果 `username` 正在登录，`usermod` 将失败，因为你不能更改登录用户的登录名。

`passwd` 命令通常被认为是“密码更改工具”，实际上它的功能比仅仅更改密码要得多。通常情况下，它会更新用户所有的验证令牌；登录密码只是其中之一。语法为：

```
passwd [-dk luf] [-S] username
```

`d` 移除 `username` 的密码，禁用该账户。`-k` 使 `passwd` 仅更新过期的验证令牌（在这种情况下为密码）。`-l` 或 `-u` 分别通过在 `/etc/shadow` 中 `username` 密码前放置或移除 `!` 来锁定或解锁 `username` 账户。`-s` 最后显示简短的状态消息，指示账户是锁定还是解锁状态、使用的加密类型等。

`chsh` 命令更改用户的登录 shell。其语法为：

```
chsh [-s shell] [-l] [username]
```

`s` 将用户的登录 shell 设置为 `shell`。除非另有配置，否则 `shell` 可以是系统中任何可执行文件的完整路径。利用此功能的一种常用方法是将 `shell` 设置为 `/bin/false` 或另一个不给用户提供登录提示符的命令来禁用账户。使用 `-t -l` 选项显示 `/etc/shells` 中列出的 shells。

`chage` 命令更改用户密码的过期策略。其语法为：

```
chage [ - ] [ m mindays ] [ M maxdays ] [ - lastday ] [ I inactive ]
[ -E expiredate ] [ W warndash ] username
```
