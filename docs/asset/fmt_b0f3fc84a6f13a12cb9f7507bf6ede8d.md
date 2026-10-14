
```
root:x:0:Super-User::/sbin/sh
daemon:x:1:::/usr/sbin::
bin:x:2:::/usr/bin
sys:x:3::/
adm:x:4:Admin:/var/adm
lp:x:8:Line Printer:/usr/spool/lp
uucp:x:5:uucp Admin:/usr/lib/uucp
muuc:x:9:uucp Admin:/var/spool/uucpublic:/usr/lib/uucp/uucico
smsmp:x:25:SendMail Message Program::/
listen:x:37:Network Admin:/usr/net/nets
gdm:x:50:50:GDM:WebServer Reserved UID:
websrv:x:80:WebServer Reserved UID:
nbody:x:6001:6003:NFS Anonymous Access User:
noaccess:x:6002:6002:No Access User:
nbody4:x:65534:65534:SunOS 4.NFS Anonymous Access User:
```

| 图 6-1 | 用户名 | UID | 登录 shell |

|---|---|---|---|

| `/etc/passwd` 文件中对应用户账户的条目 | `jerry:x:107:111` | John Jerry:/export/home/jerry:/sbin/sh |

| 加密密码的占位符 | GID | 主目录 |

| 字段名称 | 描述 |

| --- | --- |

| `<username>` | 账户唯一用户名，也称为登录名。 |

| `<password>` | 该账户的用户密码。 |

| `<UID>` | 用户账户的唯一用户 ID 编号。每个账户有一个 UID。 |

| `<GID>` | 该账户所属组的唯一组 ID 编号。 |

| `<comment>` | 可选的信息性字段。通常你可以在这里输入任何信息；通常包含用户的全名。 |

| `<home directory>` | 用户账户的主目录。 |

| `<login shell>` | 用户的默认登录 shell，例如 `/bin/sh` 或 `/bin/csh`。 |

出于历史原因，`passwd` 文件中的 `comment` 字段也称为 GECOS 字段；它最初用于存储登录信息，以便向运行 Bell 实验室 UNIX 系统的 GECOS（通用电气计算机操作系统）大型机提交批作业。

默认的 `passwd` 文件包含标准进程（也称为 `daemon`）的条目，这些进程通常在启动时运行以执行打印、网络管理和端口监控等系统级任务。`passwd` 文件中的两个相邻的冒号 (`:`) 表示空字段。`shadow` 文件和 `group` 文件等其他文件也是如此。

如果用户的密码经过加密，`passwd` 文件中的条目仅包含一个 `x`。加密密码以及其他用户信息进入 `shadow` 文件，我们接下来检查。

## shadow 文件

`shadow` 文件包含有关密码的详细信息。`shadow` 文件中条目的语法与 `passwd` 文件相似，所示如下：

```
<username>:<password>:<lastch>:<min>:<max>:<warn>:<inactive>:<expire>
```

## 用户账户基础

### 图 6-2

| 字段 | 描述 |

| :--- | :--- |

| 两次密码更改之间的最小天数 | 在密码过期日期之前多少天用户会收到警告 |

| `/etc/shadow` 文件中对应于用户账户的条目 | 用户名 | `jkerry:86K/GMNT/DGU:9675:0:90:7:10:5905` | 账户过期日期 |

| 上次修改修改时间 | 用户被强制更改密码之前的最大天数 |

| 账户被锁定前可以非活动的天数 |

例如，图 6-2 解释了 `shadow` 文件中的一个条目。`shadow` 文件条目中的字段描述见表 6-4。请记住，`shadow` 文件只能由超级用户（例如 `root` 账户）查看。`/etc/passwd` 文件包含了大多数用户账户信息，包括密码的占位符，而详细的密码信息包含在 `/etc/shadow` 文件中。

### 表 6-4

| 字段名 | 描述 |

| :--- | :--- |

| `<username>` | 账户的唯一用户名，也称为登录名。 |

| `<password>` | 用户密码。可能包含以下内容之一：加密的用户密码（13 个字符）、表示该账户已锁定且无法访问的字符串 `*LK*`，或者表示此账户没有密码的字符串 `NP`。 |

| `<lastchg>` | 从 1970 年 1 月 1 日到上次修改密码的日期之间的天数。 |

| `<min>` | 两次连续密码更改之间的最小天数。 |

| `<warn>` | 在密码过期日期之前用户收到警告的天数。 |

| `<inactive>` | 用户账户在被锁定前可以非活动的天数。 |

| `<expire>` | 用户账户过期日期，之后用户将无法使用此账户登录系统。 |

## 组文件 (group)

多个用户可以组织成一个组以便以便管理。组文件中的条目包含有关组的信息。`/etc/group` 文件中条目的语法与 `/etc/passwd` 文件中的条目相似，如下所示：

```
<group name>:<group password>:<gid>:<user-list>
```

例如，图 6-3 显示了组文件条目中的一个示例。组文件条目中的字段描述见表 6-5。组密码字段通常不使用——即留空。这是 UNIX 早期的遗留。如果一个组有密码，`newgrp` 命令将提示用户输入密码。但请注意，没有设置组密码的实用程序。这里显示了 Solaris 10 系统创建的默认组文件。

### 表 6-5

| 字段名 | 描述 |

| :--- | :--- |

| `<group name>` | 分配给组的名称：最大长度为八个字符。 |

| `<group password>` | 可选字段，通常包含星号或留空。 |

| `<GID>` | 组 ID 号。 |

| `<user list>` | 该组成员的用户列表；任何两个成员之间用逗号分隔。 |

```
root::0:
other::1:
bin::2:root, daemon
sys::3:root, bin, adm
adm::4:root, daemon
uucp::5:root
mail::6:root
tty::7:root, adm
lp::8:root, adm
nucup::9:root
staff::10:
daemon::12:root
smsmp::25:
sysadmin::14:
gdm::50:
websrvd::8:
```

`root::0:`

`other::1:`

`bin::2:root, daemon`

`sys::3:root, bin, adm`

`adm::4:root, daemon`

`uucp::5:root`

`mail::6:root`

`tty::7:root, adm`

`lp::8:root, adm`

`nucup::9:root`

`staff::10:`

`daemon::12:root`

`smsmp::25:`

`sysadmin::14:`

`gdm::50:`

`websrvd::8:`

`<group name>:<group password>:<gid>:<user-list>`

`<group name>:<group password>:<gid>:<user-list>`

body:

-

games:

-

man:

-

websrvd:-

```

这里显示了组文件中的一个条目。`shadow` 文件条目中的字段包含在 `/etc/passwd` 文件中的条目。现在，`/etc/passwd` 文件中的条目显示了关于用户账户的信息。请记住，`shadow` 文件只能由超级用户（如 `root` 账户）查看。`/etc/passwd` 文件包含了大多数用户账户信息，包括密码的占位符，而详细的密码信息包含在 `/etc/shadow` 文件中。

现在，你已经了解了 `/etc/passwd` 文件的结构。现在，我们将使用命令行来管理账户。

## 管理账户

命令行提供了许多创建、修改和删除账户的命令。图形界面 (`GUI`) 也可以管理账户，但命令行提供了更强大的选项。命令行通常更具灵活性，而另一方面，`GUI` 则更简单，但提供了较少的选项。

### 命令行管理用户和组账户

命令行提供了许多创建、修改和删除账户的命令。在本节中我们将探索 `useradd` 命令。

### useradd 命令

你使用 `useradd` 命令创建账户。其语法如下：

```
useradd [-c comment] [-b basehome] [-d home] [-e expire] [-f inactive] [-g group] [-G group]]
```
