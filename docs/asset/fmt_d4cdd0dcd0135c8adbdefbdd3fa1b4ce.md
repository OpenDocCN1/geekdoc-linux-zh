
`openvpn:x:986:986:/etc/openvpn`

`radvs:x:75:75:/var/run`

`lusync:x:975:975:/shutdown`

`abrt:x:173:173:/etc`

`pipewire:x:982:980:/var/run`

`dm:x:42:42:/var/lib`

`grpc:x:29:29:/var/nfs`

`user:x:1000:1000:Jason Eckert:/home:/bin/zsh`

`[root@server1]#`

```
root 用户通常列在 /etc/passwd 文件的顶部，如所示，守护进程登录的用户账户以及普通用户账户。输出的最后一行表示该用户 UID 为 1000，主 GID 为 0，GECOS 为 "Jason Eckert"，主目录为 /home，且使用 zsh shell。
```

## 第 10 章 常见管理任务 111

```
dbus::!!17646:::::

pulse::!!17646:::::

chrony::!!17646:::::

dnsmasq::!!17646:::::

rpc::!!17646:0:99999:7:::

usbmxd::!!17646:::::

openvpn::!!17646:::::

radvd::!!17646:::::

sasluth::!!17646:::::

abrt::!!17646:::::

pipeworker::!!17646:::::

gdm::!!17646:::::

rpcuser::!!17646:::::

user1=$6QY.IZYvu0.GV2kgYQbMca0TDWNF5Aefaa9.2WBKnbm2pofKZZeARUvuzZTJ.

UycrcQVvVIKy7=HaSlgY2ar2vX8Upml.1721:0:99999:7::

[rootserver]# 
```

注意：输出显示，大多数用户不会接收到加密密码。
虽然每个用户必须在 `/etc/passwd` 文件中列出一个组，但每个用户可以是多个组的成员。所有组及其成员都列在 `/etc/group` 文件中。`/etc/group` 文件具有由冒号分隔的字段：

`name:password:GID:members`
第一个字段是组名，随后是组密码。

注意 18
`/etc/passwd` 文件中的密码字段通常包含一个 `x`，因为很少使用组密码。如果你的系统使用了组密码，则你需要使用本章讨论的 `newgrp` 命令指定密码来更改你的主组成员身份。这些密码存储在 `/etc/shadow` 文件中以增加安全性。请设置 `passwd` 命令或管理页面以获取更多信息。

GID 代表该组的唯一组 ID（Group ID），members 字段表示组员列表。
`[root@server ~]# cat /etc/group`

```
root:x:0:

bin:x:1:root,bin

daemon:x:2:

sys:x:3:

adm:x:4:

tty:x:5:

tty:x:6:

disk:x:7:

lp:x:8:

mem:x:9:

wheel:x:10:user1

user1

cdrom:x:11:

mail:x:12:

man:x:15:

dialout:x:18:
```

```
floppy:x:19:

games:x:20:

tape:x:33:

video:x:39:

ftp:x:54:

lock:x:63:

audio:x:100:

users:x:100:

nobody:x:65536:

utmp:x:22:

apache:x:48:

ssh_keys:x:999:

input:x:998:

kvm:x:36qemu

render:x:997:

dbus:x:81:

dip:x:40:

pulse:x:171:

avah:x:70:

chrony:x:988:

slasauth:x:76:

abrt:x:173:

pipewire:x:980:

gdm:x:42:

rpcuser:x:29:

sshd:x:74:

slocate:x:21:

user1:x:1000:

[root@server1]#
```

根据前面的输出，“bin” 组的 GID 为 1，有三个用户作为成员：root、bin 和 daemon。同样，wheel 组的 GID 为 10，user1 是其中的成员。

> 注意 19
> wheel 组是一个特殊组，它为成员提供了运行 `su` 和 `sudo` 命令的能力，因为第一个创建 Linux 安装的用户会被添加到 wheel 组中，以允许他们使用 `sudo` 命令设置 root 密码。某些 Linux 发行版（包括 Ubuntu）使用 `sudo` 组来代替 `wheel` 组。

> 注意 20
> 你可以使用 `getent` 命令查看系统数据库中的记录，例如 `/etc/passwd`、`/etc/shadow`、`/etc/group` 和 `/etc/shadow`；例如，`getent shadow` 将显示 shadow 数据库（`/etc/shadow`）中的记录。

## 创建用户账户

你可以使用 `useradd` 命令在 Linux 系统上创建用户账户，并将用户名作为参数，如下：

```
[root@server1]# useradd binigir

[root@server1]#
```

## 第 10 章 常见管理任务 413

在这种情况下，所有其他信息（如 UID、shell 和家目录）都从两个文件 `/etc/login.defs` 获取，该文件包含了账户创建的默认值。

第一个文件 `/etc/login.defs` 包含设置默认邮件位置、密码过期信息、最小密码长度以及可用的 UID 和 GID 范围的参数。此外，它还决定了在创建用户时是否会自动创建家目录，以及用于在 `/etc/shadow` 中对密码进行加密的算法。如下所示 `/etc/login.defs` 文件的示例：

```
[root@server1]# useradd binigir

[root@server1]#
```

## 修改用户账户

在创建用户账户后，要修改有关用户账户的信息，可以编辑 `/etc/passwd` 或 `/etc/shadow` 文件。不建议这样做，因为这些文件中的拼写错误可能会导致系统无法运行。相反，最好使用 `usermod` 命令，你可以用它修改更多关于用户账户的信息。例如，要更改用户 `binig` 的登录名，可以使用 `usermod` 命令的 `-l` 选项：

```
[root@server1 ~]# usermod -l barig binig

[root@server1 ~]#
```

表 10-7 显示了用于修改账户的 `usermod` 命令选项列表。

| 选项 | 描述 |
| --- | --- |
| -a | 与 -o 使用，向用户已所属的组列表添加其他组成员 |
| -c "description" | 在 `/etc/passwd` 的 GECOS 字段中为用户指定新描述 |
| -d directory | 指定新家目录的绝对路径 |
| -e expiredate | 指定禁用账户登录的日期 |
| -f days | 指定密码过期的用户账户被禁用的天数 |
| -g group | 为用户账户指定新组 |
| -G group1,group2,... | 为用户账户指定主组以外的所有组成员 |
| -l name | 指定新的登录名 |
| -s shell | 为用户账户指定新 shell 的绝对路径 |
| -u UID | 为用户账户指定新的 UID |

**表 10-7** `usermod` 命令的常用选项

> 注意 25
> 如果安装了 `finger` 命令，可以使用它查看用户信息。这些信息存储在 `/etc/passwd` 的 GECOS 字段中。因此，通过 `usermod` 命令的 `-c` 选项，用户可以使用 `chfn` 命令更改他们自己的 GECOS 或 `finger` 信息。

> 注意 26
> 你也可以使用 `change` 命令查看密码过期信息。例如，`change -l binig` 显示用户 `binig` 的密码过期信息。

`usermod` 命令无法修改的唯一用户账户信息是存储在 `/etc/shadow` 中的密码过期时间（min, max, warn），这些在之前已讨论过。要更改这些信息，你可以使用带有适当选项的 `change` 命令。例如，要指定用户 `binig` 在收到新密码后必须等待 2 天才能更改密码，并指定其密码每 50 天过期一次，过期前 7 天预警，你可以使用 `change` 命令的以下选项：

```
[root@server1 ~]# change -m 2 -M 50 -W 7 binig

[root@server1 ~]#
```

## 第 10 章常见管理任务

有时有必要通过锁定账户来临时防止用户登录。要锁定一个账户，你可以在提示符处使用 `usermod -l username`。这会在 `/etc/shadow` 文件中的加密密码开头处放置一个 `!`。要解锁，在提示符处输入 `usermod -U username`，这会从 `/etc/shadow` 字段中移除 `!` 字符。

或者，你可以使用 `passwd -l username` 命令锁定用户账户，并使用 `passwd -u username` 命令解锁用户账户。这些命令分别在 `/etc/shadow` 文件的加密密码开头处放置和移除 `!` 字符。

另一种锁定账户的方法是将 `/etc/passwd` 中用户账户指定的 shell 从 `/bin/bash` 更改为无效 shell，如 `/bin/false` 或 `/bin/nologin`。如果没有有效的 shell，用户无法登录。你可以编辑 `/etc/passwd` 文件，或使用 `usermod` 命令的 `-s` 选项或 `chsh` 命令（在第 7 章讨论）将 shell 更改为非交互程序。

以下示例使用 `chsh` 将用户的 shell 更改为 `/bin/false`：

```
[server1 ~]# chsh -s /bin/false binig

Changing shell for binig.

sh: Warning: /bin/false is not listed in /etc/shells

Changed.

[server1 ~]#
```

## 删除用户账户

要删除用户账户，可以使用 `userdel` 命令并将用户名作为参数。这会从 `/etc/passwd` 和 `/etc/shadow` 文件中删除与用户账户对应的条目。此外，你可以指定 `userdel` 命令的 `-r` 选项来删除用户及其所有内容。当账户被删除时，之前由用户拥有的文件将由替换删除用户的数字所有。未来的任何账户都将使用与删除的相同的 UID。例如，假设用户 `bin` 离开公司。要删除 `bin` 并显示其旧文件的所有权，你可以使用以下命令：

```
[server1 ~]# userdel bin

[server1 ~]# ls -la /home/bin

total 52

drw-xr-x 4 1002 root 4096 Aug 27 15:37 .bash_logout

drw-xr-x 5 root 4096 Aug 27 15:37 .bash_profile

-rw-r--r-- 1 1002 root 191 Aug 27 15:37 .profile

-rw-r--r-- 1 1002 root ...（此处省略部分内容，格式与原文保持一致）
```

# 第 10 章 常见管理任务

要将组临时更改为 `groups` 和 `id` 命令输出列出的其他组，你可以使用 `newgrp` 命令。新创建的文件将具有新的组所有。以下输出演示了更改 root 用户的主组如何影响文件：

```
[root@server1] # newgrp sys

[root@server1] # id

uid=0(root) gid=3(sys)

groups=(root), 1(bin), 2(daemon), 3(sys), 4(adm), 6(disk), 10(wheel)

[root@server1] # touch samplefile

[root@server1] # ls -l samplefile

-rw-r--r-- 1 root  sys    Aug 27 19:28 samplefile

[root@server1] ~#
```
