
`-rw-rw-- 1 candace mail 0 Oct 21 23:53 /var/spool/mail/candace`

`-rw-rw-- 1 marshall mail 554 Jan 25 20:48 /var/spool/mail/marshall`

`-rw-rw-- 1 miss_pea mail 0 Jan 19 2000 /var/spool/mail/miss_peacock`

`-rw-rw-- 1 miss_scarlet root 7396 Feb 21 2000 /var/spool/mail/miss_scarlet`

`-rw-rw-- 1 root root 6416 Jan 26 06:04 /var/spool/mail/root`

`-rw-rw-- 1 sherlock mail 513 Oct 21 22:48 /var/spool/mail/sherloc`

为了安全起见，请确保所有邮箱文件仅允许所有者读写。

- `/etc/mail/access` 不允许向你的系统发送邮件的地址列表。
- `/etc/mail/relay-domains` 允许通过你的系统中继邮件的主机列表。
- `/etc/mail/local-host-names` 系统的其他名称。
- `/etc/mail/virtertable` 将邮件地址映射到系统上的用户名。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_450_0.png)

# 配置电子邮件客户端端

在你和用户读读发送邮件之前，你需要配置一个电子邮件客户端（MUA）。你决定配置的 MUA 取决于用户偏好以及计算机上提供的用户界面。如果你的 Linux 系统没有图形界面（GUI），你必须选择一个基于文本的电子邮件客户端。下面的章节将向你如何配置一个 GUI MUA（Netscape Messenger）和一个基于文本的 MUA（elm）。虽然其他客户端的步骤不同，但配置所有 MUA 的基本概念是相同的。

## 介绍 Netscape Messenger

大多数 Linux 用户熟悉 Linux 自带的浏览器 Netscape Navigator。Navigator 只是 Communicator 套件中的一个程序。Communicator 套件中的另一个程序是 Netscape Messenger。

```bash
root@redbird# rpm -q netscape
netscape is installed
```

绝大多数 Linux 用户熟悉 Linux 自带的浏览器 Netscape Navigator。Navigator 只是 Communicator 套件中的一个程序。Communicator 套件中的另一个程序是 Netscape Messenger。

```bash
# 基本系统别名 -- 这些必须存在。
mailer-daemon: postmaster
postmaster: root
# 针对伪账户的通用重定向。
daemon: root
ip: root
sync: root
shutdown: root
user: news
ftpadmin: ftp
ftpadmin: ftp
ftp-admin: ftp
ftp-admin: ftp
```

```bash
# 用于捕获安全攻击的 trap decode
decode: root
```

```bash
# 应该接收 root 邮件的人
root: candace
```

```bash
# 用户
miss_scarlet: bad_girl
wilensky: marshall_wilensky, marshall
```

```bash
# 分发列表 TCPAuthors
candace, marshall:
emily, elly, emma@fakeremote.com : Kids
```

你可以使用本地或远程地址。当用户移动到另一个系统时，此功能非常有用。你可以在计算机上禁用他们的账户，但继续将他们的邮件转发到新地址。

## 第 24 章 ♦ 配置电子邮件和其他通信服务 421

若要在别名文件中创建条目，请使用你喜欢的编辑器。每个条目由用户名、冒号、空格（或制表符）以及别名组成。保存文件后，你必须运行 `newaliases` 命令使更改生效。这是因为 `sendmail` 通过读取二进制文件 `/etc/mail/aliases.db` 来获取别名信息。`newaliases` 命令会读取你的别名文件并更新二进制文件。

## 与 sendmail 使用的文件和其他命令

浏览你的 `sendmail` 配置文件可以发现 `sendmail` 使用多个文件。以下列表描述了其中一些文件。你的系统可能没有使用所有这些文件。

- `/usr/bin/sendmail` 以及 `/usr/lib/sendmail`，取决于你的发行版，`sendmail` 守护进程执行该镜像
- `mailq` 或 `sendmail -bp` 显示邮件队列的内容：

```bash
root@redbird# mailq
/var/spool/mqueue is empty
root@redbird# sendmail -bp
/var/spool/mqueue is empty
```

- `/var/spool/mqueue` 存放邮件队列的文件取决于发行版。
存放用户邮件的文件（邮箱文件）如下例所示。

```bash
root@redbird# ls /var/spool/mail/*
-rw-rw-- 1 candace mail 0 Oct 21 23:53 /var/spool/mail/candace
-rw-rw-- 1 marshall mail 554 Jan 25 20:48 /var/spool/mail/marshall
-rw-rw-- 1 miss_pea mail 0 Jan 19 2000 /var/spool/mail/miss_peacock
-rw-rw-- 1 miss_scarlet root 7396 Feb 21 2000 /var/spool/mail/miss_scarlet
-rw-rw-- 1 root root 6416 Jan 26 06:04 /var/spool/mail/root
-rw-rw-- 1 sherlock mail 513 Oct 21 22:48 /var/spool/mail/sherloc
```
