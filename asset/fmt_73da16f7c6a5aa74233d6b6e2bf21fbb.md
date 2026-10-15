
# mailstats

```
# mailstats
Statistics from Fri Jan 16 23:45:20 2009
M msgsfr bytes_from mgsto  bytes_to msgsrej msgsdis mssqur Mailer
4 2 8K 0K 0 0 0 esmtp
9 29 130K 39K 0 0 0 local

T 31 138K 8 39K 0 0 0
C 15 0 0
```

输出显示了若干列，在表 24-6 中列出并解释了这些列。

| 列 | 说明 |
| --- | --- |
| M | 列出邮件数量。 |
| msgsfr | 从邮件代理收到的消息数量。 |
| btes_from | 从邮件代理收到的字节数（KB）。 |
| mgsto | 发送到邮件代理的消息数量。 |
| bytes_to | 发送到邮件代理的字节数（KB）。 |
| msgsrej | 被拒绝的消息数量。 |
| msgsdis | 被丢弃的消息数量。 |
| mssqur | 被隔离的消息数量。 |
| Mailer | 邮件代理的名称。 |

表 24-6 `mailstats` 命令输出

# 配置 Postfix

本节提供了有关 Postfix 的详细信息，并展示了如何将 RHEL 系统配置为 Postfix 邮件服务器。Postfix 兼容 `sendmail`，更容易管理，支持用于模式匹配过滤垃圾邮件，并支持在单个系统中运行多个虚拟邮件域。

## Postfix 守护进程

Postfix 的主守护进程称为 `master`，位于 `/usr/libexec/postfix` 目录。该守护进程启动子守护进程 —— `nmqgr`、`pickup` 和 `smtpd` —— 代表其进行工作。`nmqgr` 守护进程负责邮件传输、中继和本地投递；`pickup` 守护进程将邮件从 `/var/spool/mqueue` 传输到 `/var/spool/mail` 目录；`smtpd` 则将入站邮件重定向到 `/var/spool/mail` 目录。

## Postfix 配置文件

Postfix 有两个关键的配置文件，称为 `master.cf` 和 `main.cf`，它们都位于 `/etc/postfix` 目录中。`master.cf` 文件包含控制 `master` 守护进程的设置。它列出了 Postfix 需要的服务并适当地地启动它们。下面是 `master.cf` 的摘录：

```
# cat /etc/postfix/master.cf
----------------------------
# service type private unpriv chroot wakeup maxproc command + args
# -------------------------------------------------------
#          (yes) (yes) (yes) (never) (100)
smtp     inet n       n       n        smtpd
pickup fifo n       n       n      60 1 pickup
cleanup unix n       n       n       0 cleanup
qmgr     n       n       n     300 1 qmgr
```

对于第一列列出的每个服务，都有七个相关列，定义了该服务如何被使用。这些列在表 24-7 中列出并解释。

| 列 | 说明 |
| --- | --- |
| service | 服务名称。 |
| type | 使用的传输机制。 |
| private | 该服务是否仅供 Postfix 使用。 |
| unpriv | 服务是否由非 root 用户运行。 |
| chroot | 服务是否为邮件队列配置了 chroot（根目录环境）。 |
| wakeup | 服务的唤醒间隔。 |
| maxproc | 服务可以启动的最大线程数。 |
| command | 服务相关的命令以及任何参数。 |

表 24-7 `master.cf` 文件内容

`main.cf` 文件是主要的 Postfix 配置文件，定义了 Postfix 操作的全局设置。这些设置包括要服务的宿主机、域名和网络、邮件所有者以及要监听的网络接口等。该文件的默认内容所示。请注意，指令在文件中出现的顺序是重要的。

```
# cat /etc/postfix/main.cf
# SOFT BOUNCE
# soft_bounce 参数为测试提供了一个有限的安全网。
# 当启用 soft_bounce 时，原本会被退回的邮件将保持在队列中这。
# 此参数禁用了本地生成的退回，并防止 SMTP 服务器永久拒绝邮件。
```

互联网服务与电子邮箱 507

```
# (通过将 5xx 回复改为 4xx 回复)。然而，soft_bounce
# 并不是解决地址重写错误或邮件路由错误的良方。
#soft_bounce = no
# LOCAL PATHNAME INFORMATION
# queue_directory 指定了 Postfix 队列的位置。
# 这也是运行 chroot 的 Postfix 守护进程的根目录。
# 请查看 examples/chroot-setup 中的文件以设置
queue_directory = /var/spool/postfix
```

`main.cf` 中可以设置若干指令。表 24-8 列出并解释了其中一些。

| 指令 |  |
| --- | --- |
| myhostname | 指定 Postfix 的完整主机名。 |
| mydomain | 指定 Postfix 的域名。 |
| myorigin | 指定邮件看似源自的域名。 |
| inet_interfaces | 指定使用的网络接口。 |
| mydestination | 指定 Postfix 接收邮件的域名。 |
| mynetworks | 指定受信的 IP 地址范围。 |
| virtual_maps | 在 `/etc/` 中定义虚拟别名。 |

## 显示和修改 main.cf

`postconf` 命令是一个 Postfix 配置工具，可用于显示和修改 `main.cf`。例如，要显示默认和非默认设置，分别运行 `-d` 和 `-n` 命令：

```
# postconf -n
alias_database = hash:/etc/aliases
alias_maps = hash:/etc/aliases
command_directory = /usr/sbin
config_directory = /etc/postfix
demo_directory = /usr/libexec/postfix
debug_level = 2
html_directory = no
inet_interfaces = localhost
mail_owner = postfix
mail_path = /usr/bin/mailq
manpage_directory = /usr/share/man
newaliases_path = /usr/bin/newaliases
queue_directory = /var/spool/postfix
readme_directory = /usr/share/doc/postfix-2.3.3/README_FILE
sample_directory = /usr/share/doc/postfix-2.3.3/samples
sendmail_path = /usr/sbin/sendmail
setgid_group = postfix
unknown_local_recipient_reject_code = 550
```

例如，如果你想将指令 `queue_directory` 的值 `/var/spool/postfix` 修改为 `/var/spool/defaultmail`，请运行命令：

```
# postconf -e queue_directory=/var/spool/defaultmail
```

## 配置 Postfix 服务器

要将系统 `rhel03` 配置为 Postfix 服务器，请按照以下步骤操作。注意，用户邮件在发送之前临时存在 `/var/spool/postfix` 目录中。

1. 检查是否安装了 Postfix 软件包：

```
# rpm -qa | grep postfix
postfix-2.3.2-1.el5_2
```

如果没有安装，请使用第 11 章“软件包管理”中描述的任何软件包方法进行安装，

2. 打开 `main.cf` 配置文件并设置或修改以下指令：
