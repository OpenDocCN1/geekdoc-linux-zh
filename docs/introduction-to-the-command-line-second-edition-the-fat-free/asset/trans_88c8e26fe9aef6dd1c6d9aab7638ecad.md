

## sudo

用途：以不同用户的身份运行单个命令。

用法语法：`sudo [OPTIONS] [COMMAND]`

```bash
$ whoami
nick
$ sudo whoami
[sudo] password for nick: ******
root
$ whoami
nick
```
使用 sudo 以 root 用户身份运行命令

`sudo` 命令允许你以另一个用户的身份运行单个命令。它最常用于执行需要 root 权限的命令。在此示例中，通过 `sudo` 命令以 root 身份执行了 `whoami`。

使用 `sudo` 命令是运行需要提升权限的命令的推荐方式，因为它限制了使用 root 权限的时间。这极大地有助于防止意外删除重要系统文件等灾难。

> **注意**：用户（或组）账户必须列在 `/etc/sudoers` 文件中，才能使用 `sudo` 以 root 身份执行命令。

常见用法示例：
- `sudo [COMMAND]`：以 root 身份运行指定的命令
- `sudo -u [USER] [COMMAND]`：以指定的用户身份运行命令
- `sudo !!`：以 root 身份运行上一条命令

## id

**用途**：显示用户身份的信息。

**用法语法**：`id [OPTIONS] [USER]`

```bash
# id
uid=0 (root) gid=0 (root) groups=0 (root)
```
显示当前用户的用户和组信息

`id` 命令显示指定用户的用户和组信息。不带选项执行 `id` 会显示当前用户的信息，如上述示例所示。下一个示例演示了使用 `id` 命令显示特定用户的信息。

```bash
# id nick
uid=1000 (nick) gid=1000 (nick) groups=4 (adm), 20 (dialout), 24 (cdrom), 46 (plugdev), 106 (lpadmin), 121 (admin), 122 (sambashare), 1000 (nick)
```
显示特定用户的用户和组信息

> **注意**
> 
> **Unix、Linux 和 BSD** 系统为系统中的每个用户和组分配一个数字 UID（**用户 ID**）和 GID（**组 ID**）。还会为每个 UID 和 GID 分配一个用户友好的名称，该名称显示在每个 ID 号码旁边的括号中。用户的此信息存储在 `/etc/passwd` 中，组的信息存储在 `/etc/group` 中。

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `id` | 显示当前用户的 ID 信息 |
| `id [USER]` | 显示指定用户的用户和组信息 |

## groups

**用途**：显示用户所属的组。

**用法语法**：`groups [OPTIONS] [USER]`

```bash
# groups
root
```
显示当前用户的组信息

`groups` 命令显示用户的组成员资格。不带选项执行 `groups` 会显示当前用户的组，如上述示例所示。可以使用用户名配合 `groups` 命令来显示指定用户的组成员资格，如下一个示例所示。

```bash
# groups nick
nick adm dialout cdrom plugdev lpadmin admin sambashare
```
显示指定用户的组信息

**常见用法示例**：

| 命令 | 描述 |
| :--- | :--- |
| `groups` | 显示当前用户的组成员资格 |
| `groups [USER]` | 显示指定用户的组成员资格 |

## who / whoami

**用途**：显示谁登录到系统中。

**用法语法**：`who [OPTIONS]`

```bash
$ who
root  tty2  2010-05-17 11:32
nick  tty1  2010-05-17 11:31
nick  pts/0 2010-05-17 08:40 (10.10.1.251)
dave  pts/1 2010-05-17 12:32 (10.10.1.188)
mike  pts/2 2010-05-17 14:28 (10.10.1.167)
lisa  pts/3 2010-05-17 14:50 (10.10.1.204)
nick  pts/4 2010-05-17 15:33 (10.10.1.251)
```
who 命令的输出

`who` 命令显示当前登录到系统的用户信息。`who` 命令的默认输出显示用户名、终端 ID 以及用户登录的日期/时间，如上述示例所示。

> **注意**：通过 telnet 或 SSH 会话登录的用户也会显示远程客户端的 IP 地址，位于括号内。

`whoami` 命令显示当前用户的用户名。这在切换不同账户时验证当前可用的用户环境和安全权限时很有用。

**用法语法**：`whoami`

```bash
$ whoami
nick
```
使用 whoami 显示当前用户的名称

常见用法示例：
- `who`：显示当前登录到系统的用户
- `who -b`：显示最后一次系统启动时间
- `who -r`：显示当前运行级别
- `whoami`：显示当前用户的名称

## w

用途：显示登录到系统的用户的详细信息。

**用法语法**：`w [OPTIONS] [USER]`

```bash
$ w  
15:39:12 up 4 days, 6:09, 5 users, load average: 0.06, 0.05, 0.01
```

| USER | TTY | FROM | LOGIN | IDLE | JCPU | PCPU | WHAT |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| nick | pts/0 | 10.10.1.251 | 08:40 | 1:10 | 0.18s | 0.15s | -bash |
| dave | pts/1 | 10.10.1.188 | 12:32 | 0.00s | 0.14s | 0.14s | vim |
| mike | pts/2 | 10.10.1.167 | 14:28 | 0.00s | 0.12s | 0.12s | tail |
| lisa | pts/3 | 10.10.1.204 | 14:50 | 9.00s | 0.14s | 0.14s | -bash |
| nick | pts/4 | 10.10.1.251 | 15:33 | 0.00s | 0.15s | 0.01s | w |

`w` 命令的输出

`w` 命令显示登录到系统的用户的详细信息。它与之前讨论的 `who` 命令类似，但提供了额外的信息，如用户最后登录时间、空闲时长以及当前正在运行的程序。

`w` 命令还显示一行系统摘要，显示主机正常运行时间、连接用户数以及过去 1、5 和 15 分钟的系统负载平均值样本。

> 第一行显示的信息与 `uptime` 命令生成的输出相同。有关系统正常运行时间和负载平均值的更多信息，请参见第 215 页。

**常见用法示例**：

- `w`：显示当前登录到系统的用户的详细信息

## last / lastb

用途：显示上次成功/失败的用户登录记录。

**用法语法**：`last [OPTIONS] [USER]`

```bash
$ last
nick    pts/1      192.168.1.50   Sat May 22 13:42   still logged in
nick    pts/0      192.168.1.50   Sat May 22 13:42   still logged in
nick    tty7        :0            Sat May 22 13:40   still logged in
reboot  system boot  2.6.32-21-ge  Sat May 22 13:40 -  14:02  (00:21)
nick    pts/0      :0.0          Thu May 20 21:33 -  21:56  (00:03)
nick    pts/0      :0.0          Thu May 20 21:30 -  21:33  (00:02)
root    pts/0      :0.0          Thu May 20 21:27 -  21:30  (00:03)
nick    tty7        :0          Thu May 20 21:25 - crash (1+16:14)
...
```
last 命令的输出

`last` 命令显示系统中每个用户的登录和注销时间。它还显示有关系统关闭和重启的信息，如上述示例所示。

`lastb` 命令显示失败的登录尝试，如下一个示例所示。

**用法语法**：`lastb [OPTIONS] [USER]`

```bash
$ lastb
nick    tty1       Sat May 22 13:59 -  13:59  (00:00)
nick    tty1       Thu May 20 21:27 -  21:27  (00:00)
root    tty1       Thu May 20 15:27 -  15:27  (00:00)

btmp begins Sat May 20 13:59:28 2010
```
lastb 命令的输出

> **注意**：用户登录/注销活动存储在 `/var/log/wtmp` 文件中。失败的登录尝试记录在 `/var/log/btmp` 中。

常见用法示例：
- `last`：显示最后一次用户登录信息
- `last -[NUMBER]`：显示指定数量的登录记录
- `last [USER]`：显示指定用户的最后登录记录
- `lastb`：显示失败的登录尝试
- `lastb -[NUMBER]`：显示指定数量的失败登录尝试
- `lastb [USER]`：显示指定用户的失败登录尝试

## lastlog

用途：显示最近的用户登录信息。

用法语法：`lastlog [OPTIONS]`

```bash
$ lastlog | more
Username Port From Latest
root tty2 Sat May 30 11:32:33 -0500 2009
dave tty3 Sat May 30 10:22:51 -0500 2009
nick pts/0 10.10.1.251 Sat May 30 11:31:51 -0500 2009
steve **Never logged in**
bin **Never logged in**
sync **Never logged in**
lp **Never logged in**
...
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_96_0.png)

`lastlog` 命令显示系统中每个用户的最近一次用户登录时间和日期。不带选项执行 `lastlog` 会显示所有用户的最后登录信息，如上述示例所示。此输出类似于 `last` 命令，但 `lastlog` 仅显示最新的登录活动，而 `last` 显示所有可用的登录事件。

可以使用 `-u` 选项来显示特定用户的最后登录，如下一个示例所示。

```bash
$ lastlog -u nick
Username Port From Latest
nick pts/0 10.10.1.251 Sat May 30 11:31:51 -0500 2009
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_96_1.png)

常见用法示例：
- `lastlog`：显示所有用户的最后登录信息
- `lastlog -u [USER]`：显示指定用户的最后登录信息

