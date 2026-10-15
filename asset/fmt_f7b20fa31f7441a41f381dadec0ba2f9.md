
密码字段中的星号表示密码相关数据位于其他处。密码字段中的星号表示密码相关数据位于`/auth`文件中，星号在`/etc/passwd`密码字段中有不同的含义，这可能让人感到困惑。`/auth`文件的条目格式如下：

`UID:lastch:min:warn:inactive:expire:flag`

其中：

- `UID`: 用户 ID
- `password`: 加密密码
- `lastch`: 最后一次更改（修改）的时间
- `min`: 更改之间的最小天数
- `max`: 密码有效的最大天数
- `accmask`: 账户的参数（此处此处描述可能略有有误）
- `count`: 失败登录尝试的次数
- `auditID`: 用于生成审计记录的标识符
- `auditctrl`: 生成审计记录的控制
- `auditmask`: 决定哪些事件将被审计的掩码

在 AIX 平台上，以下文件包含用户数据：

- `/etc/passwd`: 用户 ID、用户名、主目录、登录 shell 以及 finger 信息
- `/etc/shadow`: 包含加密密码和安全信息
- `/etc/security/passwd`: `/etc/security/passwd`的格式是典型的，不同之处在于密码字段中的星号（`*`）表示无效密码（无法登录），必须根据`/etc/security/login.cfg`中的“密码规则”来指定密码，其中包括：

- `min_alpha`: 字母的最小数量
- `min_other`: 其他字符的最小数量
- `min_diff`: 新密码中不同于旧密码的字符数量——如果新密码是 abcd 而旧密码是 edcb，则差异数量为 1
- `max_repeats`: 单个字符在密码中的最大次数
- `min_age`: 密码更改的最小年龄
- `max_age`: 密码的最大年龄。超过此年龄必须更改密码。以周为单位

如果`/etc/security/passwd`文件中的条目标记为`NOCHECK`，则超级用户不需要满足密码限制。如果是`ADMIN`，则只有超级用户可以更改密码。当超级用户更改密码时，`/etc/security/passwd`中的用户条目会被标记为`ADMCHG`，用户下次登录时必须更改密码。

支持 7-8 个 ASCII 字符。密码的前 8 个字符是有意义的。

`/etc/security/`目录的访问权限授予超级用户和 "security" 组。除了提到的`login.cfg`和`passwd`文件，该目录下还有几个文件：

- `/etc/security/mkuser`: 包含新用户的默认属性
- `/etc/security/group`: 包含组的扩展属性（`/etc/group`文件之外）
- `/etc/security/user`: 包含用户的扩展属性
- `/etc/security/environ`: 包含用户的环境属性
- `/etc/security/limits`: 包含用户的资源限制

显然，AIX 平台提供了多种工具来管理密码。

## 8.3 安全控制台和终端

保护系统的方法之一是限制超级用户登录的方式；如果将超级用户访问限制在特定的系统设备上，就会引入额外的安全性，增加入侵者的破解难度。这个想法源于 BSD 平台，该平台仅允许从控制台和声明安全的终端直接登录超级用户。否则，只有普通用户可以直接登录（直接指的是输入登录名称的常规验证程序）；随后用户可以切换到超级用户账户（如果授权）。对于其他终端，必须输入两个密码才能获得超级用户权限。

## 8.3.1 BSD 方法

在 BSD 平台上，终端行配置文件`/etc/tty`定义了终端（此文件对应 SunOS 中的`/etc/ttyab`）。这两个文件在第 11 章中有更详细的介绍。该文件列出了所有可用的系统终端。每个使用的终端端口必须有一个条目，未使用的则可以任意。一个终端条目有四个字段：

```
terminal-port   command   terminal-type status
```

下表解释了每个字段的含义。

| 字段 | 含义 |
|---|---|
| terminal-port | /dev 中与行通信的特殊文件名称。 |
| command | init 应该执行以监控此行的命令。 |
| getty | 用于终端和调制解调器 |
| none | 创建监控进程 |
| terminal-type | /etc/termcap 中描述的终端类型名称；变量 `TERM` 将设置为此值。 |
| status | 零或多个关键字，用空格分隔： |
| on | 行已启用 |
| off | 行已禁用并忽略该条目 |
| secure | 允许超级用户（root）登录 |
| window = cmd | init 在运行字段中指定的命令之前应运行 cmd |
| command | |

终端通过其条目中`status`字段的`secure`关键字来指定。建议仅将系统控制台指定为`secure`，永远不要给调制解调器或网络终端赋予`secure`状态。

### 8.3.2 轮组 (Wheel Group)

在非安全终端上登录时成为超级用户必须使用两个密码：首先是登录用户账户的用户密码，然后是切换到超级用户账户的 root 密码。从安全角度来看，这是一种改进。通常，可以从任何用户账户切换到超级用户账户。

通过使用 wheel 组，可以将执行切换到 root 的用户数量限制仅限该组成员。wheel 组成员必须在`/etc/group`文件中指定。在这里，最敏感的安全问题——超级用户状态（user root）得到了额外的保护；只有特定用户（一个或多个管理员）才能从任何给终端成为超级用户。

### 8.3.3 安全终端 — 其他方法

HP–UX 10.x 引入了文件`/etc/securetty`，它定义了允许超级用户登录的安全终端。通常情况下是如此。这里是一个示例：

```
# cat /etc/securetty

console
```

Solaris 2.x 引入了目录`/etc/default`，其中包含许多定义默认系统行为的文件。其中，文件`/etc/default/login`定义了登录规则，包括安全终端：

```
# ls -l /etc/default

total 26

-r--xr--x-- 1 bin 12 Jan 8 15:08 cron

-r--xr--x-- 1 bin 10 Jan 8 15:08 fs

-r--xr--x-- 1 root sys 367 Jan 8 15:08 initinit

-r--xr--x-- 1 root sys 462 Jan 8 15:27 init

-r--xr--x-- 1 root sys 678 Jan 8 15:08 kbd

-r--xr--x-- 1 root sys 1251 Jan 9 17:26 login

-r--xr--x-- 1 root sys 74 Jan 9 17:26 password

-r--xr--x-- 1 root sys 609 Oct 30 1996 sys-suspend

-r--xr--x-- 1 root sys 526 Jan 8 15:08 tar

-r--xr--x-- 1 root sys 16 Jan 8 15:08 utmpd
```

文件`/etc/default/login`的内容（请注意 CONSOLE 部分）：

```
$ cat /etc/default/login

#ident(@#)login.dfl 1.7 93/08/20 SMI* /* SVR4.0 L1.1.1.1 */

# 设置 shell 的 TZ 环境变量。

TZZONE = ESTEDDT

# 设置 shell 的 HZ 环境变量。

HZ = 100

# ULIMIT 设置登录的文件大小限制。单位是磁盘块。

# 默认值 0 意味着没有限制。

#ULIMIT = 0

# 如果设置了 CONSOLE，root 只能登录该设备。

# 注释此行以允许 root 登录。

CONSOLE = /dev/console

# PASSWD 决定登录是否需要密码。

PASSWD = YES

# ALTSHEL 决定是否应该设置 SHELL 环境变量

ALTSHEL = YES

# PATH 设置初始 PATH 变量

PATH = /usr/bin:/usr/openbin/bin:/usr/ucb/: share/local/bin

# SPATH 设置 root 的初始 PATH 变量

/sbin:/usr/bin:/usr/openbin/bin:/usr/ucb/: /usr/ucb/: share/local/bin

# TIMEOUT 设置放弃登录会话之前等待的秒数（0 到 900 之间）。

TIMEOUT = 300

# UMASK 设置初始 shell 文件创建模式。见 umask(1)。

UMASK = 022

# SYSLOG 决定是否使用 syslog(3) LOG_AUTH 设施

# 在 LOG_NOTICE 级别记录所有 root 登录，并在 LOG_CRIT 级别记录多次失败登录尝试。

SYSLOG = YES
```

## 8.4 监控和检测安全问题

### 8.4.1 系统安全重要文件

表 8.1 列出了系统的一些重要文件。

表 8.1：系统安全重要文件

| 描述 | 文件 |
|---|---|
| Root 账户初始化文件： | /.profile, /.kshrc, /.cshrc, /.login, /.logout |
| 其他 root 初始化文件： | /forward, /mailrc, /exec, /netrc (见注释) |
| 全局初始化文件： | /etc/profile, /etc/login, /etc/csh/etc/login |
| 主机等效相关文件： | /etc/hosts.equiv, /hosts (见注释) |
| 设备文件的文件权限： | /dev/* |
| **cron** 和 **at** 文件： | /usr/spool/crontabs/*, /usr/spool/cron/at/* |
| 所有与拨号相关的文件： | /etc/dialup, /etc/d_passwd, /etc/* |
| 默认系统设置： | /etc/default/* |
| 文件系统配置： | /etc/stab, /etc/vstab, /etc/checklist (HP-UX), /etc/filesystem (AIX) |
| NFS 导出的（共享）文件系统： | /etc/exports, /etc/dfs/share, /etc/dfs/sharetab |
| 用户和组配置： | /etc/passwd, /etc/shadow, /etc/security/* (AIX) |
| 网络相关文件： | /etc/hosts, /etc/protocols, /etc/services, /etc/netgroup |
| Internet 超守护进程配置： | /etc/inetd.conf |
| FTP 相关文件： | /etc/ftpusers, $shells, $HOME |
| 系统日志配置： | /etc/syslog.conf |
| 系统启动文件： | /etc/init.d/*, /etc/rc.config.d/* /sbin/init.d/* (HP-UX) |
| 系统初始化 (System V): | /etc/init.d/* |
| 电子邮件相关文件： | /etc/aliases |
| UUID 和 SGID 文件： | /etc/utmp |
| 登录相关文件： | /etc/wtmp |
| 计费文件： | /etc/btmp |
| 安全文件： | /etc/uocp |

以下是一个脚本示例。它将检查日志文件的大小并防止不受控的增长。

```bash
#!/bin/ksh

# Purpose：监控日志文件的大小并防止

# 不控的增长。一旦达到日志文件限制

=====================================

# 设置环境

TXT = /tmp/MF.txt

HOST = hostname

MAILTO = sysadmin

LBIN = /usr/bin

LIST = $(BIN)/ListofFiles

# 准备邮件标头

$(BIN)/echo "\n$TXT$(date):" >> $TXT

$(BIN)/echo "Checking the size of log files:" >> $TXT

$(BIN)/echo "--------------------------------------" >> $TXT

# 从列表中提取限制

-A LSA $LIST | awk '{print $2}'

# 重置计数器

i=0

ML="*"

for FILE in $LIST; do

    # 从列表中提取文件

    awk '{print $1}' "$FILE"

    FS=$(LSA[$i])

    # 提取字节的文件的大小

    FS=$(LSA[$i]) - 1 "$FILE" | /bin/awk '{print $5}'

    SZ=$FS

    # 检查文件大小与限制

    if [ $SZ -gt $ML ]; then

        #  .old -> *

        $(BIN)/cp -p $FILE ${FILE}.old

        $(BIN)/cp -p $FILE ${FILE}.old

        # 将文件重置为零

        $(BIN)/cat /dev/null $FILE

        $(BIN)/echo "The log file \$FILE\" is larger than ${SZ}KB!" >> $TXT

        $(BIN)/echo "\$FILE\" copied into \$FILE\.old" >> $TXT

    else

        $(BIN)/echo "--------------------------------------" >> $TXT

        # 设置标记

        ML="YES"

    fi

    i=$(expr $i + 1) # 计数

done

# 检查是否有操作

if [ "$ML" = "YES" ]; then

    $(BIN)/mailx -s "$HOST: Log File Check and Resize!" $MAILTO<$$TXT

fi

# 删除临时文本文件

$(BIN)/rm $TXT > /dev/null 2>&1

# ------------------------------------- 这是脚本的结束
```

### 8.4.2 监控系统活动

监控系统上的进程是降低系统安全风险的另一种方法。这应该定期进行，有时甚至每天进行几次。通过这种方式，你可以很好地了解什么是“正常”系统活动（哪些程序正在运行、运行了多久以及是谁运行的等），并且能够更容易识别任何异常活动。

`ps`命令列出运行中的系统进程的特征。要以实用的格式显示所有运行中的进程，命令格式如下：

```
ps -ax (BSD)
ps -ef (System V)
```
注意：`ps`命令在第 2 章中详细讨论过。

### 8.4.3 监控登录尝试

如果对登录尝试进行监控（特别是失败的尝试），有时可以及时发现入侵者试图进入系统的尝试。当然，超级用户账户特别受关注，因为攻入超级用户账户可能是致命的。

### 8.4.3.1 日志文件

所有的 UNIX 系统都提供了机制来记录用户尝试访问超级用户的尝试。此类日志文件对于追踪由 root 操作引起的潜在问题非常有帮助；至少我们可以查出当时是谁在使用超级用户。根据所实现的 UNIX 平台，日志文件的位置可能不同（通常，日志文件指定在 /etc/syslog 文件中，该文件将在第 9 章中讨论）；这里给出几个示例。

在 BSD 平台上（通常是文件 /usr/adm/messages）：

```
cat /usr/adm/messages
```

```
09:57:53 patsy named[82]; zoneref: Masters for secondary zone 95.146.in-addr.arpa unreachable
10:02:53 patsy named[82]; zoneref: Masters for secondary zone hunter.cuny.edu unreachable
    10:22:10 patsy su: 
    'root' succeeded for george on /dev/ttyp2
    10:22:35 patsy named[82]: 
    reloading nameserver
    15:34:24 patsy su: 
    'root' succeeded for levi on /dev/ttyp2
```

在 V 平台上（通常是文件 /usr/adm/sulog）。Solaris 2.x 的文件 /etc/default/su 指定了 `su` 命令存储的位置：

```
$ cat /usr/adm/sulog
...
...
SU 04/07 15:48 + ttyq1 balwin-root
SU 04/11 14:41 + ttyq0 levi-root
SU 04/12 13:56 + ttyq0 levi-root
SU 04/12 14:55 + ttyq0 frank-gargiulo
...
...
SU 05/02 12:00 + console root-lp
SU 05/10 10:46 + tty0 balwin-root
SU 05/12 16:15 + tty2 levi-root
```
