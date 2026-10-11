
表11-6 列出了 `useradd` 命令可用的一些选项及其描述。

# 表11-6 useradd 命令常用选项

| 选项 |  |
| :--- | :--- |
| `-c "description"` | 为 `/etc/passwd` 中的 GECOS 字段添加用户描述。 |
| `-d directory` | 指定家目录的绝对路径。 |
| `-e expiredate` | 指定禁用账户的日期。 |
| `-f days` | 指定密码过期后的天数。 |
| `-g group` | 指定账户的主组。在 Red Hat Linux 中，默认创建一个与用户同名的组作为该用户的主组。 |
| `-G group1,group2,etc.` | 指定账户的所有组成员身份。 |
| `-m` | 指定为用户账户创建家目录。在 Red Hat Linux 中，通过 `/etc/login.defs` 文件中的项为所有用户创建家目录。 |
| `-k directory` | 指定复制文件到新家目录时使用的骨架目录。 |
| `-s shell` | 指定账户使用的 shell 的绝对路径。 |
| `-u UID` | 指定账户的 UID |

# 表11-6 useradd 命令常用选项（续）

| 选项 | 描述 |
| :--- | :--- |
| `-u UID` | 指定账户的 UID |

在添加用户账户后，`/etc/shadow` 文件中的密码字段两个字符，表示未为账户设置密码。要设置密码，只需输入 `passwd` 命令，在提示符处输入新账户名称，然后提供相应的密码。为 `bobg` 用户设置密码的示例所示：

```
[root@server1 root]# passwd bobg

正在更改 bobg 的密码。

新 UNIX 密码：

输入新的 UNIX 密码：

passwd: 所有身份令牌已更新。

[server1 root]# _
```

> 不带参数，`passwd` 命令更改当前用户的密码。

+ 所有用户账户在登录系统之前必须设置密码。
+ `root` 用户可以使用 `passwd` 命令为任何用户账户设置密码；但普通用户只能使用此命令更改自己的密码。
+ 密码应该是难以猜测的，并包含大写、小写和特殊字符以增加系统安全性。良好的密码示例是 `C2jr;Pwr`。

# 修改用户账户

要在创建后修改用户账户的信息，可以编辑 `/passwd` 或 `/etc/shadow` 文件；但并不建议这样做，因为这些文件中的拼写错误可能会导致系统异常。可以使用 `usermod` 命令修改有关用户账户的大多数信息。例如，将用户 `bobg` 的登录名改为 `barbg`，可以使用 `usermod` 命令的 `-l` 选项：

```
[root@server1 root]# usermod -l barbg bobg

[root@server1 root]# _
```

# 第11章常见管理任务

表11-7 显示了用于 `usermod` 命令修改用户账户的完整选项列表。

| 选项 | 描述 |
| :--- | :--- |
| `-c "description"` | 为 `/etc/passwd` 中的 GECOS 字段指定用户的新描述。 |
| `-d homedirectory` | 指定新家目录的绝对路径。 |
| `-e expiredate` | 指定禁用账户登录的日期。 |
| `-f days` | 指定密码过期后账户禁用的天数。 |
| `-g group` | 为账户指定一个新的主组。 |
| `-G group1,group2, etc.` | 指定账户的所有组成员身份。 |
| `-l name` | 指定一个新的登录名。 |
| `-s shell` | 指定账户使用的新 shell 的绝对路径。 |
| `-u UID` | 为账户指定一个新的 UID |

`usermod` 命令无法修改的唯一用户账户信息是前面讨论的 `/etc/shadow` 中的密码过期信息（`min`、`max`、`warn`）。要更改这些信息，可以使用带有适当选项的 `change` 命令。例如，要指定用户 `bob` 在接收新密码后等待2天再更改密码，指定其密码在50天后过期并在过期前7天发出警告，可以使用 `change` 命令的以下选项：

```
[server1 root]# chage -m 2 -M 50 -W 7 bobg

[server1 root]# _
```

在某些情况下，可能临时防止用户登录；这通常被称为锁定账户。要锁定账户，可以在提示符处使用 `usermod -L username`。这会在 `/etc/shadow` 文件的加密密码字段开头放置 `!` 字符。要解锁账户，只需在提示符处输入 `usermod -U username`，这将移除 `/etc/shadow` 文件中密码字段的 `!` 字符。

或者，可以使用 `passwd -l username` 命令锁定用户账户，使用 `passwd -u username` 命令解锁账户。

另一种常用的锁定用户账户的方法是将 `/etc/passwd` 中为账户指定的 shell 从 `/bin/bash` 更改为无效 shell 如 `/bin/false`。没有有效的 shell，用户无法使用系统。要锁定账户，你可以编辑 `/etc/passwd` 文件并进行相应的更改、使用 `usermod` 命令的 `-s` 选项，或使用 `chsh` 命令。以下示例使用 `chsh` 命令将 `bobg` 的 shell 更改为 `/bin/false`：

## 管理用户和组 501

```
[root@server1]# chsh -s /bin/false bobg

Changing shell for bobg.

Warning: "/bin/false" is not listed in /etc/shells

Shell changed.

[root@server1]# _
```

## 删除用户账户

要删除用户账户，你可以使用 `userdel` 命令并将用户名作为参数；这将从 `/etc/passwd` 和 `/etc/shadow` 中移除对应用户账户的条目。此外，你可以为 `userdel` 命令指定 `-r` 选项，以删除该用户的家目录及其所有内容。

当用户账户被删除时，以前属于该用户的所有文件将归一个代表已删除用户 UID 的数字所有。任何未来获得相同 UID 的用户账户都将成为这些文件的所有者。

例如，假设用户 `bobg` 离开了公司。要删除 `bobg` 的账户并显示其旧文件的所有权，你可以使用以下命令：

```
[root@server1]# userdel bobg

[root@server1]# ls -la /home/bobg

total 52

drwx------- 4 502 502 4096 Jul 17 15:37 .

drwxr-xr-x 5 root 502 root 4096 Jul 17 15:37 .bash_logout

-rw-r--r-- 1 502 502 24 Jul 17 15:37 .bash_profile

-rw-r--r-- 1 502 502 191 Jul 17 15:37 .bashrc

-rw-r--r-- 1 502 502 124 Jul 17 15:37 .bash_history

-rw-r--r-- 1 502 502 5542 Jul 17 15:37 .emacs

-rw-r--r-- 1 502 502 832 Jul 17 15:37 .canna

-rw-r--r-- 1 502 502 118 Jul 17 15:37 .gtkrc

-rw-r--r 3 502 502 4096 Jul 17 15:37 .kde

drwxr-xr-x 2 502 502 4096 Jul 17 15:37 .x-enas

-rw-r--r-- 1 502 502 3511 Jul 17 15:37 .zshrc

[root@server1]# _
```

从上述输出中，你可以看到 `bobg` 用户的 UID 是 502。如果用户 `sueb` 加入公司，你可以将 UID 502 分配给她的用户账户，这样她就可以拥有 `bobg` 的所有旧文件并在需要时重新使用。

创建一个 UID 为 502 的用户 `sueb` 并列出 `bobg` 目录下文件的所有权，请使用以下命令：

```
[root@server1]# useradd -u 502 sueb

[root@server1]# ls -la /home/bobg

total 52

drwx------ 4 sueb sueb 4096 Jul 17 15:37 .

drwxr-xr-x 5 root root 4096 Jul 17 18:56 ..
```

## 第 11 章 常见管理任务

```
-rw-r--r--  1 sueb  sueb         24 Jul 15:37 .bash_logout

-rw-r--r--  1 sueb  sueb         191 Jul 15:37 .bash_profile

-rw-r--r--  1 sueb  sueb         124 Jul 15:37 .bashrc
```
