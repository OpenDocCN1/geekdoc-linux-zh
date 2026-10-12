

### 230 来宾登录成功，访问限制已生效。
远程系统类型为 UNIX。
使用二进制模式传输文件。
ftp>

在本示例中，使用 `ftp` 进行连接，然后通过匿名访问进行登录。这是通过在 `Name` 提示符处输入单词 `anonymous` 来实现的。按下 Enter 键后，会显示 `password` 提示符。在使用匿名访问时，出于礼貌，通常建议输入您的电子邮件地址。系统不会验证输入的地址，但许多 FTP 服务器被配置为仅接受有效的电子邮件地址格式（即 user@somewhere.com），如果在提示符处输入了文本。

> **提示**
> 许多 FTP 服务器在接受匿名访问时，允许在密码提示符处直接按 Enter 键。

现在，与服务器之间已建立并验证了连接，您可以配置 FTP 会话以符合您的需求。如前一节所述，`ftp` 命令有许多不同的内置命令，您可以在 `ftp>` 提示符处输入问号来查看这些命令。这些命令可以影响会话显示、设置文件传输类型，或获取有关远程服务器的信息。

```bash
ftp> hash
Hash mark printing on (1024 bytes/hash mark).
ftp> prompt
Interactive mode off.
ftp> bin
200 Type set to I.
```

在本示例中，您已指示 `ftp` 每传输 1024 字节打印一个哈希（#）字符，关闭交互式提示，并将传输类型设置为二进制（这通常是默认设置）。哈希字符的显示提供了下载和上传进度的视觉指示。关闭提示允许您在无需确认每次传输的情况下发送和接收多个文件。将传输类型设置为二进制可确保二进制文件以正确的格式传输，而不是文本格式，这意味着可执行文件和图片能够正确传输。

接下来，您要求服务器显示服务器上可用的目录和文件列表：

```bash
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for directory listing.
total 32
d--x--x-x  2 root  root  4096 Aug 31 07:15 bin
d--x--x-x  2 root  root  4096 Aug 31 07:15 etc
d--x--x  2 root  root  4096 Aug 31 04:44 lib
d--x--x 2 root 50 4096 Sep 3 07:34 pub
226 Transfer complete.
```

如果 FTP 存储库中的目录权限设置正确，`pub` 目录应该是唯一显示其下文件的目录。为了验证这一点，更改目录到 `etc` 并列出其内容：

```bash
ftp> cd etc
250 CWD command successful.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for directory listing.
total 0
226 Transfer complete.
```

通过将目录 `bin`、`lib` 和 `etc` 的权限设置为仅可执行，系统管理员可以限制用户查看这些目录中的任何文件。良好的安全规定要求拒绝远程用户获取系统信息，因为任何信息都可能有助于黑客攻击尝试。

既然您看到服务器相对安全，请更改目录到 `pub` 并列出其内容：

```bash
ftp> cd pub
250-Please read the file README
250- it was last modified on Sun Sep 2 19:25:47 2001 - 1 day ago
250 CWD command successful.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for directory listing.
total 552
-rw-r--r-- 1 root 50 100 Sep 2 19:25 README
-rw-r--r-- 1 root 50 8 Sep 3 07:33 configuration
-rw-r--r-- 1 root 50 8 Sep 3 07:33 temp.txt
-rw-r--r-- 1 root 50 15798 Sep 3 10:29 tftp-0.17-14.i386.rpm
-rw-r--r-- 1 root 50 26011 Sep 3 10:30 tftp-server-0.17-14.i386.rpm
-rw-r--r-- 1 root 50 219332 Sep 3 10:29 wu-ftpd-2.6.1-22.i386.rpm
226 Transfer complete.
```

为了将所有 RPM 文件传输到您的本地机器，请发出 `mget *.rpm` 命令：

```bash
ftp> mget *.rpm
local: tftp-0.17-14.i386.rpm remote: tftp-0.17-14.i386.rpm
200 PORT command successful.
150 Opening BINARY mode data connection for tftp-0.17-14.i386.rpm
(15798 bytes).###############################
226 Transfer complete.
15798 bytes received in 0.974 secs (16 Kbytes/sec)
local: ftp-server-0.17-14.i386.rpm remote: ftp-server-0.17-14.i386.rpm
200 PORT command successful.
150 Opening BINARY mode data connection for ftp-server-0.17-14.i386.rpm (26011 bytes).
############################################
226 Transfer complete.
26011 bytes received in 2.5 secs (10 Kbytes/sec)
local: wu-ftp-2.6.1-22.i386.rpm remote: wu-ftp-2.6.1-22.i386.rpm
200 PORT command successful.
150 Opening BINARY mode data connection for wu-ftp-2.6.1-22.i386.rpm (219332 bytes).
############################################################
############################################################
####
226 Transfer complete.
219332 bytes received in 50.3 secs (4.3 Kbytes/sec)
```

如前所述，`mget` 命令将所有具有 `.rpm` 扩展名的文件传输到了我们的本地机器。此外，由于我们关闭了提示，它没有要求我们确认每个文件。`ftp` 客户端在每传输 1024 字节到我们的机器时打印一个 #。这在通过慢速连接传输时很有帮助，因为它提供了连接仍然处于活动状态的视觉提醒。

> **提示**
> 在每个操作之后，FTP 服务器都会返回一个状态代码和一条简短消息，显示您发出的命令的结果。您可以在请求评论 959（Request for Comments 959）中找到所有状态代码及其对应消息的列表；您可以在此处访问该列表的副本：http://www.ietf.org/rfc/rfc959.txt。

现在，本次会话已结束；您可以发出 `quit` 或 `bye` 命令来结束会话。FTP 服务器会告知您本次会话传输了多少字节、多少个文件，以及您的本地机器与服务器之间传输的总数据量（以字节为单位）。

```bash
ftp> bye
221-You have transferred 503818 bytes in 5 files.
221-Total traffic for this session was 506422 bytes in 7 transfers.
221 Thank you for using the FTP service on phoenix.
```

这是一个简单的示例，但典型的 FTP 会话通常也是微不足道的。在 FTP 会话期间还有其他可用的命令，但它们很少被使用。FTP 具有接收脚本输入并定义宏的功能，从而允许进行更复杂的会话。

> **提示**
> FTP 的信息页面与 Linux 中几乎每个命令都附带的手册（man）页面非常相似。可以在命令的源代码包中找到更详细的信息。

## 使用 lftp 命令进行文件传输

`lftp` 命令可用于使用 FTP、HTTP 以及各种安全协议（如 HTTPS 和 FTP）进行文件传输（如果启用了远程代理）。此命令的两个强大功能是能够重新启动停滞的下载（在文件传输中途），以及能够在单个会话中启动和运行多个下载（带作业控制）。

例如，下面是一个简单的会话，展示了从运行 Apache Web 服务器的远程计算机通过 HTTP 获取文件：

```bash
$ lftp http://192.168.2.37
cd ok, cwd=/ 
lftp 192.168.2.37:/> ls
-rw-r--r--  --  manual/mod/core.html
-rw-r--r--  --  manual/index.html
-rw-r--r--  --  icons/apache_pb.gif
-rw-r--r--  --  poweredby.png
lftp 192.168.2.37:/> get poweredby.png
1154 bytes transferred
lftp 192.168.2.37:/> bye
```

`lftp` 命令也可以用作传统的 FTP 客户端，但具有一些有趣的功能：

```bash
$ lftp 192.168.2.67 -u phudson
Password:
lftp phudson@192.168.2.67:~> cd /d2/isos/redhat/limbo
cd ok, cwd=/d2/isos/redhat/limbo
lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> mget disc1 &
[0] mget *disc1* &
lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> jobs
[0] mget *disc1*
    'limbo-1386-disc1.iso' at 56436448 (8%) 1.08Mi/s eta:9m [Receiving data]
lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> bye
[1843] Moving to background to complete transfers...
$ ps aux | grep lftp
phudson 1843 7.6 1.0 5456 2404 ? S 19:09 0:02 lftp 192.168.2.67
```

可以使用 `-u` 选项在命令行上传递用户名（和密码）。您可以使用此功能来减少获取远程文件时所需的交互式输入量，作为在 shell 脚本中使用 `lftp` 的辅助，以及当作为后台进程使用 `lftp` 获取文件时。

通过使用 ampersand（`&`），获取操作在后台进行，如前面的示例所示。`jobs` 命令用于显示当前的传输。如果用户注销会话（使用 `bye` 命令），文件传输将作为后台进程继续，直到完成。（这可以通过使用 `ps` 命令来验证。）

`lftp` 客户端具有许多额外功能，可以使文件传输工作比使用其他 FTP 客户端更容易。

> **注意**
> 另一个随 Fedora 提供的便捷的基于文本的文件传输实用程序是 `curl`，它支持使用 HTTP 进行文件获取。

## 使用 wget 命令进行文件传输

`wget` 命令用于使用 FTP、HTTP 以及各种安全协议（如 HTTPS 和 HTTP，如果启用了远程代理）进行文件传输。然而，与其他 FTP 客户端不同，`wget` 仅支持非交互式传输。这实际上是一个功能，因为 `wget` 可以作为后台进程下载文件，并递归复制远程文件目录。该命令还支持完成部分下载的文件，这可以在连接中断或不稳定的期间节省大量时间。

例如，下面是一个示例调用，展示了使用 `wget` 和 FTP URL 从远程计算机进行 FTP 获取：

```bash
$ wget ftp://phudson:mypasswd@stinky/mp3/*
--13:13:28--  ftp://phudson:*password*@stinky/mp3/*
             => '.listing'
Resolving stinky... done.
Connecting to stinky[192.168.2.33]:21... connected.
Logging in as phudson ... Logged in!
=> SYST ... done.     => PWD ... done.
=> TYPE I ... done.    => CWD /home/paul/mp3 ... done.
=> PORT ... done.      => LIST ... done.
 [ <=>                             ] 648          632.81K/s
13:13:28 (632.81 KB/s) - '.listing' saved [648]

Removed '.listing'.
--13:13:28--  ftp://phudson:*password*@stinky/mp3/C318121-01A.mp3
              => 'C318121-01A.mp3'
```

