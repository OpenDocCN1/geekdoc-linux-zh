
密码字段通常包含一个 `x`。如果你的系统使用了组密码，你需要指定一个密码以便在使用在本章稍后讨论的 `newgrp` 命令更改所讨论的主组成员身份。这些密码使用 `gpasswd` 命令设置，并可以存储在 `/etc/shadow` 文件中以增加安全性。更多信息请参阅 `gpasswd` 手册或 info 页面。

![](img/bafa5678973f896b93838a140b8f7840_479_0.png)

`GID` 代表组的唯一 ID，`members` 字段表示组成员列表。下面显示了一个 `/etc/group` 示例：

```
# /etc/group 示例代码块保持不变
```

从前面的输出可以看出，“bin”组的 `GID` 为 1，并有三个用户作为成员：`root`、`bin` 和 `daemon`。

## 创建用户账户

你可以使用 `useradd` 命令在 Linux 系统上创建用户账户，并将用户名作为参数，如下：

```
[root@server1 ~]# useradd bobg
[root@server1 ~]#
```

在这种情况下，所有信息（如 UID、shell 和家目录位置）都取自包含用户账户创建默认值的文件。

第一个文件 `/etc/login.defs` 包含了用于设置电子邮件默认位置、密码过期信息、最小密码长度以及可用 UID 和 GID 范围的参数。此外，它还决定了在创建用户时是否会自动创建家目录，以及用于存储密码的密码算法。

`/etc/group` 文件具有以下冒号分隔的字段：

`name:password:GID:members`

第一个字段是组名，后面是组密码。

# 第 10 章 常见管理任务

## 修改用户账户

| 选项 | 描述 |
| :--- | :--- |
| `-c "description"` | 在 `/etc/passwd` 的 GECOS 字段中为用户指定新描述 |
| `-d homdirectory` | 指定新主目录的绝对路径 |
| `-e expiredate` | 指定禁用账户登录的日期 |
| `-f days` | 指定密码过期的账户被禁用的前等待天数 |
| `-g group` | 为用户账户指定新的主组 |
| `-G group1,group2, etc.` | 为用户账户指定所有其他组组成 |
| `-l name` | 指定新的登录名 |
| `-s shell` | 指定用于用户账户的新 shell 绝对路径 |
| `-u UID` | 为用户账户指定新的 UID |

**表 10-7** `usermod` 命令的常用选项

`usermod` 命令无法修改的账户信息是存储在 `/etc/shadow` 中的密码过期信息（之前讨论过的 `min`, `max`, `warn`）。要更改这些信息，可以使用 `chage` 命令配合相应的选项。例如，要指定用户在收到新密码后必须等待两天才能更改密码，并指定密码在 50 天后过期且提前 7 天发出警告，可以使用 `chage` 命令的以下选项：

```bash
[root@server1-#] chage -m 2 -M 50 -W 7 bobg
[root@server1-#]
```

有时有必要锁定账户——即防止用户登录。要锁定账户，可以在命令行提示符下使用 `usermod -L username`。这会在 `/etc/shadow` 的过期密码字段开头放置一个 `!` 字符。要解锁账户，只需在命令行提示符下输入 `usermod -U username`，这将移除 `/etc/shadow` 文件中密码字段的 `!` 字符。或者，你可以使用 `passwd -l username` 锁定账户，使用 `passwd -u username` 解锁账户。这些命令分别在 `/etc/shadow` 文件的过期字段开头放置或移除 `!` 字符。

另一种常用的锁定账户方法是将 `/etc/shadow` 中的账户 shell 字段更改为无效 shell（如 `/bin/false`）。如果没有有效的 shell，用户将无法登录系统。要锁定账户，可以编辑 `/etc/shadow` 文件、使用 `usermod` 命令的 `-s` 选项或使用 `chsh` 命令。以下示例使用 `chsh` 命令将 `bobg` 的 shell 更改为 `/bin/false`：

```bash
[root@server1-#] chsh -s /bin/false bobg
Changing shell for bobg.
Warning: "/bin/false is not listed in /etc/shells
Shell changed.
[root@server1]#
```

## 删除账户

要删除账户，可以使用 `userdel` 命令并指定用户名。此方法会删除 `/etc/passwd` 和 `/etc/shadow` 中对应的账户条目。此外，可以使用 `userdel` 命令的 `-r` 选项删除用户的主目录及其所有内容。当用户账户被删除时，之前属于该用户的文件将变为 `root` 所有。任何未来赋予相同 UID 的用户账户将成为这些文件的所有者。

例如，假设用户 `bobg` 离开了公司。要删除 `bobg` 账户并显示其旧文件的所有权，可以使用以下命令：

```bash
[root@server1]# userdel bobg
[root@server1]# ls -la /home/bobg
total 52
drwx-------- 4 502 4096 Jul 17 15:37 .
drwx-xr-x 5 root 4096 Jul 17 18:56 .
-rw-r--r-- 1 502 24 Jul 17 15:37 .bash_logout
-rw-r--r-- 1 502 191 Jul 17 15:37 .bash_profile
-rw-r--r-- 1 502 124 Jul 17 15:37 .bashrc
-rw-r--r-- 1 502 5542 Jul 17 15:37 .canna
-rw-r--r-- 1 502 820 Jul 17 15:37 .emacs
-rw-r--r-- 1 502 118 Jul 17 15:37 .gtstrc
-rw-r--r-- 1 502 4096 Jul 17 15:37 .kde
drwx-xr-x 2 502 502 Jul 17 15:37 .xemas
-rw-r--r-- 1 502 3511 Jul 17 15:37 .zsh
```

从之前的输出可以看出，`bobg` 用户的 UID 是 502。假设公司雇佣了 Sue 来代替 `bobg`。此时你可以将 UID 502 分配给 Sue 的账户。虽然她会有自己的主目录，但 `/home/bobg` 中的所有 `bobg` 文件，她可以根据工作需要将需要的文件复制到自己的主目录，并删除不需要的文件。

要创建一个 UID 为 502 的用户并列出 `bobg` 主目录中的文件所有权，使用以下命令：
