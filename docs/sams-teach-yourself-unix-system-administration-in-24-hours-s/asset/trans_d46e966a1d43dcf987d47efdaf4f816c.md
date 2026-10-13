
Feb 25 22:44:44 staging sendmail: sendmail 关闭成功
Feb 25 22:44:44 staging xinetd: xinetd 关闭成功
Feb 25 22:44:44 staging crond: crond 关闭成功
Feb 25 22:44:45 staging dd: 1+0 条记录输入
Feb 25 22:44:45 staging dd: 1+0 条记录输出
Feb 25 22:44:45 staging random: 保存随机种子：成功
Feb 25 22:44:45 staging nfslook: rpc.statd 关闭成功
Feb 25 22:44:45 staging portmap: portmap 关闭成功
Feb 25 22:44:46 staging syslog: klogd 关闭成功
Feb 25 22:47:37 staging syslog: syslogd 启动成功
Feb 25 22:47:37 staging syslog: klogd 启动成功
Feb 25 22:47:37 staging portmap: portmap 启动成功
Feb 25 22:47:37 staging nfslook: rpc.statd 启动成功
Feb 25 22:47:11 staging rc.sysinit: 挂载 proc 文件系统：成功
Feb 25 22:47:11 staging rc.sysinit: 卸载 initrd：成功
Feb 25 22:47:11 staging sysctl: net.ipv4.ip_forward = 0
Feb 25 22:47:11 staging sysctl: net.ipv4.conf.default.rp_filter = 1

这些消息记录了 2 月 25 日的系统关机（或更改了 init 状态，需要在启动新服务前执行一系列关机事件）。最需要注意的事情可能是错误、警告等：

```
# grep -E '(warning|error|crit|fail)' boot.log*
```

一切正常。太棒了！

6. 相比之下，使用相同的正则表达式检查 Solaris 8 上的 syslog 文件（Solaris 没有单独的启动日志文件；所有启动信息都进入 syslog）会发现：

```
# egrep '(warning|error|crit|fail)' syslog
Jan 22 22:36:35 solaris sendmail[347]: [ID 702911 mail.crit] My unqualified host name (solaris) unknown; sleeping for retry
Jan 15 00:06:08 solaris sendmail[223]: [ID 702911 mail.crit] My unqualified host name (solaris) unknown; sleeping for retry
Jan 15 00:34:43 solaris sendmail[224]: [ID 702911 mail.crit] My unqualified host name (solaris) unknown; sleeping for retry
```

很明显，sendmail 在启动时解析自身名称存在问题。这值得进一步探索，最终修复。

> 根据 Solaris 日志文件中显示的 sendmail 错误，有什么可能出错的理论吗？我猜想我们需要在某处正确设置主机名，但没有做到。显然 solaris 不是一个好的非限定主机名，也不会正确进行反向 DNS 查找。

7. 让我们快速查看一些其他日志文件，以了解发生了什么：

```
# head -5 cron
Mar 17 04:05:00 staging CROND[27157]: (root) CMD
(/usr/bin/mrtg /etc/mrtg/mrtg.cfg)
Mar 17 04:10:00 staging CROND[27160]: (root) CMD
(/usr/bin/mrtg /etc/mrtg/mrtg.cfg)
Mar 17 04:10:00 staging CROND[27161]: (root) CMD
(/usr/lib/sa/sa 1)
Mar 17 04:15:00 staging CROND[27164]: (root) CMD
(/usr/bin/mrtg /etc/mrtg/mrtg.cfg)
Mar 17 04:20:00 staging CROND[27167]: (root) CMD
(/usr/bin/mrtg /etc/mrtg/mrtg.cfg)
```

正如预期的那样，cron 日志文件显示了 cron 守护进程执行的命令和操作。括号中显示了用户账户，也显示了命令。如果你认为有人使用基于 cron 的程序试图破坏安全，这里会记录下来。

8. 如果你准备对有人试图访问你的计算机感到偏执，请查看 xferlog 或 ftp.log，具体取决于你的操作系统。例如，在我的 Mac OS X 服务器上，日志文件显示

```
# cat ftp.log | grep -v taylor
Jan 21 12:24:36 dsl-132 ftp[369]: connection from dsl-155.dsldesigns.com
Jan 21 12:24:40 dsl-132 ftp[369]: FTP LOGIN REFUSED
FROM dsl-155.dsldesigns.com, root
Jan 21 12:28:06 dsl-132 ftp[390]: connection from 63.101.93.250
Jan 21 12:35:40 dsl-132 ftp[412]: connection from dsl-155.dsldesigns.com
Jan 21 19:44:24 dsl-132 ftp[491]: connection from 63.101.93.250
Jan 21 19:45:28 dsl-132 ftp[492]: connection from dsl-155.dsldesigns.com
Jan 21 20:00:39 dsl-132 ftp[516]: connection from 63.101.93.250
Jan 22 09:45:04 dsl-132 ftp[332]: connection from webpac.clemson.edu
Jan 22 12:27:23 dsl-132 ftp[460]: connection from 63.101.93.250
Jan 22 13:34:18 dsl-132 ftp[461]: connection from 63.101.93.250
Jan 24 18:00:40 dsl-132 ftp[369]: connection from dsl-155.dsldesigns.com
Jan 26 22:44:59 dsl-132 ftp[927]: connection from dsl-155.dsldesigns.com
Jan 29 18:27:33 dsl-132 ftp[359]: connection from 157.161.112.208
Jan 29 21:48:12 dsl-132 ftp[378]: connection from
port-212.202-160-251.reverse.qds1.home.de
Jan 29 21:48:13 dsl-132 ftp[378]: ANONYMOUS FTP LOGIN REFUSED
FROM port-212.202-160-251.reverse.qds1.home.de
Feb 6 12:10:23 dsl-132 ftp[525]: connection from 199.98.128.27
Feb 6 15:54:41 dsl-132 ftp[554]: connection from pd955f64e.dip.t-dialin.net
Feb 6 21:52:56 dsl-132 ftp[685]: connection from pd955f64e.dip.t-dialin.net
Feb 6 21:52:58 dsl-132 ftp[685]: ANONYMOUS FTP LOGIN REFUSED
FROM pd955f64e.dip.t-dialin.net
Feb 7 00:01:09 dsl-132 ftp[612]: connection from maptech-inc.com
Feb 7 00:01:12 dsl-132 ftp[613]: connection from maptech-inc.com
Feb 7 00:01:21 dsl-132 ftp[614]: connection from maptech-inc.com
```

公众无法访问任何文件，我们系统的 IP 地址也没有在任何地方公布。这些站点是如何找到我们系统的是个谜，但它们正在尝试连接并登录，这不是谜。

这显然是试图破坏我们系统安全的企图，所以现在是关闭 ftpd 程序的好时机，直到我准备好重新启用它。在 Mac OS X 中，最快的方法是进入系统偏好设置、共享控制面板并取消选中启用 FTP 访问。这不仅在未来活动之前将其关闭，而且还会终止当前正在运行的 ftpd。

9. 另一个值得关注的日志文件是 maillog，它记录所有发生的电子邮件交易。例如，如果我给自己发送一封快速的电子邮件，以下两行将被写入文件：

```
# tail -2 maillog
```

```
Mar 18 14:24:35 staging sendmail[5459]: g2IM0Zb05459: from=root, size=58, class=0, nrcpts=1, msgid=<200203182224.g2IM0Zb05459@staging.intuitive.com>, relay=root@localhost
```

```
Mar 18 14:24:52 staging sendmail[5462]: g2IM0Zb05459: to=taylor@intuitive.com, ctladdr=root (0/0), delay=00:00:17, xdelay=00:00:17, mailer=esmtp, pri=30058, relay=mail-fwd.verio-web.com. [161.58.148.40], dsn=2.0.0, stat=Sent (036711929 Message accepted for delivery)
```

有很多内容，但最重要的是注意这两行可以通过 jobID（g2IM0Zb05459）匹配，并且第一条条目表示 from=，第二条表示 to=。无需复杂操作，我们可以按字段值排序，然后提取 from= 和 to= 值来查看发生了什么：

```
# sort -k6 maillog* | awk '{print $7 }' | grep -v root | grep 'to='
to=taylor@intuitive.com,
```

有点复杂，但这个管道会提取日志文件中所有的 from= 和 to= 值，剔除发往或来自 root 的邮件，然后报告所有系统外的地址。正如该服务器所预期，只有一条消息被发送。

毫无疑问，有很多日志文件需要跟踪，每个文件中都有重要的信息片段。花时间探索每个文件并在系统运行时不断返回查看，开始了解其中包含的内容是非常值得的。

## 追踪黑客

在日志文件中你会发现的一个常见现象是存在奇怪且令人惊讶的条目。让我们尝试向后追踪一个，看看是否能弄清发生了什么。

### 任务 16.2：向后追踪

虽然某些 Unix 系统会将所有日志条目都放入 syslog 文件，但 Linux 提供了一个不同且有用的日志文件，称为 secure，其中包含所有安全相关的日志事件。

- 1. 在 Linux 上，有一个非常重要的日志文件称为 secure，值得查看其内容：

```
# head secure
Mar 10 10:22:14 staging sshd[12114]: Did not receive identification string from 208.37.77.153.
Mar 10 22:27:39 staging sshd[12659]: Could not reverse map address 198.76.82.132.
Mar 10 22:27:42 staging sshd[12659]: Accepted password for taylor from 198.76.82.132 port 49154 ssh2
Mar 10 23:39:43 staging sshd[12796]: Accepted password for taylor from 198.76.82.132 port 49156 ssh2
Mar 11 11:19:29 staging sshd[14368]: Could not reverse map address 198.76.82.132.
Mar 11 11:19:32 staging sshd[14368]: Accepted password for taylor from 198.76.82.132 port 49152 ssh2
Mar 11 16:02:00 staging sshd[14716]: Could not reverse map address 198.76.82.132.
Mar 11 16:02:05 staging sshd[14716]: Accepted password for taylor from 198.76.82.132 port 49153 ssh2
Mar 11 17:15:38 staging sshd[14891]: Did not receive identification string from 129.132.250.236.
Mar 12 15:01:13 staging sshd[16846]: Could not reverse map address 198.76.82.132.
```

这记录了所有安全相关事件，包括 sshd 连接。如你所见，taylor 从 198.76.82.132（一个已知的 IP 地址）登录，但也有来自 208.37.77.153 的连接。

host 命令可以进行反向 IP 映射，因此给定一个 IP 地址，我们可以确定其域名：

```
# host -v 208.37.77.153
;; res_nmkquery(QUERY, 153.77.37.208.IN-ADDR.ARPA., IN, PTR)
;; res_send()
;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 65086
;; flags: rd; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 0
;; 153.77.37.208.IN-ADDR.ARPA., type = PTR, class = IN
;; Querying server (# 1) address = 192.216.138.10
;; new DG socket
;; got answer:
;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 65086
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 4, ADDITIONAL: 0
```
