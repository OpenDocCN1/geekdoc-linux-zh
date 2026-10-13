
`irc:x:56:56:irc:/root:/sbin/nologin`

`messagebus:x:57:57:messagebus:/var/cache/dbus:/sbin/nologin`

`mj:x:1000:1000:mj:/home/mj:/bin/bash`

## /etc/group 文件

`/etc/group` 文件包含关于组的信息。每行包含组名、密码字段（通常为 `x`）、组 ID（GID）以及该组成员的用户列表。要创建新组，可以使用 `groupadd` 命令。要将用户添加到组中，可以使用 `usermod` 命令。要将用户从组中移除，可以使用 `gpasswd` 命令。

## 用户账户管理

表 6-2 `/etc/group` 结构

| 字段 | 示例 | 说明 |
| --- | --- | --- |
| 组名 | reviewers | 每个用户都有自己的主组，其组名与其用户名相同。你也可以创建辅助组。 |
| 组密码 | x | 密码。你看到一个 `x`，它指向 `/etc/shadow` 以获取实际密码。 |
| 组 ID (GID) | 2000 | 与组关联的数字 GID。默认情况下，RHEL 会为每个新用户创建一个组。如果你想创建一个辅助组，应该在标准范围之外分配 GID；否则，Red Hat 的 UID 和 GID 将会不同步。 |
| 组成员 | mj,ao | 列出该组成员的用户名。如果某个用户名在 `/etc/passwd` 中将该组的 GID 列为其主组，那么该用户名也是该组的成员。 |

以及周围（此处省略部分内容）。你将看到相同模式的信息，从 `root` 管理用户开始。图 6-3 显示了 `/etc/shadow` 文件的片段。

如表 6-3 所示，`/etc/shadow` 在第二列包含了加密后的密码，其余信息与密码管理方式有关。第二列的前两个字符指定了密码的加密哈希。如果你看到 `$1`，则密码使用消息摘要 5 (MD5) 算法进行哈希，这是 RHEL 5 之前的标准。如果你看到 `$6`，则密码使用 512 位安全哈希算法 (SHA-512) 保护，这是自 RHEL 6 以来的标准。

图 6-3 `/etc/shadow` 文件

```
root1:~cat /etc/shadow

root:*:99999:0:::6$Y9mD.nyjZnPtNofia6Iz6vCq09HD51..j3KGnNpOqX0q13n1XkgpyV4qtublv2pkScmk6kdue7eA

elson:*:99999:0:::

david:*:99999:0:::

adm:*:99999:0:::

imp:*:99999:0:::

sync:*:99999:0:::

shutdown:*:99999:0:::

halt:*:99999:0:::

mail:*:99999:0:::

operator:*:99999:0:::

games:*:99999:0:::

ftp:*:99999:0:::

nnbody:*:99999:0:::

dbd:18223:::::

system-coredum:18223:::::

tss:18223:::::

poldi:18223:::::

geclus:18223:::::

rtkit:18223:::::

pulse:18223:::::

emeu:18223:::::

ubound:18223:::::

unbound:18223:::::

frpc:18223:::::

gluster:18223:::::

chrony:18223:::::
```

## 第 6 章 用户管理

表 6-3 `/etc/shadow` 结构

| 列 | 字段 | get |
| --- | --- | --- |
| 1 | 用户名 | 用户名 |
| 2 | 密码 | 加密密码；要求 `/etc/passwd` 的第二列中为 `x` |
| 3 | 上次修改密码日期 | 上次修改密码的日期，自 1970 年 1 月 1 日起的天数 |
| 4 | 密码最小年龄 | 用户在更改密码之前保持密码的最少天数 |
| 5 | 密码最大年龄 | 密码必须更改的最少天数 |
| 6 | 密码警告期 | 密码过期前发出警告的天数 |
| 7 | 密码空闲期 | 过期后仍接受密码的持续数，但期间会提示用户更改密码 |
| 8 | 账户过期日期 | 自 1970 年 1 月 1 日起密码过期的天数 |
| 9 | 预留 | 预留供以后使用 |

注意图 6-3 中的某些用户在密码字段中有 `*` 或 `!!` 字符。这意味着该用户将无法使用密码登录。这是系统账户的标准配置。

## /etc/gshadow 文件

`/etc/gshadow` 文件是影子密码套件中的组配置文件。它包含了组管理员，管理员可以使用 `gpasswd` 命令添加其他组成员。如果你可以配置哈希密码，一旦设置了密码，组管理员就可以使用 `gpasswd` 命令并输入所需的密码从组中添加或删除成员。图 6-4 显示了 `/etc/gshadow` 文件的片段。例如，该行定义的组四个字段，如表 6-4 所示：

`reviewers:!mj:mj,ao,sd`

（此处接图 6-4）

## 用户账户管理

图 6-4

`/etc/gshadow` 文件

```
[root@server1 ~]# cat /etc/gshadow

root::

bin::

damon::

sys::

ade::

tty::

disk::

p::

mem::

kmem::

wheel::alex

cdrom::\mail::

dialout::

floppy::

games::

tape::

video::

ftp::

lock::

audio::

users::

dbus::

utmp::

utemp::

input::
```

表 6-4 `/etc/gshadow` 结构

| 字段 | 示例 | 说明 |
| --- | --- | --- |
| 组名 | reviewers | 组名。 |
| 密码 | ! | 某些组有哈希密码。 |
| 管理员 | mj | 使用 `gpasswd` 命令更改组的用户。 |
| 组成员 | mj,ao,sd | 组成员用户名列表。 |

如果你不记得本节描述文件的含义，请打开相应的手册。注意 `man passwd` 显示的是 `passwd` 命令的手页，而 `man 5 passwd` 是查看 `/etc/passwd` 文件的正确命令。

## /etc/login.defs 文件

`/etc/login.defs` 文件提供了影子套件中某些参数的基准。这些设置仅对新用户有效。

## 第 6 章 用户管理

老化 配置

| 参数 | 说明 |
| --- | --- |
| `PASS_MAX_DAYS` | 必须更改的天数 |
| `PASS_MIN_DAYS` | 用户在更改密码之前保持密码的最少天数 |
| `PASS_WARN_DAYS` | 密码过期前发出警告的天数 |
| `MAIL_DIR` | 邮件箱所在的目录。 |
| `UMASK` | 普通用户的默认 `umask`。 |
| `CREATE_HOME` | `useradd` 是否创建家目录 |
| `USERGROUPS_ENAB` | 是否为每个新用户创建一个组 |
| `ENCRYPT_METHOD` | 用于加密密码的算法 |
| `SYS_UID_Min` | 系统账户的最小 UID |
| `SYS_UID_Max` | 系统账户的最大 UID |
| `SYS_GID_Min` | 系统账户的最小 GID |
| `SYS_GID_Max` | 系统账户的最大 GID |

## 用户账户管理

命令行工具

通过命令行界面添加用户有两种种方法。作为 `root` 用户，你可以直接编辑 `/etc/passwd` 文件来添加用户。或者，你可以使用为此目的定制的工具。

### 直接添加用户

在你喜欢的编辑器中打开 `/etc/passwd` 文件。如第 2 章所述，你可以通过 `vipw` 命令执行。然而，如果你直接编辑影子套件的文件添加用户，你需要做两件事：

- 添加用户家目录。
- 填充用户家目录。

### 直接将用户添加到组

每个 Linux 用户都分配给一个组，至少是自己的私有组。`/etc/group` 文件中列出的用户主组 GID 必须与 `/etc/passwd` 中显示的该 GID 匹配。该用户通常是该组的唯一成员。

## 第 6 章 用户管理

当然，用户也可以是其他组的成员。例如，为了创建一个名为 `project` 的组，你可以将条目添加到 `/etc/group` 和 `/etc/gshadow` 文件中。在文本编辑器中执行此操作的一种方法是使用 `vi` 命令。作为一个例如，以下条目对于名为 `project` 的组来说可能是合适的：

```
project:x:6001:
```
