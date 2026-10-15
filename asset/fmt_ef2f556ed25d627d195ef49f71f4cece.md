
| Soft DATA segment | 软 DATA 段限制 |

| Soft STACK size | 软 STACK 大小限制 |

| Soft CORE file size | 设置 CORE 文件大小的软限制 |

# 表 20-2. `mkuser` 字段（续）

| 字段 | 用途 |

| :--- | :--- |

| Soft physical MEMORY | 设置软 MEMORY 限制 |

| Hard FILE size | 用户的硬资源限制 |

| Hard CPU time | 硬 CPU 时间限制 |

| Hard DATA segment | 硬 DATA 段限制 |

| Hard STACK size | 硬 STACK 大小限制 |

| Hard CORE fie size | 硬 CORE 文件大小限制 |

| Hard physical MEMORY | 物理内存限制的硬设置 |

| File creation MASK | 用户的默认 umask |

| AUDIT Classes | 代表此 UID 的审计类别 |

| TRUSTED PATH | 受信任路径状态 |

| PRIMARY authentication method | 用于验证此用户到系统的身份验证程序；默认 SYSTEM 代表标准用户名和密码 |

| SECONDARY authentication method | 次要身份验证程序；如果失败，不会拒绝访问 |

表 20-2. `mkuser` 字段（续）

用户，否则当您需要管理大型环境时就会迷失方向。

关于更改用户的 SMIT 面板，请参阅图 20-3 和 20-4。

```
# smit chuser
```

图 20-3 中的 SMIT 面板提示输入要更改的用户名。单击列表按钮可显示系统中定义的所有用户的列表。当您输入或选择

![](img/82f851021955589d82b22750fb3b1646_465_0.png)

图 20-3. 更改/显示用户特征名称请求 SMIT 面板

![](img/82f851021955589d82b22750fb3b1646_466_0.png)

选择列表中的用户后，您将被呈现图 20-4 中所示的 SMIT 面板。在此面板中，您可以更改 SMIT 中的特定用户属性。

您可以使用 `luser` 命令在命令行中列出当前定义的用户属性集，如下所示：

```
# luser stimpv
```

```
stimpv id=17742 pgrp=uadmin groups=uadmin,staff,printq,ecotools
```

```
home=/home/stimpy shell=/usr/bin/ksh gecos=Stimpy - AIX System Admin login=true active=true rlogin=true daemon=true admin=false eugroups=ALL admgroups= tpath=nsok ttya=ALL expires=0 auth1=SYSTEM auth2=pad_method usage=22 registry=files SYSTEM=compare logintries= loginretries=5 pwdwarn=49 account_locked=false minage=0 maxage=7 maxexpired=-1 minalpha=3 minother=1 mindiff=0 maxrepeat=2 minlen=6 histexpire=0 histsize=8 pwdchecks= dictionlist= fsize=-1 cpu=-1 datas=-1 stack=-1 core=2048 rss=-1 time_last_login=1021398808 time_last_unsuccessful_login=1021141628 tty_last_login=/dev/pts/4 tty_last_unsuccessful_login=/dev/pts/4 host_last_login=10.10.10.10 host_last_unsuccessful_login=167.105.28.110 unsuccessful_login_count=0 roles=
```

## 移除用户账户

要从系统中移除用户，请使用 `rmuser` 命令。可以从命令行调用，也可以使用 SMIT 和 WebSM。 `rmuser` 命令负责将用户从系统表中移除。您也可以选择保留 `/etc/security/passwd` 文件中的用户数据。从系统中移除用户的 SMIT 面板如图 20-5 所示。

```
# rmuser -p stimpy
# smit rmuser
```

若要自动化从系统中移除账户的过程，您可以使用 cron 运行一个夜间进程，该进程查找已过期的账户并调用 `rmuser`。有关使用 cron 的详细信息，请参见第 21 章。

![](img/82f851021955589d82b22750fb3b1646_467_0.png)

图 20-5. 从系统中移除用户的 SMIT 面板

## 限制访问

如果需要限制特定用户访问系统，您可以根据情况通过多种机制拒绝访问。将 `LOGIN User` 和 `User Can LOGIN` 字段设置为 false 可以限制登录访问。您还可以通过重置 `EXPIRATION` 字段中的日期来限制访问。最简单的方法是 `LOCK`（锁定）该账户。如果您希望向用户发送有关账户状态的告知信息，可以创建一个脚本或程序，将该信息写入 `stdout`，并将程序名称添加到该用户的 `Initial PROGRAM` 字段中。用户在登录时提供用户名和密码后，该信息将被显示，用户将被注销。使用 `chuser` 命令启用所需的访问限制级别。

# 密码文件

AIX 账户管理工具创建的所有信息最终都作为条目存储在多个用户账户支持表中。我在前面的章节中讨论了其中一些文件提供的结构。还有三个其他文件主要负责向操作系统和应用集标识账户。这些是 `/etc/passwd`、`/etc/security/passwd` 和 `/etc/security/user` 文件。

## /etc/passwd 文件

`/etc/passwd` 文件使用大多数 UNIX 系统上可用的标准密码文件格式，唯一的例外是使用影子密码文件。影子密码支持将加密的密码从可被所有人读取的 `/etc/passwd` 文件中移除，并将其放入另一个具有受限访问权限的文件中。在 `/etc/passwd` 中的密码字段中插入占位符，即感叹号 (!)。`/etc/passwd` 文件中的字段以冒号分隔，如下所示。

## /etc/passwd 文件示例

```
# USER NAME:UID:GID:GECOS:HOME DIRECTORY:SHELL
root::1:0:0:System O overseer::/bin/ksh
daemon::1:1:1::/etc:
bin::2:2:2::/bin:
sys::3:3:3:/usr/sys:
adm::4:4:4:/usr/adm:
uucp::5:5:5:/usr/lib:/usr/uucp:
stimpy::1:4084:30:Stimpyson Cat::/home/stimpy::/bin/ksh
```

必须解析用户信息的 AIX 命令和应用程序通过使用如 `getpwnam()` 这样的库调用来查询 `/etc/passwd`。解析大型密码文件可能导致命令响应时间出现显著延迟。 `mkpasswd` 命令用于创建带索引的安全文件。这些索引被库子程序 getpwnam, getpwpid, getuserrattr, 和 putuserattr 使用。其结果是对于拥有大量用户基础的系统，性能显著提升。索引在 `/usr/include/usersec.h` 文件中定义。默认情况下，创建以下索引：

```
/etc/passwd.nm.idx <— 使用用户名作为键的 /etc/passwd 索引
/etc/passwd.id.idx <— 使用用户 ID 作为键的 /etc/passwd 索引
/etc/security/passwd.idx <— 带索引的 /etc/security/passwd 文件
/etc/security/lastlog.idx <— 带索引的 /etc/security/lastlog 文件
```

以下是一些使用 mkpasswd 命令的示例：

### 创建并启用安全文件的带索引读取

```
# mkpasswd -f
```

### 仅为 /etc/security/passwd 文件创建并启用带索引读取

```
# mkpasswd /etc/security/passwd.idx
```

### 检查，如有必要则重建所有索引

```
# mkpasswd -c
```

### 删除所有索引

```
# mkpasswd -d
```

## /etc/security/passwd 文件

影子密码支持由 `/etc/security/passwd` 文件提供。每个用户账户由一个用户名存根表示。该存根包含加密的密码、上次更新时间和更新标志。更新标志包含 null 值或以下之一：

- `ADMIN` 仅 root 可以更改此密码。

- `ADMCHG` 安全组的成员重置了此密码，因此必须在下次登录时更改。

- `NOCHECK` 对于此账户，不执行 `/etc/security/user` 文件中设置的任何限制。

### /etc/security/passwd 存根示例

```
stumpy:
    password = dWe3assEf2u0J6
    lastupdate = 722287867
    flags = NOCHECK
```

## /etc/security/user 文件

`/etc/security/user` 文件包含为用户定义的扩展属性。每个用户由一个用户名存根标识，随后跟随每个属性及其值。在文件中的头部注释之后，有一个默认存根。每个用户条目可以通过指定本地值来覆盖默认属性。参见以下示例：

```
default:
admin = false
login = true
su = true
daemon = true
rlogin = true
sugroups = ALL
ttys = ALL
auth1 = SYSTEM
auth2 = NONE
tpath = nosak
umask = 022
expires = 0
stimpy:
login = false
rlogin = false
```

## 给 Group 和 Passwd 文件加盐（补充）

在大型环境中，可能需要在所有新安装中同步系统的应用程序的 user 和 group 空间。这意味着在安装 TXSeries、MQSeries 和 freeware.Isolfrte 应用程序之前，必须定义 mqm、cics 和 kmem 组，以及 cics 和 mqm 用户 ID 号。当应用程序安装时，如果用户和组尚不存在，它们将创建用户和组，并产生不同的结果。解决方案是从 AIX 5L 基础安装 CD 创建一个最小安装镜像，然后添加（或加盐）企业可能需要的所有未来组和用户 ID 列表。可以使用自己的脚本通过原生命令添加组和用户来对该镜像进行加盐，或者如果没有 ID 冲突，系统也可以从控制工作站拉取主文件。以下是您可能希望从主库工作站拉取或推送的一些文件列表：

```
/etc/passwd
/etc/passwd.nm.idx
/etc/passwd.id.idx
/etc/group
/etc/security/passwd
/etc/security/passwd.idx
/etc/security/group
/etc/security/user
/etc/security/login.cfg
/etc/security/
/etc/resolv.conf
/etc/netsvc.conf
```

## 检查清单

以下是“管理用户环境”中要点的检查清单。

- 定义默认环境策略。

- 简化账户管理。

- 识别物理资源。

- 管理 UID 空间和组。

- 识别资源限制。

- 定义用户账户访问权限。

- 为每个新账户设置默认环境。

- 管理用户账户。

- 识别密码文件。

- 在所有新安装中同步系统的应用程序的 user 和 group 空间。

![](img/82f851021955589d82b22750fb3b1646_472_0.png)

# 第 21 章

进程管理

在 AIX 下运行的一组进程类似于家谱中的世代。父进程 衍生出 子 进程。进程出生，履行职责，然后消亡。进程 ID 1，即 `init`，是所有进程世代追溯其起源的曾祖父级进程。像一位慈爱的祖父一样，`init` 接收那些失去父进程的孤儿进程。每个进程都有机会在 CPU 上执行。就像小孩子一样，它们需要调度器的指导，以确保每个人都能公平地分配到 CPU 资源。系统管理员是进程宇宙的总监督者，掌握着所有进程生死的最终控制权。一位仁慈且明察秋毫的系统管理员将学习 AIX 世界中进程生存的法则，以便他能平静、安宁地开展自己的工作。

## 进程属性

一个进程由正在执行的程序及其地址空间组成。每个进程都由一个称为 进程标识符（PID）的正整数命名。PID 是内核进程表中的向量索引。PID 是唯一的，并且以某种随机方式分配。进程表条目指向 每进程 内核数据结构。在 `/usr/include/sys/proc.h` 中定义的 `proc` 数据结构进而定义了与进程相关联的属性值。全局 AIX 进程表可以支持每个用户最多 131,073 个进程。你可以使用 SMIT 快速路径 smitty system，然后选择“更改/显示操作系统特性”来设置每个用户允许的最大进程数。选项列表中的第一项是“每个用户允许的最大进程数”。按下 F4 时，会显示有效范围。在大多数系统环境中，值为 200 到 2000 是足够的，但并非所有环境都相同。你选择的值将取决于系统运行的应用程序和数据库。

以下是一些可观察到的进程属性的简要示例：

- 进程标识符

- 进程组标识符

- 进程父标识符

- 进程所有者

- 有效用户和组以及真实用户和组标识符

- 优先级

- 控制终端

- 地址空间

- 页数大小

- 分页统计

- 资源利用率

- 进程状态

### 显示进程属性

当你需要查看系统中的进程时，`ps` 命令是你的好朋友。`ps` 命令的选项非常多，和许多 AIX 命令一样，你可以使用 System V 或 BSD 命令开关。当命令行参数前面带有连字符（-）时，使用 System V `ps` 命令；否则，使用 BSD 格式。你也可以使用 SMIT 和基于 Web 的系统管理器（WBM）来调用 `ps`，但你会发现从命令行使用 `ps` 更快。

`ps -eLk SYSV` 命令使用以下格式显示进程：

```text
F       S  UID  PID  PPID  C  PRI  NI  ADDR  SZ   WCHAN  TTY     TIME     CMD
103     A  0     0     0    120 16    --    2412  12         -  6:51  swapper
200003  A  0     1     0    60  20   142a  836   -          -  1:13  init
103     A  0     516   0    120 255   --    2613  8         *    775:05 wait
103     A  0     1032  0    0   37    --    1028  64         -  21:01 g11
103     A  0     129   0    0   16    --    1229  16   6ae819  -    0:00 lmched
46201   A  0     2608  0    0   60   20   2472  16   0c46b3   0:00 lvmbd
40401   A  0     2672  1    0   60   20   134c  572  14b774   0:00 kerdsmon
240001  A  0     2919  1    0   60   20   1b4d  780  -          0:00 rcmsmt
40103   A  0     3128  1    0   39   --    1f2f  16   -          0:00 loServer
241001  A  0     3392  1    0   60   20   663   320  309eb298  5:06 synccd
```

`ps auxww` BSD 命令使用以下格式显示进程：
