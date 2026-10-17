
`$ sftp dtaylor@intuitive.com`

The authenticity of host 'intuitive.com (104.131.46.171)' can't be established.

ECDSA key fingerprint is

9e:f5:53:3d:3f:41:e1:ee:19:9b:ee:0e:11:11

9:0c:df. Are you sure you want to continue connecting (yes/no)? yes

Warning: Permanently added 'intuitive.com,104.131.46.171' (ECDSA) to list of

known hosts.

`dtaylor@intuitive.com`'s password: -

```
Since I haven’t used sftp to connect to the remote system before, it asks about the RSA encryption key. I’m sure that’s the right server, so yes gets me to the password prompt.

Once I’ve correctly entered the remote account password, I’m ready to go:
```

```
Connected to intuitive.com.

.

sftp> _
```

## 2.

Now I’m at the `sftp` program prompt, and any of the commands shown in Table 21.1 will work here. I use `dir` and `ls` to list my files in different formats:

```
sftp> ls -l
-rw-r--r--x 1 taylor users0 4941 Oct 4 1991 .Pnews.header
-rw-r--r-- 1 taylor users0 2103 Sep 30 19:17 .article
-rw-r--r-- 1 taylor users0 752 Apr 17 1998 .cshrc
drwx-- 2 taylor daemon 4096 Dec 6 14:25 .elm
-rw-r--r-- 1 taylor users0 28 Nov 5 09:50 .forward
-rw-r--r-- 1 taylor users0 1237 Dec 13 09:40 .login
-rw-r--r-- 1 taylor users0 6 Aug 6 1991 .logout
-rw-r--r-- 1 taylor users0 538 Dec 6 14:32 .newsrc
-rw-r--r-- 1 taylor users0 1610 Feb 17 1992 .plan
-rw-r--r-- 1 taylor users0 0 Aug 6 1991 .pnewsxpert
-rw-r--r-- 1 taylor users0 45 Feb 2 1993 .rlogin
-rw-r--r-- 1 taylor users0 6 Feb 8 1993 .rnlock
-rw-r--r-- 1 taylor users0 16767 Jan 27 1993 .rnsoft
-rw-r--r-- 1 taylor users0 114 Apr 6 1998 .sig
drwxr-xr-x 4 taylor users0 4096 Nov 13 11:09 .tin
-rw-r--r-- 1 taylor users0 1861 Jun 2 1997 Global.Software
-rw--- 1 taylor users0 21194 Oct 1 1995 Interactive.Unix
drwx--- 4 taylor users0 4096 Nov 13 11:09 Mail
drwxr-xr-x 2 taylor users0 4096 Nov 13 11:09 News
drwxr-xr-x 2 taylor users0 4096 Nov 13 11:09 Src
drwxr-xr-x 2 taylor users0 4096 Nov 13 11:09 bin
-rw-r--r-- 1 taylor users0 12445 Sep 17 14:56 history.usenet.Z
-rw-r--r-- 1 taylor users0 1237 Oct 18 20:55 login
-rw-r--r-- 1 taylor users0 174 Nov 20 19:21 testme
sftp> dir
Mail News bin Global.Software history.usenet
Src Interactive.Unix testme login
sftp>
```

As you can see, there’s a surprising amount of difference between the `dir` command (which you use to get a directory listing in `ftp`) and the `ls -l` command. I definitely prefer the latter.

### Note

使用 `sftp` 中的 `ls` 命令的一个技巧是，如果你把一组命令标志作为第二个词指定，它就能正常工作，如图所示。然而，如果指定第三个参数，`sftp` 会将命令的输出保存到以该名称命名的本地文件中；因此 `ls -l -C` 会在你的系统上创建一个名为 `-C` 的文件，其中包含 `ls -l` 命令的输出。很别扭。

## 3.

要从远程系统传输文件 `login.txt`，我可以使用 `get` 命令：

```
sftp> get login.txt
Fetching /home/taylor/login.txt to login.txt
100%  46    0.0KB/s   00:00
/home/taylor/login.txt
sftp>
```

这可能会变得有点棘手。我刚刚把 `login.txt` 文件从 `intuitive.com`（我通过 SFTP 登录的地方）复制到了我运行 `sftp` 命令的本地 Unix 系统上。在本地系统上，SFTP 给文件起了与远程系统上相同的文件名：`login.txt`。

## 4.

或者，我也可以使用 `get` 并指定一个类似我会给 `shell` 的通配符模式：

```
sftp> get log*
Fetching /home/taylor/login.txt to login.txt
/home/taylor/login.txt    100%   46    0.0KB/s   00:01    f
```

只有一个匹配项，所以传输很简单。`get` 和 `put` 的通配符形式在你想一次传输多个文件时特别有用，例如 `get *.?` 就会获取 `*.c`、`*.h` 以及文件名后缀为单个字母的其他源文件。

这项工作很容易完成。在下一个任务中，我将在另一个支持匿名 FTP 的系统上查看有什么可用资源。

## 5.

要断开连接，我输入 `quit`：

```
sftp> quit
$
```

尽管界面相对粗糙，SFTP 仍提供了一种在两种系统之间快速高效传输文件的方法，无论操作系统如何。它值得学习，但如果你愿意，你也可以获得一个漂亮的图形前端，无论是在 X11、Windows 还是 Mac 环境中。

## Task 21.4: Exploring Anonymous FTP Archives

FTP 是一种简单但不安全的传输文件方法，但事实证明，即使你没有该系统的实际登录账户，也可以使用许多 FTP 档案。被称为匿名 FTP 档案，这些站点通常是庞大的数据和应用程序档案库，是比常见基于 Web 的档案站点更有价值的替代方案。让我们来看看吧！

- 1. Internet 上有数百个信息服务器，提供令人惊叹的各种信息，从天气预报图到《圣经》和《爱丽丝梦游仙境》的全文，以及数千个程序的源代码清单。在本示例中，我想查看一个名为 The Armory 的软件仓库中的匿名 FTP 档案。名为 `ftp.armory.com` 的主机。这次我们将使用 FTP 程序，而不是 SFTP，很容易打开一个新的档案站点：

```
$ ftp ftp.armory.com
Connected to ftp.armory.com.
220 deepthought FTP server ready.
Name (ftp.armory.com:taylor): ftp
```
