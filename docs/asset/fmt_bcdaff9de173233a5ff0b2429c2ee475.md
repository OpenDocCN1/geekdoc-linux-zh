
## Plan

I will be on vacation Oct 16-17, 2000.

以下是不带参数的 `finger` 命令，显示每个当前登录用户的行：

```
finger
```

| | Tty | Idle | Login Time | Where |
|---|---|---|---|---|
| beltran | Rene Beltran | *p0 | 4:44 | Mon Sep 20 15:39 | 10.1.1.101 |
| dbhelp | dbhelp System | *p20 | 7:42 | Mon Sep 20 12:53 |
| ingrid | Ingrid Van Zalingen | *p2 | 9:54 | Mon Sep 20 07:10 | iv |
| mori | Steve Moritsugu | *p1 | 1 | Mon Sep 20 08:35 |
| mori | Steve Moritsugu | *p14 | 8 | Mon Sep 20 08:59 |

# 第三部分 关于 UNIX 密码文件的信息显示

## 第三章

| 用户 | 信息 |
| :--- | :--- |
| Sloan Bill Sloan |
| stall Michael Stall |
| stall Michael Stall |
| stall Michael Stall |
| stall Michael Stall |

## 关于 UNIX 密码文件的信息显示

与大多数安全系统一样，UNIX 不仅要求用户在系统中注册，还要求通过提供用户 ID（UID）和密码来验证登录。尽管如此，这并非万无一失，因为用户有时会与他人共享密码，或者有人使用他人的密码。

首先，查看 UNIX 密码文件 (`passwd`)。以下是位于 `/etc` 目录下的密码文件示例：

```
root:Thisisasecret:0:3::/sbin/sh

deamon*:1:5::/sbin/sh

bin*:2:2:/usr/bin/sbin/sh

sys*:3:3::

adm*:4:4:/var/adm:/sbin/sh

uuuc*:5:3:/var/spool/uucpublic:/usr/lib/uucp

lp*:9:7:/var/spool/lp:/sbin/sh

nuuc*:11:11:/var/spool/uucpublic:/usr/lib/uucp

hdpdb*:20:1:ALBASE::/sbin/sh

nobody*:2:-24::/

oracle:BJXXXXTHWSLI:201:200,,,/home/usr/bin/sh

clfiss:XXXXXXX:102:200,,,/home/cfiss:/usr/bin/sh

dwilson:Can'tguessme!:101:200:DanWilson,Indy,_317.555.555,/home/dwilson:/usr-/bin/sh
```

`passwd` 文件中的每一行都标识系统中的单个用户。每个字段由冒号 (`:`) 分隔。你可以按照如下方式拆解每个条目：

- 登录名称
- 加密密码
- 数字用户标识
- 数字组标识
- 用户信息字段
- 用户家目录
- 登录时使用的使用的 Shell 程序

在上述的 `passwd` 示例中，你会注意到某些账户的加密密码字段中有一个星号 (`*`)。这指示操作系统防止任何人直接登录这些账户。

注意 `root` (`userid 0`) 账户。该账户是超级用户账户。登录此账户的人通常是系统管理员，因为该账户允许他们执行系统中的任何命令，并启动和关闭机器。

再看一眼 `nobody` 账户。注意它的用户 ID 为 -2。该账户预留用于远程访问，特别是 NFS。NFS 是一种网络文件系统，允许你将目录（通过远程文件系统）挂载到你的宿主机上。

大多数版本的 UNIX 都支持影子密码 (`shadow passwords`)。正如你在 `passwd` 文件示例中所注意到的，你可以看到每个设置了密码的用户加密密码（虽然没有密码的账户上是可能的，但这是不可接受的）。这在某种程度上是一个安全问题，因为用户可以使用这些信息来破解其他用户的密码。为了防止这种情况，UNIX 供应商开始实施影子密码系统。该系统将加密密码信息放在另一个目录的特殊影子密码文件中，该目录只有特权用户才能访问。某些系统拥有 `/etc/shadow` 文件，只有特权用户可以访问。无论哪种方式，目标都是防止普通用户读取加密密码。

## 修改你的密码

现在是查看如何使用 `passwd` 命令更改密码的好时机。

### 如果你忘记了密码

即使是系统管理员 (`root`) 也无法查询某人的密码，因为密码在保存之前已经过加密。当你输入密码时，系统通过首先对其进行加密并与保存的加密密码进行比较来验证。因此，系统不需要知道你的实际密码，只需要你的加密密码。如果你忘记了密码，系统管理员可以为你重置。

在提示符下输入 `passwd`：

```
$ passwd
Old password:
New password:
Retype new password:
```

`passwd` 命令可以交互式地让你更改密码。

## 组

![](img/groups)

另一个值得关注的文件是 `group`。它位于 `/etc` 目录，列出了系统中所有的组。你可以查看组的组成：

```
root:x:0:
bin:x:1:
sys:x:3:
adm:x:4:
uuuc:x:5:
lp:x:9
nuuc:x:11:
hdpdb:x:20:
nobody:x:-24:
oracle:x:200:
clfiss:x:102:
dwilson:x:101
```

`group` 文件中的每一行都标识一个组。每个字段由冒号 (`:`) 分隔：

- 组名
- 密码文件标识（通常为 `x`）
- 组 ID (`GID`)
- 用户列表

你可以使用 `groups` 命令查看当前用户所属的组：

```
$ groups
user group
```

## 进程显示

![](img/processes)

`ps` 命令用于显示当前运行的进程。常用的用法 `ps` 只显示当前终端运行的进程：

```
$ ps
PID TTY          STIME TIME CMD
1234 pts/0    10:00 0:00:00 bash
```

使用 `-ef` 参数可以显示更详细的信息：

```bash
$ ps -ef
UID        PPID    PID TTY START     TIME CMD
root         1      0 ?        Oct24   0:00:02 [kthreadd]
root         1    1000 ?        Oct24   0:00:00 /sbin/init
user       1234   5678 pts/0    10:00   0:00:00 bash
user       5678   9012 pts/0    10:05   0:00:00 top
```

`top` 命令提供了实时更新的系统状态信息：

```
top - 10:10:05 up 1 day,  2:30,  1 user,  0 min,  98 idle, load average: 0.01, 0.05, 0.10
Tasks: 150 total,   1 running, 149 sleeping,   0 zombie,   0 stopped,   0 wait
Cpu(s):  5.0%us,  2.0%sy,  0.0%ni, 93.0%id, 0.0%wa, 0.0%hi
Mem:      8192.0 total,   2000.0 free,   4000.0 used,   2000.0 buff/cache
MiB0.0 Swap:      2048.0 total,   2048.0 free,            0.0 used
```
