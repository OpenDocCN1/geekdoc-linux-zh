
```
# cat interrupts
0: 27222899 timer
1: 3152 keyboard
2: 0 cascade
9: 450448 eth0
12: 4477 PS/2 Mouse
13: 1 math error
14: 15196 8 ide0
15: 0 + ide1
```

左侧列中的每个数字代表一个正在使用的中断。动态检查 `proc` 文件的内容会生成相关数据并将其显示在屏幕上。`/proc` 文件系统的部分是只读的；但某些文件允许更改内核变量。这提供了一种在无需重新编译和重启的情况下实际调整内核的机制。

`procinfo` 工具将 `/proc` 文件系统信息汇总为如下所示的显示：

```
# /usr/bin/procinfo
```

Linux 2.0.35 (root@buildmeister.caldera.com) (gcc 2.7.2.3) #1 [train2]

| Memory | Total | Used | Free | Shared | Buffers | Cached |
|---|---|---|---|---|---|---|
| Mem | 30884 | 20332 | 10552 | 10840 | 8900 | 5292 |
| Swap | 0 | 0 | 0 | 0 | 0 | 0 |

`/proc` 目录下的文件与进程 ID 子目录非常相似。例如，查看 `/proc/interrupts` 文件的内容会显示如下所示：

```
# cat interrupts
0: 27222899 timer
1: 3152 keyboard
2: 0 cascade
9: 450448 eth0
12: 4477 PS/2 Mouse
13: 1 math error
14: 15196 8 ide0
15: 0 + ide1
```

# 第 9 章 理解 LINUX 文件系统

```
-r--r--r-- root      @ Dec 6 01:13 mdstat
-r--r--r-- root      @ Dec 6 01:13 meminfo
-r--r--r-- root      @ Dec 6 01:13 modules
-r--r--r-- root      @ Dec 6 01:13 mounts
-dr-xr-x root      @ Dec 6 01:13 net
-r--r--r-- root      @ Dec 6 01:13 pci
-dr-xr-x root      @ Dec 6 01:13 scsi
lrwxrwxrwx root      64 Dec 6 01:13 self -> 889
-r--r--r-- root      @ Dec 6 01:13 stat
-dr-xr-x root      @ Dec 6 01:13 sys
-r--r--r-- root      @ Dec 6 01:13 uptime
-r--r--r-- root      @ Dec 6 01:13 version
```

每个带有数字的目录都对应一个实际的进程 ID（PID）。通过进程表，你可以将进程与相关的进程 ID 相匹配。例如，进程表可能为 Web 服务器显示以下内容：

```
# ps ax | grep S 0:00 -f /etc/httpd/apache/conf/http.conf
```

可以通过查看该进程对应目录（`/proc/460`）中的相关文件来检查此进程的详细信息。你可能会好奇如何查看一个大小为 0 的进程的详细信息。如果你将其看作通往内核的窗口，这样就更符合逻辑。该文件实际上并不包含任何数据；它充当指向实际所在进程信息的指针。`/proc/460` 目录下的文件列表看起来如文所示：

```
-r--r--r-- root      @ Dec 6 21:21 cmdline
lrwxrwx------ root      64 Dec 6 21:21 cwd -> [0303]:2
-r--r--r-- root      @ Dec 6 21:21 environ
lrwxrwx------ root      64 Dec 6 21:21 exe -> [0303]:2
-dr-xr-x root      @ Dec 6 21:21 fd
dr-xr-x root      @ Dec 6 21:21 maps
-rw-r--r-- root      @ Dec 6 21:21 mem
lrwxrwxrwx  root      64 Dec 6 21:21 root -> [0303]:2
-r--r--r-- root      @ Dec 6 21:21 stat
-r--r--r-- root      @ Dec 6 21:21 statm
-r--r--r-- root      @ Dec 6 21:21 status
```

尽管文件显示大小为 0，但检查其内容后会发现事实并非如此：

```
# cat status
Name:     httpd.apache
State:    S (sleeping)
Pid:      460
PPid:     1
Uid:      0 0 0 0
Gid:      0 0 0 0
VmSize:   1332 kB
VmLck:    0 kB
VRSS:     688 kB
VmData:   300 kB
VmStk:    20 kB
VmEx:     376 kB
VLib:     592 kB
SigPnd:   00000000
SigBlk: 00000000
SigIgn: 80000000
SigCgt: 0000466b
```

`proc` 的帮助页详细描述了与运行中的进程 ID 相关的每个文件。

# 第 10 章 用户、组、权限

## 网络登录

登录 Linux 服务器的一种非常常见的方法是通过网络连接。事实上，Linux 服务器作为一个运行特定服务的独立、无显示器设备运行得非常出色。例如，在类似设备的基于 Linux 的机器上运行域名服务器 (DNS) 是很常见的现象。这类没有显示器和键盘的服务器只需要偶尔通过远程登录会话进行检查。通过网络链接连接服务器的最常用方法是使用 `telnet` 工具。也可以使用 `login` 等工具建立网络连接。

## 账户设置

添加和删除用户非常简单，但理解与用户账户管理相关的的文件有点复杂。编写了许多工具来管理与用户账户关联的数据文件，包括默认的 `usadder` 工具，但管理用户账户的关键在于理解底层的配置文件。

## 关键配置文件

用于用户账户设置和配置的文件是 `/etc/passwd` 文件。这是一个简单的 ASCII 文本文件，对于 Linux 的多用户概念至关重要。安装成功后，`/etc/passwd` 文件的内容类似于：

```
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/bin
daemon:x:2:daemon:/sbin
adm:x:3:adm:/var/adm
lp:x:4:7:lp:/var/spool/lpd
sync:x:5:0:sync:/bin/sync
shutdown:x:6:11:sbin/shutdown
halt:x:7:7:sbin/halt
mail:x:8:12:mail:/var/spool/mail
news:x:9:13:news:/var/news
uuccp:x:10:14:uucp:/var/spool/uucp
operator:x:11:0:operator:/root
games:x:12:120:games:/games
gopher:x:13:30:gopher:/usr/bin
ftp:14:58:FTP User:/home/ftp
man:x:15:15:Manual Owner::
majordomo:x:16:16:Majordomo:/bin/false
postgres:x:17:17:postgres User:/home/postgres:/bin/bash
nnody:x:65534:65534:Nobody::/bin/false
col:x:100:100:COL User:/home/col/bin/bash
natalie:x:101:100:OpenLinux User:/home/natalie/bin/bash
ryan:x:102:100:OpenLinux:/home/ryan/bin/bash
bryan:x:103:100 User:/home/bryan/bin/bash
kelsey:x:104:100:OpenLinux User:/home/kelsey/bin/bash
```

每一行代表一个用户。每个用户的信息被分为由冒号分隔的七个字段。这些字段的描述列于表 10.2。

### 表 10.2 /ETC/PASSWD 文件的字段描述

| 字段 | 描述 |
| --- | --- |
| 1 | 第一个字段是用户名或登录 ID。 |
| 2 | 第二个字段是密码字段。此字段中的小写 `x` 表示在使用影子密码。出于安全考虑，实际的加密密码存储在单独的文件。 |
| 3 | 此字段中的数字是用户 ID `UID`。它用于识别唯一的用户账户。没有两个用户账户具有相同的数字。 |
| 4 | 此字段是组 ID `GID` 字段数字。此数字用于创建逻辑用户组。 |
| 5 | 此字段是注释字段。它通常包含用户的全名。 |
| 6 | 第六个字段用于标识用户在登录系统时被放置在文件层次结构的哪个位置。用户账户通常配置为使用 `/home` 目录。 |
| 7 | 此字段用于配置默认 shell。默认 shell 是 `bash` 壳。 |

可以通过直接编辑 `/etc/passwd` 文件来添加新用户，但必须使用 `/usr/bin/password` 工具创建密码。需要此工具是因为因为它创建了正确的加密。

## 密码

任何账户的访问都通过密码控制。OpenLinux 默认使用影子密码。

> 影子密码是存储在单独文件中的密码。该文件 `/etc/shadow` 增加了额外的安全级别。

在影子密码出现之前，密码（尽管经过了加密）存储在 `/etc/passwd` 文件中。`/etc/passwd` 文件允许系统上的任何用户读取，但只能由 root 用户修改。然而，这带来了一个问题，意味着任何人都可以看到加密密码。有了今天强大的机器，破解即使是良好的密码也变得更容易。为了对抗这种威胁，定义了影子密码。通过将密码存储在单独的文件 `/etc/shadow` 中，可以使得 `/etc/passwd` 文件对所有账户可见，但加密密码本身仅对 root 用户可见。你稍后将在“权限”部分详细查看此处。

使用 `pwconv` 和 `useradd` 工具转换 `/etc/passwd` 文件或影子文件。

`/etc/shadow` 文件类似于：

```
root:0:0:19999:0:99999:7:::
bin:1:1:19999:0:99999:7:::
daemon:2:2:19999:0:99999:7:::
adm:3:3:19999:0:99999:7:::
lp:4:7:19999:0:99999:7:::
sync:5:0:19999:0:99999:7:::
shutdown:6:11:19999:0:99999:7:::
halt:7:7:19999:0:99999:7:::
mail:8:12:19999:0:99999:7:::
news:9:13:19999:0:99999:7:::
uuccp:10:14:19999:0:99999:7:::
operator:11:0:19999:0:99999:7:::
games:12:120:19999:0:99999:7:::
gopher:13:30:19999:0:99999:7:::
ftp:14:58:19999:0:99999:7:::
man:15:15:19999:0:99999:7:::
majordomo:16:16:19999:0:99999:7:::
postgres:17:17:19999:0:99999:7:::
nnody:65534:65534:19999:0:99999:7:::
col:100:100:19999:0:99999:7:::
natalie:101:100:19999:0:99999:7:::
ryan:102:100:19999:0:99999:7:::
bryan:103:100:19999:0:99999:7:::
kelsey:104:100:19999:0:99999:7:::
```

与 `/etc/passwd` 文件一样，`/etc/shadow` 文件由冒号分隔的单行条目组成。第一个字段是用户账户，第二个字段是存储加密密码的地方。

## 添加用户

可以通过直接编辑 `/etc/passwd` 文件或使用 `useradd` 工具添加用户账户。每个用户账户的默认特性由 `/etc/login.defs` 文件中的设置定义如下：
