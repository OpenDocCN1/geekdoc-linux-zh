
表 18-3 列出了 `chage` 接受的有效选项。

# 表 18-3 CHAGE 命令的选项

| 选项 | 描述 |
| --- | --- |
| username | 指定 `username` 为查询或修改的账户名 |
| -l | 显示 `username` 的过期信息 |
| -m minddays | 设置 `minddays` 为密码更改之间允许的最小时间 |
| -M maxdays | 设置 `maxdays` 为密码有效的天数 |
| -d lastday | 设置 `lastday` 为最后更改密码的日期，表示为自 1970 年 1 月 1 日以来的天数。`lastday` 可以使用更方便的日期格式，例如 2001 年6 月 21 日或 2001-0621 |
| I inactive | 设置 `inactive` 为密码更改后 `username` 账户处于非活动状态的天数 |
| -E expiredate | 设置 `expiredate` 为账户过期的日期 |
| -W warndash | 设置 `warnotime` 为账户过期前发出警告的天数 |

正如章节开头，命令行工具的优势之一是它们可以用于批量更改。两个命令 `passwd` 和 `newusers` 对用户密码进行多次更改。

# 组的操作

+   `useradd` - 创建账户
+   `userdel` - 删除账户
+   `usermod` - 修改账户

要创建一个新组，使用 `useradd` 并传递名称。其语法为：

```
useradd [-g default_group] [-b default_home_dir]
  [-f default_inactive_time] [-e default_expire_date]
  -s default_shell
```

默认情况下，`last` 列出 `/var/log/wtmp` 中的所有记录，你可以使用 `-n` 指定输出行数。通常，`last` 在第三列显示主机名，但使用 `-a` 将主机名放在最后一列。`-i` 显示主机的 IP 地址，`-R` 完全不显示主机名。要查看特定用户的登录活动，使用 `username` 和 `tty` 可以让你按 TTY 查看登录。可以列出多个用户名和 TTY。

# 查看登录和进程信息

查看当前和过去的登录信息并确定用户运行的进程，可以使用以下命令之一：

+   `last` - 显示历史登录信息
+   `who` - 显示当前运行的进程
+   `w` - 显示用户的当前活动

`last` 打印用户名、TTY、日期、经过的时间以及远程主机的主机名或 IP 地址（适用），从最近的登录开始。其语法为：

```
last [-R] [-ai] [-n username] [tty]
```

默认情况下，`last` 列出 `/var/log/wtmp` 中的所有记录，你可以使用 `-n` 指定输出行数。通常，`last` 在第三列显示主机名，但使用 `-a` 将主机名放在最后一列。`-i` 显示主机的 IP 地址，`-R` 完全不显示主机名。要查看特定用户的登录活动，使用 `username` 和 `tty` 可以按 TTY 查看登录。可以列出多个用户名和 TTY。

# 修改现有账户

语法为：

```
usermod [-c comment] [-d home_dir [-m]] [-e expire_date]
 [- inactive] [q initial_group]
 [-G group...] [-n new_username] [-p passwd]
 [-s shell] [-u uid [-o]] [-L--U] username
```

`usermod` 接受表 18-1 列出的 `useradd` 选项和参数，并增加了三个：`-n new_username` 和 `-U`。`-l new_username` 将账户名从 `username` 更改为 `new_username`。`-l` 通过在 `/etc/shadow` 中用户的加密密码前放置 `!` 来禁用（锁定）用户账户。`-u` 通过移除 `!` 来启用账户。必须指定至少一个选项；`-p`、`-U` 和 `-L` 可以任意组合使用。如果 `username` 正在登录，`usermod` 将失败，因为你不能更改登录用户的登录名。

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
chage [ - ] [ m minddays ] [ M maxdays ] [ - lastday ] [ I inactive ]
[ -E expiredate ] [ W warndash ] username
```

表 18-3 列出了 `chage` 接受的有效选项。

# 同时修改多个账户

正如章节开头，命令行工具的优势之一是它们可以用于批量更改。两个命令 `passwd` 和 `newusers` 对用户密码进行多次更改。

# passwd 和 newusers 命令

同样，对于新用户和现有用户，`newusers` 在家目录不存在时创建它。`passwd` 命令批量更新现有密码。它读取一个由冒号分隔的 `username:password` 对组成的文件。密码必须是明文，并在运行时进行加密，除非在调用 `passwd` 时使用了 `-e` 选项，在这种情况下密码必须使用兼容 `crypt(3)` 的加密算法预过加密。

```
username:password:uid:gid:gecos:homdir:shell
```

# 472 第四部分：红帽 Linux 系统维护

`who` 命令显示当前登录用户的信息。它的默认输出包括用户名、登录的 TTY 以及每个用户登录的日期和时间。`who's` 的语法为：

```
who [-Hl] [-q]
```

使用 `-H` 选项为 `who` 的输出添加列标题。指定 `-i` 会将每个用户的空闲时间添加到显示内容中。使用 `-l` 强制 `who` 显示完整的 FQDN（完全限定域名名）。要获取登录用户的总数，请单独使用 `q` 选项。

`w` 命令与 `who` 非常相似，不同之处在于它还会显示每个用户运行进程的命令行以及每个用户 CPU 使用情况的摘要。`w` 的语法为：

```
w [-huf] [username]
```
