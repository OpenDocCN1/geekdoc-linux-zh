

sendmail 的 SafeFileEnvironment 选项控制当邮件通过别名或 .forward 文件重定向到文件时，文件可以写入的位置。它会使 sendmail 执行 chroot 系统调用，使文件系统的根不再是 / 而是 /safe 或你在 SafeFileEnvironment 选项中指定的路径。例如，指向 /etc/passwd 文件的别名，实际上会被写入到 /safe/etc/passwd。

SafeFileEnvironment 选项还通过只允许写入常规文件来保护设备文件、目录和其他特殊文件。除了提高安全性之外，此选项还能减轻用户错误的影响。某些站点将该选项设置为 /home 以允许访问主目录，同时将系统文件设为禁止访问。

邮件程序也可以在 chroot 目录中运行。

## 隐私选项

sendmail 还具有隐私选项，用于控制

- 外部人员通过 SMTP 能查明你站点的哪些信息
- 你对 SMTP 连接另一端主机要求的条件
- 你的用户能否查看或运行邮件队列

表 20.15 列出了截至本文撰写时隐私选项的可能取值；请参阅发行版中的文件 doc/op/op.ps 以获取当前信息。

### Table 20.15 Values of the PrivacyOption variable

| Value | Meaning |
|---|---|
| public | 不进行任何隐私/安全检查 |
| needmailhelo | 要求 SMTP HELO（标识远程主机） |
| noexpn | 禁止 SMTP EXPN 命令 |
| novrfy | 禁止 SMTP VRFY 命令 |
| needexpnhelo | 未发送 HELO 时不展开地址（EXPN） |
| needvrfyhelo | 未发送 HELO 时不验证地址（VRFY） |
| noverb* | 禁止 EXPN 的详细模式 |
| restrictmailq | 仅允许邮件队列目录的组查看队列 |
| restrictqrun | 仅允许邮件队列目录的所有者运行队列 |
| restrictexpand | 限制 -bv 和 -v 标志显示的信息* |
| noetrn* | 禁止异步队列运行 |
| authwarnings | 若外发邮件似乎被伪造则添加警告头 |
| noreceipts | 关闭成功回执的投递状态通知 |
| nobodyreturn | 在 DSN 中不返回邮件正文 |
| goaway | 禁用所有 SMTP 状态查询（EXPN、VRFY 等） |

a. 详细模式在给出 EXPN 命令时会跟随 .forward 文件并报告用户邮件所在位置的更多信息。在任何暴露于外部世界的机器上使用 noverb 或更好的是 noexpn。
b. 除非由 root 或 TrustedUser 执行。
c. ETRN 是专为拨号主机设计的 ESMTP 命令。它请求仅对该主机的邮件运行队列。

## 我们推荐保守做法；在你的 `.mc` 文件中，使用

```
define(`confPRIVACY_OPTIONS', `goaway, authwarnings, restrictmailq,
    restrictrun')
```

**sendmail's** 隐私选项的默认值是 `authwarnings`；上面的行会重置该值。注意双重引号；某些版本的 **m4** 需要它们来保护隐私选项列表中的逗号。Red Hat、Solaris 和 AIX 默认使用 authwarnings；SUSE 和 Ubuntu 默认使用 authwarnings、needmailhelo、novrfy、noexpn 和 noverb；HP-UX 默认使用 restrictrun、goaway 和 authwarnings，最为安全——干得好，HP！

## 运行 chrooted sendmail（给真正偏执的人）

如果你担心 **sendmail** 对你文件系统的访问权限，可以在 **chrooted** jail 中启动它。（有关 **chroot** 的更多信息，请参阅第 22 章 *Security* 中的第 913 页。）在你的 jail 中创建一个最小的文件系统，包括诸如 `/dev/null`、`/etc` 必要文件（`passwd`、`group`、`resolv.conf`、`sendmail.cf`、任何映射文件、`mail/*`）、**sendmail** 所需的共享库、**sendmail** 二进制文件、邮件队列目录以及任何日志文件。你可能需要调整列表以使其完全正确。使用 `chroot` 命令启动受限的 **sendmail**。例如：

```
$ sudo chroot /jail /usr/sbin/sendmail -bd -q30m
```

## 拒绝服务攻击

拒绝服务攻击很难防范，因为事先没有办法确定一条消息是攻击还是合法的邮件。攻击者可以尝试各种恶劣手段，包括用虚假连接淹没 SMTP 端口、用巨型邮件填满磁盘分区、堵塞外发连接以及邮件轰炸。**sendmail** 有一些配置参数可以帮助减缓或限制拒绝服务攻击的影响，但这些参数也可能干扰合法邮件。Milters 可以帮助系统管理员挫败长时间的拒绝服务攻击。

MaxDaemonChildren 选项限制 **sendmail** 进程的数量。它可防止系统因 **sendmail** 工作而不堪重负，但也允许攻击者轻松关闭 SMTP 服务。MaxMessageSize 选项可以帮助防止邮件队列目录被填满，但如果设置过低，合法邮件会被退回。（你可能需要告知用户你的限制，以免他们在邮件退回时感到意外。我们建议设置一个相当高的限制，因为有些合法邮件非常大。）ConnectionRateThrottle 选项限制每秒允许的连接数，可以稍微减缓速度。最后，设置 MaxRcptsPerMessage，该选项控制单条消息允许的最大收件人数，也可能有所帮助。

**sendmail** 一直能够根据系统负载平均值拒绝连接（选项 REFUSE_LA）或排队邮件（QUEUE_LA）。一种变体，

