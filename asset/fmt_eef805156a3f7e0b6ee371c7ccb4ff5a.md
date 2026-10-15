
使用密码登录 workstation 为 `student` 用户。在 workstation 上运行 `lab start` 命令。该命令运行一个脚本来判断服务器是否可用，并安装 `postfix` 软件包。

```
[student@workstation ~]$ lab start
```

1. 使用 `ssh` 命令以 student 用户身份登录服务器。系统配置为使用 SSH 密钥进行验证，因此不需要密码。

```
[student@workstation ~]$ ssh servera
...output omitted...
[student@servera ~]$
```

2. 使用 `sudo -i` 切换到 root 用户。student 用户的密码是 `student`。

```
[student@servera ~]$ sudo -i
[sudo] password for student: student
[root@servera ~]$
```

3. `postfix` 软件包是由 `start` 脚本安装的。使用 `grep` 命令查找 postfix 和 postdrop 组的 GID 和 UID。为了减少 grep 输出，显示从特定启动时间开始的所有日志

### 3.1 使用 `date` 命令确定当前时间。

```
[root@servera ~]$ date
Fri Mar 22 08:23:56 CET 2019
```

### 3.2 使用带有日期、启动时间以及 GID 选项的 `grep` 命令查找 postfix 和 postdrop 用户的 GID 和 UID。启动脚本在当前时间之前的几分钟运行。在搜索 `/var/log/secure` 日志文件时考虑到这一点。

```
[root@server ~]# grep '^Mar 22 08:2.*.GID' /var/log/secure
Mar 22 08:02:04 serva groupadd[2514]: group added to /etc/group: name=postdrop, GID=90
Mar 22 08:02:04 serva groupadd[2514]: new group: name=postdrop, GID=90
Mar 22 08:02:04 serva groupadd[2520]: group added to /etc/group: name=postfix, GID=89
Mar 22 08:02:04 serva groupadd[2520]: new group: name=postfix, GID=89
Mar 22 08:02:04 serva useradd[2527]: new user: name=postfix, UID=89, GID=89, home=/var/spool/postfix, shell=/sbin/nologin
```

- 修改你的正则表达式以定位 `/var/log/mailog` 文件中的前两条消息。注意，在这次搜索中你没有使用脱符号 (`^`)，因为你正在搜索行的第一个字符。
- 你需要找到 Postfix 服务器队列目录的名称。搜索 `/etc/postfix/main.cf` 配置文件获取关于队列的所有信息。使用 `i` 选项忽略大小写。

```
[root@server ~]# grep 'postfix' /var/log/mailog | head -n 2
Mar 22 08:21:02 serva postfix/script[3879]: starting The Postfix mail system
Mar 22 08:21:02 serva postfix/master[3881]: daemon started -- version 3.3.1, configuration /etc/postfix
```

```
[root@server ~]# grep 'queue' /etc/postfix/main.cf
# testing. 当启用 soft_bounce 时，邮件将保持队列状态
# queue_directory 指定 Postfix 队列的位置。
queue_directory = /var/spool/postfix
# QUEUE AND PROCESS 参数指定 Postfix 队列的所有者
# mail_owner 指定 Postfix 队列
# 是 Sendmail 兼容的队列列表命令。
# setid_gid: 邮件提交和队列管理的组
```

- 确认 postfix 正在向 `/var/log/messages` 写入消息。使用 `less` 命令然后斜杠 (`/`) 搜索文件。按 `n` 移动到下一个匹配搜索的项目。按 `q` 退出 `less` 命令。

```
[root@server ~]$ less /var/log/messages
... output omitted...
Mar 22 07:58:04 serva systemd[1]: Started Postfix Mail Transport Agent.
... output omitted...
Mar 22 08:12:26 serva systemd[1]: Stopping Postfix Mail Transport Agent...
Mar 22 08:12:26 serva systemd[1]: Stopped Postfix Mail Transport Agent...
```

# 第 1 章 | 提高命令行效率

- 7. 使用 `ps aux` 确认 postfix 服务器当前正在运行。通过与 `grep` 命令结合来减少 `ps aux` 的输出。

```
[root@servera ~]# ps aux | grep postfix
root      3881  0.0 121664 5364 ? Ss       08:21 0:00 /usr/
libexec/postfix/master -w -
root      3882  0.0 0.4 147284 9088 ? S       08:21 0:00 pickup -l
trix -u
root      3883  0.0 0.4 147336 9124 ? S       08:21 0:00 qmgr -l -t
unix -u
```

- 8. 确认 qmgr、cleanup 和 pickup 队列配置正确。使用带有 `-e` 选项的 `grep` 命令匹配同一文件中的多个项。配置文件位于 `/etc/postfix/master.cf`

```
[root@servera ~]# grep -e qmgr -e pickup -e cleanup /etc/postfix/master.cf
pickup  unix n      -       n      60 1  pickup
cleanup unix n      -       n       0  cleanup
qmgr   unix n      -       n     300 1  qmgr
#qmgr   unix n      -       n     300 1  oqmgr
```

- 9. 从服务器登出。

```
[root@servera ~]# exit
logout
[student@servera ~]$]$ exit
logout
Connection to server closed.
[student@workstation ~]$
```

## 结束

在工作站上，运行 `lab console-regex finish` 脚本完成此练习。

```
[student@workstation ~]$ lab console-regex finish
```

引导练习结束。

# 第 I 章 | 提高命令行效率

## 实验

## 提高命令行效率

## 性能检查清单

在本实验中，你将创建一个 Bash 脚本，该脚本可以从不同的主机过滤并获取相关信息。

## 预期结果

你应该能够：

- 创建一个 Bash 脚本并输出重定向到文件。
- 使用循环简化你的代码。
- 使用 `grep` 和正则表达式过滤相关内容。

## 准备工作

使用 student 作为密码登录工作站。

在工作站上，运行 `lab console-review start` 命令。该命令运行一个启动脚本，判断工作站、servera 和 serverb 机器在网络上是否可访问。如果它们不可用，脚本将提醒你。它会在需要时安装 `vim-enhanced` 和 `util-linux` 包，配置 `sudo`，并准备 servera 和 serverb 上的 `/var/log/secure` 内容。

```
[student@workstation ~]$$ lab console-review start
```

- 1. 在工作站上创建 `/home/student/bin/bash-lab` 脚本文件。
