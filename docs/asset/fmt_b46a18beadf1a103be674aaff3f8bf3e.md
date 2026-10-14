
在前面的示例中，用户连接到主机 `opus` 开启了一个 FTP 会话并以 `smith` 的身份登录。远程 FTP 服务器提示密码，用户输入密码（屏幕上不显示）。`ftp` 登录到远程系统并显示用于交互模式的 `ftp>` 提示符。用户告诉 `ftp` 使用 `dir` 命令列出远程目录，并使用 `get` 命令传输 `README` 文件。完成 FTP 会话后，这位勇敢的用户使用 `quit` 命令注销，返回到本地 Linux shell 提示符。

## 匿名 FTP 会话示例

在接下来的章节中，你将与一个系统进行 FTP 会话并查看一些目录。该用户在远程系统中拥有有效的用户名和密码。现在来看一个指向互联网上主要软件库的匿名 FTP 会话。列表 30.2 与列表 30.1 非常相似，但它有一些有趣的区别。

### 列表 30.2 执行匿名 FTP 连接

```
$ ftp.uu.net
Connected to ftp.uu.net.
220 ftp.uu.net server (Version wu-2.4(1) Wed Nov 13 15:45:10 EST 1996) ready.
Name (ftp.uu.net:bubba): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password: your_e_mail_address
```

## 使用 FTP 进行远程传输

```
230-          欢迎访问 UUET 存档。

230-          弗弗吉尼亚州 Falls Church UUET Technologies 公司的服务

230-          有关 UUET 的信息，请拨打 +1 703 204 8000，

230-          或查看 /unet-info 中的文件

230-          全天候允许访问。

230-          当地时间为 1996 年 11 月 13 日 星期三 15:53:02。

230-          所有传输都会记录您的主机名和电子邮件地址。

230-          如果您不喜欢此策略，请立即断开连接！

230-          如果您的 FTP 在登录后不久

230-          崩溃或挂起，请尝试使用

230-          破折号 (-) 作为密码的第一个字符。

230-          这将关闭可能干扰

230-          您的 ftp 客户端的信息消息。

230-          请阅读 /info/README 文件

230-          文件最后修改于 1996 年 11 月 11 日 星期一 17:39:53

230-          2 天前

230-          客人登录成功，有访问限制。

ftp

dir

200 PORT command successful for /bin/ls.

total 4149

-drwxr-sr-x 2 34 512 Jul 26 1992 .forward

-rw-r--r-- 1 34 Jul 26 1992 login

-rw-r--r-- 1 34 May 31 1992 kerc

-rw-r--r-- 1 34 Jul 26 1992 .not

-drwx-s-x 5 34 512 Jul 23 1900 admin

-drwxr-xr-x 1 34 1092 Jul 26 1992 archive ->

-drwxr-xr-x 4 34 4012 Apr 20 16:29 bin

-rw-r--r-- 1 34 2234 Sep 23 1993 by-name.gz-index/master/by.gz

-drwxr-xr-x 1 34 723 Sep 14 1993 by-time.gz ->index/master/by.gz

-rw-r--r-- 1 34 90112 Apr 26 1991 compress.tar

-drwx-xr-x 0 0 Jul 23 18:50 66 ->/dev/null

-drwxr-xr-x 2 34 512 Jul 26 1992 du

-drwxr-xr-x 21 34 1024 Sep 29 25:18 doc

-drwxr-xr-x 5 34 512 Apr 14 16:42 etc

-drwxr-xr-x 1 34 31 Dec 8 1993 feeds ->archive/published/unix

-drwxr-xr-x 2 34 512 Jul 26 1992 ftp

-drwxr-xr-x 4 34 512 Sep 29 10:34 graphics

-drwxr-xr-x 18 34 1024 Sep 29 10:28 graphics

-rw-r--r-- 1 27 79828 Jul 21 20:54 griz.tar

-drwxr-xr-x 1 34 171618 Jul 17 18:26 help -> info/archive

-drwxr-xr-x 20 34 1024 Dec 2 1993 index

-drwxr-xr-x 19 34 512 Sep 29 10:30 inet

-drwxr-xr-x 4 34 512 Sep 29 15:36 info

-drwxr-xr-x 25 34 512 Sep 29 10:29 languages

-drwxr-xr-x 4 34 512 Sep 29 10:28 library

-drwx-s-x 2 0 0 8192 Jul 26 1992 last+found
```

## 30.2 续

```
lrwxr-xrwx 1 34 20 Aug 1992 ls-lR.Z ->index/master/ls-itr.Z
lrwxr-xrwx 1 34 21 Sep 14 1993 ls-lR.gz ->index/master/ls-itr.gz
lrwxr-xrwx 1 34 21 Aug 1992 ls-ltR.Z ->index/master/ls-itr.Z
lrwxr-xrwx 1 34 22 Sep 14 1993 ls-lR.gz ->
drwxr-xr-x 2 34 1824 Sep 29 15:10 networking
drwxr-xr-x 2 34 512 Aug 10 09:26 packages
d-xr-xr-x 17 34 512 Sep 26 12:29 prime
drwxr-xr-x 25 34 1536 Sep 25 15:30 pub
drwxr-xr-x 17 34 160 Sep 17 19:38
lrwxr-xrwx 1 34 1096 Jun 26 19:02 sc-archive -> vendor/
drwxr-xr-x 20 34 512 Sep 29 04:18 systems
drwxr-xr-x 14 34 1536 Sep 29 15:36 tmp
lrwxr-xrwx 1 34 17 Jul 26 1992 unix-today ->vendor/unix-today
lrwxr-xrwx 1 34 17 Jul 26 1992 unix-world ->vendor/unix-world
drwxr-xr-x 3 34 1824 Sep 29 15:29 usenet
```

## login

`login` 命令与 `telnet` 命令非常相似，因为它允许你在远程系统上启动交互式命令会话。`login` 的语法如下：

# 第 30 章使用 telnet、ftp 和 r 命令访问网络

```
login [-BEKLdx] [-e char] [-k realm] [-l user-name] hostname
```

然而，最常用的用法仅仅是：

```
login hostname
```

表 30.3 解释了 `login` 命令的各种选项。

### 表 30.3 login 命令的命令行选项

| 选项 | 描述 |
| - | - |
| `-B` | 始终允许 8 位输入数据路径，这允许发送格式化的 ANSI 字符和其他特殊代码。如果未使用此选项，当远程停止和开始字符な其他于 `<Ctrl-s>` 和 `<Ctrl-q>` 时，将剥除校验位。 |
| `-E` | 停止将任何字符识别为转义字符。当与 `-e` 选项配合使用时，这将提供一个完全透明的连接。 |
| `-K` | 关闭 Kerberos 认证。它仅用于连接到使用 Kerberos 认证协议的主机时。 |
| `-L` | 允许登录会话处于显示输出模式（litout mode）。更多信息请参阅 tty 手页。 |
| `-d` | 在用于与远程主机通信的 TCP socket 上开启调试。更多信息请参阅 setsocket 手页。 |
| `-e` | 用于设置登录会话的转义字符。转义字符是默认的。你可以指定字面字符或形式为 `\\` 的八进制值。 |
| `-k` | 请求指定领域（realm）内远程主机的 Kerberos 票，而不是由 `krb_realmfhost(3)` 确定的远程主机领域。 |
| `-l` | 允许指定远程。如果可用，将使用 Kerberos 认证。 |
